### 3DSalad 문의하기 버튼 개선
    - CSS Animation을 너무 단순하게 바라봤다. 사실 너무 단순한 트랜지션인데도 오전부터 3시까지 시간을 날렸다. vue3의 유용한 컴포넌트인 Transition에서 등장과 퇴장을 템플릿화 해놓았지만, 좀 더 디테일하게 만지려면 아무래도 css로 조작하려면 css로 제어해야 했던 것 같다. 결국 layerpop과 내부의 wrap-inner에 적용되어있던 Transition을 없애고 클래스로 open 상태를 제어하여 애니메이션을 만들었다.
        
        그리고 [[원티드 레퍼런스]((https://www.wanted.co.kr/jobsfeed?utm_source=google&utm_medium=sa&utm_campaign=kr_recruit_web_sa_signup&utm_term=%EC%9B%90%ED%8B%B0%EB%93%9C&utm_content=brand&gclid=CjwKCAjw3oqoBhAjEiwA_UaLtqJXMMWfRiIIqsMt2--8KeJnj2q1Adgg1zOkRGgjZx1rY8SZXTFMhBoCsesQAvD_BwE))]를 따르려할 때 oppacity 타이밍이 거의 사라지기 직전에 적용되어야 했기 때문에 keyframe로 따로 조절했다. 
        
        버튼이 아래서 위로 쓸어올린 것처럼 translateY를 주는 동시에 물리적으로 통통 튀기는 느낌을 주어야 했기 때문에 마찬가지로 keyframe으로 통제했다. 의외로 또 시간이 걸린 점이, 버튼을 누를 때 전환되는 아이콘 중, 메시지 아이콘이 좌표값 상 버튼을 넘어가도록 위로 이동하되, 버튼에 마스크가 있는 것처럼 지나쳐가면 안되었는데, overflow: hidden 속성으로 해결 가능함을 깨닫는데 오래걸렸다.
        
        - button: 바운스 애니메이션
        - modal: bottom → top, opacity 0 → 1 타이밍 조절하기
        
### Button 컴포넌트에서도 emit으로 이벤트를 올릴 때, @btn-click=”$emit(””)”
    
    isPending을 부모 컴포넌트의 부모 컴포넌트까지 전달하는 방법
    
    ```jsx
    <ButtonBlack @btn-click="({ isPending }) => $emit('event-name', isPending)" >
        <template v-slot:content>
    	    <div>{{ $t("common.follow") }}</div>
        </template>
    </ButtonBlack>
    ```
    
    - 해당 컴포넌트의 부모 컴포넌트에서 emit을 받아 연결한 함수에 isPending 전달하는 방법
        - 이벤트 핸들러로 데이터를 넘겨받을 때 사용하는 VueJS의 특별한 변수, [‘$event’](https://v3-docs.vuejs-korea.org/guide/essentials/event-handling.html#accessing-event-argument-in-inline-handlers)로 넘겨받을 수 있음
            
            <aside>
            💡 [$event](https://v3-docs.vuejs-korea.org/guide/essentials/event-handling.html#accessing-event-argument-in-inline-handlers)
            
            Vue.js에서 이벤트 핸들러로 전달되는 인자는 **`$event`**라는 이름의 특별한 변수입니다. 이 변수는 이벤트가 발생할 때 이벤트 핸들러로 전달되는 데이터를 나타냅니다. 일반적으로 **`$event`** 변수를 사용하여 컴포넌트 간 데이터를 전달하거나 이벤트 핸들러에서 데이터를 수신할 수 있습니다. 
            
            이것은 Vue.js에서 제공하는 편리한 기능 중 하나이며, 이벤트 핸들러로 데이터를 전달할 때 사용됩니다.
            
            </aside>
            
        
        ```jsx
        <UserProfile @event-name="functionName($event)" />
        ```
        
    - 부모 컴포넌트의 script에서 연동할 function에 isPending 전달하는 방법
