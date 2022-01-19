## 컴포넌트 정복하기 

  ### 컴포넌트란? 
  * 독립적인 단위모듈 (독립적으로 구성되어 재사용이 가능한 부품같은 느낌)

  ### Vue에서 컴포넌트?
  1. HTML Element를 확장하고 재사용 가능한 형태로 구현하는 것
  2. Vue.js에서 사용된 모든 컴포넌트는 하나하나가 Vue.js의 인스턴스


  ### Component 의 종류 
  ##### 전역 컴포넌트 (Global)
  생성하고나면 전체 페이지(모든 인스턴스)에서 모두 사용 가능(전역변수 느낌)

  ##### 지역 컴포넌트 (Local)
  사용될 곳에 바로 삽입해서 생성. 해당 영역에서만 사용. 인스턴스 생성할때 마다 등록해야 됨  

  ```vue
  /* 전역 컴포넌트 등록 */
  //App.vue

  Vue.component(GlobalComponent.name, GlobalComponent)

  new Vue({
    el: '#app'
  });


  /* 지역 컴포넌트 등록 */
  //App.vue

  new Vue({
    el: '#app',
    components: { LocalComponent }
  })

  ```


### Component 통신 규칙 
  ##### 데이터 방향: props는 아래로, events 위로
   부모는 props를 통해 자식에게 데이터를 전달하고 자식은 events를 통해 부모에게 메세지를 보내는 형태 
   1. Props  
   * 상위 컴포넌트의 정보를 전달하기 위해서 props 지정 
   * 하위 컴포넌트는 props 옵션을 사용해서 수신 예정인 props를 선언해야함 
   * Props의 성격
     1. 상위 데이터 변경 시 하위 항목에 바로 반영되는 Reactivity  
     2. 단방향 바인딩 형태기 때문에 자식은 부모 상태를 변경할 수 없음 
     + 하위 컴포넌트에서 상위에서 받은 데이터 그대로 쓰고 싶지 않을 때? 
          - 로컬 데이터 속성은 따로 선언 해서 초기값으로 prop 사용 
          - computed 속성 사용해서 형태를 바꾸어 return 


  2. Events 
  * v-on 사용해서 이벤트 감지 
    - $emit은 Vue에서 제공하는 이벤트 전달하는 API
    - 사용법: `v-on:이벤트형태 = "메서드이름"`
  * 상위 컴포넌트는 `fuction(value)`으로 받을 수 있음


  ##### 같은 컴포넌트 레벨 간의 통신 
    ① 이벤트로 데이터 상위 컴포넌트로 전달
    ② Props에 담아 하위 컴포넌트로 전달

  