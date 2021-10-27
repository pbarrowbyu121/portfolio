```js
function PollItem({ questionObj, optionsList }) {
  const [selectedOption, setSelectedOption] = useState("select");
  const [newOptionText, setNewOptionText] = useState("");
  const dispatch = useDispatch();

```