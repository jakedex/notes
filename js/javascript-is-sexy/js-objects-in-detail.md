# [Javascript Objects In Detail](http://javascriptissexy.com/javascript-objects-in-detail/)

### Object data properties have attributes
Each data property (object property that store data) has not only the name-value pair, but also 3 attributes (the three attributes are set to true by default):  

* Configurable Attribute: Specifies whether the property can be deleted or changed.
* Enumerable: Specifies whether the property can be returned in a for/in loop.
* Writable: Specifies whether the property can be changed.

#### Constructor Pattern for Creating Objects
```javascript
function Fruit (theColor, theSweetness, theFruitName, theNativeToLand) {
​
    this.color = theColor;
    this.sweetness = theSweetness;
    this.fruitName = theFruitName;
    this.nativeToLand = theNativeToLand;
​
    this.showName = function () {
        console.log("This is a " + this.fruitName);
    }
​
    this.nativeTo = function () {
    this.nativeToLand.forEach(function (eachCountry)  {
       console.log("Grown in:" + eachCountry);
        });
    }
​
​
}
```

#### Prototype Pattern for Creating Objects
```javascript
function Fruit () {
​
}
​
Fruit.prototype.color = "Yellow";
Fruit.prototype.sweetness = 7;
Fruit.prototype.fruitName = "Generic Fruit";
Fruit.prototype.nativeToLand = "USA";
​
Fruit.prototype.showName = function () {
console.log("This is a " + this.fruitName);
}
​
Fruit.prototype.nativeTo = function () {
            console.log("Grown in:" + this.nativeToLand);
}
```


### Own and Inherited Properties
Objects have both inherited and own properties. To find out if a property exists on an object (either as an inherited or an own property), you use the `in` operator. To find out whether a property is one of the object's own properties, use `hasOwnProperty`
