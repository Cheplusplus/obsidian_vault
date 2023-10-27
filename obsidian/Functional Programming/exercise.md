# Exercise: Function Programming

## Overview

**This exercise  requires the formation of teams, comprising 3 to 6 members, to collaboratively develop a tic-tac-toe app in JavaScript.** 

It is important to note that the primary objective of this exercise is not necessarily the final product, but the learning and insights gained during the process. At the end of the exercise each team will be required to presentation the insights that were gained during the process, with a specific focus on knowledge or understanding that they did not have before starting the process.

## Requirements
    
- HTML should be created by means of `lit-html` library alone (via CDN)
- `lit-html` should derive HTML structure from `state` object
- No direct DOM manipulations are allowed

Teams will make use of the following global store file called `store.js` to manage interactions in the app:

```js
// @ts-check

/**
 * @typedef {object} State
 *
 * @prop {string} example - Describe your store object here with props...
 */

/**
 * @typedef {object} Action - An object that describes chan ges that should be
 * made to global state. Actions are often dispatched to the due to a specific
 * user interaction, such as a button click, and is therefore best described
 * from the perspective of what occurred instead of what should be done. This
 * leaves the reducer to decide what to should actually change based on the
 * action.
 *
 * @prop {'example1' | 'example2'} type - Possible action types that can be
 * dispatched to the store
 *
 * @prop {Record<string, any>} payload - An object that can be any shape. The
 * payload object is dispatched along with the action type, and provide
 * additional context about the specific action to the reducer.
 *
 */

/**
 * @callback Subscription
 *
 * A function that is automatically called whenever a new state is add to the
 * store. This ensures that all side-effects in the app are contained and scoped
 * exclusively to the subscription function. This allows the rest of the app to
 * remain purely functional.
 *
 * @param {State} state - Most recent state added to the store
 * @returns {void}
 */

/**
 * @callback Reducer
 *
 * A pure function that takes an existing state and uses the information
 * supplied by means of an action to determine what the next state should be.
 * The reducer should never mutate the existing state, but instead return a new
 * state object that is the result of the action. This makes it easy to debug
 * how state changes in our app.
 *
 * @param {State} state
 * @param {Action} action
 * @returns {State}
 */

/**
 * @typedef {object} Store
 * @prop {State} State
 * @prop {Subscription} Subscription
 * @prop {Reducer} Reducer
 */

/**
 * @type {Reducer}
 */
const reducer = (state, action) => {
  const { type, payload } = action;

  switch (type) {
    case "example1": {
      return {
        ...state,
      };
    }

    case "example2": {
      return {
        ...state,
      };
    }

    default:
      return state;
  }
};

/**
 * @param {object} props
 *
 * @param {State} props.starting - The initial starting state of the store, will
 * be placed at the start of the history.
 *
 * @param {Subscription} props.subscription - A function that is called whenever a
 * new state is created by an action.
 */
export const create = (props) => {
  const { starting, subscription } = props;

  /**
   * A linear list of states, ordered chronological as changes are made to the
   * internal app store. This allows the preservation of all states transitions
   * for debugging purposes, and also user-facing functionality such as undo,
   * redo and viewing their interaction history.
   *
   * Note that when it is declared the first time in the store, it is important
   * to include ensure that a starting state object is created.
   *
   * @type {State[]}
   */
  let history = [starting];

  /**
   * ...
   *
   * @returns {State} - The latest state in the store
   */
  const getState = () => Object.freeze({ ...history[0] });

  /**
   * ...
   *
   * @param {Action} action
   */
  const dispatch = (action) => {
    const prev = getState();
    const next = reducer(prev, action);
    history = [next, ...history];
    subscription(getState());
  };

  return {
    getState,
    dispatch,
  };
};

export const Store = {
  create,
};
```
