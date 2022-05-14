## Understanding Redux: Demystifying Store, Action and Reducers

# Introduction

*As a pre-requisite, I will be assuming that the readers of this article are familiar with React.*

As per the official docs of Redux, it is a **Predictable State Container for JS Apps**. If we try to dig deep into this statement, it's very much clear that Redux is a state management library that can be used with any JS library or framework like React, Angular, Vue etc. 


![1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652462823595/zDQL_8Yf4.png align="left")

## Why is redux termed as a state container?

Well, an application has its state, which in turn can be a combination of the states of its internal components. Let's take an e-commerce website for example. An e-commerce website will have several components like the cart component, user profile component, previously viewed section component etc. Let's take the cart component for e.g. which displays the number of items in the cart of a user. The state of the cart component will comprise of all the items the user has added to the cart and the total number of such items. At all the times the application is up and running, this component has to show the updated number of items in the cart of the user. 

Whenever a user adds an item to the cart, the application has to internally handle that action by adding that item to the cart object, maintaining its state internally and also it has to show the user the total number of items in the cart in the UI. Similarly, removing an item from the cart should decrease the number of items in the cart internally, remove the item from the cart object and also display the updated total number of items in the cart in the UI. 

We may very well maintain the internal state of the components inside them, but as and when an application grows bigger, it may have to share some state between components, not just only to show them in the view, but also to manage/ update them or perform some logic based on their value. This part of handling multiple states from multiple components efficiently can become a challenging task when the application grows in size.

This is where Redux comes into the picture. Being a state management library, Redux will basically store and manage all the application's states. It also provides us with some important APIs using which we can make changes to the existing state as well as fetch the current state of the application. 


## What makes Redux predictable? 


The state is **Read-only** in redux. What makes Redux predictable is to make a change in the state of the application we need to dispatch an action which describes what changes we want to do in the state. These actions are then consumed by something known as reducers, whose sole job is to accept two thing i.e. action and the current state of the application and return a new updated instance of the state. *(Actions and Reducers are described further in the following sections.)* Note that reducers do not change any part of the state. Rather it produces a new instance of the state with all the necessary updates. According to @[Dan Abramov](@gaearon) *(the creator of Redux)* himself "Actions can be recorded and replayed later, so this makes state management predictable. With the same actions in the same order, you're going to end up in the same state." Thus continuing with our above example of an e-commerce website, if the initial state of the Cart is that it has 0 items, then an action of **adding one item** to the cart will increase the number of items in the cart to 1. Again firing the action of **adding one item** to the cart will increase the number of items in the cart to 2. Given an initial state, with a specific list of **actions** in a specific order, will always provide us with the exact same final state of the entity. This is how Redux makes state management predictable.

In the following section, we will dive deep into the core concepts of redux i.e. store, actions and reducers.

## Core Principles of Redux

![2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652463960151/j64XEAsVL.png align="left")

### 1. Store

> The global state of an application is stored in an object tree within a single store

The Redux store is the main, central bucket which stores all the states of an application. It should be considered and maintained as a **single source of truth**, for the state of the application. If the `store` is provided to the **App.js** (by wrapping the `App` component within the `<Provider>` `</Provider>` tag) as shown in the code snippet below, then all its children (children components of `App.js`) can also access the state of the application from the store, thus making it act as a global state. 

```
// src/index.js

import React from 'react'
import ReactDOM from 'react-dom'
import { Provider } from 'react-redux'

import { App } from './App'
import createStore from './createReduxStore'

const store = createStore()

// As of React 18
const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(
  <Provider store={store}>
    <App />
  </Provider>
)

```

![4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652519024186/Q2Bj8g36s.png align="left")

The state of the whole application is stored in the form of a **JS object tree** in a **single store** as shown below. 

```
// this is how the store object structure looks like
{
    noOfItemInCart: 2,
    cart: [
        {
            bookName: "Harry Potter and the Chamber of Secrets",
            noOfItem: 1,
        },
        {
            bookName: "Harry Potter and the Prisoner of Azkaban",
            noOfItem: 1
        }
    ]
}

``` 

### 2. Action

> The only way to change the state is to emit an action, which is an object describing what happened

As mentioned above, the state in redux is read-only. This helps in restricting any part of the view or any network calls to write/ update the state directly. Instead, if anyone wants to change the state of the application, then it needs to express its intention of doing so by **emitting or dispatching an action**. 

Let's take the example of the above store example where we have 2 books in the store, namely *"Harry Potter and the Chamber of Secrets"* and *"Harry Potter and the Prisoner of Azkaban"* both having only one item for each. Now if the user wants to add another item to the cart, then he will have to click on the **"Add to Cart"** button next to the item. 

On the click of the **"Add to Cart"** button, an action will be dispatched where the **action** is nothing but a JS object describing what changes need to be done in the store. Something like this

```
// Rest of the code

const dispatch = useDispatch()

const addItemToCart = () => {
return {
    type: "ADD_ITEM_TO_CART"
    payload: {
        bookName: "Harry Potter and the Goblet of Fire",
        noOfItem: 1,
        }
    }
}


<button onClick = {() => dispatch(addItemToCart())}>Add to cart</button>

// Rest of the code
```

Note how in the above example, we dispatch an action on click of the button. Or rather to be more specific, we dispatch something known as an **action creator** i.e. the function `addItemToCart()`, which in turn returns an `action` which is a plain JS object describing the purpose of the action denoted by the `type` key along with any other data required for the state change (which in this case is the name of the book to be added to the cart denoted by the `payload` key). **Every action must compulsorily have at least** a `type` associated with it. Any other detail that needs to be passed is optional and will depend on the type of action we dispatch. For e.g. the above code snippets dispatches the following action

```
// Action that got created by the action creator addItemToCart()

{
    type: "ADD_ITEM_TO_CART" // Note: Every action must have a type key
    payload: {
        bookName: "Harry Potter and the Goblet of Fire",
        noOfItem: 1,
    }
}
```

### 3. Reducers

> To specify how the state tree is transformed by actions, we write pure reducers

![3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652519582634/T8a2OAZeX.png align="left")

Reducers, as the name suggests, take in **two** things, i.e. **previous state and an action** and reduce it (read it return) to one entity i.e. the **new updated instance of state**. Thus reducers are basically **pure JS functions** which take in the previous state and an action and return the newly updated state. There can be either one reducer if it is a simple app or multiple reducers taking care of different parts or slices of the global state in case of a bigger application. For e.g. there can be a reducer handling the state of the cart in a shopping application, then there can be a reducer handling the user's details part of the application etc. Whenever an action is dispatched, **all the reducers are activated**. Each reducer filters out the action using a switch statement switching on the **action type**. Whenever the switch statement matches with the action passed, the corresponding reducers take the necessary action to make the update and return a fresh new instance of the global state. Continuing with our above example we can have a reducer as follows

```

const initialCartState = {    
    noOfItemInCart: 0,          
    cart: []                              
}

// NOTE: 
// It is important to pass an initial state as default to 
// the state parameter to handle the case of calling 
// the reducers for the first time when the 
// state might be undefined

const cartReducer = (state = initialCartState, action) => {
    switch (action.type) {
        case "ADD_ITEM_TO_CART": 
            return {
                ...state,
                noOfItemInCart: state.noOfItemInCart + 1,
                cart : [
                    ...state.cart,
                    action.payload
                ]
            }
        case "DELETE_ITEM_FROM_CART":
            return {
                // Remaining logic
            }
        default: 
            return state  
    }       // Important to handle the default behaviour
}           // either by returning the whole state as it is 
            // or by performing any required logic

```

In the above code snippet, we created a reducer called `cartReducer` which is a pure JS function. This function accepts two parameters i.e. `state` and `action`. Note that the `state` parameter is a default parameter which accepts an initial state. This is to handle the scenario when **the reducer is called for the first time** when the `state` value is `undefined`.  Also note that every reducer should handle the `default` case where if none of the switch cases matches with the passed action, then the reducer should return `state` as it is or perform any required logic on it before passing the state.

Whenever we dispatch an action with a certain type, we need to make sure to have **appropriate reducers** to handle that action. In the above example, on clicking the button, we had dispatched an **action** with an **action creator** called `addItemToCart()`. This action creator has dispatched an action with the `type` `ADD_ITEM_TO_CART`. Next, we have created a **reducer** called `cartReducer` which takes the state *(with the default initial state)* and the action as parameters, switches on the **action type**, and then whichever case matches with the dispatched action type, it makes the necessary update and **returns the fresh new version of the updated state**. Please note here that the **state in redux is immutable**. Hence, the reducers **make a copy** of the entire current state first, make necessary changes and then **return a fresh new instance of the state** with all the necessary changes/ updates. Thus in the above example, we first make a copy of the entire state using the spread operator `...state`, then increment the `noOfItemInCart` by 1, update the cart array by adding the new object passed in the `action.payload` shown below and then finally return the updated object.

```
{
    bookName: "Harry Potter and the Goblet of Fire",
    noOfItem: 1,
}

```

After the reducers have updated the state if we go and `console.log` the `state`, then we would see the following result.

```
// Updated store

{
    noOfItemInCart: 3, // Incremented by 1
    cart: [
        {
            bookName: "Harry Potter and the Chamber of Secrets",
            noOfItem: 1,
        },
        {
            bookName: "Harry Potter and the Prisoner of Azkaban",
            noOfItem: 1
        },
        { // Newly added object
            bookName: "Harry Potter and the Goblet of Fire",
            noOfItem: 1,
        }
    ]
}

``` 

## Summary

In short, the following three principles govern the entire working procedure of Redux

- The global state of an application is stored in an object tree within a single **store**
- The only way to change the state is to emit an **action**, which is an object describing what happened
- To specify how the state tree is transformed by actions, we write **pure reducers**

In the next blog, I'll show how to get started with your first redux powered react application. Till then, stay tuned.

## Wrapup
*Thanks for reading! I really hope you enjoyed reading about redux and its core principles and found this blog useful. Do consider hitting the like button and sharing it with your friends, I'd really appreciate that.  Stay tuned for more amazing content! Peace out! 🖖*

## Social Links

- LinkedIn : https://www.linkedin.com/in/sohamderoy/
- Website: https://www.sohamderoy.dev/












