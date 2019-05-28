# DEVELOPMENT GUIDE

## Add a new API request

Imagine that we need to get a list of dogs' names through an API.

### 1. API

First you need the `api`: create the file `api\dogs.js`, and create the method that makes the HTTP request to the API to get the dogs' names.

### 2. Constants

Then you need the actions names, which are `constants\dogs.js`: create the file `constants\dogs` and add there the constants: `DOGS_GET_NAMES_REQUEST`, `DOGS_GET_NAMES_SUCCESS` and `DOGS_GET_NAMES_FAILURE`.
You can use the method `createRequestConstants` to make it easier.

### 3. Actions creators

Next step is to write the action creator: create the file `actions\dogs.js` and export there a function which returns an object, which is the action itself.
The action object has a property `type`, which is the name of the action (example: `DOGS_GET_NAMES_REQUEST`), and the other properties represent the payload.

### 4. Sagas

Then we need to write the saga, which specifies for each action, the API request to make: create the file `sagas\dogs.js`.
Create a generator (`function*`) that invokes the api (`api\dogs`) and that invokes with `put` the actions for `SUCCESS` or `FAILURE`.

Export it in an array, then import it and add it in the root saga in the file `sagas\index.js`.

### 5. Reducers

Next step is to manage the state of the application based on the dispatched actions: create the file `reducers\dogs`.
Create an object as the initial state, then export a function that takes it as a parameter and returns a new objects, based on the actions dispatched (with a `switch`).

The initial state should have (at least) 3 properties:

```js
const initialState = {
  dogsFetching: false,
  dogsData: null,
  dogsError: null,
};
```

Export the function and import it in the root reducer in the file `reducers\index.js`.

### 6. Component (UI)

Last step is to create a component which dispatches the action to `REQUEST` the data and then shows it when it's ready: create the file `components\Dogs`.
