# Работа с шаблонизатором Pug

В сборке используется шаблонизатор [Pug](https://pugjs.org/) (ранее назывался Jade).

Pug предоставляет множество возможностей, упрощающих работу с шаблонами:

* Переменные.
* Циклы.
* Условия.
* Фильтры.
* Наследование шаблонов.
* Миксины.

Шаблоны страниц размещаются в `src`, а дополнительные файлы и миксины в `src/pug`:

```text
project-template
└── src
    ├── pug
    │   ├── mixins
    │   │   └── svg.pug
    │   └── base.pug
    └── index.pug
```

За сборку и преобразование Pug в HTML отвечает задача `pug`:

```bash
gulp pug
```

После выполнения команды в папке `build` появятся HTML-файлы:

```text
project-template
└── build
    └── index.html
```

## Базовый шаблон и создание страниц

В качестве базового шаблона используется `src/pug/base.pug`.

Пример наследования и использования шаблона:

```jade
extends pug/base

block content
    // Содержимое страницы
```

Базовый шаблон определяет блоки (участки кода или место в шаблоне), которые можно изменять и дополнять при наследовании.

### `vars`

Блок `vars` хранит основные настройки шаблона:

* `title` — заголовок страницы (используется в `<title>` и метатегах).

* `description` — описание страницы (используется в метатегах).

* `image` — изображение страницы (используется в метатегах).

* `html` — настройки тега `<html>`:
  * `html.attrs` — объект для задания дополнительных атрибутов.
  * `html.classList` — массив классов.

* `body` — настройки тега `<body>`:
  * `body.attrs` — объект для задания дополнительных атрибутов.
  * `body.classList` — массив классов.

* `meta` — значения метатегов.

* `link` — значения тегов `<link>`.

Пример использования:

```jade
prepend vars
    - title = 'Заголовок'
    - description = 'Описание'
    - image = 'http://example.com/images/image.png'

append vars
    - html.classList.push('page-index')
    - link.icon['16x16'] = 'favicon_16x16.png'
    - link.icon['32x32'] = 'favicon_32x32.png'
```

### `head-start`

Блок `head-start` является альтернативой `prepend meta`.

### `meta`

В блоке `meta` подключаются метатеги.

Пример использования:

```jade
append meta
    meta(name="referrer" content="none")
```

### `links`

В блоке `links` подключаются стили, иконки и прочие ресурсы.

Пример использования:

```jade
append links
    link(rel="stylesheet" href="css/custom.css")
```

### `head-end`

Блок `head-end` является альтернативой `append links`.

### `body-start`

Блок `body-start` является альтернативой `prepend content`.

### `content`

Блок `content` предназначен для хранения содержимого страницы.

Пример использования:

```jade
block content
    .container
        h1 Заголовок страницы
```

### `scripts`

В блоке `scripts` подключаются скрипты.

Пример использования:

```jade
append scripts
    script(src="js/custom.js")
```

### `body-end`

Блок `body-end` является альтернативой `append scripts`.

## Правила написания кода и использование линтера

В сборку интегрирован линтер [pug-lint](https://www.npmjs.com/package/pug-lint).
Файл настроек — `.pug-lintrc.json`.
Данный линтер позволяет поддерживать Pug-код в соответствии с заданным регламентом.

Проверка осуществляется с помощью задачи `lintPug`.

Пример использования (`src/index.pug`):

```jade
extends pug/base

append vars
  - html.classList.push('page-index')

block content
  a(href='#').link Ссылка
```

Результаты проверки:

```text
project-template/src/index.pug:7:14
    5|
    6| block content
  > 7|   a(href='#').link Ссылка
--------------------^
    8|

All class literals must be written before any attribute blocks

project-template/src/index.pug:7:5
    5|
    6| block content
  > 7|   a(href='#').link Ссылка
-----------^
    8|

Invalid attribute quote mark found

project-template/src/index.pug:4:1
    2|
    3| append vars
  > 4|   - html.classList.push('page-index')
-------^
    5|
    6| block content
    7|   a(href='#').link Ссылка

Invalid indentation

project-template/src/index.pug:7:1
    5|
    6| block content
  > 7|   a(href='#').link Ссылка
-------^
    8|

Invalid indentation
```

Исправленный код:

```jade
extends pug/base

append vars
    - html.classList.push('page-index')

block content
    a.link(href="#") Ссылка
```

В дополнение к проверкам кода линтером следует придерживаться следующих правил:

* Повторяющиеся участки кода по возможности выносить в отдельные миксины.
* Схожие по структуре страницы выносить в отдельный шаблон и наследоваться от него.
