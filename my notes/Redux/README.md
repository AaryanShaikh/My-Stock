# Redux Setup (React + NextJs + Inertia-React + React-Native)
## Recommended Extensions
<ul>
  <li>Material Icon Theme - <i>helps you understand folder structure easily using icons</i></li>
  <li>ES7+ React/Redux/React-Native snippets - <i>helps in code faster</i></li>
</ul>

## NPM Packages
<ul>
  <li><b>redux</b> ( <i>The Bigg Boss</i> )</li>
  <li><b>react-redux</b> ( <i>The react variant</i> )</li>
  <li><b>redux-devtools-extension</b> ( <i>To view the store in browser</i> )</li>
  <li><b>redux-persist</b> ( <i>Helps you persist and rehydrate your Redux state</i> )</li>
  <li><b>redux-thunk</b> ( <i>Allows you to write asynchronous logic in your Redux actions</i> )</li>
  <li>npm i redux react-redux redux-persist redux-thunk redux-devtools-extension</li>
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
    <img height="300" src="https://dummyimage.com/134x118/000/fff" />
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
<li>Go inside <b>reducer</b> folder & create an <b>index.js</b> file </li>
</ul>

### store.js
```javascript
import { createStore ,applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage';

const persistConfig = {
    key: 'root',
    storage,
  }
   
const persistedReducer = persistReducer(persistConfig, rootReducer)

const configureStore = () => {
    const store = createStore(persistedReducer, composeWithDevTools(applyMiddleware(thunk)))
    const persistor = persistStore(store)
    return { store, persistor }
}

export default configureStore;
```

## Fetch and Store data in Redux
<ul>
  <li>Create a folder by the name of the component (e.g. Taxi)</li>
  <li>Create these files
    <ul>
      <li>[name]ActionTypes.js (e.g. taxiActionTypes.js)
        <ul>
          <code>SET_GROUP_BOOKING_TAXI_DATA: 'SET_GROUP_BOOKING_TAXI_DATA'</code>
        </ul>
      </li>
      <li>[name]Action.js (e.g. taxiAction.js)
        <ul>
          <pre>export const setGroupBookingTaxiData = data => ({
              type: taxiActionTypes.SET_GROUP_BOOKING_TAXI_DATA,
              payload: data
           })</pre>
        </ul>
      </li>
      <li>[name]Reducer.js (e.g. taxiReducer.js)
        <ul>
          <li>Initial State
            <ul>
              <code>groupBookingTaxiData: [] </code>
            </ul>
          </li>
          <li>below in the reducer
            <ul>
              <pre>case taxiActionTypes.SET_GROUP_BOOKING_TAXI_DATA:
  return {
   ...state,
   groupBookingTaxiData: action.payload
}</pre>
            </ul>
          </li>
        </ul>
      </li>
      <li>[name]Selector.js (e.g. taxiSelector.js)
        <ul>
          <pre>export const selectGroupBookingTaxiData = createSelector(
    [selectTaxiAll],
    (taxiData) => taxiData.groupBookingTaxiData
)</pre>
        </ul>
      </li>
    </ul>
  </li>
  <li>In Program
    <ul>
      <li>imports
        <ul>
          <pre>import { connect } from 'react-redux';
import { setGroupBookingTaxiData } from '../../redux/taxi/taxiAction';
import { createStructuredSelector } from 'reselect';
import { selectGroupBookingTaxiData } from '../../redux/taxi/taxiSelector';</pre>
        </ul>
      </li>
      <li>Access data from redux
        <ul>
          <li>the (groupBookingTaxiData) value should be passed to props (this is used to accessed the data)</li>
          <pre>const mapStateToProps = createStructuredSelector({
    groupBookingTaxiData: selectGroupBookingTaxiData
})</pre>
        </ul>
      </li>
      <li>Store data from redux
        <ul>
          <li>the (setGroupBookingTaxiData) value should be passed to props (this is used to set the data)</li>
          <pre>const mapDispatchToProps = (dispatch) => ({
    setGroupBookingTaxiData: (data) => dispatch(setGroupBookingTaxiData(data))
})</pre>
        </ul>
      </li>
      <li>changing default export
        <ul>
          <code>export default connect(mapStateToProps, mapDispatchToProps)(TaxiSearchContainer)</code>
        </ul>
      </li>
    </ul>
  </li>
</ul>
