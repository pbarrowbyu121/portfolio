```
onSubmit() {
      let editedCarObj = {
        ...this.car,
        year: this.year,
        make: this.make,
        model: this.model,
        color: this.color,
        vin: this.vin,
        license: this.license,
        name: this.name,
        image: this.image
      };
      this.editCarAction(editedCarObj).then(res => this.getCarsAction())
    }
```
