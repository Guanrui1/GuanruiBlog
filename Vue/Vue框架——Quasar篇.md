![banner-1.jpg](https://i.loli.net/2019/10/17/KRZr1YjuXhe2gJW.jpg)
## Quasar简述
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;作为一个兼容多端到极致的Ui框架，Quasar确实做到了，除了微信小程序，你能想到的所有前端可以做的他都已经做到了，并且都有相应的构建策略和实现方式，最最主要的是这些不同的项目可以做到复用一套代码，在这个科技高速发展的时代，无疑又为我们的前端项目带来了方便和效率。下面我们就几个方面对Quasar进行评测。
<br><br>
### 一、Quasar项目的搭建及主要配置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一如往常，Quasar其本质和vue-cli，mpvue类似，都是一款基于webpack构建的一款可以打包js（主要是vue）的前端构建工具，只不过相比vue-cli只能打包网页，mpvue只能打包小程序（说是以后会支持打包h5），Quasar的功能就显得比较丰富了。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;和vue-cli项目一样，刚开始我们要安装这个脚手架，安装的方式也一样，安装一个全局命令
```
npm install -g @quasar/cli
```
安装失败和报错？那应该是老版本没有卸载，那就应该安装前先执行
```
npm uninstall -g quasar-cli
```
当这个全局命令安装好了之后，我们就可以使用它来构建项目了，这个时候在指定文件夹打开命令行，输入
```
quasar create <folder_name>
```
其中的folder_name其实就是项目名，随便输入即可，命令输入完成后回车，便会自动开始构建，但是会提示一些东西让你选择，基本一路回车即可。
<br><br>
### 二、Quasar项目代码结构分析
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;执行玩上述的命令后，我们就会得到一个像下面一样结构的项目，其中的src就是存放我们业务逻辑代码的地方，也是多端复用最为关键的部分。但是这里需要插一句，就是Quasar的src里居然没有实例化vue对象的那个main.js，可能是Quasar故意这样做的，因为像axios，vuex这些，初始化项目是我们就可以直接选上了，不用自己后续安装，所以如果我们还想自行往Vue实例上绑定对象，那就只能在app.vue这个根组件上动手了。
<br><br>
<pre>
[ '|-- quasar',
  '    |-- .editorconfig',
  '    |-- .eslintignore',
  '    |-- .eslintrc.js',
  '    |-- .gitignore',
  '    |-- .postcssrc.js',
  '    |-- .stylintrc',
  '    |-- babel.config.js',
  '    |-- package.json',
  '    |-- quasar.conf.js',
  '    |-- README.md',
  '    |-- yarn.lock',
  '    |-- src',
  '        |-- App.vue',
  '        |-- index.template.html',
  '        |-- assets',
  '        |   |-- quasar-logo-full.svg',
  '        |   |-- sad.svg',
  '        |-- boot',
  '        |   |-- .gitkeep',
  '        |   |-- axios.js',
  '        |-- components',
  '        |   |-- .gitkeep',
  '        |-- css',
  '        |   |-- app.styl',
  '        |   |-- quasar.variables.styl',
  '        |-- layouts',
  '        |   |-- MyLayout.vue',
  '        |-- pages',
  '        |   |-- Error404.vue',
  '        |   |-- Index.vue',
  '        |-- router',
  '        |   |-- index.js',
  '        |   |-- routes.js',
  '        |-- statics',
  '        |   |-- app-logo-128x128.png',
  '        |   |-- icons',
  '        |       |-- apple-icon-120x120.png',
  '        |       |-- apple-icon-152x152.png',
  '        |       |-- apple-icon-167x167.png',
  '        |       |-- apple-icon-180x180.png',
  '        |       |-- favicon-16x16.png',
  '        |       |-- favicon-32x32.png',
  '        |       |-- favicon-96x96.png',
  '        |       |-- favicon.ico',
  '        |       |-- icon-128x128.png',
  '        |       |-- icon-192x192.png',
  '        |       |-- icon-256x256.png',
  '        |       |-- icon-384x384.png',
  '        |       |-- icon-512x512.png',
  '        |       |-- ms-icon-144x144.png',
  '        |       |-- safari-pinned-tab.svg',
  '        |-- store',
  '            |-- index.js',
  '            |-- module-example',
  '                |-- actions.js',
  '                |-- getters.js',
  '                |-- index.js',
  '                |-- mutations.js',
  '                |-- state.js',
  '' ]
  </pre>
<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当然，除了src文件夹，外部的babel.config.js和quasar.conf.js（注意是conf不是config）很多时候也很重要，毕竟打包的配置就是要靠这两个文件。<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;进入到src文件夹内部，正式上面显示的结构，和vue-cli生成的项目基本没什么区别。这个要重点说下，其中的boot是axios放的地方，也就是网络请求部分，css文件默认用的stylus，但是我们也能换成我们熟悉的sass，官网给出的说法是
![QQ截图20190915100209.png](https://user-gold-cdn.xitu.io/2019/9/15/16d32a8dfc092235?w=785&h=419&f=png&s=45270)
<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;但是，平凡当中却孕育者伟大，正如Quasar官网所说，当使用Quasar时，你不需要像Hammerjs，Momentjs或Bootstrap这样的额外重型库。它拥有这些功能，而且体积很小！对于Bootstrap,想必大家都已经很熟悉了，但是Hammer.js和Moment.js，这两个一听就是js库，
#### Hammer.js
> 1、用于检测触摸手势的 JavaScript库<br>
> 2、添加了对触摸手势的支持并移除了点击的300ms<br>
> 3、还支持最常见的单点和多点触摸手势，并且可以完全扩展以添加自定义手势
#### Moment.js
> Moment.js是一个轻量级的JavaScript时间库，它方便了日常开发中对时间的操作，提高了开发效率。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;所以说，Quasar相比我们之前的vue项目，帮我们省了很多引入三方包的操作，而这些用起来也很简单，直接
``` javascript
import { date } from 'quasar'
const { addToDate } = date
let newDate = addToDate(new Date(), { days: 7, month: 1 })
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Quasar设定的组件之间有个全局事件总线的通信机制，没有新建vue实例，而是直接使用this.$root来进行，有了这个全局的通信机制，各个组件的通信就显得尤其简单了，组件之间互相传值、互相调用方法就显得不是那么复杂了。