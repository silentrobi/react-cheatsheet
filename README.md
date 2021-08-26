# react-cheatsheet
## REACT REDUX

**terminologies:**
- **STORE:** store all data states
- **ACTION:** Describes what you want to do
- **REDUCER:** Describes how action transforms the state into next state. It checks which action is called and based on the action name, it modifies state related to that.
- **DISPATCH:** Execute the action means sending action to reducer and reducer executes the logic to change the state.

**Example 1**
```js
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

