```js
const pollReducer = (state = { questions: [], options: [] }, action) => {
  if (action.type === "setQuestions") {
    return {
      questions: action.questions,
      options: state.options,
    };
  }
  if (action.type === "setOptions") {
    return {
      questions: state.questions,
      options: action.options,
    };
  }
  return state;
};
```