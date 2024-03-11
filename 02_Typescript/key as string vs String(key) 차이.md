# key as string vs String(key) 차이

목차

- [key as string vs String(key) 차이](#key-as-string-vs-stringkey-차이)
  - [이슈](#이슈)
  - [해결과정](#해결과정)
  - [ChatGPT를 통한 정리](#chatgpt를-통한-정리)
  - [결론](#결론)

## 이슈

Vue3에서 v-for를 사용할 때 (item, index) index는 number이기 때문에, 불러낸 데이터가 객체인데 각 index가 string이라면, index의 타입을 String(key)로 변경해서 조건절을 적용해야한다.

```js
// 이슈 상황
<div v-for="(item, key) in readingList" :key="key">
  <div v-show="key === 'Characters'">...</div>
</div>
```

<br />

## 해결과정

```js
// 해결
<div v-for="(item, key) in readingList" :key="key">
  <div v-show="String(key) === 'Characters'">...</div>
</div>
```

```js
  <MyComponent v-for="(item, index) in items" :item="item" :index="index" :key="item.id" />
```

<br />

## ChatGPT를 통한 정리

1. **(key as string):** 이는 TypeScript에서 사용되는 타입 단언이다. 여기서 `(key as string)`은 "key를 문자열로 취급해!"라고 TypeScript에게 알려주는 것이다. 이것은 런타임에서 아무런 영향을 주지 않고, 오로지 TypeScript 컴파일러에게만 의미가 있다. 코드 작성자가 "나는 key가 언제나 문자열이라고 확신해"라고 명시하는 것이다.
   <br />
   ```js
   const myKey: string = key as string;
   ```
   <br />
2. **String(key):** 이는 JavaScript에서 기본적으로 제공되는 `String` 함수를 사용한 변환이다. `String(key)`는 `key` 값을 강제로 문자열로 변환하는 것이다. 이 변환은 런타임에 실제로 발생하며, `key`가 어떤 타입이든 간에 해당 타입을 문자열로 변환한다.
   <br />
   ```js
   const myKey = String(key);
   ```

<br />

## 결론

어떤 것을 선택할지는 상황에 따라 다르다. TypeScript 컨텍스트에서는 `(key as string)`이 주로 사용되며, 일반적으로는 `String(key)`를 사용하지 않는다. 하지만 `String(key)`는 런타임에서 문자열로 변환하므로 코드가 더 명시적이고 직관적일 때 사용할 수 있다.

_작성일 2023년 12월 1일 18:46_
