# Работа с дополнительными ресурсами

Дополнительными ресурсами считается все то, что не попадает ни под одну из предыдущих категорий файлов.
Это могут быть различные favicon, шрифты, аудио, видео, документы и прочее.

Подобные файлы следует хранить в папке `src/resources`.

```text
project-template
└── src
    └── resources
        └── ...
```

Задача `copy` копирует содержимое папки `src/resources` в `build`:

```bash
gulp copy
```

## Работа со шрифтами

Подключить шрифт можно двумя способами:

* CDN ([Google Fonts](https://fonts.google.com/))
* Конвертировать и подключить с помощью [`@font-face`](https://developer.mozilla.org/ru/docs/Web/CSS/@font-face).

### Подключение шрифта с помощью Google Fonts

Если шрифт и его требуемая языковая версия имеются в Google Fonts, то данный вариант подключения является приоритетным.

Порядок подключения шрифта на примере Roboto:

1. Находим шрифт — [Roboto](https://fonts.google.com/specimen/Roboto)
2. Нажимаем `Select this font`.
3. Открываем появившееся снизу экрана окно.
4. Во вкладке `Customize` выбираем нужное начертание и языковую версию.
5. Во вкладке `Embed` переключаемся в `@import` и копируем содержимое тега `<style>`.
6. В файл `src/scss/_fonts.scss` вставляем скопированный `@import`.
7. В файл `src/scss/_variables.scss` добавляем переменную `$font-family-roboto`.
8. Используем переменную в стилях.

### Конвертирование шрифта и подключение с помощью `@font-face`

Если шрифт отсутствует в Google Fonts, или нет подходящей языковой версии (отсутствует кириллица), то необходимо получить файл шрифта.

Требуемые форматы — `.woff` (обязательно) и `.woff2` (опционально).

Файлы `.ttf`, `.otf` или `.eot` можно сконвертировать в `.woff` и `.woff2` с помощью онлайн сервисов:

* [onlinefontconverter.com](https://onlinefontconverter.com/)
* [everythingfonts.com](https://everythingfonts.com/)

Полученные файлы следует хранить в папке `src/resources/fonts`:

```text
project-template
└── src
    └── resources
        └── fonts
            └── ...
```

Подключение шрифтов происходит в файле `src/scss/_fonts.scss`:

```scss
@font-face {
    src: url("../fonts/my-font-regular.woff2") format("woff2"), url("../fonts/my-font-regular.woff") format("woff");
    font-family: "My Font";
    font-weight: 400;
    font-style: normal;
}
```

При наличии множества начертаний шрифты следует подключать в следующем порядке:

1. 100 normal (thin)
2. 100 italic (thin italic)
3. 200 normal (extra light)
4. 200 italic (extra light italic)
5. 300 normal (light)
6. 300 italic (light italic)
7. 400 normal (regular)
8. 400 italic (regular italic)
9. 500 normal (medium)
10. 500 italic (medium italic)
11. 600 normal (semi bold)
12. 600 italic (semi bold italic)
13. 700 normal (bold)
14. 700 italic (bold italic)
15. 800 normal (extra bold)
16. 800 italic (extra bold italic)
17. 900 normal (heavy)
18. 900 italic (heavy italic)

Пример:

```scss
@font-face {
    src: url("../fonts/my-font-light.woff") format("woff");
    font-family: "My Font";
    font-weight: 300;
    font-style: normal;
}

@font-face {
    src: url("../fonts/my-font-light-italic.woff") format("woff");
    font-family: "My Font";
    font-weight: 300;
    font-style: italic;
}

@font-face {
    src: url("../fonts/my-font-regular.woff") format("woff");
    font-family: "My Font";
    font-weight: 400;
    font-style: normal;
}

@font-face {
    src: url("../fonts/my-font-regular-italic.woff") format("woff");
    font-family: "My Font";
    font-weight: 400;
    font-style: italic;
}

@font-face {
    src: url("../fonts/my-font-bold.woff") format("woff");
    font-family: "My Font";
    font-weight: 700;
    font-style: normal;
}

@font-face {
    src: url("../fonts/my-font-bold-italic.woff") format("woff");
    font-family: "My Font";
    font-weight: 700;
    font-style: italic;
}
```

После подключения шрифта в файл `src/scss/_variables.scss` следует добавить переменную в формате `$font-family-[name]`.
Пример:

```scss
$font-family-my-font: "My Font", sans-serif;
```

Затем переменную можно использовать в любом SCSS-файле:

```scss
body {
    font-family: $font-family-my-font;
}
```
