```
getCarMakes() {
	this.loading = true
	fetch(`https://vpic.nhtsa.dot.gov/api/vehicles/getallmakes?format=json`, {
	method: "GET",
	})
	.then(res => {
	console.log("external GET Makes", res)
	return res.json()
	})
	.then(res => {
	this.makeOptionsAll = res.Results.map(result => result.Make_Name).sort()
	this.loading = false
	})
}
```
