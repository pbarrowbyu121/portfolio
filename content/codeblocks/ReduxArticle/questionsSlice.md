```js
import { createSlice } from "@reduxjs/toolkit";

const questionsSlice = createSlice({
  name: "questions",
  initialState: { questions: [] },
  reducers: {
    setQuestions(state, action) {
      state.questions = action.payload;
    },
  },
});

export default questionsSlice;
```