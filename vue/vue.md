# vue

## vue 설치

- node가 깔려져 있는 상태여야 한다.

```bash
$ sudo npm install -g vue
$ npm install -g @vue/cli
```

## 프로젝트 생성

```bash
$ vue create 프로젝트명
```

- your connection 너무 느려 → n
- preset → manually select features
- feature → Bable, Router, Vuex, Linter
- version → vue 3
- history → Yes
- formatting → Standard
- save as a preset → 나중에도 쓰고 싶으면 Yes → preset as → 원하는 이름

## 프로젝트 실행

```bash
# 해당 프로젝트 폴더로 이동
$ cd project

# 프로젝트 실행하기
$ npm run serve
```

- 종료는 `ctrl + c`

## 추가 파일

- 생성한 project 파일에 `.prettierrc` 생성

```bash
{
    "semi": false,
    "bracketSpacing": true,
    "singleQuote": true,
    "useTabs": false,
    "trailingComma": "none",
    "printWidth": 80
}
```

- 다음과 같이 추가해준다. string “” 쌍따옴표 및 홀따옴표 문제 방지

```bash
"eslintConfig": {
    "root": true,
    "env": {
      "node": true
    },
    "extends": [
      "plugin:vue/vue3-essential",
      "@vue/standard"
    ],
    "parserOptions": {
      "parser": "@babel/eslint-parser"
    },
    "rules": {
      "space-before-function-paren": "off"
    }
  },
```

- 맨 마지막 `“rules”` 에 `“space-before-function-paren” : “off”` 추가

## 라우터

```jsx
// about

component: () =>
  import(
    /* webpackChunkName: "about", webpackPrefetch:true */ "../views/AboutView.vue"
  );
```

- `webpackPrefetch:true`
- 미리 캐시를 불러와준다.
- 해당 페이지에서 들어갈 가능성이 높거나, 용량 측면에서 미리 불러오는 것이 좋을것이라 판단되는 페이지등에 설정해준다.
- 사이즈가 작거나, 해당 페이지를 들어갈 확률이 낮다면, webpackPrefetch 를 설정해주지 않는다.

## 데이터 바인딩

- vue 컴포넌트를 만들어보자
- vue 는 양방향 데이터 바인딩이 가능하다

- 템플릿 태그

  ```html
  <!-- vue 2 에서 에러. vue 3에서도 권장하지 않음 태그 계층 주의 --->
  <template>
    <h1></h1>
    <p></p>
  </template>

  <!-- 맞는 표기 --->
  <template>
    <div>
      <h1></h1>
      <p></p>
    </div>
  </template>
  ```

- 스타일 태그
  ```jsx
  <style scoped></style>
  ```
  - style scoped는 해당 화면에서만의 스타일 적용을 위한 태그이다. 전체적으로 적용하고 싶다면 scoped 를 빼주면 된다.
- Vue 의 엄청난 장점은, HTML / CSS / JS 를 전부 완벽하게 분리하여 관리할 수 있다는 것이다.
  ```jsx
  <template> html 태그가 들어가는 부분 </template>
  <script> 스크립트가 들어가는 부분 </script>
  <style scoped> 스타일이 들어가는 부분 </style>
  ```

### databinding string

`vue > project > src > views > 1_databinding(생성) > DataBindingStringView.vue(생성)`

```jsx
<template>
    <div>
        <h1>Hello {{ userName }}</h1>
        <p>{{message}}</p>
    </div>
</template>
<script>
export default {
  data() {
    return {
      userName: 'M-ur-phy',
      message: 'Welcome Vue world',
      arr: [],
      obj: {}
    }
  }
}
</script>
```

`vue > project > src > router > index.js`

```jsx
import { createRouter, createWebHistory } from "vue-router";
import HomeView from "../views/HomeView.vue";

const routes = [
  {
    path: "/",
    name: "home",
    component: HomeView,
  },
  {
    path: "/about",
    name: "about",
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () =>
      import(/* webpackChunkName: "about" */ "../views/AboutView.vue"),
  },
  {
    path: "/databinding/string",
    name: "DataBindingStringView",
    component: () =>
      import(
        /* webpackChunkName: "databinding", webpackPrefetch:true */ "../views/1_databinding/DataBindingStringView.vue"
      ),
  },
];

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes,
});

export default router;
```

- databinding 용 객체 하나 더 추가

로컬호스트 주소창에서

```jsx
http://localhost:8080/databinding/string
```

을 치면

![스크린샷 2022-12-04 오후 3.21.12.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d09fe90e-b867-452b-a8d0-4b9648ababfe/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-12-04_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_3.21.12.png)

이런 화면을 볼 수 있다.

### vue user snippet 등록하기

- vsCode 기어 모양 클릭 → 사용자 조각 (user-snippet) 클릭 → vue 검색 → vue.json or vue 클릭

```jsx
"Generate Basic Vue Code": {
		"prefix": "vue-start",
		"body": [
			"<template>\n\t<div></div>\n</template>\n<script>\nexport default {\n\tcomponents: {},\n\tdata() {\n\t\treturn {\n\t\t\tsampleData: ''\n\t\t}\n\t},\n\tsetup() {},\n\tcreated() {},\n\tmounted() {},\n\tunmounted() {},\n\tmethods:{}\n}\n</script>"
		],
		"description": "Generate Basic Vue Code"
	}
```

- 붙여넣기 후 저장
- vue 파일에서 vue-start snippet 실행

```jsx
<template>
    <div></div>
</template>
<script>
export default {
    components: {},
    data() {
        return {
            sampleData: ''
        }
    },
    setup() {},
    created() {},
    mounted() {},
    unmounted() {},
    methods:{}
}
</script>
```

- 다음과 같이 작성된다.

### databinding html

`vue > project > src > views > 1_databinding > DataBindingHtmlView.vue(생성)`

```jsx
<template>
    <div>
        <div>{{ htmlString }}</div>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      htmlString: '<p style="color:red;">빨간색 문자</p>'
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

`vue > project > src > router > index.js`

```jsx
{
    path: '/databinding/string',
    name: 'DataBindingStringView',
    component: () => import(/* webpackChunkName: "databinding", webpackPrefetch:true */ '../views/1_databinding/DataBindingStringView.vue')
  },
  {
    path: '/databinding/html',
    name: 'DataBindingHtmlView',
    component: () => import(/* webpackChunkName: "databinding", webpackPrefetch:true */ '../views/1_databinding/DataBindingHtmlView.vue')
  }
```

- 다음과 같이 databinding html 버전 객체를 추가해준다. import 부분에 webpackChunkName 이 “databinding”으로 동일하기 때문에 어떤것을 먼저 불러도 같이 로딩된다.
- 즉 연관성 있는 내용이라면 wbpackCunkName 을 동일하게 해주는 것이 효율적이다.

`vue > project > src > App.vue`

- 아래와 같이 nav 를 추가해주면 된다.

```jsx
<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
    <router-link to="/databinding/string">String</router-link>
    <router-link to="/databinding/html">Html</router-link>
  </nav>
  <router-view />
</template>
```

- html 자체로 (innerHTML) 을 하는 방법은 v-html

```jsx
<template>
  <div>
    <div>{{ htmlString }}</div>
    <div v-html="htmlString"></div>
  </div>
</template>
```

여기까지가 단방향 데이터 바인딩이다

---

### 양방향 데이터 바인딩 (input 이용)

`vue > project > src > views > 1_databinding > DataBindingInputView.vue(생성)`

```jsx
<template>
    <div>
        <input type="text" v-model="userId" />
        <button @click="myFunction">클릭</button>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      userId: 'murphy.go'
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    myFunction() {
      console.log(this.userId)
    }
  }
}
</script>
```

- v-model

  - 양방향 데이터 바인딩 디렉티브
  - 실시간으로 바뀌어서 적용된다.

- 함수
  ```jsx
  methods: {
      myFunction() {
        console.log(this.userId)
      }
    }
  ```
  - function 을 쓰지 않는다.

ex) 숫자 처리 예제

```jsx
<template>
    <div>
        <input type="text" v-model="userId">
        <button @click="myFunction">클릭</button>
        <button @click="changeData">클릭</button>
        <br>
        <input type="text" v-model="num1"> +
        <input type="text" v-model="num2"> =
        <span>{{ num1 + num2 }}</span>
        <br>
        <input type="text" v-model.number="num3"> +
        <input type="text" v-model.number="num4"> =
        <span>{{ num3 + num4 }}</span>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      userId: 'murphy.go',
      num1: 0,
      num2: 0,
      num3: 0,
      num4: 0
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    myFunction() {
      console.log(this.userId)
    },
    changeData() {
      this.userId = 'happy.go'
    }
  }
}
</script>
```

- 숫자 처리 시 `.number` 함수를 이용해주어야한다.

### select

`vue > project > src > views > 1_databinding > DataBindingSelectView.vue(생성)`

```jsx
<template>
    <div>
        <select name="" id="" v-model="selectedCity">
            <option value=""></option>
            <option value="02">서울</option>
            <option value="051">부산</option>
            <option value="064">제주</option>
        </select>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      selectedCity: '02'
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

`router > index.js`

```jsx
{
    path: '/databinding/select',
    name: 'DataBindingSelectView',
    component: () => import(/* webpackChunkName: "databinding", webpackPrefetch:true */ '../views/1_databinding/DataBindingSelectView.vue')
  }
```

- select 또한 양방향 데이터 바인딩이 가능하다.

### checkbox

`vue > project > src > views > 1_databinding > DataBindingCheckboxView.vue(생성)`

```jsx
<template>
    <div>
        <div>
            <input type="checkbox" name="" id="html" value="html" v-model="favoriteLang">
            <label for="html">HTML</label>
        </div>
        <div>
            <input type="checkbox" name="" id="css" value="css" v-model="favoriteLang">
            <label for="css">CSS</label>
        </div>
        <div>
            <input type="checkbox" name="" id="js" value="js" v-model="favoriteLang">
            <label for="js">JS</label>
        </div>
        <div>선택한 지역:{{favoriteLang}}</div>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      favoriteLang: ['js']
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

- checkbox 는 data() 를 배열로 받아준다!

`router > index.js`

```jsx
{
    path: '/databinding/select',
    name: 'DataBindingSelectView',
    component: () => import(/* webpackChunkName: "databinding", webpackPrefetch:true */ '../views/1_databinding/DataBindingSelectView.vue')
  }
```

### radio

```jsx
<template>
    <div>
        <div>
            <input type="radio" name="" id="html" value="html" v-model="favoriteLang">
            <label for="html">HTML</label>
        </div>
        <div>
            <input type="radio" name="" id="css" value="css" v-model="favoriteLang">
            <label for="css">CSS</label>
        </div>
        <div>
            <input type="radio" name="" id="js" value="js" v-model="favoriteLang">
            <label for="js">JS</label>
        </div>
        <div>선택한 지역:{{favoriteLang}}</div>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      favoriteLang: ''
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

- radio 는 checkbox 와 달리 일반 문자열로 받는다.`vue > project > src > views > 1_databinding > DataBindingCheckboxView.vue(생성)`

라우터에 radio 이름만 바꿔서 동일하게 추가

### Attribute

- `v-bind:value=”userId”`
- 태그의 속성을 건드리는 방법!

```jsx
<template>
    <div>
        <input type="text" name="" id="" v-bind:value="userId" readonly>
        <input type="text" name="" id="" :value="userId" readonly>
        <br>
        <img :src="imgSrc" alt="" style="width: 100px; height: auto;">
        <br>
        <input type="search" name="" id="" v-model="txt1">
        <button :disabled="txt1 === ''">조회</button>
    </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      userId: 'happy',
      imgSrc: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/1184px-Vue.js_Logo_2.svg.png'
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

### List

```jsx
<template>
  <div>
    <div>
      <select name="" id="">
        <option value=""></option>
        <option :value="city.code" :key="city.code" v-for="city in cities">
          {{ city.title }}
        </option>
      </select>
    </div>
    <div>
      <table>
        <thead>
          <tr>
            <th>제품번호</th>
            <th>제품명</th>
            <th>가격</th>
            <th>합계</th>
            <th>주문수량</th>
          </tr>
        </thead>
        <tbody>
          <tr :key="drink.drinkId" v-for="drink in drinkList">
            <td>{{ drink.drinkId }}</td>
            <td>{{ drink.drinkName }}</td>
            <td>{{ drink.price }}</td>
            <td><input type="number" name="" id="" v-model="drink.qty" /></td>
            <td>{{ drink.price * drink.qty }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      cities: [
        { title: '서울', code: '02' },
        { title: '부산', code: '051' },
        { title: '제주', code: '064' }
      ],
      drinkList: [
        {
          drinkId: '1',
          drinkName: '코카콜라',
          price: 700,
          qty: 1
        },
        {
          drinkId: '2',
          drinkName: '코카dd콜라',
          price: 80,
          qty: 1
        },
        {
          drinkId: '3',
          drinkName: 'ㅇㅇ',
          price: 280,
          qty: 1
        }
      ]
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

- v-for 을 사용할때는 꼭!!!! key!!!!!!!! 를!!!!!!!

### class

```jsx
<template>
  <div>
    <div :class="{ 'text-red': hasError, active: isActive }">클래스 바인딩</div>
    <div :class="class2">클래스 바인딩2</div>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      isActive: false,
      hasError: false,
      class2: ['active', 'hasError']
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
<style scoped>
.active {
  background-color: greenyellow;
  font-weight: bold;
}
.text-red {
  color: red;
}
</style>
```

- hasError 에 false 를 넣어두고, 조건을 주었을 때 true 로 바꾸면 바로바로 적용할 수 있다.

### style

```jsx
<template>
  <div>
    <div style="color: red; font-size: 30px">
      스타일 바인딩: 글씨는 red, 폰트크기: 30px
    </div>
    <div :style="style1">스타일 바인딩: 글씨는 green, 폰트크기: 30px</div>
    <button @click="style1.color = 'blue'">색상바꾸기</button>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      style1: {
        color: 'green',
        fontSize: '30px' // - 대신에 낙타등표기법으로
      }
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {}
}
</script>
```

- style 은 object(객체) 로!

---

## event

### click

```jsx
<template>
  <div>
    <button @click="increaseCounter">Add 1</button>
    <p>{{ counter }}</p>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      counter: 0
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    increaseCounter() {
      this.counter += 1
    }
  }
}
</script>
```

- counter 늘리기

### change

```jsx
<template>
  <div>
    <select name="" id="" @change="changeCity($event)" v-model="selectedCity">
      <option value="">==도시선택==</option>
      <option :value="city.code" :key="city.code" v-for="city in cityList">
        {{ city.title }}
      </option>
    </select>
    <select name="" id="">
      <option
        :value="dong.dongCode"
        :key="dong.dongCode"
        v-for="dong in selectedDongList"
      >
        {{ dong.dongTitle }}
      </option>
    </select>
    <!-- <select name="" id="">
      <option
        :value="dong.dongCode"
        :key="dong.dongCode"
        v-for="dong in this.dongList.filter(
          (dong) => dong.cityCode === this.selectedCity
        )"
      >
        {{ dong.dongTitle }}
      </option>
    </select> -->
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      selectedCity: '',
      cityList: [
        { code: '02', title: '서울' },
        { code: '051', title: '부산' },
        { code: '054', title: '제주' }
      ],
      dongList: [
        {
          cityCode: '02',
          dongCode: '1',
          dongTitle: '서울 1동'
        },
        {
          cityCode: '02',
          dongCode: '2',
          dongTitle: '서울 2동'
        },
        {
          cityCode: '02',
          dongCode: '3',
          dongTitle: '서울 3동'
        },
        {
          cityCode: '02',
          dongCode: '4',
          dongTitle: '서울 4동'
        },
        {
          cityCode: '051',
          dongCode: '1',
          dongTitle: '부산 1동'
        },
        {
          cityCode: '051',
          dongCode: '2',
          dongTitle: '부산 2동'
        },
        {
          cityCode: '051',
          dongCode: '3',
          dongTitle: '부산 3동'
        },
        {
          cityCode: '054',
          dongCode: '1',
          dongTitle: '제주 1동'
        },
        {
          cityCode: '054',
          dongCode: '2',
          dongTitle: '제주 2동'
        }
      ],
      selectedDongList: []
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    changeCity(event) {
      console.log(event.target.tagName) // event 받아오기
      this.selectedDongList = this.dongList.filter(
        (dong) => dong.cityCode === this.selectedCity
      )
    }
  }
}
</script>
```

- 도시 번호에 따라서 맞추어 정보를 제공하는 예제
- 주석 표시처럼 vue 는 자유롭게 v-for에 그냥.. 함수 기능을 가져다 넣을 수도 있다. 하지만 가독성 측면에서는 추천하지 않는다.
- 이해하기 좋았던 예제

### key

```jsx
<template>
  <div>
    <!-- <input
      type="search"
      name=""
      id=""
      @keyup="checkEnter($event)"
      v-model="searchText"
    /> -->
    <input
      type="search"
      name=""
      id=""
      @keyup.enter="doSearch"
      v-model="searchText"
    />
    <button @click="doSearch">조회</button>
    <button type="submit" @click.prevent="doSearch"></button>
  </div>
</template>
<script>
// .enter
// .tab
// .delete
// .esc
// .space
// .up
// .down
// .left
// .right
// ... etc
// .stop - event.stopPropagation();
// .prevent - event.preventDefault();
export default {
  components: {},
  data() {
    return {
      searchText: ''
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    doSearch() {
      console.log(this.searchText)
    },
    checkEnter(event) {
      if (event.keyCode === 13) {
        this.doSearch()
      }
    }
  }
}
</script>
```

- event 내에서 key 즉 키보드 키를 사용해서 제어할수 있는 부분이다.
- stop 과 e.preventDefault 도 가능하다!!!
