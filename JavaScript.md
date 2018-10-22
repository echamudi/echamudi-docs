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

        // Get koohii mnemoics
        .then(function () {
            return fetch('_ezzat-koohii-mnemoics.json');
        })
        .then(function (response) {
            return response.json();
        })
        .then(function (response) {
            koohii_mnemoics = response[0];
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
