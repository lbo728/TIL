
[참고]
[VS Code에서 나만의 Snippets 만들기 | 향로](https://jojoldu.tistory.com/491)

[Tool]
[Snippet Generaotr](https://snippet-generator.app/?description=&tabtrigger=&snippet=export+default+%7B%0A++setup%28%29+%7B%0A++++return+%7B%7D%0A++%7D%2C%0A%7D%0A&mode=vscode): 내가 작성한 코드를 스니펫 json 코드 형태로 변환
<img src="https://github.com/lbo728/TIL/assets/72309817/4f4aa3ab-6fbe-4a16-8f66-5ce57450f451"  />



<br />

1. Code → Preference → Configure User Snippet
  <img src="https://github.com/lbo728/TIL/assets/72309817/67a42d12-439a-45f3-97a7-8249c8c51644" width="80%" />
<br />
2. 사용하고자 하는 Snippet의 파일 확장자 선택
  <img src="https://github.com/lbo728/TIL/assets/72309817/08aca128-8214-4f2e-b5b9-0b8b272eec0b" width="80%" />
<br />

3. 스니펫을 작성 후, prefix를 이용해 스니펫을 불러낸다.
  <img src="https://github.com/lbo728/TIL/assets/72309817/162aa933-6919-4aa0-98f8-72095adc008f" width="80%" />
<br />

# 용법 설명
  <img src="https://github.com/lbo728/TIL/assets/72309817/1cc5cc85-dce9-48c5-bdbd-7f1ffc17620c" width="80%" />
<br />

1. Vue Base: Snippet의 이름이다.
2. prefix: 스니펫으로 이용할 문자열을 작성한다. 예시에서는 `Vb`라는 단축어를 사용했다.
3. body: 해당 스니펫을 이용했을 때 나타날 코드를 작성한다. json 배열로 작성해야하기 때문에, `"(큰따옴표)`는 `\"` 형태로 변환해주어야 한다. 이를 고려하지 않고 편리하게 작성하고자 한다면, [`Snippet Generator`](https://snippet-generator.app/?description=&tabtrigger=&snippet=export+default+%7B%0A++setup%28%29+%7B%0A++++return+%7B%7D%0A++%7D%2C%0A%7D%0A&mode=vscode)를 이용하는 방법도 있다.
4. description: 스니펫을 입력했을 때 나타날 설명을 작성한다.



