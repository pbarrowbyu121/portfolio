```
// POST requests
export function addCarAction({ commit }, payload) {
  const addCarPromise = fetch("http://localhost:5000/cars", {
    method: "POST",
    headers: {
      "Content-type": "application/json"
    },
    body: JSON.stringify(payload)
  })
  console.log("response from addCar POST", addCarPromise)
  return addCarPromise
}
```
