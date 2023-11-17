# 이벤트(Emit)

[참고]
[컴포넌트 이벤트 | Vue.js](https://v3-docs.vuejs-korea.org/guide/components/events.html){: target="_blank"} | [Composition API와 타입스크립트 | Vue.js](https://v3-docs.vuejs-korea.org/guide/typescript/composition-api.html#typing-component-emits){: target="_blank"}
<br />

> 목차
[1. 용법](#1-용법)
[2. 이슈](#2-이슈)
[3. 해결과정](#3-해결과정)



# 1. 용법

### 상위 컴포넌트
컴포넌트는 내장 메서드 `$emit`을 사용하여 템플릿 표현식(예: `v-on` 핸들러에서)에서 직접 사용자 정의 이벤트를 발신할 수 있습니다:

```js
<!-- MyComponent -->
<button @click="$emit('someEvent')">클릭하기</button>
```

그러면 부모는 `v-on`을 사용하여 수신 할 수 있습니다:


```js
<MyComponent @some-event="callback" />
```

`.once` 수식어는 컴포넌트 이벤트 리스너에서도 지원됩니다.


```js
<MyComponent @some-event.once="callback" />
```

###Script 작성

`<script setup>` 대신 명시적으로 `setup` 함수를 사용하는 경우, 이벤트는 [`emits`](https://v3-docs.vuejs-korea.org/api/options-state.html#emits) 옵션을 사용하여 선언되어야 하며 `emit` 함수는 `setup()` 컨텍스트에 노출되어야 합니다:

`setup()` 컨텍스트의 다른 속성과 마찬가지로 `emit`는 안전하게 분해할당할 수 있습니다:

```js
export default {
  emits: ['inFocus', 'submit'],
  setup(props, { emit }) {
    emit('submit')
  }
}
```

`emits` 옵션은 객체 구문도 지원하므로, 발신되는 이벤트의 전달 내용(payload)에 대한 런타임 유효성 검사를 수행할 수 있습니다:

Typescript를 사용한다면, 

`<script setup>` 에서 런타임 선언 또는 타입 선언을 사용하여 `emit` 함수를 입력할 수 있습니다.

```js
<script setup lang="ts">
// runtime
// 런타임
const emit = defineEmits(['change', 'update'])

// type-based
// 타입기반
const emit = defineEmits<{
  (e: 'change', id: number): void
  (e: 'update', value: string): void
}>()
</script>
```

타입 전달인자는 [Call Signatures 호출 서명 ](https://www.typescriptlang.org/docs/handbook/2/functions.html#call-signatures) 이 있는 타입 리터럴이어야 합니다. 타입 리터럴은 반환된 `emit` 함수의 타입으로 사용됩니다. 보시다시피, 타입 선언은 emit된 이벤트의 타입 제약 조건에 대해 훨씬 상세한 제어를 제공합니다.

`<script setup>` 을 사용하지 않을 때, `defineComponent()` 는 설정 컨텍스트에 노출된 `emit` 함수에 대해 허용된 이벤트를 추론할 수 있습니다.

``` ts
import { defineComponent } from 'vue'

export default defineComponent({
  emits: ['change'],
  setup(props, { emit }) {
    emit('change') // <-- type check / auto-completion
  }
})
```

# 2. 이슈
Home에 있는 컴포넌트를 분리해서 ACompoent에서 `emit`으로 'clickTo'라는 이름의 Function을 연결했을 때는 의도한대로 동작하지만, BComponent 컴포넌트를 만들어 `emit`에 clickTo를 연결했을 때는 버튼을 누르지 않았는데도 바로 '/detail1'로 리다이렉션 시켜버러리는 오류가 발생했다.
```js
// Home.vue
...
<AComponent @btn-click="clickTo('detail1')" />
<BComponent @btn-click="clickTo('detail2')" />
...
```



# 3. 해결과정

여러가지 시도를 해보다 AComponent에서 emit을 없앴는데도 @btn-click이 동작하는 것을 확인하게 되었다.
AComponent script에서 만든 `defineComponent`가 전역적으로 동작하는 것인가?

```js
// AComponent.vue
import { defineComponent } from 'vue'

export default defineComponent({
	emits: ['btn-click'],
	setup(props, { emit }) {
		emit('btn-click')
	},
})
```
놀랍게도, 이 AComponent에서 emit을 없애도 작동했다.

```js
<VButton color="primary" bold rounded raised @click="$emit('btn-click')">
	See My Scores
</VButton>
```
중요한건, 자식 컴포넌트의 vue에서 `$emit('btn-click')`이라고 명명한 emit의 이름과, 부모 컴포넌트의 vue에서 

```js
<HeroSection @btn-click="clickTo('detail1')" />
```
`v-on` 에 이름을 맞춰주는 것인 것 같다. 이벤트 이름을 매칭시켜준 것 이상으로 콜백함수를 담아서 넘긴다면 script에 그 이상의 코드를 담아주어야 하지만, 단순히 매칭시킬 뿐이면 이렇게 이름을 맞춰주는 것만으로도 정상 작동하는 것으로 보인다.