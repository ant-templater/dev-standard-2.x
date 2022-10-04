<h1>Vue2.x 开发规范</h1>



<!-- 项目指南 -->
<h2># 项目指南</h2>

<details>
<summary>项目依赖</summary>

```bash
  # 本地初始化 项目
  yarn init
  yarn init -yes

  # 本地安装 package.json 依赖包
  yarn install

  # 全局安装 某个依赖包
  yarn add -g [package]
  yarn add -g [package]@[tag]
  yarn add -g [package]@[version]

  # 本地安装 仅编译环境所需 依赖包
  yarn add -D [package]
  yarn add -D [package]@[tag]
  yarn add -D [package]@[version]

  # 本地安装 编译及生产环境所需 依赖包
  yarn add [package]
  yarn add [package]@[tag]
  yarn add [package]@[version]

  # 本地升级 某个依赖包
  yarn upgrade [package]
  yarn upgrade [package]@[tag]
  yarn upgrade [package]@[version]


  # 本地移除 某个依赖包
  yarn remove [package]

  # 本地检查 依赖包情况
  # <red>    : Major Update backward-incompatible updates --- (不建议更新)
  # <yellow> : Minor Update backward-compatible features ---- (可以更新)
  # <green>  : Patch Update backward-compatible bug fixes --- (建议更新)
  yarn outdated

  # 本地更新 一键按需升级
  # Press <space> to select ----------------------- (空格切换选中)
  # Press <a> to toggle all ----------------------- (所有依赖选中)
  # Press <i> to invert selection ----------------- (所有依赖反选)
  # Press <Enter> install selected dependencies --- (所选依赖安装)
  yarn upgrade-interactive --latest
```

</details>

<details>
<summary>项目结构</summary>

```bash
  ├── .vscode                              # 编辑器配置
  │   ├── settings.json                    # 项目设置文件, 统一格式化、风格等
  │
  ├── dist                                 # 编译后代码
  ├── node_modules                         # yarn 本地依赖包
  │
  ├── config                               # 编译配置
  │   ├── themePluginConfig.js             # 示例: 主题风格系列
  │   ├── webpackPluginConfig.js           # 示例: 更换主题风格(webpack)
  │
  ├── public                               # 静态资源（不参与编译）
  │   ├── index.html                       # webpack 编译时所使用的 html 模版文件
  │   ├── logo.png                         # html 模版文件所引用的 logo 图片
  │
  ├── src                                  # 源代码
  │   ├── api                              # 定义与后端交互的接口
  │   │   ├── user.js                      # 示例: 规范1 - 文件名 根据后台接口 (如/user/add 定义user)
  │   │   ├── auth.js                      # 示例: 规范2 - 文件名【 camelCase 】命名
  │   │
  │   ├── assets                           # 静态资源
  │   │   ├── grid_icon                    # 示例: 规范1 - 分组名 根据内容进行文件夹
  │   │   │   ├── grid_app.png             # 示例: 规范2 - 文件名【 kebab_case 】命名
  │   │
  │   ├── components                       # 公共组件
  │   │   ├── BaseSearchQuery              # 示例: 建议1 - 文件名 以类型化单词开头 (如 Base)
  │   │   ├── BaseIconSelect               # 示例: 规范1 - 文件名 应倾向于完整单词而不是缩写
  │   │   ├── BaseSvgIcon                  # 示例: 规范2 - 文件名【 PascalCase 】命名
  │   │
  │   ├── config                           # 默认配置
  │   │   ├── defaultSettings.js           # 示例: 规范1 - 文件名 应倾于完整语义, 建议【 default + 类型 】
  │   │   ├── defaultRouter.js             # 示例: 规范2 - 文件名【 camelCase 】命名
  │   │
  │   ├── core                             # 核心依赖初始化
  │   │   ├── action                       # 示例: 初始化 权限指令
  │   │   ├── bootstrap                    # 示例: 初始化 个性化
  │   │   ├── module                       # 示例: 懒加载 Ant Design Vue
  │   │   ├── moment                       # 示例: 初始化 moment
  │   │   ├── storage                      # 示例: 初始化 vue-ls
  │   │   ├── index.js                     # 示例: 引入 action、bootstrap...等上述文件
  │   │
  │   ├── filters                          # 全局过滤器
  │   │   ├── filterDateFormat.js          # 示例: 规范1 - 文件名 语义明了而精简, 建议【 filter + 方法名 】
  │   │   ├── filterTimeFormat.js          # 示例: 规范2 - 文件名【 camelCase 】命名
  │   │
  │   ├── layouts                          # 布局组件
  │   │   ├── components                   # 说明: 储存仅布局组件依赖的组件
  │   │   │   ├── BasicLayout              # 示例: 规范1 - 组件库 以相应 .vue 文件名建立
  │   │   │   │   ├── LayoutLogo           # 示例: 规范2 - 文件名 应倾向于完整单词而不是缩写
  │   │   │                                #
  │   │   ├── BasicLayout.vue              # 示例: 规范3 - 文件名【 PascalCase 】命名
  │   │
  │   ├── mixins                           # 混入配置
  │   │   ├── mixinApp.js                  # 示例: 规范1 - 文件名 命名语义明了而精简, 建议【 mixin + 方法名 】
  │   │   ├── mixinUser.js                 # 示例: 规范2 - 文件名【 camelCase 】命名
  │   │
  │   ├── mock                             # 模拟数据交互 -（规范与api保持一致）
  │   │   ├── user                         # 示例: 用户接口
  │   │   │   ├── addUser.js               # 示例: 用户接口 - 新增
  │   │   │   ├── queryUser.js             # 示例: 用户接口 - 查询
  │   │
  │   ├── router                           # 动态路由处理
  │   │   ├── generatorRouters.js          # 示例: 规范1 - 文件名【 camelCase 】命名
  │   │
  │   ├── store                            # vuex 储存配置
  │   │   ├── modules                      # 说明: 全局状态模块化定义
  │   │   │   ├── user.js                  # 示例:
  │   │   │   ├── system.js                # 示例:
  │   │   │                                #
  │   │   ├── variable                     # 说明: 全局常量模块化定义
  │   │   │   ├── system.js                # 示例:
  │   │   │                                #
  │   │   ├── variable.js                  # 说明: 引入全局常量模块
  │   │   ├── index.js                     # 说明: 初始化vuex实例
  │   │
  │   ├── styles                           # 公共样式
  │   │   ├── normalize.less               # 示例: 规范1 - 文件名 样式名应倾向于完整单词而不是缩写
  │   │   ├── variable.less                # 示例: 规范2 - 文件名【 kebab_case 】
  │   │
  │   ├── themes                           # 主题样式
  │   │   ├── theme_dark.less              # 示例: 规范1 - 文件名 样式名应倾向于完整单词而不是缩写
  │   │   ├── theme_light.less             # 示例: 规范2 - 文件名【 kebab_case 】
  │   │
  │   ├── utils                            # 工具类方法
  │   │   ├── request.js                   # 示例: 规范1 - 文件名 命名语义明了而精简
  │   │   ├── util.js                      # 示例: 规范2 - 文件名【 camelCase 】命名
  │   │
  │   ├── views                            # 路由组件
  │   │   ├── system                       # 示例: 菜单栏/系统管理
  │   │   │   ├── components               # 示例:
  │   │   │   │   ├── UserManage           # 示例: 规范1 - 组件库 以相应 .vue 文件名建立
  │   │   │   │   │   ├── UserTable.vue    # 示例: 规范2 - 文件名【 PascalCase 】命名
  │   │   │   │                            #
  │   │   │   ├── UserManage.vue           # 示例:
  │   │
  │   ├── App.vue                          # 顶层路由组件
  │   ├── main.js                          # 程序入口文件
  │   ├── main.less                        # 样式入口文件
  │   ├── permission.js                    # 路由权限文件
  │   ├── register.component.js            # 注册全局组件
  │   ├── router.constant.js               # 配置静态路由组件
  │   ├── router.dynamic.js                # 注入动态路由组件
  │   ├── router.js                        # 初始化 Router 实例
  │   ├── store.js                         # 动态注册 Store 模块
  │
  ├── .browserslistrc                      # 指定项目的浏览器范围
  ├── .editorconfig                        # 指定项目的编码规范
  ├── .env.development                     # 本地开发环境配置, 会覆盖 .env 文件同名属性配置
  ├── .env.production                      # 正式运行环境配置, 会覆盖 .env 文件同名属性配置
  ├── .env.test                            # 测试运行环境配置, 会覆盖 .env 文件同名属性配置
  ├── .env                                 # 默认基础环境配置
  ├── .eslintignore                        # 指定 eslint 哪些文件不需要校验
  ├── .eslintrc.js                         # 指定 eslint 校验的规则配置
  ├── .gitattributes                       # 指定由 git 使用的文件和路径的属性
  ├── .gitignore                           # 指定 git 哪些文件不需要添加到版本管理中
  ├── .prettierignore                      # 指定 prettier 哪些文件不需要校验
  ├── .prettierrc.js                       # 指定 prettier 格式的规则配置
  ├── babel.config.js                      # 指定 babel 编译的相关配置
  ├── jsconfig.json                        # 指定 rootDir 和 JavaScript 服务提供的功能选项
  ├── package.json                         # 项目模块描述文件
  ├── README.md                            # 项目介绍文件
  ├── vue.config.js                        # @vue/cli 的可选配置, 会被 @vue/cli-service 自动加载
  ├── yarn.lock                            # 记录 yarn 依赖项更多信息，如准确存储每个依赖项安装版本
```

</details>



<!-- 注释规范 -->
<h2># 注释规范</h2>

<details>
<summary>文档注释 -- 常用于文件的摘要描述</summary>

```html
  <!--
    * @file 404 页面
    * @author lin pengteng
    * @date 2022-01-14
    * @lastModifiedBy
    * @lastModifiedDate
  -->
  <template>
    <a-result title="404页面">
      <template #extra>
        <a-button>返回首页</a-button>
      </template>
    </a-result>
  </template>
```

```js
  import T from 'ant-design-vue/es/table/Table'

  /**
   * @file 表格组件
   * @author lin pengteng
   * @date 2022-01-14
   * @lastModifiedBy
   * @lastModifiedDate
   */
  export default {
    name: 'BaseTable',
    props: {
      ...T.props
    },
    data() {
      // ...
    },
    method: {
      // ...
    }
  }
```

```css
  /**
  * @file 规范标签默认样式
  * @author lin pengteng
  * @date 2022-01-14
  * @lastModifiedBy
  * @lastModifiedDate
  */
  html,
  body,
  #app,
  #root {
    height: 100%;
  }
```

</details>

<details>
<summary>方法注释 -- 常用于函数的摘要描述</summary>

```js
  import moment from 'moment'

  /**
   * @description 根据格式转换 日期
   * @author lin pengteng
   * @date 2022-01-14
   * @lastModifiedBy
   * @lastModifiedDate
   *
   * @param {Date | String | Number} date
   * @param {String} format?
   * @return {Moment | null}
   */
  export const takeTimeToDate = (date, format) => {
    if (date) {
      try {
        return moment(date, format)
      } catch {}
    }
    return null
  }
```

</details>

<details>
<summary>多行注释 -- 常用于字段、逻辑、注解等多行描述</summary>

```js
  /* 
    这是一个临时储存区
    记录用户操作过的用户ID
  */
  const CACHES = []
```

</details>

<details>
<summary>单行注释 -- 常用于字段、逻辑、注解等单行描述</summary>

```js
  export default {
    name: 'CustomButton',
    props: {
      // 按钮图标
      icon: {
        type: String,
        default: 'filter'
      },
      // 按钮类型
      type: {
        type: String,
        default: 'default'
      }
    }
  }
```

</details>



<!-- Vue2.x 规范 -->
<h2># Vue 规范</h2>

<details>
<summary>组件顶级元素的顺序 <sup style="color: #f34d4d;">(必要)</sup></summary>

- `template`、`script` 和 `style` 顺序必须一致，之间空一行隔开

  ```html
    <template>
      <section class="container">
        <a-button>自定义</a-button>
      </section>
    </template>

    <script>
      export default {
        name: 'CustomButton'
      }
    </script>

    <style scoped>
      .container {
        width: 100%;
        height: auto;
      }
    </style>
  ```

</details>

<details>
<summary>组件名由多个单词组成 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 这样做可以避免跟现有的以及未来的 HTML 元素相冲突，因为所有的 HTML 元素名称都是单个单词的

  ```javascript
    // Bad
    export default {
      name: 'Todo'
      // ...
    }

    // Good
    export default {
      name: 'TodoItem'
      // ...
    }
  ```

</details>

<details>
<summary>组件名应为完整单词而非缩写 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 编辑器中自动补全已经让书写长命名的代价非常之低，而其带来的明确性却是非常宝贵的

  ```bash
    # Bad
    components/
      |- SdSettings.vue
      |- UProfOpts.vue

    # Good
    components/
      |- StudentDashboardSettings.vue
      |- UserProfileOptions.vue
  ```

</details>

<details>
<summary>组件名中单词顺序按语境排序 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 组件名应该以高级别的(通常是一般化描述的)单词开头，以描述性的修饰词结尾，组件间排序关系一目了然

  ```bash
    # Bad
    components/
      |- ClearSearchButton.vue
      |- RunSearchButton.vue

    # Good
    components/
      |- SearchButtonClear.vue
      |- SearchButtonRun.vue
  ```

</details>

<details>
<summary>高耦合子组件名以父组件名为前缀 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 如果一个组件只在某个父组件的场景下有意义，这层关系应该体现在其名字上

  ```bash
    # Bad
    components/
      |- TodoList.vue
      |- TodoItem.vue
      |- TodoButton.vue

    # Good
    components/
      |- TodoList.vue
      |- TodoListItem.vue
      |- TodoListItemButton.vue
  ```

</details>

<details>
<summary>单文件组件文件名应 PascalCase 命名 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 单文件组件的文件名应该始终是单词大写开头 PascalCase

  ```bash
    # Bad
    components/
      |- mycomponent1.vue
      |- myComponent2.vue
      |- Mycomponent3.vue
      |- my-component4.vue

    # Good
    components/
      |- MyComponent1.vue
      |- MyComponent2.vue
      |- MyComponent3.vue
      |- MyComponent4.vue
  ```

</details>

<details>
<summary>.vue 单文件模板应该只包含简单的表达式 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 组件模板应该只包含简单的表达式，复杂的表达式则应该重构为计算属性或方法

  ```html
    <!-- Bad -->
    <template>
      <div class="container">
        {{
          fullName.split(' ').map(function (word) {
            return word[0].toUpperCase() + word.slice(1)
          }).join(' ')
        }}
      </div>
    </template>

    <script>
      export default {
        name: 'Todo',
        data() {
          return {
            fullName: 'todo component'
          }
        }
      }
    </script>

    <!-- Good -->
    <template>
      <div class="container">
        {{ computedFullName }}
      </div>
    </template>

    <script>
      export default {
        name: 'Todo',
        data() {
          return {
            fullName: 'todo component'
          }
        },
        computed: {
          computedFullName: function () {
            return this.fullName.split(' ').map(function (word) {
              return word[0].toUpperCase() + word.slice(1)
            }).join(' ')
          }
        }
      }
    </script>
  ```

</details>

<details>
<summary>.vue 单文件的自闭合组件应省略闭合标签 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 自闭合组件表示它们不仅没有内容，没有了额外的闭合标签，代码也更简洁

  ```html
    <!-- Bad -->
    <template>
      <my-component></my-component>
    </template>

    <!-- Good -->
    <template>
      <my-component/>
    </template>
  ```

</details>

<details>
<summary>.html 文件的自闭合组件不能省略闭合标签 <sup style="color: #f34d4d;">(必要)</sup></summary>

- HTML 并不支持自闭合的自定义元素——只有官方的“空”元素

  ```html
    <!-- Bad -->
    <body>
      <div/>
    </body>

    <!-- Good -->
    <body>
      <div></div>
    </body>
  ```

</details>

<details>
<summary>.vue 单文件的组件以 kebab-case 方式引用  <sup style="color: #f34d4d;">(必要)</sup></summary>

- 采用 DOM Element 风格，同时避免跟现有的以及未来的 HTML 元素相冲突

  ```html
    <!-- Bad -->
    <template>
      <ToComponent/>
    </template>

    <script>
      import ToComponent from 'ToComponent'

      export default {
        name: 'Todo',
        components: {
          ToComponent
        }
      }
    </script>

    <!-- Good -->
    <template>
      <to-component/>
    </template>

    <script>
      import ToComponent from 'ToComponent'

      export default {
        name: 'Todo',
        components: {
          ToComponent
        }
      }
    </script>
  ```

</details>

<details>
<summary>.jsx? 文件的组件以 PascalCase 方式使用  <sup style="color: #f34d4d;">(必要)</sup></summary>

- 使得代码的读者更容易分辨 Vue 组件和 HTML 元素

  ```javascript
    import ToComponent from 'ToComponent'

    // Bad
    export const Component1 = {
      name: 'Todo',
      render () {
        return <to-component>
      }
    }

    // Good
    export const Component2 = {
      name: 'Todo',
      render () {
        return <ToComponent>
      }
    }
  ```

</details>

<details>
<summary>组件多个 attribute 应该分多行撰写 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 组件多个 attribute 元素每个一行，更具可读性

  ```html
    <!-- Bad -->
    <template>
      <my-component foo="a" bar="b" baz="c"/>
    </template>

    <!-- Good -->
    <template>
      <my-component 
        foo="a" 
        bar="b" 
        baz="c"
      />
    </template>
  ```

</details>

<details>
<summary>组件的 data 必须是一个函数 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 避免多个实例组件使用中因 data property 共享，导致组件状态混乱

  ```javascript
    // Bad
    export default {
      data: {
        foo: 'bar'
      }
    }

    // Good
    export default {
      data () {
        return {
          foo: 'bar'
        }
      }
    }
  ```

</details>

<details>
<summary>组件的 Prop 定义尽量详细 <sup style="color: #f34d4d;">(必要)</sup></summary>

- prop 定义尽量详细，至少需要指定类型，如果提供不正确的 prop，Vue 会帮助你捕获错误

  ```javascript
    // Bad
    export default {
      props: ['status']
    }

    // Good
    export default {
      props: {
        status: {
          type: String,
          default: ''
        }
      }
    }
  ```

</details>

<details>
<summary>组件的 Prop 名应为驼峰式 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 在声明 prop 及 模板和 JSX 使用时，其命名应使用 camelCase

  ```html
    <!-- Bad -->
    <template>
      <welcome-message :greeting-text="greetingText" />
    </template>

    <script>
    export default {
      name: 'WelcomeMessage',
      props: {
        'greeting-text': {
          type: String,
          default: ''
        }
      }
    }
    </script>

    <!-- Good -->
    <template>
      <welcome-message :greetingText="greetingText" />
    </template>

    <script>
    export default {
      name: 'WelcomeMessage',
      props: {
        greetingText: {
          type: String,
          default: ''
        }
      }
    }
    </script>
  ```

</details>

<details>
<summary>避免将 v-if 和 v-for 用在一起 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 为了不渲染本应该隐藏的列表, 则可将 v-if 移动至其父容器元素上

  ```html
    <!-- Bad -->
    <ul>
      <li 
        v-for="user in users" 
        v-if="shouldShowUsers" 
        :key="user.id"
      >{{ user.name }}</li>
    </ul>

    <!-- Good -->
    <ul v-if="shouldShowUsers">
      <li 
        v-for="user in users" 
        :key="user.id"
      >{{ user.name }}</li>
    </ul>
  ```

- 根据某属性过滤列表中的项目, 则可替换为一个计算属性, 让其返回过滤后的列表

  ```html
    <!-- Bad -->
    <ul>
      <li 
        v-for="user in users" 
        v-if="user.isActive" 
        :key="user.id"
      >{{ user.name }}</li>
    </ul>

    <!-- Good -->
    <ul>
      <li 
        v-for="user in activeUsers" 
        :key="user.id"
      >{{ user.name }}</li>
    </ul>
  ```

</details>

<details>
<summary>必须为 v-for 设置键值 key <sup style="color: #f34d4d;">(必要)</sup></summary>

- 在组件上总是必须用 key 配合 v-for，以便维护内部组件及其子树的状态

  ```html
    <!-- Bad -->
    <ul>
      <li v-for="todo in todos">{{ todo.text }}</li>
    </ul>

    <!-- Good -->
    <ul>
      <li 
        v-for="todo in todos" 
        :key="todo.id"
      >{{ todo.text }}</li>
    </ul>
  ```

</details>

<details>
<summary>应为组件样式设置作用域 <sup style="color: #f34d4d;">(必要)</sup></summary>

- 基于有作用域的样式可以避免与其他组件的样式发生冲突

  ```html
    <!-- Bad -->
    <template>
      <button class="btn btn-close">X</button>
    </template>

    <style>
      .btn-close {
        background-color: red;
      }
    </style>

    <!-- Good -->
    <template>
      <button class="btn btn-close">X</button>
    </template>

    <style scoped>
      .btn-close {
        background-color: red;
      }
    </style>
  ```

</details>

<details>
<summary>组件/实例各指令采用简写  <sup style="color: #42b983;">(推荐)</sup></summary>

- 用 : 表示 v-bind: ,  @ 表示 v-on: ,  # 表示 v-slot:

  ```html
    <!-- Bad -->
    <template>
      <div class="container">
        <template v-slot:header>
          <h1>A page title</h1>
        </template>
        <input
          v-bind:value="newValue"
          v-on:input="onInput"
        >
      </div>
    </template>

    <!-- Good -->
    <template>
      <div class="container">
        <template #header>
          <h1>A page title</h1>
        </template>
        <input
          :value="newValue"
          @input="onInput"
        >
      </div>
    </template>
  ```

</details>

<details>
<summary>组件/实例的选项顺序 <sup style="color: #42b983;">(推荐)</sup></summary>

- 组件/实例的选项应该有统一的顺序

  ```bash
    # 副作用 (触发组件外的影响)
    el

    # 全局感知 (要求组件以外的知识)
    name
    parent

    # 组件类型 (更改组件的类型)
    functional

    # 模板修改器 (改变模板的编译方式)
    delimiters
    comments

    # 模板依赖 (模板内使用的资源)
    components
    directives
    filters

    # 组合 (向选项里合并 property)
    extends
    mixins

    # 接口 (组件的接口)
    inheritAttrs
    model
    props/propsData

    # 本地状态 (本地的响应式 property)
    data
    computed

    # 监听事件 (通过响应式事件触发的回调)
    watch

    # 生命周期钩子 (按照它们被调用的顺序)
    beforeCreate
    created
    beforeMount
    mounted
    beforeUpdate
    updated
    activated
    deactivated
    beforeDestroy
    destroyed

    # 非响应式的 property
    methods

    # 渲染 (组件输出的声明式描述)
    template/render
    renderError
  ```

</details>

<details>
<summary>组件/实例的属性顺序 <sup style="color: #42b983;">(推荐)</sup></summary>

- 组件/实例的属性应该有统一的顺序

  ```bash
    # 引用 (提供组件的引用)
    is
    id
    ref

    # 双向绑定 (把绑定和事件结合起来)
    v-model

    # 列表渲染 (创建多个变化的相同元素)
    v-for

    # 条件渲染 (元素是否渲染/显示)
    v-if
    v-else-if
    v-else
    v-show
    v-cloak

    # 其他属性 (attribute 或 prop)
    key
    ...

    # 渲染方式 (改变元素的渲染方式)
    v-pre
    v-once
    v-html
    v-text

    # 事件 (组件事件监听器)
    v-on
  ```

</details>



<!-- Git规范 -->
<h2># Git 规范</h2>

<details>
<summary>Git 分支设计 <sup style="color: #42b983;">(推荐)</sup></summary>

- 基于如下四种常用系统开发环境，而设计的 `Git` 五种分支类型
  * PRO 环境：用于生产环境
  * DEV 环境：用于开发者调试使用
  * FAT 环境：功能验收测试环境，用于测试环境下的测试人员测试使用
  * UAT 环境：生产预发布环境，用于生产环境下的测试人员测试使用

  <div style="margin-bottom: 20px"></div>

  |分支|名称|命名规范|运行环境|
  |:---|:---|:---:|:---:|
  |master|主分支|/|PRO|
  |release|预上线分支|/|UAT|
  |develop|测试分支|/|FAT|
  |feature|需求开发分支|feat-xxx|DEV|
  |hotfix|紧急修复分支|fix-xxx|DEV|
    
  ```bash
    # master 分支
    a. master 为主分支，用于部署到正式环境（PRO）
    b. 一般由 release 或 hotfix 分支合并，任何情况下不允许直接在 master 分支上修改代码

    # release 分支
    a. release 为预上线分支，用于部署到预上线环境（UAT）始终保持与 master 分支一致
    b. 一般由 develop 或 hotfix 分支合并，不建议直接在 release 分支上直接修改代码
    c. 如果在 release 分支测试出问题，需要回归验证 develop 分支看否存在此问题

    # develop 分支
    a. develop 为测试分支，用于部署到测试环境（FAT），始终保持最新完成以及 bug 修复后的代码
    b. 可根据需求大小程度确定是由 feature 分支合并，还是直接在上面开发
    c. 一定是满足测试的代码才能往上面合并或提交。

    # feature 分支
    a. feature 为需求开发分支，命名规则为【 feat- 】开头，一旦该需求上线，分支本地预留 3-7 天后将其删除

    # hotfix 分支
    a. hotfix 为紧急修复分支，命名规则为【 fix- 】开头
    b. 当线上出现紧急问题需要马上修复时，需要基于 release 或 master 分支创建 hotfix 分支
    c. 修复完成后，再合并到 release 或 develop 分支，一旦修复上线，分支本地预留 1-3 天后将其删除
  ```

</details>

<details>
<summary>Git 版本号规范 <sup style="color: #42b983;">(推荐)</sup></summary>

- 版本号 Tag 采用三段式，v版本.里程碑.序号，如：v1.0.0
    
  ```bash
    修改第1位 - 架构升级或架构重大调整
    修改第2位 - 新功能上线或者模块大的调整
    修改第3位 - bug修复上线、需求完善等调整
  ```

</details>

<details>
<summary>Git 提交规范 <sup style="color: #f34d4d;">(重要)</sup></summary>

- 目前社区流行的 commit 规范（来自于 Angular 团队的 commit 规范）
    
  ```bash
    # Commit Message 的三个部分：Header，Body 和 Footer, 注意两两之前空行间隔
    <type>(<scope>): <subject>
    <BLANK LINE>
    <body>
    <BLANK LINE>
    <footer>

    # Commit Message 之 Header 部分
    type（必需）--- 用于说明 commit 的类别
      a. init: 初始化
      b. feat: 新增feature
      c. fix: 修复bug
      d. docs: 仅仅修改了文档，如readme.md
      e. style: 仅仅是对格式进行修改，如逗号、缩进、空格等。不改变代码逻辑
      f. refactor: 代码重构，没有新增功能或修复bug
      g. perf: 优化相关，如提升性能、用户体验等
      h. test: 测试用例，包括单元测试、集成测试
      i. chore: 改变构建流程、或者增加依赖库、工具等
      j. revert: 版本回滚
      k. merge：代码合并
      l. sync：同步分支

    scope（可选）--- 用于说明 commit 影响范围，可以通过 src 名下文件夹定义，例如
      a. all or *
      b. api
      c. components
      d. utils
      e. views
      f. ...

    subject（必需）--- commit 内容的简短描述，不超过50个字符


    # Commit Message 之 Body 部分（可选）
    a. 对本次 commit 修改内容的具体描述, 可以分为多行
    b. 描述为什么修改, 做了什么样的修改, 以及开发的思路等等


    # Commit Message 之 footer 部分（可选，仅处理 不兼容 或 关闭 Issue使用）
    a. 处理当前代码与上个版本不兼容, 以 BREAKING CHANGE: 开头进行详细描述
    b. 当前 commit 关闭 issue，如 Closes #123, #245, #992
  ```


- 基于社区流行的 commit Message 示范

  ```bash
    # Commit Message - Header + Body
    init: Vue2.x 开发规范首次提交

    a. 包含了项目指南、注释规范、Vue规范、Git规范
    b. 目前仅支持 Vue2.x, 不兼容 Vue.3.x 


    # Commit Message - 仅 Header
    docs(README.md): Vue2.x 开发规范完善VSCode开发等
  ```

</details>



<!-- VSCode 开发 -->
<h2># VSCode 开发</h2>

<details>
<summary>常用插件推荐</summary>

- 基于功能性分类: Git分支管理、代码智能提示、校验优化代码
    
  ```bash
    # Git分支管理
    name:        GitLens — Git supercharged
    author:      GitKraken
    description: 增强内置的 Git 功能, 一目了然地可视化代码作者身份, 无缝导航和探索 Git 存储库等等
      


    # 代码智能提示
    name:        Vue 3 Snippets
    author:      hollowtree
    description: Vue2.x 和 Vue3.x 代码片段智能提示

    name:        Vue Peek
    author:      Dario Fuzinato
    description: 允许 Vue 单文件组件的 peek 和 goto 定义

    name:        vue-helper
    author:      shenjiaolong
    description: 增强 Vue 文件智能提示，如函数、方法跳转查看



    # 校验优化代码
    name:        ESLint
    author:      Dirk Baeumer
    description: 将 ESLint JavaScript 集成到 VSCode 中
    attention:   需要 yarn install 相关依赖

    name:        Prettier - Code formatter
    author:      Prettier
    description: 使用 prettier 格式化代码
    attention:   需要 yarn install 相关依赖

    name:        Vetur
    author:      Pine Wu
    description: 格式化 vue 单文件组件
  ```

</details>

<details>
<summary>项目开发配置</summary>

- 项目根目录下建立 .vscode/settings.json 文件，统一开发配置
    
  ```json
    {
      "[css]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[less]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[scss]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[stylus]": {
        "editor.defaultFormatter": "thisismanta.stylus-supremacy"
      },
      "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[javascript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
      "[typescript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
      "[jsonc]": {
        "editor.defaultFormatter": "vscode.json-language-features"
      },
      "[json]": {
        "editor.defaultFormatter": "vscode.json-language-features"
      },
      "[vue]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
      },
      "editor.codeActionsOnSave": {
        "source.fixAll": true
      },
      "editor.tabSize": 2,
      "editor.formatOnSave": true,
      "editor.formatOnPaste": true,
      "javascript.format.enable": false,
      "javascript.validate.enable": false,
      "files.exclude": {
        "**/.project": true,
        "**/.settings": true,
        "**/.classpath": true,
        "**/.factorypath": true
      },
      "eslint.format.enable": true,
      "eslint.probe": [
        "javascript",
        "javascriptreact",
        "typescriptreact",
        "typescript",
        "html",
        "vue"
      ],
      "prettier.semi": false,
      "prettier.useTabs": false,
      "prettier.tabWidth": 2,
      "prettier.printWidth": 100,
      "prettier.singleQuote": true,
      "prettier.bracketSpacing": true,
      "prettier.bracketSameLine": false,
      "prettier.jsxSingleQuote": false,
      "prettier.vueIndentScriptAndStyle": false,
      "prettier.htmlWhitespaceSensitivity": "ignore",
      "prettier.quoteProps": "consistent",
      "prettier.arrowParens": "avoid",
      "prettier.trailingComma": "es5",
      "stylusSupremacy.insertColons": true,
      "stylusSupremacy.insertBraces": false,
      "stylusSupremacy.insertSemicolons": false,
      "stylusSupremacy.insertNewLineAroundImports": false,
      "stylusSupremacy.insertNewLineAroundBlocks": false,
      "vetur.format.enable": true,
      "vetur.validation.style": true,
      "vetur.validation.script": true,
      "vetur.validation.template": false,
      "vetur.format.options.tabSize": 2,
      "vetur.format.options.useTabs": false,
      "vetur.format.defaultFormatter.js": "prettier",
      "vetur.format.defaultFormatter.ts": "prettier",
      "vetur.format.defaultFormatter.css": "prettier",
      "vetur.format.defaultFormatter.scss": "prettier",
      "vetur.format.defaultFormatter.less": "prettier",
      "vetur.format.defaultFormatter.postcss": "prettier",
      "vetur.format.defaultFormatter.stylus": "stylus-supremacy",
      "vetur.format.defaultFormatter.html": "prettier",
      "vetur.format.defaultFormatterOptions": {
        "prettier": {
          "semi": false,
          "useTabs": false,
          "tabWidth": 2,
          "printWidth": 100,
          "singleQuote": true,
          "bracketSpacing": true,
          "bracketSameLine": false,
          "jsxSingleQuote": false,
          "vueIndentScriptAndStyle": false,
          "htmlWhitespaceSensitivity": "ignore",
          "quoteProps": "consistent",
          "arrowParens": "avoid",
          "trailingComma": "es5"
        },
        "prettyhtml": {
          "tabWidth": 2,
          "printWidth": 100,
          "singleQuote": false,
          "wrapAttributes": true,
          "sortAttributes": false,
          "usePrettier": true,
          "useTabs": false
        }
      }
    }
  ```

</details>

<details>
<summary>项目脚本指令</summary>

- 命令行 Prettier 一键格式化，需 [.prettierignore](https://github.com/ant-templater/dev-template-vue2.x/blob/main/.prettierignore)、[.prettierrc](https://github.com/ant-templater/dev-template-vue2.x/blob/main/.prettierrc) 配置
    
  ```bash
    npx prettier --write --loglevel warn "src/**/*.vue"
  ```

- 命令行 ESlint 一键校验并格式化，需 [.eslintignore](https://github.com/ant-templater/dev-template-vue2.x/blob/main/.eslintignore)、[.eslintrc.js](https://github.com/ant-templater/dev-template-vue2.x/blob/main/.eslintrc.js) 配置
    
  ```bash
    npx eslint --fix --quiet src --ext .vue,.js
  ```

</details>

