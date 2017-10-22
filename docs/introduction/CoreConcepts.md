# Core Concepts

Redux itself is very simple.

Redux それ自体は非常にシンプルです。

Imagine your app’s state is described as a plain object. For example, the state of a todo app might look like this:

あなたの作ったアプリケーションの状態が、一つのシンプルなオブジェクトに記述されているとしましょう。例えば todo アプリの状態が次のような場合を想定しましょう。

```js
{
  todos: [{
    text: 'Eat food',
    completed: true
  }, {
    text: 'Exercise',
    completed: false
  }],
  visibilityFilter: 'SHOW_COMPLETED'
}
```

This object is like a “model” except that there are no setters. This is so that different parts of the code can’t change the state arbitrarily, causing hard-to-reproduce bugs.

このオブジェクトはいわゆる”model”に似ていますが、少し違うのは、setter を持っていない点です。なぜこうなっているかというと、コード内の様々な場所で状態を恣意的に変更すると、再現不可能なバグが生じてしまうからです。

To change something in the state, you need to dispatch an action. An action is a plain JavaScript object \(notice how we don’t introduce any magic?\) that describes what happened. Here are a few example actions:

状態に変更を加える場合には、”action”を”dispatch”します。”action”はただのJSオブジェクトで、何が起きるのかが記述されています。次のコードは、”action”の例です。

```js
{ type: 'ADD_TODO', text: 'Go to swimming pool' }
{ type: 'TOGGLE_TODO', index: 1 }
{ type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }
```

Enforcing that every change is described as an action lets us have a clear understanding of what’s going on in the app. If something changed, we know why it changed. Actions are like breadcrumbs of what has happened.  
Finally, to tie state and actions together, we write a function called a reducer. Again, nothing magical about it—it’s just a function that takes state and action as arguments, and returns the next state of the app.  
It would be hard to write such a function for a big app, so we write smaller functions managing parts of the state:

全ての変更に関する内容が”action”として定義されているので、私たちはアプリケーションの中で何が起きているのかを正確に把握することができます。何かが変更されときにはいつでも、どうしてそうなったのかを知ることができます。Action は何が起きたのかということに関するパンくずリストのようなものです。最後に、状態とactionを結びつけるために、reducer と呼ばれる関数を書きます。特殊なものではありません。単に状態とアクションを引数として受取り、そして次の状態を return するファンクションです。アプリケーションが大きくなった場合には、このような関数を書くのは難しくなってくるので、そのような場合には、状態の一部分だけを担当する小さなファンクションを書くこともできます。

```js
function visibilityFilter(state = 'SHOW_ALL', action) {
  if (action.type === 'SET_VISIBILITY_FILTER') {
    return action.filter
  } else {
    return state
  }
}

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([{ text: action.text, completed: false }])
    case 'TOGGLE_TODO':
      return state.map(
        (todo, index) =>
          action.index === index
            ? { text: todo.text, completed: !todo.completed }
            : todo
      )
    default:
      return state
  }
}
```

And we write another reducer that manages the complete state of our app by calling those two reducers for the corresponding state keys:

そして、状態全体を担当する reducer を書いて、この中で先程の２つのreducer を実行します。この2つのreducer それぞれは、対応する state の key の部分で実行されます。

```js
function todoApp(state = {}, action) {
  return {
    todos: todos(state.todos, action),
    visibilityFilter: visibilityFilter(state.visibilityFilter, action)
  }
}
```

This is basically the whole idea of Redux. Note that we haven’t used any Redux APIs. It comes with a few utilities to facilitate this pattern, but the main idea is that you describe how your state is updated over time in response to action objects, and 90% of the code you write is just plain JavaScript, with no use of Redux itself, its APIs, or any magic.

ここまでが Redux の基本的な概念です。まだ Redux API は一つも使っていないことにお気づきでしょうか。Redux API はいくつかパターン管理を楽にしてくれる諸機能を提供してくれますが、Redux の主要な概念は、Action オブジェクトに搬送して、状態がどのように変更されるかを自分で書く、というものであって、コードの90％は単なるJSで記述されます。そういう意味ではReduxも、そのAPIも必要ありません。

