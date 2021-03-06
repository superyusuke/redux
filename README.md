# <a href='http://redux.js.org'><img src='https://camo.githubusercontent.com/f28b5bc7822f1b7bb28a96d8d09e7d79169248fc/687474703a2f2f692e696d6775722e636f6d2f4a65567164514d2e706e67' height='60'></a>

Redux is a predictable state container for JavaScript apps.  
(If you're looking for a WordPress framework, check out [Redux Framework](https://reduxframework.com/).)

Redux は javaScript アプリケーションのための、予測可能な state コンテイナです。(訳注:Redux は state 状態を管理するためのツールで、特に state の変更が追跡できる、純粋関数を元にした変更なので、挙動が一定である = "Predictable" である、といった点が特徴。)

It helps you write applications that behave consistently, run in different environments (client, server, and native), and are easy to test. On top of that, it provides a great developer experience, such as [live code editing combined with a time traveling debugger](https://github.com/gaearon/redux-devtools).

その性質のおかげで、一貫した挙動をする、そして様々な環境で動く(クライアントサイドでも、サーバーサイドでも、そしてネイティブアプリ上でも動きます)、テストが簡単なアプリケーションを書くことができます。さらに、次のアプリケーションのような非常に快適な開発体験をも提供します。([live code editing combined with a time traveling debugger](https://github.com/gaearon/redux-devtools))

You can use Redux together with [React](https://facebook.github.io/react/), or with any other view library.  
It is tiny (2kB, including dependencies).

Redux を React と組み合わせ使うことができますし、React 以外のライブラリと組み合わせることもできます。Redux のサイズは非常に小さく、依存ファイルを含めても2kB しかありません。

[![build status](https://img.shields.io/travis/reactjs/redux/master.svg?style=flat-square)](https://travis-ci.org/reactjs/redux)
[![npm version](https://img.shields.io/npm/v/redux.svg?style=flat-square)](https://www.npmjs.com/package/redux)
[![npm downloads](https://img.shields.io/npm/dm/redux.svg?style=flat-square)](https://www.npmjs.com/package/redux)
[![redux channel on discord](https://img.shields.io/badge/discord-%23redux%20%40%20reactiflux-61dafb.svg?style=flat-square)](https://discord.gg/0ZcbPKXt5bZ6au5t)
[![#rackt on freenode](https://img.shields.io/badge/irc-%23rackt%20%40%20freenode-61DAFB.svg?style=flat-square)](https://webchat.freenode.net/)
[![Changelog #187](https://img.shields.io/badge/changelog-%23187-lightgrey.svg?style=flat-square)](https://changelog.com/187)

>**Learn Redux from its creator:**
>**Redux の作者から学ぶ動画コンテンツ:**
>**[Part 1: Getting Started with Redux](https://egghead.io/series/getting-started-with-redux) (30 free videos)**<br>
>**[Part 2: Building React Applications with Idiomatic Redux](https://egghead.io/courses/building-react-applications-with-idiomatic-redux) (27 free videos)**

### Testimonials

>[“Love what you're doing with Redux”](https://twitter.com/jingc/status/616608251463909376)  
>Jing Chen, creator of Flux

>[“I asked for comments on Redux in FB's internal JS discussion group, and it was universally praised. Really awesome work.”](https://twitter.com/fisherwebdev/status/616286955693682688)  
>Bill Fisher, author of Flux documentation

>[“It's cool that you are inventing a better Flux by not doing Flux at all.”](https://twitter.com/andrestaltz/status/616271392930201604)  
>André Staltz, creator of Cycle

### Before Proceeding Further

>**Also read:**  
>**[You Might Not Need Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)**

### Developer Experience

I wrote Redux while working on my React Europe talk called [“Hot Reloading with Time Travel”](https://www.youtube.com/watch?v=xsSnOQynTHs). My goal was to create a state management library with minimal API but completely predictable behavior, so it is possible to implement logging, hot reloading, time travel, universal apps, record and replay, without any buy-in from the developer.

### Influences

Redux evolves the ideas of [Flux](http://facebook.github.io/flux/), but avoids its complexity by taking cues from [Elm](https://github.com/evancz/elm-architecture-tutorial/).  
Whether you have used them or not, Redux only takes a few minutes to get started with.

Redux は [Flux](http://facebook.github.io/flux/) を発展させたもので、それでいて [Elm](https://github.com/evancz/elm-architecture-tutorial/) からヒントを得たことで、Flux の複雑性を取り除いています。

### Installation

To install the stable version:

Redux の安定バージョンをインストールするためには以下のコマンドを実行します。

```
npm install --save redux
```

This assumes you are using [npm](https://www.npmjs.com/) as your package manager.

上記のコマンドは、[npm](https://www.npmjs.com/) をパッケージ・マネージャーとしている前提のものです。

If you're not, you can [access these files on unpkg](https://unpkg.com/redux/), download them, or point your package manager to them.

npm を使わない場合には、[unpkg から](https://unpkg.com/redux/) ファイルを手に入れることができます。ファイルをダウンロードするか、もしくはお使いのパッケージマネージャー上記URLを指定してください。

Most commonly people consume Redux as a collection of [CommonJS](http://webpack.github.io/docs/commonjs.html) modules. These modules are what you get when you import `redux` in a [Webpack](https://webpack.js.org/), [Browserify](http://browserify.org/), or a Node environment. If you like to live on the edge and use [Rollup](http://rollupjs.org), we support that as well.

If you don't use a module bundler, it's also fine. The `redux` npm package includes precompiled production and development [UMD](https://github.com/umdjs/umd) builds in the [`dist` folder](https://unpkg.com/redux/dist/). They can be used directly without a bundler and are thus compatible with many popular JavaScript module loaders and environments. For example, you can drop a UMD build as a [`<script>` tag](https://unpkg.com/redux/dist/redux.js) on the page, or [tell Bower to install it](https://github.com/reactjs/redux/pull/1181#issuecomment-167361975). The UMD builds make Redux available as a `window.Redux` global variable.

The Redux source code is written in ES2015 but we precompile both CommonJS and UMD builds to ES5 so they work in [any modern browser](http://caniuse.com/#feat=es5). You don't need to use Babel or a module bundler to [get started with Redux](https://github.com/reactjs/redux/blob/master/examples/counter-vanilla/index.html).

#### Complementary Packages

Most likely, you'll also need [the React bindings](https://github.com/reactjs/react-redux) and [the developer tools](https://github.com/gaearon/redux-devtools).

```
npm install --save react-redux
npm install --save-dev redux-devtools
```

Note that unlike Redux itself, many packages in the Redux ecosystem don't provide UMD builds, so we recommend using CommonJS module bundlers like [Webpack](https://webpack.js.org/) and [Browserify](http://browserify.org/) for the most comfortable development experience.

### 概要
The Gist

The whole state of your app is stored in an object tree inside a single *store*.  
The only way to change the state tree is to emit an *action*, an object describing what happened.  
To specify how the actions transform the state tree, you write pure *reducers*.

あなたが作っているアプリケーションの状態 state を全て、たったひとつのオブジェクトで管理し、そしてそれを”store” という変数に入れる。(訳注：もしくは store という概念と紐付けて運用する) 状態を変更する方法は制限されており、”action”を発行する(=emit) 方法だけしかない。action は”何を起こすか”が述べられているオブジェクトである。”action”が state をどのように変更するのかは、”reducer” によって定義する。reducer は純粋関数である必要がある。

(訳注：純粋関数については例えばこの記事を参照。Redux と state の関連では、私が理解する限り、関数の引数で与えられたもの以外の変動する値を関数内部で使わない(例えば引数では与えられていないグローバル変数など)、引数で与えられたものそのものを変更しない＝イミュータブル、return で新たなstateを返す、というルールを守れば良い。)

That's it!

それで全てです!

```js
import { createStore } from 'redux'

/**
 * This is a reducer, a pure function with (state, action) => state signature.
 
 * 次の関数がReducerです。これは純粋関数でなければいけず、
 * また(state, action ) の２つを与えて、state を return するというのが、特徴です。
 
 * It describes how an action transforms the state into the next state.
 
 * Reducer は、"action"がどのように状態satateを変更し、
 * 新しい状態 next state を作り出すかを定義しています。
 
 * The shape of the state is up to you: it can be a primitive, an array, an object,
 
 * 状態の形式は自由で、普通の配列やオブジェクトでもいいですし、
 
 * or even an Immutable.js data structure. The only important part is that you should
 
 * ほかにも Immutable.js を使ったデータ形式でも良いです。重要なのは、状態を変更する場合に、
 
 * not mutate the state object, but return a new object if the state changes.
 
 * 状態管理用のオブジェクトを、直接変化させるのではなく、
 * 新しく新しい状態を持ったオブジェクトを作り、それを return することです。
 
 * In this example, we use a `switch` statement and strings, but you can use a helper that
 
 * この例では、"switch文"と文字列を使って分岐を行っていますが、
 * 他の方法、例えば maps 関数などを使うこともできます。
 
 * follows a different convention (such as function maps) if it makes sense for your
 * project.
 */
function counter(state = 0, action) {
  switch (action.type) {
  case 'INCREMENT':
    return state + 1
  case 'DECREMENT':
    return state - 1
  default:
    return state
  }
}

// Create a Redux store holding the state of your app.
// Its API is { subscribe, dispatch, getState }.

// 次のコードは、Redux 用のstore を作り、それに自分のアプリケーションの
// 状態を与えています。
// (訳注：さらに、引数としてreducerであるcounterを与えている。
// reducerには初期値が与えられているので結果として、ここではstate=0が与えられている。)
// このようにして作られたstore は{ subscribe, dispatch, getState } などの API を持っています。
let store = createStore(counter)

// You can use subscribe() to update the UI in response to state changes.
// Normally you'd use a view binding library (e.g. React Redux) rather than subscribe() directly.
// However it can also be handy to persist the current state in the localStorage.

store.subscribe(() =>
  console.log(store.getState())
)

// The only way to mutate the internal state is to dispatch an action.
// The actions can be serialized, logged or stored and later replayed.
store.dispatch({ type: 'INCREMENT' })
// 1
store.dispatch({ type: 'INCREMENT' })
// 2
store.dispatch({ type: 'DECREMENT' })
// 1
```

Instead of mutating the state directly, you specify the mutations you want to happen with plain objects called *actions*. Then you write a special function called a *reducer* to decide how every action transforms the entire application's state.

状態を直接変更するのではなく、まずどのような変化を起こしたいのかを plain なオブジェクトに記述します。これを action と呼びます。次に reducer とよばれる特別な関数を書き、それぞれの action がどのように状態全体を変更するのかを規定します。

If you're coming from Flux, there is a single important difference you need to understand. Redux doesn't have a Dispatcher or support many stores. Instead, there is just a single store with a single root reducing function. As your app grows, instead of adding stores, you split the root reducer into smaller reducers independently operating on the different parts of the state tree. This is exactly like how there is just one root component in a React app, but it is composed out of many small components.

もし以前に Flux を使ったことがあるのであれば、Flux と Redux には一つ重要な違いがありますので、その点を理解してください。Redux は Dispathcer を持たず、また複数の store を持つこともできません。Redux は一つだけ sotre を持ち、それに対して一つだけ reducer を付加することができます。アプリケーションの規模が大きくなる場合には、store を増やすのではなく、root reducer をより小さな reducer へと分割し、それぞれの reducer が、状態ツリーのの異なる場所を担当するようにします。これはちょうど、React がルートコンポーネントをひとつだけ持ち、しかしルートコンポーネントが、沢山の小さなコンポーネントの組み合わせでできているのと、同じようなものです。

This architecture might seem like an overkill for a counter app, but the beauty of this pattern is how well it scales to large and complex apps. It also enables very powerful developer tools, because it is possible to trace every mutation to the action that caused it. You can record user sessions and reproduce them just by replaying every action.

このような構造は、恐らくちょっとしたカウンター・アプリには大げさすぎるのでしょうが、その強みは、より大きく複雑なアプリケーションになったときに発揮されます。また強力な開発者ツールも提供していますので、これによって全ての変更を追いかけることができます。ユーザーの操作を全て記録し、その全てのアクションを再度実行することで、これを再現することもできます。

### Learn Redux from Its Creator

[Getting Started with Redux](https://egghead.io/series/getting-started-with-redux) is a video course consisting of 30 videos narrated by Dan Abramov, author of Redux. It is designed to complement the “Basics” part of the docs while bringing additional insights about immutability, testing, Redux best practices, and using Redux with React. **This course is free and will always be.**

>[“Great course on egghead.io by @dan_abramov - instead of just showing you how to use #redux, it also shows how and why redux was built!”](https://twitter.com/sandrinodm/status/670548531422326785)  
>Sandrino Di Mattia

>[“Plowing through @dan_abramov 'Getting Started with Redux' - its amazing how much simpler concepts get with video.”](https://twitter.com/chrisdhanaraj/status/670328025553219584)  
>Chris Dhanaraj

>[“This video series on Redux by @dan_abramov on @eggheadio is spectacular!”](https://twitter.com/eddiezane/status/670333133242408960)  
>Eddie Zaneski

>[“Come for the name hype. Stay for the rock solid fundamentals. (Thanks, and great job @dan_abramov and @eggheadio!)”](https://twitter.com/danott/status/669909126554607617)  
>Dan

>[“This series of videos on Redux by @dan_abramov is repeatedly blowing my mind - gunna do some serious refactoring”](https://twitter.com/gelatindesign/status/669658358643892224)  
>Laurence Roberts

So, what are you waiting for?

#### [Watch the 30 Free Videos!](https://egghead.io/series/getting-started-with-redux)

If you enjoyed my course, consider supporting Egghead by [buying a subscription](https://egghead.io/pricing). Subscribers have access to the source code for the example in every one of my videos, as well as to tons of advanced lessons on other topics, including JavaScript in depth, React, Angular, and more. Many [Egghead instructors](https://egghead.io/instructors) are also open source library authors, so buying a subscription is a nice way to thank them for the work that they've done.

### Documentation

* [Introduction](http://redux.js.org/docs/introduction/index.html)
* [Basics](http://redux.js.org/docs/basics/index.html)
* [Advanced](http://redux.js.org/docs/advanced/index.html)
* [Recipes](http://redux.js.org/docs/recipes/index.html)
* [FAQ](http://redux.js.org/docs/FAQ.html)
* [Troubleshooting](http://redux.js.org/docs/Troubleshooting.html)
* [Glossary](http://redux.js.org/docs/Glossary.html)
* [API Reference](http://redux.js.org/docs/api/index.html)

For PDF, ePub, and MOBI exports for offline reading, and instructions on how to create them, please see: [paulkogel/redux-offline-docs](https://github.com/paulkogel/redux-offline-docs).

For Offline docs, please see: [devdocs](http://devdocs.io/redux/)

### Examples

Almost all examples have a corresponding CodeSandbox sandbox. This is an interactive version of the code that you can play with online.

* [Counter Vanilla](http://redux.js.org/docs/introduction/Examples.html#counter-vanilla) ([source](https://github.com/reactjs/redux/tree/master/examples/counter-vanilla))
* [Counter](http://redux.js.org/docs/introduction/Examples.html#counter) ([source](https://github.com/reactjs/redux/tree/master/examples/counter), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/counter))
* [Todos](http://redux.js.org/docs/introduction/Examples.html#todos) ([source](https://github.com/reactjs/redux/tree/master/examples/todos), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/todos))
* [Todos with Undo](http://redux.js.org/docs/introduction/Examples.html#todos-with-undo) ([source](https://github.com/reactjs/redux/tree/master/examples/todos-with-undo), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/todos-with-undo))
* [TodoMVC](http://redux.js.org/docs/introduction/Examples.html#todomvc) ([source](https://github.com/reactjs/redux/tree/master/examples/todomvc), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/todomvc))
* [Shopping Cart](http://redux.js.org/docs/introduction/Examples.html#shopping-cart) ([source](https://github.com/reactjs/redux/tree/master/examples/shopping-cart), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/shopping-cart))
* [Tree View](http://redux.js.org/docs/introduction/Examples.html#tree-view) ([source](https://github.com/reactjs/redux/tree/master/examples/tree-view), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/tree-view))
* [Async](http://redux.js.org/docs/introduction/Examples.html#async) ([source](https://github.com/reactjs/redux/tree/master/examples/async), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/async))
* [Universal](http://redux.js.org/docs/introduction/Examples.html#universal) ([source](https://github.com/reactjs/redux/tree/master/examples/universal))
* [Real World](http://redux.js.org/docs/introduction/Examples.html#real-world) ([source](https://github.com/reactjs/redux/tree/master/examples/real-world), [sandbox](https://codesandbox.io/s/github/reactjs/redux/tree/master/examples/real-world))

If you're new to the NPM ecosystem and have troubles getting a project up and running, or aren't sure where to paste the gist above, check out [simplest-redux-example](https://github.com/jackielii/simplest-redux-example) that uses Redux together with React and Browserify.

### Discussion

Join the [#redux](https://discord.gg/0ZcbPKXt5bZ6au5t) channel of the [Reactiflux](http://www.reactiflux.com) Discord community.

### Thanks

* [The Elm Architecture](https://github.com/evancz/elm-architecture-tutorial) for a great intro to modeling state updates with reducers;
* [Turning the database inside-out](http://www.confluent.io/blog/turning-the-database-inside-out-with-apache-samza/) for blowing my mind;
* [Developing ClojureScript with Figwheel](https://www.youtube.com/watch?v=j-kj2qwJa_E) for convincing me that re-evaluation should “just work”;
* [Webpack](https://webpack.js.org/concepts/hot-module-replacement/) for Hot Module Replacement;
* [Flummox](https://github.com/acdlite/flummox) for teaching me to approach Flux without boilerplate or singletons;
* [disto](https://github.com/threepointone/disto) for a proof of concept of hot reloadable Stores;
* [NuclearJS](https://github.com/optimizely/nuclear-js) for proving this architecture can be performant;
* [Om](https://github.com/omcljs/om) for popularizing the idea of a single state atom;
* [Cycle](https://github.com/cyclejs/cycle-core) for showing how often a function is the best tool;
* [React](https://github.com/facebook/react) for the pragmatic innovation.

Special thanks to [Jamie Paton](http://jdpaton.github.io) for handing over the `redux` NPM package name.

### Logo

You can find the official logo [on GitHub](https://github.com/reactjs/redux/tree/master/logo).

### Change Log

This project adheres to [Semantic Versioning](http://semver.org/).  
Every release, along with the migration instructions, is documented on the Github [Releases](https://github.com/reactjs/redux/releases) page.

### Patrons

The work on Redux was [funded by the community](https://www.patreon.com/reactdx).  
Meet some of the outstanding companies that made it possible:

* [Webflow](https://github.com/webflow)
* [Ximedes](https://www.ximedes.com/)

[See the full list of Redux patrons.](PATRONS.md), as well as the always-growing list of [people and companies that use Redux](https://github.com/reactjs/redux/issues/310).

### License

MIT
