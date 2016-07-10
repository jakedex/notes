## [CSS](https://medium.freecodecamp.com/leveling-up-css-44b5045a2667#.3cuv9q1ss) Notes

### [BEM naming scheme](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

```
.block {}  
.block__element {}  
.block--modifier {}  
```

_block_ repesents the high level of an abstraction or component

_.block__element_ repesents a descendent of block

_.block--modifier_ repesents a different state or version of block

```
.person {}
.person__hand {}
.person--female {}
.person--female__hand {}
.person__hand--left {}
```

