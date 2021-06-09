```js
export function getCarsAction({ commit }) {
  fetch('http://localhost:5000/cars')
    .then((res) => res.json())
    .then((res) => {
      console.log('response from GET cars', res)
      commit('GET_CARS_MUTATION', res)
    })
    .catch((e) => {
      console.log(e)
    })
}
```
