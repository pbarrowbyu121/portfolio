```js
import { createSlice } from "@reduxjs/toolkit";

const optionsSlice = createSlice({
  name: "options",
  initialState: { options: [] },
  reducers: {
    setOptions(state, action) {
      state.options = action.payload;
    },
  },
});

export default optionsSlice;
```