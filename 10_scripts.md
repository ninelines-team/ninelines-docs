# Работа со скриптами

> При работе со скриптами **важно** придерживаться установленных [правил по оформлению кода](18_codestyle-javascript.md).

Скрипты размещаются в папке `src/js`:

```text
ninelines-template
└── src
    └── js
        ├── vendor
        │   └── .keep
        ├── main.js
        ├── variables.js
        └── vendor.js
```

За сборку и преобразование JS отвечают задачи `jsMain` и `jsVendor`:

```bash
gulp jsMain jsVendor
```

После выполнения команды в папке `build/js` появятся файлы `main.js` и `vendor.js`:

```text
ninelines-template
└── build
    └── js
        ├── main.js
        └── vendor.js
```

Также дополнительно подключены библиотеки:

* [jQuery](https://jquery.com/)
* [ninelines-ua-parser](https://github.com/ninelines-team/ninelines-ua-parser)

[ninelines-ua-parser](https://github.com/ninelines-team/ninelines-ua-parser) основана на
[ua-parser-js](https://github.com/faisalman/ua-parser-js) и отвечает за определение устройства, браузера и операционной
системы пользователя, а также автоматически проставляет классы `<html>` элементу:

* `.is-os-mac-os`
* `.is-os-windows`
* `.is-os-linux`
* `.is-os-android`
* `.is-os-ios`
* `.is-device-mobile`
* `.is-device-tablet`
* `.is-device-desktop`
* `.is-engine-webkit`
* `.is-engine-gecko`
* `.is-browser-chrome`
* `.is-browser-firefox`
* `.is-browser-ie`
* `.is-browser-safari`

Данные классы можно использовать для стилизации элементов:

```scss
.for-desktop {
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

**Неправильно:**

```js
$('.elements').each((i, e) => {
    // ...
});
```

**Правильно:**

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

**Неправильно:**

```js
let element = $('.element');
```

**Правильно:**

```js
let $element = $('.element');
```

### jQuery-селекторы

Следует избегать дублирования jQuery-селекторов.
Если обращение к элементу происходит многократно, то jQuery-объект можно сохранить в отдельную переменную, либо переписать код так, чтобы избежать дублирования.

**Неправильно:**

```js
$('.element').on('click', () => {
    // ...
});

$('.element').on('mouseenter', () => {
    // ...
});
```

**Правильно:**

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

**Неправильно:**

```js
$('button').click(() => {
    // ...
});

$('form').submit(() => {
    // ...
});
```

**Правильно:**

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
