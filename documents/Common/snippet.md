
[참고]
[VS Code에서 나만의 Snippets 만들기 | 향로](https://jojoldu.tistory.com/491)

[Tool]
[Snippet Generaotr](https://snippet-generator.app/?description=&tabtrigger=&snippet=export+default+%7B%0A++setup%28%29+%7B%0A++++return+%7B%7D%0A++%7D%2C%0A%7D%0A&mode=vscode): 내가 작성한 코드를 스니펫 json 코드 형태로 변환
![Alt text](<스크린샷 2023-11-20 오전 11.36.04.png>)

<br />

1. Code → Preference → Configure User Snippet
   ![Alt text](<스크린샷 2023-11-20 오전 11.23.28.png>)
   <br />
2. 사용하고자 하는 Snippet의 파일 확장자 선택
  ![Alt text](<스크린샷 2023-11-20 오전 11.24.32.png>)
  <br />
3. 스니펫을 작성 후, prefix를 이용해 스니펫을 불러낸다.
  ![Alt text](<스크린샷 2023-11-20 오전 11.33.08.png>)

# 용법 설명
![Alt text](<스크린샷 2023-11-20 오전 11.35.05.png>)
1. Vue Base: Snippet의 이름이다.
2. prefix: 스니펫으로 이용할 문자열을 작성한다. 예시에서는 `Vb`라는 단축어를 사용했다.
3. body: 해당 스니펫을 이용했을 때 나타날 코드를 작성한다. json 배열로 작성해야하기 때문에, `"(큰따옴표)`는 `\"` 형태로 변환해주어야 한다. 이를 고려하지 않고 편리하게 작성하고자 한다면, `Snippet Generator`를 이용하는 방법도 있다.
4. description: 스니펫을 입력했을 때 나타날 설명을 작성한다.



