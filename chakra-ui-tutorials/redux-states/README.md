## Adding Redux based state manager to Chakra UI Project ##

1. Adding required package to package.json

```
    "react-redux": "^7.2.6",
    "redux-logger": "^3.0.1",
    "redux-thunk": "^2.4.1",
    "react-router-redux": "^4.0.8",
    "redux-devtools-extension": "^2.13.9",
    "web-vitals": "^0.2.4"
```
Note: We have the Chakra UI project with React & React-dom V 17.0.2 with react-router & react-router-dom V 5.1.2.

2. Adding store.js at the src-root (src/store.js).

3. Add reportWebVitals.js at the src-root (src/reportWebVitals.js).

4. Add agents.js at the src-root (src/agents.js)

5. Create a folder name state inside src as src/state and add the following files:

All page specific const will be defined in this index.js
/src/state/actions/
- index.js
```
export const APP_LOAD = 'APP_LOAD';
export const REDIRECT = 'REDIRECT';
export const HOME_PAGE_LOADED = 'HOME_PAGE_LOADED';
export const HOME_PAGE_UNLOADED = 'HOME_PAGE_UNLOADED';
export const LOGIN = 'LOGIN';
export const LOGOUT = 'LOGOUT';
export const REGISTER = 'REGISTER';
export const LOGIN_PAGE_UNLOADED = 'LOGIN_PAGE_UNLOADED';
export const REGISTER_PAGE_UNLOADED = 'REGISTER_PAGE_UNLOADED';
export const ASYNC_START = 'ASYNC_START';
export const ASYNC_END = 'ASYNC_END';
````

All Page specific reducers will be listed here inside reducers folder:
/src/state/reducers/
- /homeReducers.js
```
import { HOME_PAGE_LOADED, HOME_PAGE_UNLOADED } from '../actions/index';


const initialState = {
    data: [],
    loading: true,
    error: ''
}
// eslint-disable-next-line import/no-anonymous-default-export
export default (state = initialState, action) => {
    switch (action.type) {
        case HOME_PAGE_LOADED:
            return {
                ...state,
                data: action.payload,
                loading: false
            };
        case HOME_PAGE_UNLOADED:
            return {
                loading: false
            };
        default:
            return state;
    }
};

```

- /index.js
```
import {
    combineReducers
} from 'redux';

import homeReducer from './homeReducer';

export default combineReducers({
    homeReducer
});
```

6. Create a folder name utils inside src as src/utils and add the following files:

```
src/utils/helpers.js
export const createActions = (type, payload) => {
    const dto = {
        type,
    };

    if (payload) {
        dto.payload = payload;
    }

    return dto;
};
```

7. 