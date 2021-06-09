```js
// PUT requests
export function editCarAction({}, payload) {
  const editCarPromise = fetch(`http://localhost:5000/cars/${payload.id}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(payload),
  })
  console.log('response from PUT car', editCarPromise)
  return editCarPromise
}
```
