# study_vue

## v-if vs v-show

v-if 일 경우 태그 자체가 주석처리 된것 처럼 표현된다.

v-show 경우는 display 가 none 으로 표현된다.

## compute

화면과 무관하게 계산을 해야 되는 경우에는 compute 를 사용하는게 좋다. 그렇지 않을경우 화면을 다시 그릴때마다 계산도 다시 하기 때문에 속도가 느려질 수 있다.

## lifeCycle

Created : 컴포넌트가 보여지긴 하지만 화면에 나타나기 전. Javascript 상에는 존재하나 아직 화면에 그려지지는 않는다. Data 만 준비된 상태.

Mounted : 컴포넌트가 화면에 나타난후.

Updated : 화면의 data 가 바껴서 화면이 다시 그려질때

Destroyed : 컴포넌트가 화면에서 사라질때.

## props

부모가 자식에게 값을 전달 할 수 있다.

자식이 props 로 전달 받은 값을 변경하는건 금지한다.

props: [] or props: {} 로 선언.

## Watch

어떤 기능이 변경되었는지 감지하는 기능. (되도록 안쓰는게 좋다)

computed 는 특정 값을 반환하고 watch 는 특정 동작을 실행한다.

## Object, Array 사용시 주의 할점

객체, Array 사용시 index를 사용해서 값을 바꿀 경우에는 화면에 반영이 안된다. 하지만 메소드를 사용할 경우에는 반영이 된다.

~~~ vue
this.tableData[1][0] = 'X'; ---> 작동하지 않음
~~~

- 해결방법

~~~ vue
import Vue from 'vue'; 선언
Vue.set(this.tableData[1], 0, 'X');
~~~

또는

~~~ vue
this.$set(this.tableData[1], 0, 'X');
~~~

## Vuex

Data 를 중앙에서 관리 할수 있게 한다.

* vuex 설치

    npm i vuex

* .js 파일 생성

~~~ vue
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
    state:{

    }, // vue 의 data 와 비슷
    mutations:{

    }, // vue 의 computed 와 비슷
    getters:{

    }, // state 를 수정할때 사용. 동기
    actions:{

    }  // 비동기를 사용할때, 또는 여러 mutations 를 실행할 때
});
~~~

* root component 에서 import

~~~ vue
import store from "./store";
                  
export default {
    store,    
};
~~~

* mapState 사용

import {mapState} from 'vuex';

## Event Bus

이벤트를 모두 중앙에서 관리 할수 있게 한다. Root Component 에서 모든 DATA 처리를 할수 있다.

EventBus.js 생성

~~~ vue
import Vue from 'vue';
export default new Vue();
~~~

EventBus 등록

~~~ vue
import EventBus from "./EventBus";
EventBus.$on('clickTd', this.onClickTd);
~~~

EventBus 사용시

~~~ vue
EventBus.$emit('clickTd');
EventBus.$emit('clickTd', param1, param2);
~~~
