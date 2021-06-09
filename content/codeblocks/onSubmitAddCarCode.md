```js
onSubmit() {
	let newCarObj = {
	id: uid(),
	year: this.year,
	make: this.make,
	model: this.model,
	color: this.color,
	vin: this.vin,
	license: this.license,
	name: this.name,
	image: this.image
	};
	this.addCarAction(newCarObj).then(response => this.getCarsAction())
},
```
