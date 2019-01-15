# named-curry

namedCurry is a JavaScript utility that turns any function that receives a single object parameter into a variadic curry version of that function

## Examples

The required parameters for the function to be executed need to be specified:
```javascript
import namedCurry, { ParamTypes } from 'named-curry';

function sumNumbers({a, b, c}) {
  return a + b + c;
}

const sumThreeNumbers = namedCurry(sumNumbers);
sumThreeNumbers.paramTypes = {
  a: ParamTypes.isRequired,
  b: ParamTypes.isRequired,
  c: ParamTypes.isRequired,
};

const sum5ToTwoNumbers = sumThreeNumbers({a: 5});
const sum8ToANumber = sum5ToTwoNumbers({b: 3});
sum8ToANumber({c: 4}); // 12
```

It allows to pass any number of arguments to the returned function:
```javascript
sumThreeNumbers({a: 1, b: 3, c: 5}); // 9
sum5ToTwoNumbers({b: 2, c: 4}); // 11
```

It allows to pass the arguments in any order:
```javascript
sumThreeNumbers({b: 2})({a: 4})({c: 8}); // 14
```

Because the required parameters need to be specified, optional parameters can be passed and the function is executed only when all required parameters are passed:
```javascript
import namedCurry, { ParamTypes } from 'named-curry';

function sumNumbers({a, b, c, msg}) {
  if (msg) {
    console.log(msg);
  }

  return a + b + c;
}

const sumThreeNumbers = namedCurry(sumNumbers);
sumThreeNumbers.paramTypes = {
  a: ParamTypes.isRequired,
  b: ParamTypes.isRequired,
  c: ParamTypes.isRequired,
};

sumThreeNumbers({a: 1})({b: 2})({c: 3}); // 6
sumThreeNumbers({a: 1, msg: 'summing...'})({b: 2})({c: 3});
// summing...
// 6

```
