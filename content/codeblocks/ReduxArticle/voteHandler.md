```js
const voteHandler = (e) => {
	e.preventDefault();
	if (selectedOption === "add-option") {
		addOptionHandler();
	} else {
		let editedOption = {
			...optionsList.find((option) => option.id === +selectedOption),
		};
		editedOption = { ...editedOption, count: +editedOption.count + 1 };

		voteOption(editedOption).then((res) =>
		  getOptions().then((response) => {
		    dispatch({ type: "addOption", options: response });
		  })
		);
	}
	setSelectedOption("select");
};
```