# Redux Setup (React + NextJs + Inertia-React + React-Native)
## Recommended Extensions
<ul>
  <li>Material Icon Theme - <i>helps you understand folder structure easily using icons</i></li>
  <li>ES7+ React/Redux/React-Native snippets - <i>helps in code faster</i></li>
</ul>

## NPM Packages
<ul>
  <li><b>redux</b> ( <i>The Bigg Boss</i> )</li>
  <li><b>react-redux</b> ( <i>To connect React to Redux</i> )</li>
  <li><b>redux-devtools-extension</b> ( <i>To view the store in browser</i> )</li>
  <li><b>redux-persist</b> ( <i>Helps you persist and rehydrate your Redux state</i> )</li>
  <li><b>redux-thunk</b> ( <i>Allows you to write asynchronous logic in your Redux actions</i> )</li>
  <li><b>prop-types</b> ( <i>Needed to connect Redux actions to components</i> )</li>
  <li>npm i react-redux@7.2.6 redux@4.1.2 redux-devtools-extension@2.13.9 redux-persist@6.0.0 redux-thunk@2.4.1 prop-types</li>
</ul>

## Folder Structure
<ul>
  <li>Create a folder with name <b><i>store</i></b> in the main project.</li>
  <li>Inside that folder create 2 sub-folders & 2 files with names </li>
  <ul>
    <li>Folders - <b><i>actions</i></b> & <b><i>reducers</i></b></li>
    <li>Files - <b><i>store.js</i></b> & <b><i>selector.js</i></b> (<i>If you're using <b>Material Icon Theme</b> it'll automatically change icon to redux instead of javascript</i>)</li>
  </ul>
  <li>
    Your folder structure should look like this <br/>
    <img height="150" src="https://github.com/AaryanShaikh/My-Stock/blob/main/redux_store_folder_structure.png" />
  </li>
</ul>

## Initial Setup
<ul>
  <li>Add a type inside <b>selector.js</b> file</li>  
</ul>

### selector.js
```javascript
export const USER_DATA = "USER_DATA";
```

<ul>
  <li>Go inside <b>reducer</b> folder & create a reducer file <b>user.reducer.js</b> </li>
</ul>

### user.reducer.js
```javascript
import { USER_DATA } from "../selector";

const initialState = {
    user_data: null,
};

export default function (state = initialState, action) {
    const { type, payload } = action;

    switch (type) {
        case USER_DATA:
            return {
                ...state,
                user_data: payload,
            }

        default:
            return state;
    }
}
```

<ul>
  <li>Go inside <b>actions</b> folder & create a action file <b>user.action.js</b> file </li>
</ul>

### user.action.js
```javascript
import { USER_DATA } from "../selector";

export const setUserData = (data) => async (dispatch) => {
    try {
        // some logic code here
        dispatch({
            type: USER_DATA,
            payload: data
        });
    } catch (err) {

    }
}
```
<ul>
  <li>Go inside <b>reducer</b> folder & create an <b>index.js</b> file </li>
</ul>

### index.js (combining all the reducers)
```javascript
import { combineReducers } from 'redux';

import user from './user.reducer';

export default combineReducers({
    user,
});  
```

<ul>
  <li>Configure the store in <b>store.js</b> file</li>  
</ul>

### store.js
```javascript
import { createStore ,applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from './reducers';
// import AsyncStorage from '@react-native-async-storage/async-storage'; /* You'll need this if you're working on react-native */

import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage'; /* remove this in react-native as it will throw sync error, use AsyncStorage instead */ 

const persistConfig = {
    key: 'root',
    storage,
// storage:AsyncStorage, for react-native
  }
   
const persistedReducer = persistReducer(persistConfig, rootReducer)

const configureStore = () => {
    const store = createStore(persistedReducer, composeWithDevTools(applyMiddleware(thunk)))
    const persistor = persistStore(store)
    return { store, persistor }
}

export default configureStore;
```

<ul>
  <li>
    After actions & reducers created the structure should look like that <br/>
     <img height="250" src="https://github.com/AaryanShaikh/My-Stock/blob/main/redux_after_setup.png" />
  </li>
</ul>

## Connecting components to store
<ul>
  <li>Lets say that this is your normal component</li>
</ul>

```javascript
import { View, Text } from 'react-native'
import React from 'react'

const MyComponent = () => {
  return (
    <View>
      <Text>MyComponent</Text>
    </View>
  )
}

export default MyComponent
```

<ul>
  <li>Make the below changes</li>
</ul>

```javascript
import { View, Text } from 'react-native'
import React from 'react'
import PropTypes from "prop-types";
import { connect } from 'react-redux'
import { setUserData } from '../store/actions/user.action';

const MyComponent = ({ setUserData, user_data }) => {
    return (
        <View>
            <Text>MyComponent</Text>
        </View>
    )
}

const mapStateToProps = (state) => ({
    user_data: state.user.user_data,
})

SelectProductScreen.propTypes = {
    setUserData: PropTypes.func.isRequired,
};

export default connect(mapStateToProps, { setUserData })(MyComponent)
```
