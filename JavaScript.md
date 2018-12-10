# JavaScript
## Simple Dropdown Toggle
```js
  document.getElementById('mobile-menu-toggle').onclick = () => {
    document.getElementById('mobile-menu-list').classList.toggle('hidden')
  }
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
