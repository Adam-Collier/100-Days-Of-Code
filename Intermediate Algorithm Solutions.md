# Intermediate Algorithm Solutions

### Sum All Number in a Range

```javascript
function sumAll(arr) {
  var a = [];
  arr= arr.sort(function(a, b){
    return a-b;
  });
  var b = arr[0]-1;

  while(b < arr[1]){
    a.push(b += 1);
}
  a = a.reduce(function(a, b){
    return a + b;
  });
  return a ;
}

sumAll([5, 10]);
```

### Diff Two Arrays

```javascript
function diffArray(arr1, arr2) {
  var newArr = [];
  // Same, same; but different.
  arr2.map(function(x){
    return arr1.indexOf(x)=== -1 ? newArr.push(x) : x;
});arr1.map(function(x){
    return arr2.indexOf(x)=== -1 ? newArr.push(x) : x;
});
  return newArr;

}   

diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]);
```

### Roman Numeral Converter

```javascript
function convertToRoman(num) {
  var thousands = Math.floor(num / 1000);
  var remainder = num % 1000;
  var hundreds = Math.floor(remainder / 100);
  remainder = remainder % 100;
  var tens = Math.floor(remainder / 10);
  remainder = remainder % 10;
  var ones = Math.floor(remainder / 1);
  remainder = remainder % 1;

  var arrhun = ["C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"];
  var arrten = ["X", "XX", "XXX" ,"XL", "L", "LX", "LXX", "LXXX", "XC"];
  var arrone = ["I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"];

  var numeral = [];

  for( x = 0; x < thousands; x++){
     numeral.push("M");
  }
  numeral.push(arrhun[hundreds-1], arrten[tens-1],arrone[ones-1]);

  return numeral.join("");
}

convertToRoman(3378);
```

### Wherfore Art Thou

```javascript

function whatIsInAName(collection, source) {
  // What's in a name?
  var arr = [];
  // Only change code below this line

  for(var x = 0; x < collection.length; x++){
    var o = Object.keys(source);
    var a = [];

    for(var i = 0; i < o.length; i++){
       a.push(collection[x].hasOwnProperty(o[i]));
}
    console.log(source[o]);
    if(collection[x][o] == source[o] && a.indexOf(false) == -1 ){
      arr.push(collection[x]);
    }

  }

// Only change code above this line
  return arr;
}

whatIsInAName([{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }], { last: "Capulet" });
```

### Search and Replace

```javascript

function myReplace(str, before, after) {

  if(before[0] == before[0].toUpperCase()){
    after = after[0].toUpperCase() + after.slice(1);
  }

  return str.replace(before, after);

}

myReplace("Let us get back to more Coding", "Coding", "algorithms");
```

### Pig Latin

```javascript
function translatePigLatin(str) {
  var reg = /[aeiou]/gi;
  var a = str.search(reg);
  str = str.split("");
  var arr = [];
  if(a > 0){
    var m = str.splice(0, a);
    m = m.join("");
    return str.join("")+m+"ay";
  }else{
    return str.join("") +"way";
  }
}

translatePigLatin("glove");
```

### DNA Pairing

```javascript
function pairElement(str) {
  var arr = [];
  str = str.split("");
  str.map(function(x){
    switch (x) {
      case 'A':
        arr.push(['A', 'T']);
        break;
      case 'T':
        arr.push(['T', 'A']);
        break;
      case 'C':
        arr.push(['C', 'G']);
        break;
      case 'G':
        arr.push(['G', 'C']);
        break;
      }

  });

  return arr;
}

pairElement("GCG");
```

### Missing Letters

```javascript
function fearNotLetter(str) {
  var arr = [];
  for(var x = 0; x < str.length; x++){
    arr.push(str.charCodeAt(x));
  }
  var r;
  var a = arr.splice(0,1);
  a = a[0];
  arr.map(function(x){
    if(a+1 !== x){
      r = String.fromCharCode(a+1);
    }else{
      a = a+1;
    }

  });

  return r;
}

fearNotLetter("abcdefghjklmno");
```

### Boo Who

```javascript
function booWho(bool) {
  // What is the new fad diet for ghost developers? The Boolean.
  if(bool === false || bool === true){
    return true;
  }else{
    return false;
  }
}

booWho(true);
```

### Sorted Union

```javascript
function uniteUnique(a, b, c, d) {
  var arr= [];

  if(arguments[3] !== undefined){
    arr = a.concat(b,c,d);
  }else if(arguments[2] !== undefined){
    arr = a.concat(b,c);
  }else{
    arr = a.concat(b);
  }

  for(var x = arr.length-1; x > 0; x--){
    if(arr.indexOf(arr[x]) !== x){
      arr.splice(x, 1);
    }
  }
  return arr;
}

uniteUnique([1, 2, 3], [5, 2, 1, 4], [2, 1], [6, 7, 8]);
```

### Convert HTML Entities

```javascript
function convertHTML(str) {
  // &colon;&rpar;
  str = str.replace('&', '&amp;').replace(/</gi, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;').replace(/'/g, '&apos;');
  return str;
}

convertHTML("Hamburgers < Pizza < Tacos");
```

### Spinal Tap Case

```javascript
function spinalCase(str) {
  // "It's such a fine line between stupid, and clever."
  // --David St. Hubbins
  return str.replace(/([a-z])([A-Z])/g, "$1 $2").toLowerCase().replace(/[\W_]/gi,"-");

}

spinalCase('AllThe-small Things');
```

### Sum All Fibonacci Numbers

```javascript
function sumFibs(bar) {
  var arr = [1,1];
  var a = bar;
  for(var x = 2; arr[x-1] <= a; x++){
    arr.push(arr[x-1]+arr[x-2]);
  }
  arr = arr.filter(function(x){
    if(x % 2 !== 0){
      return x;
    }
  });

  arr.splice(-1,1);

  arr = arr.reduce(function(a,b){
    return a + b;
  });

  return arr;
}

sumFibs(1000);
```

### Sum All Primes

```javascript
function sumPrimes(n) {
  var arr = [];

  for (var x = 2; x <= n; x++) {
    arr.push(x);
  }

  var b = arr.map(function(a) {
    return arr.slice(0, arr.indexOf(a))
      .map(function(i) {
        return a % i;
      });

  });

  var f = [];

  for (var s = 0; s < b.length; s++) {
    if (b[s].indexOf(0) === -1) {
      f.push(s + 2);
    }
  }

  f = f.reduce(function(a, b) {
    return a + b;
  });
  return f;
}

sumPrimes(10);
```

### Finders Keepers

```javascript
function findElement(arr, func) {

  var a = [];

  for(var x = 0; x < arr.length; x++){
    var num = arr[x];
    a.push(func(num));
  }

  var b = a.indexOf(true);
  return arr[b];

}

findElement([1, 2, 3, 4], function(num){ return num % 2 === 0; });
```

### Drop It

```javascript
function dropElements(arr, func) {
  // Drop them elements.
  var n = 0;
  while(func(arr[n]) === false){
    arr.shift();
  }
  return arr;

}

dropElements([0, 1, 0, 1], function(n) {return n === 1; });
```

### Steamroller

```javascript
function steamrollArray(arr) {
  // I'm a steamroller, baby
  var a = [];
  var b = [];

  for(var x = 0; x < arr.length; x++){
    if(Array.isArray(arr[x])){
      a = a.concat(steamrollArray(arr[x]));

    }else{
      a.push(arr[x]);

    }
  }
  return a;
}

steamrollArray([1, [2], [3, [[4]]]]);
```

### Binary Agents

```javascript
function binaryAgent(str) {
  str = str.split(" ");
  return str.map(function(x){
    return String.fromCharCode(parseInt(x, 2));
  }).join("");
}

binaryAgent("01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00100001 00111111");
```

### Everything be True

```javascript
function truthCheck(collection, pre) {
  // Is everyone being true?
  var arr = [];
  arr = collection.map(function(x){
    if(x[pre]){
      return true;
    }else{
      return false;
    }
  });
  if(arr.indexOf(false) === -1){
    return true;
  }else{
    return false;
  }

}

truthCheck([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex");
```

### Arguments Optional

```javascript
function addTogether() {
  var args = Array.from(arguments);
  if(args.length === 2){
    return args.reduce(function(a,b){
      if(typeof a === 'number' && typeof b === 'number'){
        return a + b;
      }
    });

  }else if(args.length === 1 && typeof args[0] === 'number'){
    return function(sum){
      if(typeof sum === 'number'){
        return args[0] + sum;
      }else{
        return undefined;
      }
    };
  }else{
    return undefined;
  }
}

addTogether("http://bit.ly/IqT6zt");
```

### Validate US Telephone Numbers

```javascript
function telephoneCheck(str) {
  // Good luck!
  var reg = /\d/g;
  var bra = /[()]/g;

  var a = str.match(reg);
  var b = str.match(bra);


  if(a.length === 10 || a.length === 11 && a[0] === "1"){
    if(str.indexOf(')') > 6 || str.indexOf('?') > 0){
      return false;
    }else if(b !== null){
      return b.length % 2 === 0;
    }else{
      return true;
    }

  }else{
    return false;
  }


}



telephoneCheck("555-555-5555)");
```

### Symmetric Difference

```javascript
function sym(args) {
  var arr = Array.from(arguments);
  //arr = [].concat.apply([], arr);
  arr = arr.reduce(function(accum, array){
    var f = array.filter(function(item, index){
      return array.indexOf(item) === index;
    });
    return accum.concat(f);
  },[]);
  arr = arr.sort();
  var count = {};
  var a = [];

  for(var x = 0; x < arr.length; x++){
    count[arr[x]] = count[arr[x]] + 1 || 1;
  }

  var b = Object.keys(count).filter(function(x){
    return count[x] % 2 !== 0;
  });

return b.map(function(x){
  return parseInt(x);
});                                           
}

sym([1, 1, 2, 5], [2, 3, 5], [3, 4, 5]);
```

### Inventory Update

```javascript 
function updateInventory(arr1, arr2) {
    // All inventory must be accounted for or you're fired!
    var obj = {};
    arr1.map(function(x){
      obj[x[1]] = x[0];
    });

    arr2.map(function(x){
      if(obj.hasOwnProperty(x[1])){
        obj[x[1]] += x[0];
      }else{
        obj[x[1]] = x[0];
      }
   });
    var arr = [];
    var keys = Object.keys(obj);
    keys.map(function(x){
      arr.push([x]);
    });
      for(var i = 0; i < arr.length; i++){
        arr[i].push(obj[keys[i]]);
      }
    arr.sort();
    arr.map(function(x){
      x.push(x[0]);
      x.splice(0, 1);
    });
    return arr;
}

// Example inventory lists
var curInv = [
    [21, "Bowling Ball"],
    [2, "Dirty Sock"],
    [1, "Hair Pin"],
    [5, "Microphone"]
];

var newInv = [
    [2, "Hair Pin"],
    [3, "Half-Eaten Apple"],
    [67, "Bowling Ball"],
    [7, "Toothpaste"]
];

updateInventory(curInv, newInv);
```
