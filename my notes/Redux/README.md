# Fetch and Store data in Redux
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
