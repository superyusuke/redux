# Actions

First, let's define some actions.

まずは”action”を定義しましょう。

**Actions** are payloads of information that send data from your application to your store. They are the _only_ source of information for the store. You send them to the store using [`store.dispatch()`](../api/Store.md#dispatch).

Action は情報を持った貨物のようなもので、アプリケーションから store へと運ばれます。Action は情報だけをもっています。store.dispatch\(\)を使ってその情報をstoreへ運びます。

Here's an example action which represents adding a new todo item:

次のサンプルは、新しい todo アイテムを追加する action です。

```js
const ADD_TODO = 'ADD_TODO'
```

```js
{
  type: ADD_TODO,
  text: 'Build my first Redux app'
}
```

Actions are plain JavaScript objects. Actions must have a `type` property that indicates the type of action being performed. Types should typically be defined as string constants. Once your app is large enough, you may want to move them into a separate module.

Action は単なるJSオブジェクトです。Action は必ず type プロパティを持たなくてはいけません。これによって実行されるアクションがどれなのかを示します。Typeは一般的に文字列を含んだ定数によって定義されます。アプリケーションが大きくなってきた場合には、これらを分割してモジュールとして管理したくなるでしょう。

```js
import { ADD_TODO, REMOVE_TODO } from '../actionTypes'
```

> ##### Note on Boilerplate
>
> You don't have to define action type constants in a separate file, or even to define them at all. For a small project, it might be easier to just use string literals for action types. However, there are some benefits to explicitly declaring constants in larger codebases. Read [Reducing Boilerplate](../recipes/ReducingBoilerplate.md) for more practical tips on keeping your codebase clean.
>
> Action タイプを定数で定義し別々のファイルに分ける必要がない、もしくはそもそも定数で定義する必要もない場合もあるでしょう。とりわけ小さなプロジェクトにおいては、単に文字列でaction タイプを指定するだけでいいかもしれません。しかし、コードが大きくなってきた場合には、action typeを定数で宣言しておく利点があります。より実践的な内容に関しては、次の記事を読んで下さい。

Other than `type`, the structure of an action object is really up to you. If you're interested, check out [Flux Standard Action](https://github.com/acdlite/flux-standard-action) for recommendations on how actions could be constructed.

typeの他にも、action オブジェクトには、どのような構造をも持たせることができます。興味があれば次の記事を読んで、action のオススメの構造について学んでください。

We'll add one more action type to describe a user ticking off a todo as completed. We refer to a particular todo by `index` because we store them in an array. In a real app, it is wiser to generate a unique ID every time something new is created.

今回はもう一つactionを追加しましょう。todo リストが完了した際に実行されるアクションです。特定のtodoアイテムをindexによって参照します。todoアイテムはstoreの中に配列として持つことになるので、これを参照するためです。実際のアプリケーションにおいては、新しいアイテムが作られる度に、ユニークなIDを生成するほうが賢いやり方でしょう。

```js
{
  type: TOGGLE_TODO,
  index: 5
}
```

It's a good idea to pass as little data in each action as possible. For example, it's better to pass `index` than the whole todo object.

なるべく少ない情報をactionには与えるほうがいいでしょう。例えばtodoオブジェクト全体を渡すよりも、indexだけを渡す方が良い、といったようなことです。

Finally, we'll add one more action type for changing the currently visible todos.

最後に、もう一つアクションタイプを追加します。これは現在のタスクの表示非表示を切り替えるためのものです。

```js
{
  type: SET_VISIBILITY_FILTER,
  filter: SHOW_COMPLETED
}
```

## Action Creators

**Action creators** are exactly that—functions that create actions. It's easy to conflate the terms “action” and “action creator,” so do your best to use the proper term.

Action creator はアクションを作る関数です。action と　action creator は混同しやすいので、適切な言葉をしっかり使えるように注意してください。

In Redux action creators simply return an action:

Redux の action creator は単純に、action を return します。

```js
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
```

This makes them portable and easy to test.

こうすることで、取り回しがよくなり、かつ、テストも容易になります。

In [traditional Flux](http://facebook.github.io/flux), action creators often trigger a dispatch when invoked, like so:

伝統的なFluxにおいては、アクションクリエイターは呼び出された場合に、たいていの場合、dispatchをもトリガーします。

```js
function addTodoWithDispatch(text) {
  const action = {
    type: ADD_TODO,
    text
  }
  dispatch(action)
}
```

In Redux this is _not_ the case.  
Instead, to actually initiate a dispatch, pass the result to the `dispatch()` function:

しかし、Redux においてはそうではありません。その代わりに、dispatchを実際に初期化し、その結果をdispatch\(\)関数へと渡します。

```js
dispatch(addTodo(text))
dispatch(completeTodo(index))
```

Alternatively, you can create a **bound action creator** that automatically dispatches:

他の方法としてbound action creator を作る方法もあります。これは自動的にdispatchを呼び出すものです。

```js
const boundAddTodo = text => dispatch(addTodo(text))
const boundCompleteTodo = index => dispatch(completeTodo(index))
```

Now you'll be able to call them directly:

こうすることで、これらのdispatchを直接実行することができます。\(訳注：addTodoというactionクリエイターとdispatachを関連付けた関数、boudAddTodoを作って、これを呼び出せば、アクションクリエイターもdispatchも同時に実行されるので、毎回それぞれを書かなくて良いので便利。\)

```
boundAddTodo(text)
boundCompleteTodo(index)
```

The `dispatch()` function can be accessed directly from the store as [`store.dispatch()`](../api/Store.md#dispatch), but more likely you'll access it using a helper like [react-redux](http://github.com/gaearon/react-redux)'s `connect()`. You can use [`bindActionCreators()`](../api/bindActionCreators.md) to automatically bind many action creators to a `dispatch()` function.

dispatch\(\)関数は、storeから直接、store.dispatch\(\)という形でアクセすることができます。ですが、より使われるのは、react-reduxのconnect\(\)というヘルパー関数を用いて、アクセスする方法です。さらにbindActionCreators\(\)をつかってたくさんのactionクリエイターをdispatch\(\)関数に紐付けることもできます。

Action creators can also be asynchronous and have side-effects. You can read about [async actions](../advanced/AsyncActions.md) in the [advanced tutorial](../advanced/README.md) to learn how to handle AJAX responses and compose action creators into async control flow. Don't skip ahead to async actions until you've completed the basics tutorial, as it covers other important concepts that are prerequisite for the advanced tutorial and async actions.

Actionクリエイターは非同期で、かつ副次的効果をもたらしてしまいます。 [async actions](http://redux.js.org/docs/advanced/AsyncActions.html) を読んで、AJAXの返答や、action creatorを同期的なフローの中に組み込む方法を学習してください。async action に進むのは、reduxの基本的なチュートリアルを終えてからにしてください。基本的なチュートリアルには、より高度なチュートリアルと、それからasync action の理解に必要な、重要な前提知識が含まれているからです。

## Source Code

### `actions.js`

```js
/*
 * action types
 */

export const ADD_TODO = 'ADD_TODO'
export const TOGGLE_TODO = 'TOGGLE_TODO'
export const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER'

/*
 * other constants
 */

export const VisibilityFilters = {
  SHOW_ALL: 'SHOW_ALL',
  SHOW_COMPLETED: 'SHOW_COMPLETED',
  SHOW_ACTIVE: 'SHOW_ACTIVE'
}

/*
 * action creators
 */

export function addTodo(text) {
  return { type: ADD_TODO, text }
}

export function toggleTodo(index) {
  return { type: TOGGLE_TODO, index }
}

export function setVisibilityFilter(filter) {
  return { type: SET_VISIBILITY_FILTER, filter }
}
```

## Next Steps

Now let's [define some reducers](Reducers.md) to specify how the state updates when you dispatch these actions!

次はreducerを定義していきましょう。これによって、actionがディスパッチされた際に、どのようにstateをアップデートするかを定義します。

