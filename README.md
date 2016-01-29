## You don't (may not) know about Lodash/Underscore 

In response to [You-Dont-Need-Lodash-Underscore](https://github.com/cht8687/You-Dont-Need-Lodash-Underscore) made by [@cht8687](https://github.com/cht8687), yes some of the methods could be replaced by native methods. This is not the case when things get a bit more complex. According to the [Lodash](https://lodash.com/) author, [@jdalton](https://github.com/jdalton):

> If you're only using a handful of methods on arrays and don't care about nullish guards, object iteration, smoothing over enviro/ES5/ES6 issues, FP goodies, iteratee shorthands, lazy evaluation, or other enhancements then built-ins are the way to go. Folks who use lodash know its 270+ modules work great combo'ed with ES6, enabling cleaner code and empowering beyond built-ins.

Here lists the differences.


## Quick links

1. [_.each](#_each)
1. [_.map](#_map)
1. [_.every](#_every)
1. [_.some](#_every)
1. [_.reduce](#_reduce)
1. [_.reduceRight](#_reduceright)
1. [_.filter](#_filter)
1. [_.find](#_find)
1. [_.findIndex](#_find)
1. [_.indexOf](#_indexof)
1. [_.lastIndexOf](#_lastindexof)
1. [_.includes](#_includes)
1. [_.keys](#_keys)
1. [_.size](#_size)
1. [_.isNaN](#_isnan)
1. [_.reverse](#_reverse) 


## _.each

Underscore/Lodash may exit iteration early by explicitly returning `false`.

  ```js
  // Underscore/Lodash
  _.each([1, 2, 3], function(value, index) {
    console.log(value);
    return false;
  });
  // output: 1

  // Native
  [1, 2, 3].forEach(function(value, index) {
    return false; // does not exit the iteration!
  });
  // output: 1 2 3
  ```

### Performance

Lodash|Underscore|Native 
--- | --- | ---
972,874|101,878|102,864 (**89% slower**)|

**[⬆ back to top](#quick-links)**


## _.map

Native doesn't support the `_.property` iteratee shorthand

  ```js
  // Underscore/Lodash
  var users = [
    { 'user': 'barney' },
    { 'user': 'fred' }
  ];
  var arr = _.map(users, 'user');
  console.log(arr);
  // output: ['barney', 'fred']

  // Native
  var users = [
    { 'user': 'barney' },
    { 'user': 'fred' }
  ];
  var arr = users.map('user');
  // error!
  ```

### Performance

Lodash|Underscore|Native 
--- | --- | ---
1,214,010|1,171,239|192,404 (**94% slower**)|

**[⬆ back to top](#quick-links)**


## _.every

  ```js
  // Underscore/Lodash
  function isLargerThanTen(element, index, array) {
    return element >=10;
  }
  var array = [10, 20, 30];
  var result = _.every(array, isLargerThanTen);
  console.log(result);
  // output: true

  // Native
  function isLargerThanTen(element, index, array) {
    return element >=10;
  }

  var array = [10, 20, 30];
  var result = array.every(isLargerThanTen);
  console.log(result);
  // output: true
  ```

**[⬆ back to top](#quick-links)**


## _.some

  ```js
  // Underscore/Lodash
  function isLargerThanTen(element, index, array) {
    return element >=10;
  }
  var array = [10, 9, 8];
  var result = _.some(array, isLargerThanTen);
  console.log(result);
  // output: true

  // Native
  function isLargerThanTen(element, index, array) {
    return element >=10;
  }

  var array = [10, 9, 8];
  var result = array.some(isLargerThanTen);
  console.log(result);
  // output: true
  ```

**[⬆ back to top](#quick-links)**


## _.reduce

  ```js
  // Underscore/Lodash
  var array = [0, 1, 2, 3, 4];
  var result = _.reduce(array, function (previousValue, currentValue, currentIndex, array) {
    return previousValue + currentValue;
  });
  console.log(result);
  // output: 10

  // Native
  var array = [0, 1, 2, 3, 4];
  var result = array.reduce(function (previousValue, currentValue, currentIndex, array) {
    return previousValue + currentValue;
  });
  console.log(result);
  // output: 10
  ```

**[⬆ back to top](#quick-links)**


## _.reduceRight

  ```js
  // Underscore/Lodash
  var array = [0, 1, 2, 3, 4];
  var result = _.reduceRight(array, function (previousValue, currentValue, currentIndex, array) {
    return previousValue - currentValue;
  });
  console.log(result);
  // output: -2

  // Native
  var array = [0, 1, 2, 3, 4];
  var result = array.reduceRight(function (previousValue, currentValue, currentIndex, array) {
    return previousValue - currentValue;
  });
  console.log(result);
  // output: -2
  ```

**[⬆ back to top](#quick-links)**


## _.filter

  ```js
  // Underscore/Lodash
  function isBigEnough(value) {
    return value >= 10;
  } 
  var array = [12, 5, 8, 130, 44];
  var filtered = _.filter(array, isBigEnough);
  console.log(filtered);
  // output: [12, 130, 44]

  // Native
  function isBigEnough(value) {
    return value >= 10;
  } 
  var array = [12, 5, 8, 130, 44];
  var filtered = array.filter(isBigEnough);
  console.log(filtered);
  // output: [12, 130, 44]
  ```

**[⬆ back to top](#quick-links)**


## _.find

  ```js
  // Underscore/Lodash
  var users = [
    { 'user': 'barney',  'age': 36, 'active': true },
    { 'user': 'fred',    'age': 40, 'active': false },
    { 'user': 'pebbles', 'age': 1,  'active': true }
  ];

  _.find(users, function(o) { return o.age < 40; });
  // output: object for 'barney'

  // Native
  var users = [
    { 'user': 'barney',  'age': 36, 'active': true },
    { 'user': 'fred',    'age': 40, 'active': false },
    { 'user': 'pebbles', 'age': 1,  'active': true }
  ];

  users.find(function(o) { return o.age < 40; });
  // output: object for 'barney'
  ```

**[⬆ back to top](#quick-links)**


## _.findIndex

  ```js
  // Underscore/Lodash
  var users = [
    { 'user': 'barney',  'age': 36, 'active': true },
    { 'user': 'fred',    'age': 40, 'active': false },
    { 'user': 'pebbles', 'age': 1,  'active': true }
  ];

  var index =  _.findIndex(users, function(o) { return o.age >= 40; });
  console.log(index);
  // output: 1

  // Native
  var users = [
    { 'user': 'barney',  'age': 36, 'active': true },
    { 'user': 'fred',    'age': 40, 'active': false },
    { 'user': 'pebbles', 'age': 1,  'active': true }
  ];

  var index =  users.findIndex(function(o) { return o.age >= 40; });
  console.log(index);
  // output: 1
  ```

**[⬆ back to top](#quick-links)**


## _.indexOf

  ```js
  // Underscore/Lodash
  var array = [2, 9, 9];
  var result = _.indexOf(array, 2);    
  console.log(result); 
  // output: 0

  // Native
  var array = [2, 9, 9];
  var result = array.indexOf(2);    
  console.log(result); 
  // output: 0
  ```

**[⬆ back to top](#quick-links)**


## _.lastIndexOf

  ```js
  // Underscore/Lodash
  var array = [2, 9, 9, 4, 3, 6];
  var result = _.lastIndexOf(array, 9);    
  console.log(result); 
  // output: 2

  // Native
  var array = [2, 9, 9, 4, 3, 6];
  var result = array.lastIndexOf(2);    
  console.log(result); 
  // output: 0
  ```

**[⬆ back to top](#quick-links)**


## _.includes

  ```js
  var array = [1, 2, 3];
  // Underscore/Lodash - also called with _.contains
  _.includes(array, 1);
  // → true

  // Native
  var array = [1, 2, 3];
  array.includes(1);
  // → true
  ```

**[⬆ back to top](#quick-links)**


## _.keys

  ```js
  // Underscore/Lodash 
  var result = _.keys({one: 1, two: 2, three: 3});
  console.log(result);
  // output: ["one", "two", "three"]

  // Native
  var result2 = Object.keys({one: 1, two: 2, three: 3});
  console.log(result2); 
  // output: ["one", "two", "three"]
  ```

**[⬆ back to top](#quick-links)**


## _.size

Return the number of values in the collection.

  ```js
  // Underscore/Lodash
  var result = _.size({one: 1, two: 2, three: 3});
  console.log(result);
  // output: 3

  // Native
  var result2 = Object.keys({one: 1, two: 2, three: 3}).length;
  console.log(result2); 
  // output: 3
  ```


## _.isNaN

  ```js
  // Underscore/Lodash
  console.log(_.isNaN(NaN));
  // output: true

  // Native
  console.log(isNaN(NaN));
  // output: true
  ```

**[⬆ back to top](#quick-links)**


## _.reverse

  ```js
  // Lodash
  var array = [1, 2, 3];
  console.log(_.reverse(array));
  // output: [3, 2, 1]

  // Native
  var array = [1, 2, 3];
  console.log(array.reverse());
  // output: [3, 2, 1]
  ```

**[⬆ back to top](#quick-links)**


## Reference

* [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
* [Underscore.js](http://underscorejs.org)
* [Lodash.js](https://lodash.com/docs)
* [jsPerf](https://jsperf.com)


# License

MIT