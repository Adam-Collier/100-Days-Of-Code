# Advanced Algorithm Solutions

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

### Friendly Date Range

```javascript
function makeFriendlyDates(arr) {

  var mon = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
  arr = arr.map(function(x){
    return x.split("-");
  });

  arr.map(function(x){

    if(x[2].indexOf("0") !== -1) x[2] = x[2].substr(1);
    switch (parseInt(x[2])) {
      case 1:
      case 21:
      case 31:
        x[2] += 'st';
        break;
      case 2:
      case 22:
        x[2] += 'nd';
        break;
      case 3:
      case 23:
        x[2] += 'rd';
        break;
      default:
        x[2] += 'th';
    }

    if(x[1].indexOf("0") !== -1) x[1] = x[1].substr(1);

    x[1] = mon[x[1]-1];
    x.push(x[0]);
    x.splice(0, 1);
  });

  //July, 1st, 2016

  var a = arr[0];
  var b = arr[1];
  if(arr[0].toString() === arr[1].toString()){
    return [a[0]+" "+a[1]+", "+a[2]];
  }
  if (a[2] == b[2] && a[0] == b[0]){
    return [a[0]+" "+a[1], b[1]];
  }
  if(Math.abs(a[2] - b[2]) == 1 && a[0] !== b[0]){
    return [a[0]+" "+a[1], b[0]+" "+b[1]];
  }
  if(a[0] == b[0] && a[1] == b[1] && a[2] !== b[2]){
    return [a[0]+" "+a[1]+", "+a[2], b[0]+" "+b[1]+", "+b[2]];
  }
  if(b[2] - a[2] > 1){
    return [a[0]+" "+a[1]+", "+a[2], b[0]+" "+b[1]+", "+ b[2]];
  }
  if(a[2] == b[2]){
    return [a[0]+" "+a[1]+", "+a[2], b[0]+" "+b[1]];
  }
  if(Math.abs(a[2] - b[2]) == 1 && a[0] == b[0]){
    return [a[0]+" "+a[1]+", "+a[2], b[0]+" "+b[1]];
  }

}

makeFriendlyDates(["2022-09-05", "2023-09-05"]);
```

### Make A Person

```javascript

var Person = function(firstAndLast) {

  this.getFullName = function(full){return firstAndLast;};
  this.getFirstName = function(first){return firstAndLast.split(" ")[0];};
  this.getLastName = function(second){return firstAndLast.split(" ")[1];};

  this.setFirstName = function(first){
    firstAndLast = first+" "+firstAndLast.split(" ")[1];
  };
  this.setLastName = function(second){
    firstAndLast = firstAndLast.split(" ")[0]+" "+second;
  };
  this.setFullName = function(full){
    firstAndLast = full;
  };
};

var bob = new Person('Bob Ross');
bob.getFirstName();
```

### Map the Debris

```javascript
function orbitalPeriod(arr) {
  var GM = 398600.4418;
  var earthRadius = 6367.4447;
  var r = 2 * Math.PI;
  arr.map(function(x){
    x.orbitalPeriod = Math.round(r * Math.sqrt(Math.pow(earthRadius + x.avgAlt, 3) / GM));
    delete x.avgAlt;

  });
  return arr;
}

orbitalPeriod([{name : "sputnik", avgAlt : 35873.5553}]);
```

### PairWise

```javascript
function pairwise(arr, arg) {
  var a = [];
  arr.map(function(x, index){
    arr.map(function(i, ind){
      console.log(index,ind);
      if(x + i == arg && a.indexOf(x) == -1 && arr.indexOf(i) !== arr.lastIndexOf(x)){
        console.log(ind, index);
        a.push(x, i);
      }
    });
  });

  a = a.filter(function(item, pos) {
    return a.indexOf(item) == pos;
  });
  var res = 0;
  a.map(function(y){
    if(arr.indexOf(y) !== arr.lastIndexOf(y)){
    res += arr.indexOf(y);
    res += arr.indexOf(y)+1;
  }else{
    res += arr.indexOf(y);
  }


  });
  return res;
}

pairwise([0, 0, 0, 0, 1, 1], 1);
```
