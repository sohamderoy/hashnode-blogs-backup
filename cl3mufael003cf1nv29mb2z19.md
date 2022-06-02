## Understanding Redux (Part 2): Creating a small Redux powered React App in 10 easy steps (with code snippets)

Before proceeding with this blog, I would recommend first going through Part 1 of the Understanding Redux series which can be found by clicking on this link [Understanding Redux (Part 1): Demystifying Store, Action and Reducers](https://blog.sohamderoy.dev/understanding-redux-part-1-demystifying-store-action-and-reducers). That will help you understand the current article. In the Part 1 blog, **I have tried to explain the fundamental principles/ concepts of Redux**. I have covered what is **Store**, **Actions**, and **Reducers**, what makes **Redux predictable** along with an example. 

In this current article, we will try to set up our own **redux powered react application**. We will go through how to **create Store and provide it to the Application**, **write Actions**, **Dispatch them on user interactions**, **make Reducers and update the store**, **read the store from other components which are children of App** and many more. I'll provide all the important code snippets along the way so that you can quickly spin up the application.

To give a glimpse in the beginning itself, this is what we will finally build

![ezgif-2-8b96ff4bf6.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1653078242537/2QHhpHTR3.gif align="left")

We will be creating a basic application where we can add and remove item in the cart. We will manage the state changes in the redux store and display the information in the UI.

![despicable-me-minions.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1653080548564/rL-GdvBUz.gif align="left")


## Code Setup

### 1. Create a react app with the create-react-app command

```
npx create-react-app react-app-with-redux
```
### 2. Go to the newly created folder using

```
cd react-app-with-redux
```
### 3. Install **redux** and **react-redux** library using the commands

```
npm install redux react-redux

``` 
### 4. Run the application using

```
npm start
```

### 5. Creating Reducer

First create a folder inside `src` named `actionTypes` and create a file inside it named `actionTypes.js`. This file will contain all the **actions** the application will be dealing with. Add the following lines in `actionTypes.js`

```
export const ADD_ITEM = "ADD_ITEM";
export const DELETE_ITEM = "DELETE_ITEM";
```
As we are making an app where we will have the functionality of adding and deleting an Item, hence the above two action types.

Next create a folder inside the `src` called `reducers` and create a new file in it named `cartReducer.js`. This file will contain all the reducer logic related to the **cart** component. *(**Note**: We will create the view/ UI in the step 8)*. Add the following lines in the `cartReducer.js`.

```
import { ADD_ITEM, DELETE_ITEM } from "../actionTypes/actionTypes";

const initialState = {
  numOfItems: 0,
};

export default const cartReducer = (state = initialState, action) => {
  switch (action.type) {
    case ADD_ITEM:
      return {
        ...state,
        numOfItems: state.numOfItems + 1,
      };

    case DELETE_ITEM:
      return {
        ...state,
        numOfItems: state.numOfItems - 1,
      };
    default:
      return state;
  }
};

```
As we discussed it [Part 1](https://blog.sohamderoy.dev/understanding-redux-part-1-demystifying-store-action-and-reducers) of this blog, we created an **initial state** for the app and assigned it to the default parameter of `state` in the `cartReducer` function. This function switches on the **type of action** dispatched, and which ever case matches with the action type, makes necessary changes in the state and returns a fresh new instance of the updated state. If none of the action type matches, then the state is returned as it is. Finally we make a **default export** of the `cakeReducer` function to use it in the store creation process.

### 6. Creating the store and providing it to the App

Create a file inside `src` with the name `store.js` and create the store using the command

```
const store = createStore()
```

Add the following lines in `store.js`

```
import { createStore } from "redux";
import { cartReducer } from "./reducers/cartReducer";

const store = createStore(cartReducer);

export default store;
```

Now it's time to provide this `store` to the `App` component. For this we make use of the `<Provider>` tag that we get from the `react-redux` library. We wrap the whole `App` component inside the `<Provider>` tag using the following syntax.

```
// rest of the code ...

<Provider store={store}>
        <div>App Component</div>
        // child components of App/ other logic
</Provider>

// rest of the code ...
```

By wrapping the `App` component inside the `<Provider>` tag, all the children component of `App` will get access of the `store`. Please visit the [Part 1](https://blog.sohamderoy.dev/understanding-redux-part-1-demystifying-store-action-and-reducers) of the blog series to know more.

Continuing with the `App.js`, add the following lines in the file.

```
import "./App.css";
import { Provider } from "react-redux";
import store from "./store";

function App() {
  return (
    <Provider store={store}>
      <div>App Component</div>
    </Provider>
  );
}

export default App;
```

### 7. Create Actions

Now create a folder inside `src` called `actions` and create a file inside it called `cartAction.js`. Here we will add all the actions to be **dispatched** on some user interactions. Add the following lines in the `cartAction.js`

```
import { ADD_ITEM, DELETE_ITEM } from "../actionTypes/actionTypes";

const addItem = () => {
  return {
    type: ADD_ITEM,
  };
};

const deleteItem = () => {
  return {
    type: DELETE_ITEM,
  };
};

export { addItem, deleteItem };
```

In the above code we created two action creators *(pure JS functions that returns `action` object)* called `addItem()` and `deleteItem()`. Both the **action creators** returns `action` object with a specific `type`. * **Note**: Each `action` object **must necessarily** have a unique `type` value. Along with it any additional data passed with the action object is optional and will depend on the logic used for updating the `state`*

### 8. Creating the view/ UI

Now that we have created all the required entities such as **Store, Actions, and Reducers**, it's time to create the UI elements. Create a `component` folder inside `src` and create a `Cart.js` file inside it. Add the following line inside `Cart.js`

```
import React from "react";

const Cart = () => {
  return (
    <div className="cart">
      <h2>Number of items in Cart:</h2>
      <button className="green">Add Item to Cart</button>
      <button className="red">Remove Item from Cart</button>
    </div>
  );
};

export default Cart;
```

Add this `Cart` component in the `App.js` 

```
import "./App.css";
import { Provider } from "react-redux";
import store from "./store";
import Cart from "./component/Cart";

function App() {
  return (
    <Provider store={store}>
      <Cart />
    </Provider>
  );
}

export default App;
```

Just to make it a bit presentable, I have added a bit of basic styling in the `App.css` as follows. 

```
button {
  margin: 10px;
  font-size: 16px;
  letter-spacing: 2px;
  font-weight: 400;
  color: #fff;
  padding: 23px 50px;
  text-align: center;
  display: inline-block;
  text-decoration: none;
  border: 0px;
  cursor: pointer;
}
.green {
  background-color: rgb(6, 172, 0);
}
.red {
  background-color: rgb(221, 52, 66);
}
.red:disabled {
  background-color: rgb(193, 191, 191);
  cursor: not-allowed;
}
.cart {
  text-align: center;
}
```

This is how the UI looks as of now

![Screenshot 2022-05-20 at 20.01.01.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653057101372/MyQOnZ6wo.png align="left")

### 9. Reading/ Accessing the store using `useSelector` hook

`useSelector` is a hook provided by the **react-redux** library that helps us in reading the `store` and thus its content(s). Import the hook from `react-redux` and use the following syntax to read the store with `useSelector` hook

```
import { useSelector } from "react-redux";
// rest of the code
const state = useSelector((state) => state);

// rest of the code
```

Thus after adding `useSelector` hook, `Cart.js` file will look some thing like this

```
import React from "react";
import { useSelector } from "react-redux";

const Cart = () => {
  const state = useSelector((state) => state);
  console.log("store", state);
  return (
    <div className="cart">
      <h2>Number of items in Cart:</h2>
      <button className="green">Add Item to Cart</button>
      <button className="red">Remove Item from Cart</button>
    </div>
  );
};

export default Cart;
```

console logging the state will give us the initial state that we set in the reducer file in step 5.

![Screenshot 2022-05-21 at 01.10.28.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1653075753753/CMvHxfbm3.png align="left")

### 10. Dispatching Action on button click (along with handling some UI behaviour based on the state) with `useDispatch` hook

The **react-redux** library gives us another hook called the `useDispatch` hook, that helps us dispatching the **actions** or **action creators** which in turn **returns actions**. The syntax is as follows

```
const dispatch = useDispatch();

dispatch(actionObject or calling the action creator);
```

Thus adding a dispatcher into our `Cart.js` will finally make the file look some thing like this

```
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { addItem, deleteItem } from "../actions/cartAction";

const Cart = () => {
  const state = useSelector((state) => state);
  const dispatch = useDispatch();
  return (
    <div className="cart">
      <h2>Number of items in Cart: {state.numOfItems}</h2>
      <button
        onClick={() => {
          dispatch(addItem());
        }}
      >
        Add Item to Cart
      </button>
      <button
        disabled={state.numOfItems > 0 ? false : true}
        onClick={() => {
          dispatch(deleteItem());
        }}
      >
        Remove Item to Cart
      </button>
    </div>
  );
};

export default Cart;
```

Note how on click on the **Add Item to Cart** button, we `dispatch` the action creator `addItem()` that we created in step no. 7. Similarly on click on the **Remove Item from Cart** button, we dispatch the action creator `deleteItem()`. The `state` variable stores the state of the app, which is basically an object with a key `numOfItems`. Thus `state.numOfItems` gives us the current number of items value in the store. We display this in the view in the line `<h2>Number of items in Cart: {state.numOfItems}</h2>`. 

To dig a bit deeper, when the **Add Item to Cart** button is clicked, it dispatches the `addItem()` action creator, which in turn returns an `action` object with **type** `type: ADD_ITEM`. As mentioned in [Part 1](https://blog.sohamderoy.dev/understanding-redux-part-1-demystifying-store-action-and-reducers) of this blog series, when an action is dispatched, all the reducers becomes active. Currently in this example we have only one reducer i.e. `cartReducer`, thus it becomes active and listens to the `action` dispatched. As shown in step 5, the reducer takes the state and the action as input, switches on the `action type` and **returns the fresh new instance of the updated state**. In this example, when the action with `type: ADD_ITEM`, matches the first switch case, it first make a copy of the entire state using spread operator `...state`, and then make the necessary update which in the case of adding item is `numOfItems: state.numOfItems + 1` i.e. **increasing** the `numOfItems` by 1. 

Similarly, using the same logic, on clicking on the **Remove Item from Cart** button, an action with **type** `type: DELETE_ITEM` is dispatched which goes and **decreases** the `numOfItems` by 1. 

Here is the demo of the working app.

![ezgif-2-8b96ff4bf6.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1653078242537/2QHhpHTR3.gif align="left")

Notice how we were able to control the behaviour of the **Remove Item from Cart** button based on the value of `numOfItems` in the **redux store**. As a negative number of items does not makes sense, we disabled the **Remove Item from Cart** button if `state.numOfItems <= 0`. This way we are able to restrict the user from decreasing the number of items in the cart if its already 0. This was a basic example to show how we can **control the behaviour of various DOM elements** based on internal state of the app.

## Github Link

Github link of the project can be found here: [Github Link](https://github.com/sohamderoy/blog-setup-react-app-with-redux/tree/master)


## Summary

In this article, we learnt how to quickly spin up a **redux** powered **react** application. We learnt how to
- Create Actions, Action creators, Reducers and Store
- Provide the Store to the App using `<Provider>`
- Read/ access the Store from components using `useSelector` hook and display the state information in the UI
- Dispatch the actions on user events such as button clicks, using `useDispatch` hook
- Control DOM element's behaviour with logic based on the state of the application


## Wrapup

Thanks for reading! I really hope you enjoyed reading about how to spin up a redux powered react application and found this blog useful. Do consider hitting the like button and sharing it with your friends, I'd really appreciate that. Stay tuned for more amazing content! Peace out! 🖖

## Social Links

- [LinkedIn](https://www.linkedin.com/feed/)
- [Website](www.sohamderoy.dev)
- [Blog site](blog.sohamderoy.dev)


 




























