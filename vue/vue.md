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

component: () => import(/* webpackChunkName: "about", webpackPrefetch:true */ '../views/AboutView.vue')
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
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  },
  {
    path: '/databinding/string',
    name: 'DataBindingStringView',
    component: () => import(/* webpackChunkName: "databinding", webpackPrefetch:true */ '../views/1_databinding/DataBindingStringView.vue')
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router
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
  <router-view/>
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