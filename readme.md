# redux-state-machine

Implementation `javascript-state-machine` to __Redux__.

Redux Action is Event for FSM. It changing FSM `state.status`
and remember in `state.event`.

Default `state.status` is `INIT`.

Features:
* Parallel and Nested states
* Recognizable API (a-lia `javascript-state-machine`)
* Encapsulate Payload
* Easy state check (by the key)

## Install

```
npm install redux-state-machine --save
```

## Usage

Describe reducer:
```ES6
import reducerBuilder from 'redux-state-machine';

export reducerBuilder({
  events: [
    { event: 'LOAD', from: 'INIT', to: 'LOADING' },
    { event: 'SUCCESS', from: 'LOADING', to: 'LOADING_SUCCESS' },
    { event: 'FAILURE', from: 'LOADING', to: 'LOADING_FAILURE' }
  ]
})
```

Initial reducer state is
```javascript
  { status: 'INIT', event: null,
    error: null, INIT: true }
```


After dispatch action `LOAD` from `INIT` state, reducer state is
```javascript
  { status: 'LOADING', action: { type: 'LOAD' /* payload */ },
    error: null, LOADING: true }
```

After dispatch action `SUCCESS` from `LOADING` state, reducer state is
```javascript
  { status: 'LOADING_SUCCESS', action: { type: 'SUCCESS' /* payload */ },
    error: null, LOADING_SUCCESS: true }
```

After dispatch action `FAILURE` from `LOADING` state, reducer state is
```javascript
  { status: 'LOADING_FAILURE', action: { type: 'FAILURE' /* payload */ },
    error: null, LOADING_FAILURE: true }
```

After dispatch action `LOAD` from `LOADING_SUCCESS` state __(error case)__ reducer state is
```javascript
  { status: 'LOADING_SUCCESS', action: { type: 'LOAD' /* payload */ },
    error: true, LOADING_SUCCESS: true }
```