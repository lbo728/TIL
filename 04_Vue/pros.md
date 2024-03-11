
# Props

목차
1. [이슈](#이슈)
2. [해결과정](#해결과정)

## 이슈


vue와 typescript를 함께 사용할 경우, props에 type을 지정해주지 않으면 다음과 같은 에러가 발생한다.

```js
export default {
	props: ['propsA', 'propsB'],
	setup(props) { 
	// Parameter 'props' implicitly has an 'any' type.ts(7006)
	watch(
		() => props.propsA,
		(value) => {
		newValue = (value / 2) * 20
	}
	return {}
	}
}
```
<br />


>`<script setup>` 을 사용하지 않는 경우 props 타입 추론을 활성화하기 위해 `defineComponent()` 를 사용해야 합니다. `setup()` 에 전달된 props 객체의 타입은 `props` 옵션에서 유추됩니다. 
[script setup 없이 사용하기 | Vue.js](https://v3-docs.vuejs-korea.org/guide/typescript/composition-api.html#without-script-setup)

<br />

```ts
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    message: String
  },
  setup(props) {
    props.message // <-- type: string
  }
})
```

<br />

때문에 다음과 같이 `defineComponent`를 적용하여  타입 추론을 활성화하면 에러를 없앨 수 있다.

<br />

```js
export default defineComponent({
	props: ['propsA', 'propsB'],
	setup(props) { 
	watch(
		() => props.propsA,
		(value) => {
		newValue = (value / 2) * 20
	}
	return {}
	}
})
```

