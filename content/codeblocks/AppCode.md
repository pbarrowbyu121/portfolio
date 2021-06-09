```js
<template>
  <div id="q-app" class="text-krona-one">
    <router-view />
  </div>
</template>
<script>
import { mapActions } from "vuex"

export default {
  name: "App",
  methods: {
    ...mapActions("carstore", ["getTanksAction", "getCarsAction"]),
  },
created() {
    this.getCarsAction()
    this.getTanksAction()
  }
};
</script>
```
