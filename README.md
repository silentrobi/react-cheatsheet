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

import { createStore, combineReducer, Provider } from 'react-redux'

/* ACTIONS*/

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


/*PASS `**store** object` TO REACT APP*/

ReactDOM.render(
      <Provider store={store}>
            <App/>
      </Provider>,
      document.getElementById('root')
);

/*Display counter state in react app*/
import { useSelector } from 'react-redux';

function App() {
      const counter = useSelector(state => state.counterReducer) // have access to all store reducers.
      return (
            <div>
                  <h1>Counter: {counter}</h1>
            </div>
      );
}

/* UPDATE counter state*/
import { useDispatch } from 'react-redux';

function App() {
      const counter = useSelector(state => state.counterReducer); // useSelector() has access to all store reducers.
      const dispatch = useDispatch();
      return (
            <div>
                  <h1>Counter: {counter}</h1>
                  <button 
                        onClick={dispatch(increment())} {// increment is action method}
                  >+</button>
            </div>
      );
}
```
**Pass paramter(s) to action method example**
```js
//changing increment action method
const increment = (number) => { 
      return {
          type: 'INCREMENT',
          payload: number
      }
};

//changing reducer method as well

const counterReducer = (state=0, action) =>{
    switch(action.type){
        case 'INCREMENT':
            return state + action.payload;
        case  'DECREMENT':
            return state - 1;
        default:
            return state;
    }
};

/* UPDATE counter state by payload*/
import { useDispatch } from 'react-redux';

function App() {
      const counter = useSelector(state => state.counterReducer); // useSelector() has access to all store reducers.
      const dispatch = useDispatch();
      return (
            <div>
                  <h1>Counter: {counter}</h1>
                  <button 
                        onClick={dispatch(increment(5))} {// increment is action method by 5. Here 5 is the payload}
                  >+</button>
            </div>
      );
}
```
**Redux devtool extension**

link ---> https://github.com/reduxjs/redux-devtools 













