# Работа со скриптами

Скрипты размещаются в папке `src/js`:

```text
project-template
└── src
    └── js
        ├── vendor
        │   └── .keep
        ├── detect.js
        ├── globals.js
        ├── main.js
        └── vendor.js
```

За сборку и преобразование JS отвечают задачи `jsMain` и `jsVendor`:

```bash
gulp jsMain jsVendor
```

После выполнения команды в папке `build/js` появятся файлы `main.js` и `vendor.js`:

```text
project-template
└── build
    └── js
        ├── main.js
        └── vendor.js
```

Обработкой скриптов занимаются следующие библиотеки:

* [gulp-file-include](https://www.npmjs.com/package/gulp-file-include)
* [gulp-babel](https://www.npmjs.com/package/gulp-babel)

[gulp-file-include](https://www.npmjs.com/package/gulp-babel) является упрощенной альтернативой ES6-модулям.
Пример подключения файлов:

```js
// @include('detect.js')
// @include('globals.js')
```

[gulp-babel](https://www.npmjs.com/package/gulp-babel) позволяет задействовать в процессе сборки JavaScript-транспайлер [Babel](https://babeljs.io/).
Таким образом, самые современные возможности JavaScript становятся доступны даже для старых браузеров.

Также дополнительно подключены библиотеки:

* [jQuery](https://jquery.com/)
* [bowser](https://github.com/lancedikson/bowser)

[bowser](https://github.com/lancedikson/bowser) отвечает за определение устройства, браузера и операционной системы пользователя.
В файле `src/js/detect.js` содержится код для автоматической расстановки классов тегу `<html>` на основе полученных значений.
Примеры классов:

* `.is-os-mac`
* `.is-os-windows`
* `.is-os-linux`
* `.is-os-android`
* `.is-os-ios`
* `.is-device-mobile`
* `.is-device-tablet`
* `.is-engine-webkit`
* `.is-engine-blink`
* `.is-engine-gecko`
* `.is-browser-chrome`
* `.is-browser-firefox`
* `.is-browser-ie`
* `.is-browser-safari`

Данные классы можно использовать для стилизации элементов:

```scss
.for-desktop {
    display: block;

    .is-device-mobile & {
        display: none;
    }
}
```

## Правила написания кода

### Глобальные переменные

Глобальные переменные следует выносить в файл `src/js/globals.js`.

### Короткие именна переменных

Не следует сокращать имена переменных.

**Неправильно**:

```js
$('.elements').each((i, e) => {
    // ...
});
```

**Правильно**:

```js
$('.elements').each((index, element) => {
    // ...
});
```

Исключение могут составить имена счетчиков в цикле (`i`, `j`, `k`):

```js
for (let i = 0; i < 10; i++) {
    // ...
}
```

### Именование jQuery-переменных

Название переменных, являющихся jQuery-объектами, следует начинать с `$`.

**Неправильно**:

```js
let element = $('.element');
```

**Правильно**:

```js
let $element = $('.element');
```

### jQuery-селекторы

Следует избегать дублирования jQuery-селекторов.
Если обращение к элементу происходит многократно, то jQuery-объект можно сохранить в отдельную переменную, либо переписать код так, чтобы избежать дублирования.

**Неправильно**:

```js
$('.element').on('click', () => {
    // ...
});

$('.element').on('mouseenter', () => {
    // ...
});
```

**Правильно**:

```js
let $element = $('.element');

$element.on('click', () => {
    // ...
});

$element.on('mouseenter', () => {
    // ...
});
```

Или так:

```js
$('.element')
    .on('click', () => {
        // ...
    })
    .on('mouseenter', () => {
        // ...
    });
```

### Обработка событий с помощью jQuery

Для создания обработчика событий следует использовать функцию [`.on()`](http://api.jquery.com/on/).

**Неправильно**:

```js
$('button').click(() => {
    // ...
});

$('form').submit(() => {
    // ...
});
```

**Правильно**:

```js
$('button').on('click', () => {
    // ...
});

$('form').on('submit', () => {
    // ...
});
```

## Использование линтера

В сборку интегрирован линтер [ESLint](http://eslint.org/).
Файл настроек — `.eslintrc`.
Данный линтер позволяет поддерживать JavaScript-код в соответствии с заданным регламентом.

Проверка осуществляется с помощью задачи `lintJs`:

```bash
gulp lintJs
```

Пример использования:

```js
var $form = $('.form')
$form.on("submit", function () {
  $.post('ajax.php', function (data) {
    $(".result").html(data);
  })
})
```

Результаты проверки:

```text
  1:1   error    Expected blank line after variable declarations    newline-after-var
  1:1   error    Unexpected var, use let or const instead           no-var
  1:23  error    Missing semicolon                                  semi
  2:10  error    Strings must use singlequote                       quotes
  2:20  error    Unexpected function expression                     prefer-arrow-callback
  2:20  warning  Unexpected unnamed function                        func-names
  3:1   error    Expected indentation of 1 tab but found 2 spaces   indent
  3:22  warning  Unexpected unnamed function                        func-names
  3:22  error    Unexpected function expression                     prefer-arrow-callback
  4:1   error    Expected indentation of 2 tabs but found 4 spaces  indent
  4:7   error    Strings must use singlequote                       quotes
  5:1   error    Expected indentation of 1 tab but found 2 spaces   indent
  5:5   error    Missing semicolon                                  semi
  6:3   error    Missing semicolon                                  semi

✖ 14 problems (12 errors, 2 warnings)
  12 errors, 0 warnings potentially fixable with the `--fix` option.
```

ESlint сообщает о 14 найденных ошибках, причем большая часть из них может быть исправлена автоматически.
За это отвечает ключ `--fix`, который можно указать при запуске задачи `lintJs`:

```bash
gulp lintJs --fix
```

Исправленный код:

```js
let $form = $('.form');

$form.on('submit', () => {
    $.post('ajax.php', (data) => {
        $('.result').html(data);
    });
});
```
