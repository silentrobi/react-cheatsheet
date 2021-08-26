# react-cheatsheet
## REACT REDUX

**terminologies:**
- **STORE:** store all data states
- **ACTION:** Describes what you want to do
- **REDUCER:** Describes how action transforms the state into next state. It checks which action is called and based on the action name, it modifies state related to that.
- **DISPATCH:** Execute the action means sending action to reducer and reducer executes the logic to change the state.

**Basic React Redux Example**
```js
import { createStore } from 'react-redux'
/*ACTIONS*/

//ACTION INCREMENT
const increment = () =>{ 
      return {
          type: 'INCREMENT'
      }
};
//ACTION DECREMENT
const decrement = () =>{ 
      return {
          type: 'DECREMENT'
      }
};

/*REDUCERS*/

//REDUCER COUNTER
const counter = (state=0, action) =>{
    switch(action.type){
        case 'INCREMENT':
            return state + 1;
        case  'DECREMENT':
            return state - 1;
        default:
            return state;
    }
};

/*STORE*/
const store = createStore(counter); // passing reducer method count

//Display it in the console
store.subscribe(() => console.log(store.getState());

/*DISPATCH*/
store.dispatch(increment()); //calling action method increment 
```

**Working with more than one `reducer` example**

```js

import { createStore, combineReducer } from 'react-redux'

/*REDUCERS*/

//REDUCER counterReducer
const counterReducer = (state=0, action) =>{
    switch(action.type){
        case 'INCREMENT':
            return state + 1;
        case  'DECREMENT':
            return state - 1;
        default:
            return state;
    }
};

//REDUCER loggedReducer

const loggerReducer = (state=false, action) =>{
     switch(action.type){
        case 'SIGN_IN':
            return !state;
        default:
            return state;
    }
}

/*STORE*/
// To connect multiple reducers use the following methods

//First combine the reducers

const allReducers = combineReducer({
      counterReducer,
      loggedReducer
});

const store = createStore(allReducers);

```














