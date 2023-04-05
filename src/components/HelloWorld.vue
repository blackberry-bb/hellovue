<template>
  <div class="hello">

    <!--
      {{}} , v-text
    -->
    <h1>{{ msg }}</h1> <!-- {{}}으로 표현 -->
    <h1 v-text="msg"></h1> <!-- v-text로 표현 -->

    <!--
      v-html
    -->
    <p>텍스트 보간법 사용: {{ rawHtml }}</p> <!-- 일반 HTML로 해석한 것으로 대체 -->
    <p>v-html 디렉티브 사용: <span v-html="rawHtml"></span></p> <!-- v-html속성으로 화면에 대체 -->

    <!--
      v-bind:id
    -->
    <div v-bind:id="dynamicId1"></div> <!-- 요소 객체의 속성들을 바인딩하기 위해 사용 -->
    <div :id="dynamicId2"></div> <!-- v-bind:id의 단축법-->

    <!--
      v-model : 양방향데이터바인딩이 필요한 경우
    -->

    <!--
      v-if : 우리가 알고있는 그것,
      v-show : v-if와 동일하다, 렌더링 여부의 차이
    -->
    <div id="account1">
      <!--<input type="text" v-model="balance"> 입력받을 수 있게 / 일단 주석처리-->
      <span v-if="balance >= 100000">GOLD</span>
      <span v-else-if="balance >= 50000">Silver</span>
      <span v-else-if="balance >= 10000">Bronze</span>
      <span v-else>Bronze</span>
    </div>

    <!-- v-for : 우리가 알고있는 그것, 반복!
      <tr v-for="(contact, index) in contacts">...</tr> : 배열의 데이터인 경우
      <tr v-for="(val, key) in regions">...</tr> : 객체의 데이터인 경우

      v-for, v-if를 함께 사용가능, 단 v-for를 먼저 수행되고 v-if가 적용됨
    -->

    <!--
      v-pre : 컴파일을 수행하지않음, 그대로 노출
    -->
    <h5 v-pre>{{ msg }}</h5>

    <!--
       v-once : 처음 한번만 렌더링를 수행(데이터가 변경되더라도 다시 렌더링 되지않는다.)
    -->
    <h5 v-once>{{ msg }}</h5>

    <!--
      methods @click 이벤트
    -->
    <h1>{{ message }}</h1>
    <button v-on:click="reverseMessage">Reverse Message</button>
    <!--<button>{{reverseMessage()}}</button>-->
    <button @click="message += '!'">Append "!"</button>
    <h5>{{ sum1() }}</h5>

    <!--
      computed(계산된 속성)
    -->
    <h5>{{ fullName }}</h5>
    <h5>{{ sum2 }}</h5>

    <!--
      *****computed 와 methods의 차이 : 캐싱차이
    -->

    <!--
      watch(관찰 속성) : 비동기처리에 적합
     -->
    <div>
      x : <input type="text" v-model="x" />
      y : <input type="text" v-model="y" />
      덧셈 결과 : {{total}}
    </div>

    <!--
      preventDefault : 기본이벤트의 특성을 실행중지시킴
    -->
    <!-- <div id="example" v-on:contextmenu="ctxStop"> -->
    <div id="example1" v-on:contextmenu.prevent="ctxStop">
      <a href="https://facebook.com" @click="confirmFB">페이스북</a>
    </div>

    <!--
      이벤트 전파와 버블링
    -->
    <div id="example2">
      <div id="outer" @click="outerClick">
        <div id="inner" @click="innerClick"></div>
      </div>
    </div>
    <!--
    <div id="example2">
      <div id="outer" @click.stop="outerClick">
        <div id="inner" @click.stop="innerClick"></div>
      </div>
    </div>
    -->

    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>


<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    rawHtml: String,
    balance: Number
  },
  methods: {
    reverseMessage() {
      this.message = this.message.split('').reverse().join('')
    },
    sum1() {
      return 1+this.num;
    },
    ctxStop : function(e) {
      e.preventDefault();
    },
    confirmFB : function(e) {
      if (!confirm("페이스북으로 이동할까요?")) {
        e.preventDefault();
      }
    },
    outerClick : function(e) {
      console.log("### OUTER CLICK")
      console.log("Event Phase : ", e.eventPhase);
      console.log("Current Target : ", e.currentTarget);
      console.log("Target : ", e.target);
      e.stopPropagation();
    },
    innerClick : function(e) {
      console.log("### INNER CLICK")
      console.log("Event Phase : ", e.eventPhase);
      console.log("Current Target : ", e.currentTarget);
      console.log("Target : ", e.target);
      e.stopPropagation();
    }
  },
  computed: {
    fullName: {
      // getter
      get() {
        console.log('2');
        return this.firstName + ' ' + this.lastName
      },
      // setter
      set(newValue) {
        // 참고: 분해 할당 문법을 사용함.
        console.log('3');
        [this.firstName, this.lastName] = newValue.split(' ')
      }
    },
    sum2() {
      return 1+this.num;
    }
  },
  watch: {
    x : function(v) {
      console.log('## x 변경')
      const result = Number(v) + Number(this.y);
      if (isNaN(result)) this.total = 0;
      else this.total = result;
    },
    y : function(v) {
      console.log('## y 변경')
      this.y = v;
      const result = Number(this.x) + Number(v);
      if (isNaN(result)) this.total = 0;
      else this.total = result;
    }
  },
  data() {
    return {
      message: 'Hello World!',
      firstName: 'John',
      lastName: 'Doe',
      num: 0,
      x: 0,
      y: 0,
      total: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#outer {
  width:200px; height:200px; border:solid 2px black;
  background-color: aqua;
  position: absolute; top:100px; left:50px;
  padding:10px 10px 10px 10px;
}
#inner {
  width:100px; height:100px; border:solid 2px black;
  background-color:yellow;
}
</style>
