```js
deleteCar() {
	if(this.tanks) {
	let deleteTanksArr = this.tanks.map(tank => tank.id)
	deleteTanksArr.forEach(id => this.deleteTankAction(id))
	}
	this.deleteCarAction(this.car.id)
	.then(res => this.getCarsAction())
	.then(res => this.$router.push({ path: '/' }))
}
```
