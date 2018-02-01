# Работа с Foundation

[Foundation](http://foundation.zurb.com/) — front-end фреймворк, предоставляющий средства для работы с системой сеток и адаптивным дизайном, а также множество UI-компонентов.

[Документация Foundation for Sites](http://foundation.zurb.com/sites/docs/).

## Установка

Для установки фреймворка следует выполнить команду:

```bash
npm install --save foundation-sites
```

После чего требуется подключить файлы и инициализировать компоненты:

`src/scss/_vendor.scss`:

```scss
@import "../../node_modules/foundation-sites/scss/foundation";

@include foundation-everything;
```

`src/js/vendor.js`:

```js
// @include('../../node_modules/foundation-sites/dist/js/foundation.js')
```

`src/js/main.js`:

```js
$(document).foundation();
```

## Настройка

Список всех возможных переменных можно найти в файле<br>
`node_modules/foundation-sites/scss/settings/_settings.scss`.

Данный файл не предназначен для редактирования (как и любой другой в папке `node_modules`).
Поэтому переменные, значения которых необходимо изменить, следует скопировать в файл `src/scss/_variables.scss`.
После чего им можно задавать новые значения.

Пример (`src/scss/_variables.scss`):

```scss
$global-width: 1024px;
$grid-column-count: 8;
```
