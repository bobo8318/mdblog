* 安装
  
  > cnpm install -g vuepress
  >
  > cnpm i vuepress-init -g
  > vuepress init
  > cd <your project> && npm install
  >
  > npm install vuepress-theme-yubisaki@next --save-dev //install theme
  >
  > npm run dev

* 目录结构

  ```
  .
  ├── docs
  │   ├── .vuepress (可选的)
  │   │   ├── components (可选的)
  │   │   ├── theme (可选的)
  │   │   │   └── Layout.vue
  │   │   ├── public (可选的)
  │   │   ├── styles (可选的)
  │   │   │   ├── index.styl
  │   │   │   └── palette.styl
  │   │   ├── templates (可选的, 谨慎配置)
  │   │   │   ├── dev.html
  │   │   │   └── ssr.html
  │   │   ├── config.js (可选的)
  │   │   └── enhanceApp.js (可选的)
  │   │ 
  │   ├── README.md
  │   ├── guide
  │   │   └── README.md
  │   └── config.md
  │ 
  └── package.json
  
  docs/.vuepress: 用于存放全局的配置、组件、静态资源等。
  docs/.vuepress/components: 该目录中的 Vue 组件将会被自动注册为全局组件。
  docs/.vuepress/theme: 用于存放本地主题。
  docs/.vuepress/styles: 用于存放样式相关的文件。
  docs/.vuepress/styles/index.styl: 将会被自动应用的全局样式文件，会生成在最终的 CSS 文件结尾，具有比默认样式更高的优先级。
  docs/.vuepress/styles/palette.styl: 用于重写默认颜色常量，或者设置新的 stylus 颜色常量。
  docs/.vuepress/public: 静态资源目录。
  docs/.vuepress/templates: 存储 HTML 模板文件。
  docs/.vuepress/templates/dev.html: 用于开发环境的 HTML 模板文件。
  docs/.vuepress/templates/ssr.html: 构建时基于 Vue SSR 的 HTML 模板文件。
  docs/.vuepress/config.js: 配置文件的入口文件，也可以是 YML 或 toml。
  docs/.vuepress/enhanceApp.js: 客户端应用的增强。
  ```

  

* System limit for number of file watchers reached

  > sudo vi /etc/sysctl.conf
  >
  > 在最下添加
  >
  > fs.inotify.max_user_watches=524288
  >
  > 保存退出
  >
  > sudo sysctl -p

* config.js

  ```
  module.exports = {
      //theme: 'vuepress-theme-yilia-plus',//指定此选项来使用自定义主题。使用 “foo” 的值，VuePress 将尝试在 node_modules/vuepress-theme-foo/Layout.vue 加载主题组件
      title: 'HOME', //网站的标题。这将是所有页面标题的前缀，并显示在默认主题的导航栏中
      description: `vuepress blog`,//网站描述。这将在页面 HTML 中表现为一个 <meta> 标签
      head: [
          ['link', { rel: 'icon', href: `/favicon.ico` }]
      ],//被注入页面 HTML <head> 额外的标签。每个标签可以用 [tagName, { attrName: attrValue }, innerHTML?] 的形式指定。例如，要添加自定义图标：
      base: '/blog/',
      port:'8888'
      repo: 'https://github.com/lewiscutey/vuepress-template',
      dest: './docs/.vuepress/dist',//指定 vuepress build 的输出目录
      ga: '',
      serviceWorker: true,//如果设置为 true，VuePress 将自动生成并注册一个 service worker ，这个 worker 将内容缓存以供离线使用（仅在生产环境中启用）。
      evergreen: true,
      themeConfig: {
          background: `/img/`,
          github: 'lewiscutey',
          logo: '/img/logo.png',
          accentColor: '#ac3e40',
          per_page: 6,
          date_format: 'yyyy-MM-dd HH:mm:ss',
          tags: true,
          comment: {
              clientID: '',
              clientSecret: '',
              repo: '',  // blog of repo name
              owner: '',  // github of name
              admin: '', // github of name
              distractionFreeMode: false
          },
          nav: require("./nave"),
          sidebar: require("./sidebar")
      },
      markdown: {
          anchor: {
              permalink: true
          },
          toc: {
              includeLevel: [1, 2]
          },
          config: md => {
              // 使用更多 markdown-it 插件！
              md.use(require('markdown-it-task-lists'))
              .use(require('markdown-it-imsize'), { autofill: true })
          }
      },
      postcss: {
          plugins: [require('autoprefixer')]
      },
  }
  
  
  ```

  * themeConfig

    ```
    nav: [
          {
            text: 'Languages',
            items: [
              { text: 'Chinese', link: '/language/chinese' },
              { text: 'Japanese', link: '/language/japanese' }
            ]
          }
        ]
        
    sidebar: [
          '/',
          '/page-a',
          ['/page-b', 'Explicit link text']
    ]
    你可以省略 .md 扩展名，以 / 结尾的路径被推断为 */README.md 。该链接的文本是自动推断的（从页面的第一个标题或 YAML front matter 中的显式标题）。如果你希望明确指定链接文本，请使用 [link,text] 形式的数组
    themeConfig.sidebarDepth //侧边栏自动显示当前激活页面中标题的链接，嵌套在页面本身的链接下
    sidebarDepth: 2
    sidebar: auto
    ```

    

* Homepage-README.MD

  ```
  ---
  home: true
  heroImage: /hero.png
  actionText: Get Started →
  actionLink: /guide/
  features:
  - title: Simplicity First
    details: Minimal setup with markdown-centered project structure helps you focus on writing.
  - title: Vue-Powered
    details: Enjoy the dev experience of Vue + webpack, use Vue components in markdown, and develop custom themes with Vue.
  - title: Performant
    details: VuePress generates pre-rendered static HTML for each page, and runs as an SPA once a page is loaded.
  footer: MIT Licensed | Copyright © 2018-present Evan You
  ---
  
  ```

  