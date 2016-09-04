# redux-call-api-middleware
Redux middleware for making async api call easy and predictably.

## Usage
1. Import the middleware first;
2. Create actions just like synchronous action creators, such as:
```javascript
  export function completeTodo(id) {
    return {
      types: {
        requestTypes: types.FETCHING,
        successTypes: [types.FETCH_SUCCESSFUL, types.COMPLETE_TODO],
        failureTypes: types.FETCH_FAILED,
      },
      callAPI: () => TodoService.getInstance().completeTodo(id),
      payload: { id },
    };
  }
```

## Parameters
- `types`
  + `requestTypes`: action type(s), can be string or array, compulsory. This/Those action(s) will be dispatched at the very beginning of async api call.
  + `successType`: action type(s), can be string or array, compulsory. This/Those action(s) will be dispatched when the async api call has been resolved. A `response` property will be attached to the action.
  + `failureTypes`: action type(s), can be string or array, optional. This/Those action(s) will be dispatched when the async api call has been rejected. A `error` property will be attched to the action.
- `callAPI`: Asynchronous function to be called, its should return a promise object.
- `payload`: Properties should be attached to action. It should be an object.
