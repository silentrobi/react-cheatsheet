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
      const counter = useSelector(state => state.counterReducer) {/* useSelector() has access to all store reducers. */}
      return (
            <div>
                  <h1>Counter: {counter}</h1>
            </div>
      );
}

/* UPDATE counter state*/
import { useDispatch } from 'react-redux';

function App() {
      const counter = useSelector(state => state.counterReducer); {/* useSelector() has access to all store reducers. */}
      const dispatch = useDispatch();
      return (
            <div>
                  <h1>Counter: {counter}</h1>
                  <button 
                        onClick={dispatch(increment())} {/* increment is action method */}
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

## Use of `connect()` HOC
**Usecase:** Changing a state in one component should update the same state in another component.
**Solution:** Wrap both components with connect() HOC and pass same `mapDispatchToProps` and `mapStatetoProps`.
Another way to pass redux store is by using `connect` HOC. The connect() function connects a React component to a Redux store.
It provides its connected component with the pieces of the data it needs from the store, and the functions it can use to dispatch actions to the store. 
**Example to use `connect`**

```js
const increment = (number) => { 
      return {
          type: 'INCREMENT',
          payload: number
      }
};
const increment = (number) => { 
      return {
          type: 'DECREMENT',
          payload: number
      }
};

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

// counter state will be passed to App component as props
const mapStatetoProps= (state) => ({
      counter: state.counterReducer   // return counter value in each state change
});

//increment and decrement dispatch methods will be passed to App component as props
const mapDispatchToProps = (dispatch) =>({
      actions:{
            increment: (payload) => {
                  dispatch(increment(payload))
            },
            decrement: (payload) => {
                  dispatch(decrement(payload))
            }
      }
});

//Wraping child component with connect() and passing only mapDispatchToProps. The reason is we don't to display counter value in child component.
const Child = connect(null, mapDispatchToProps)(props){
 const {actions} = props;
      return (
            <div>
                  <button 
                        onClick={actions.decrement(1)} {/* decrement is action method by 1. Here 1 is the payload */}
                  >-</button>
            </div>
      );
}

function App(props) {
      const {counter, actions} = props;
      return (
            <div>
                  <h1>Counter: {counter}</h1>
                  <button 
                        onClick={actions.increment(5)} {/* increment is action method by 5. Here 5 is the payload */}
                  >+</button>
                  <Child/> {/*Child component will control decrement of the counter value */}
            </div>
      );
};

export default connect(mapStateToProps, mapDispatchToProps)(App); // wraping App component with connect() HOC
```
**Redux devtool extension**

link ---> https://github.com/reduxjs/redux-devtools 













