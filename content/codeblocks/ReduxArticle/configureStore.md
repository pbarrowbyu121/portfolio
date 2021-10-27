```js
const store = configureStore({
  reducer: {
    questions: questionsSlice.reducer,
    options: optionsSlice.reducer,
  },
});

export default store;
```