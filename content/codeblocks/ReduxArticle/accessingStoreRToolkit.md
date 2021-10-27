```js
import { useSelector } from "react-redux";
import PollItem from "./PollItem";
import { Container } from "react-bootstrap";

function PollList() {
  const questions = useSelector((state) => state.questions.questions);
  const optionsList = useSelector((state) => state.options.options);

  return (
    <Container>
      {questions.map((question) => (
        <PollItem
          key={question.id}
          questionObj={question}
          optionsList={optionsList.filter(
            (option) => option.questionId === question.id
          )}
        />
      ))}
    </Container>
  );
}

export default PollList;
```