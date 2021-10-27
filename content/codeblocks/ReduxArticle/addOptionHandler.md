```js
  function addOptionHandler() {
    const newOption = {
      text: newOptionText,
      count: 1,
      questionId: questionObj.id,
    };

    addOption(newOption).then((response) => {
      getOptions().then((response) => {
        dispatch({ type: "addOption", options: response });
      });
    });
  }
```