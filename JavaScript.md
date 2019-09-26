# JavaScript

## Simple Dropdown Toggle
```js
  document.getElementById('mobile-menu-toggle').onclick = () => {
    document.getElementById('mobile-menu-list').classList.toggle('hidden')
  }
```

## Simple Promise

```js
const goodResult = true;

let simpleAsync = function(text) {
    return new Promise( function (resolve, reject) {
        if(goodResult) {
            setTimeout(() => {
                resolve(text.toUpperCase());
            }, 1000);
        } else {
            setTimeout(() => {
                reject(new Error("Bad Result"));
            }, 1000);
        }
    });
};

simpleAsync("names")
    .then(res => { 
        console.log(res);
        return simpleAsync("alice");
    }).then(res => { 
        console.log(res);
        return simpleAsync("bob");
    }).then(res => { 
        console.log(res);
        return simpleAsync("dave");
    }).then(res => { 
        console.log(res);
    }).catch(res => {
        console.log(res);
    });

//
// n
//   ====> a
//           ====> b
//                   ====> c

```

## Promise All

```js
const goodResult = true;

let simpleAsync = function(text) {
    return new Promise( function (resolve, reject) {
        if(goodResult) {
            setTimeout(() => {
                resolve(text.toUpperCase());
            }, 1000);
        } else {
            setTimeout(() => {
                reject(new Error("Bad Result"));
            }, 1000);
        }
    });
};

simpleAsync("names")
    .then(res => {
        console.log(res);
        return Promise.all([simpleAsync("alice"), simpleAsync("bob")]);
    })
    .then(res => {
        console.log(res[0]);
        console.log(res[1]);
        return Promise.all([simpleAsync("charlie"), simpleAsync("dave")]);
    })
    .then(res => {
        console.log(res[0]);
        console.log(res[1]);
    });

// n
//   ====> a
//         b
//           ====> c
//                 d
```

## Basic fetch multiple files
```js
    fetch('_ezzat-wanikani-kanji.json')
        .then(function (response) {
            return response.json();
        })
        .then(function (response) {
            wanikani_kanji = response[0];
        })

        // Get koohii mnemonics
        .then(function () {
            return fetch('_ezzat-koohii-mnemonics.json');
        })
        .then(function (response) {
            return response.json();
        })
        .then(function (response) {
            koohii_mnemonics = response[0];
        })

        // Get the word
        .then(function () {
            return document.getElementById("vocabjp").innerHTML;
        })

        // Process things
        .then(function (vocabjp) {
            vocabjp.split("").forEach(function (i) {
                if (wanikani_kanji[i]) document.getElementById('wk-table').innerHTML +=
                    `<tr>
                        <th>${i}</th>
                        <td>${wanikani_kanji[i].meaning}</td>
                        <td>${wanikani_kanji[i].reading}</td>
                        <td></td>
                    </tr>`;
            });
        });
```
## Load Multiple Files

```js
    // Files
    var fileUrls = [
        {
            id: 'kanshudo',
            url: '_ezzat-kanshudo-components.json',
        }
        ];
    var fileList = [];
    var files = {};
    
    // Get Files
    fileUrls.forEach(function(url, i) {
        fileList.push(
            fetch(url.url).then(function(res){
                return res.text(); 
            }).then(function(res){
                files[url.id] = res; 
            })
        );
    });

    // After files loaded
    Promise
        .all(fileList)
        .then(function() {

            // Do something
        });

```
## ES5 inheritence

```js
function Person(fName, lName) {
    this.firstName = fName;
    this.lastName = lName;
}

Person.prototype.human = "Yes";

Person.prototype.getFullName = function () {
    return this.firstName + ' ' + this.lastName;
}

function Employee(fName, lName, eId) {
    Person.call(this, fName, lName);
    this.empId = eId;
}

Employee.prototype = Object.create(Person.prototype); // Same concept as Employee.prototype.__proto__ = Person.prototype;
Employee.prototype.constructor = Employee;

Employee.prototype.getEmpInfo = function () {
    return [this.empId, this.firstName, this.lastName];
};
```
