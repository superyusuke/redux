# Async Flow

Without [middleware](Middleware.md), Redux store only supports [synchronous data flow](../basics/DataFlow.md). This is what you get by default with [`createStore()`](../api/createStore.md).

middleware なしでは、Redux store は synchronous data flow しかサポートしていません。\(訳注:redux-thunk 等のミドルウェアを使わない場合には、async なデータフローは実装できないということ。\) createStore\(\) をデフォルトのまま使う場合にはこのようになっています。

You may enhance [`createStore()`](../api/createStore.md) with [`applyMiddleware()`](../api/applyMiddleware.md). It is not required, but it lets you [express asynchronous actions in a convenient way](AsyncActions.md).

createStore\(\) に対して applyMiddleware\(\) を用いることで、これを強化することができます。この作業は必須ではありませんが、こうすることで、簡単に asynchronous action を実装することできます。

Asynchronous middleware like [redux-thunk](https://github.com/gaearon/redux-thunk) or [redux-promise](https://github.com/acdlite/redux-promise) wraps the store's [`dispatch()`](../api/Store.md#dispatch) method and allows you to dispatch something other than actions, for example, functions or Promises. Any middleware you use can then interpret anything you dispatch, and in turn, can pass actions to the next middleware in the chain. For example, a Promise middleware can intercept Promises and dispatch a pair of begin/end actions asynchronously in response to each Promise.

[redux-thunk](https://github.com/gaearon/redux-thunk) や [redux-promise](https://github.com/acdlite/redux-promise) といったミドルウェアは、store の dispatch\(\) メソッドをラップし、それによって action 以外の、例えば function や promise を dispatch することを可能にします。

When the last middleware in the chain dispatches an action, it has to be a plain object. This is when the [synchronous Redux data flow](../basics/DataFlow.md) takes place.

Check out [the full source code for the async example](ExampleRedditAPI.md).

## Next Steps

Now you saw an example of what middleware can do in Redux, it's time to learn how it actually works, and how you can create your own. Go on to the next detailed section about [Middleware](Middleware.md).

