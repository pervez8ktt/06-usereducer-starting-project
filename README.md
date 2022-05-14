- [Home](https://github.com/pervez8ktt/React)
# Using useReducer() Hook (v-117)
- [Git Repo](https://github.com/pervez8ktt/06-usereducer-starting-project)
- [Tutorial Git Repo](https://github.com/pervez8ktt/react-complete-guide-code-1/tree/10-side-effects-reducers-context-api)

![intro](public/images/introducing_usereducer.png)

![intro](public/images/understanding_usereducer.png)


# Steps to use useReducer hook 

#### [Login.js](src/components/Login/Login.js)

- need to import useReducer

 ```js
 import React, { useState, useEffect, useReducer } from 'react';
 ```

 - Initialize resucer function

 ```js

 const Login = (props) => {
  
  const [emailState, dispatchEmail] =  useReducer(emailReducer,{

    value:'',
    isValid:false

});


```

- **emailState**: is the state function which is used in component re-render/re-evelution
- **dispatchEmail**: A function that can be used to dispatch a new action(i.e. trigger an update of the state)
- **emailReducer**: A function that is triggered automatically  once an action is dispatched via dispatch function (dispatchEmail()). It receives the latest state snapshot and should return the new, updated state.
- **Initial Function**: The initial state.

#### Define emailReducer

```js
const emailReducer= (state, action) =>{

  if(action.type==='USER_INPUT'){
    return {

      value:action.val,
      isValid:action.val.includes('@')
  }  
  }

  if(action.type==='INPUT_BLUR'){
    return {

      value:state.value,
      isValid:state.value.includes('@')
  }
  }


  return {

      value:'',
      isValid:false

  }

};
```

- This function define outside the component. Because this function not required any data, which is genereted inside the component function.
- Reducer function always return new Snapshot of state

#### Call dispatch function.

Reducer function automatically executed, once dispatch function called

```js

const emailChangeHandler = (event) => {
    dispatchEmail({type:'USER_INPUT', val: event.target.value});

    
  };
```

```js
const validateEmailHandler = () => {
    dispatchEmail({type:'INPUT_BLUR'});
  };

```

#### use state variable to re-render/re-eveluate component

```js

<input
            type="email"
            id="email"
            value={emailState.value}
            onChange={emailChangeHandler}
            onBlur={validateEmailHandler}
          />

```

# useReducer Hook with useEffect Hook. (v-118)

As we know that useEffect hook function will call when it's dependency changes. Into useReducer state, we have an object. So if we wants to use useReducer state into useEffect dependency, we need to follow below steps

- Define a variable. We can use object extractor also which is the feature of javascript

```js
const {isValid: emailIsValid} = emailState;
```

here **isValid** is the property of *emailState* and **emailIsValid** is constant in which we pulling out the value of isValid

- Now we can use **emailIsValid** as dependency into *useEffect* hook

```js
useEffect(() => {
    const identifier = setTimeout(() => {
      console.log('Checking form validity!');
      setFormIsValid(
        emailIsValid && passwordIsValid
      );
    }, 500);

    return () => {
      console.log('CLEANUP');
      clearTimeout(identifier);
    };
  }, [emailIsValid, passwordIsValid]);
  ```

  # useState() vs useReducer() (v-120)

  ![image](public/images/use_reducer_vs_use_state.png)

# Introducing React Context (Context API) (v-121)

- It is used where long prop chain made.
![image](public/images/long_prop_chanin.png)

- It is used to trigger direct action without using component-wide prop chain
![image](public/images/introduction_react_context.png)


