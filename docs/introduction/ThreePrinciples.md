# Three Principles

３つの原則

Redux can be described in three fundamental principles:

Redux は３つの基本原則に則って記述されます。

### Single source of truth

一つだけの真実の源泉

**The **[**state**](../Glossary.md#state)** of your whole application is stored in an object tree within a single **[**store**](../Glossary.md#store)**.**

アプリケーション全体の状態を、単一のオブジェクト内に保持し、それを単一の storeと結びつける。

This makes it easy to create universal apps, as the state from your server can be serialized and hydrated into the client with no extra coding effort. A single state tree also makes it easier to debug or inspect an application; it also enables you to persist your app's state in development, for a faster development cycle. Some functionality which has been traditionally difficult to implement - Undo/Redo, for example - can suddenly become trivial to implement, if all of your state is stored in a single tree.

そうなっていれば、一般的なアプリケーションを作る際に楽です。サーバーから取得した状態は、serialize \(訳注：よくわからない\) され、余計なコーディングの面倒さなしに、クライアント側に渡すことができます。さらにデバグも簡単だし、アプリケーションの状態を調べるのも簡単です。それによって開発時に状態を検証することが容易になるので、開発サイクルをより早くすることができます。また、一般的に実装するのが難しいと考えられてきた機能、例えば unde/redo 機能も、状態が単一の場所で管理されていれば、簡単に実装できます。

```js
console.log(store.getState())

/* Prints
{
  visibilityFilter: 'SHOW_ALL',
  todos: [
    {
      text: 'Consider using Redux',
      completed: true,
    },
    {
      text: 'Keep all state in a single tree',
      completed: false
    }
  ]
}
*/
```

### State is read-only

状態は、読み取り専用

**The only way to change the state is to emit an **[**action**](../Glossary.md#action)**, an object describing what happened.**

状態を変更する手段は限定されており、action を発行することによってのみ可能です。action とは、何が起きるのかが書かれているオブジェクトです。

This ensures that neither the views nor the network callbacks will ever write directly to the state. Instead, they express an intent to transform the state. Because all changes are centralized and happen one by one in a strict order, there are no subtle race conditions to watch out for. As actions are just plain objects, they can be logged, serialized, stored, and later replayed for debugging or testing purposes.

これによって、view や network callbacks\(訳注：なんのことかよくわからず\)が直接状態を書き換えることを、防ぐことができます。そうではなくて、状態を変更する「意図」を表明します。全ての変更は、一箇所で中央管理され、１つづつ厳密な順番で発生させられるので、注意が必要な不明瞭な競合状態が発生しません。action 自体は単なるオブジェクトなので、記録され、serialized され、保持され、そして後からそれを再現してデバグをしたり、テストをすることができます。

```js
store.dispatch({
  type: 'COMPLETE_TODO',
  index: 1
})

store.dispatch({
  type: 'SET_VISIBILITY_FILTER',
  filter: 'SHOW_COMPLETED'
})
```

### Changes are made with pure functions

変更は、純粋関数で行われる

**To specify how the state tree is transformed by actions, you write pure **[**reducers**](../Glossary.md#reducer)**.**

状態がactionによってどのように変化させられるかを記述する場合には、純粋関数によるruducerを用いること。

Reducers are just pure functions that take the previous state and an action, and return the next state. Remember to return new state objects, instead of mutating the previous state. You can start with a single reducer, and as your app grows, split it off into smaller reducers that manage specific parts of the state tree. Because reducers are just functions, you can control the order in which they are called, pass additional data, or even make reusable reducers for common tasks such as pagination.

Reducer は単なる純粋関数で、現在の状態とactionを引数として受け取って、次の状態をreturnするものです。この際に、状態を直接変更するのではなく、新しい状態用のオブジェクトをreturnするようにしてください。最初は一つのreducerで始めれば良いのですが、アプリケーションが大きくなってきた場合には、reducer をより小さなreducerへと分割して、状態の特定の場所だけを担当させるようにします。reducerは単なる関数ですから、実行される順番をコントロールすることができ、また追加の情報を与えたり、さらにいえばページネーション用のものなど、一般的によくあるタスクに対して、繰り返し利用可能reducerを作ることもできます。

```js
function visibilityFilter(state = 'SHOW_ALL', action) {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.filter
    default:
      return state
  }
}

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case 'COMPLETE_TODO':
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: true
          })
        }
        return todo
      })
    default:
      return state
  }
}

import { combineReducers, createStore } from 'redux'
const reducer = combineReducers({ visibilityFilter, todos })
const store = createStore(reducer)
```

That's it! Now you know what Redux is all about.

以上です！Redux の全貌がわかりましたね！

