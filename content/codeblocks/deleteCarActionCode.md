```
// DELETE requests
export function deleteCarAction({}, payload) {
  const deleteCarPromise = fetch(`http://localhost:5000/cars/${payload}`, {
    method: "DELETE"
  })
  console.log("response from DELETE car", deleteCarPromise)
  return deleteCarPromise
}
```
