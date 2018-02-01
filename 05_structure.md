# Структура папок и файлов

```text
project-template
├── src
│   ├── images
│   │   └── sprites
│   │       ├── png
│   │       │   └── .keep
│   │       └── svg
│   │           └── .keep
│   ├── js
│   │   ├── vendor
│   │   │   └── .keep
│   │   ├── detect.js
│   │   ├── globals.js
│   │   ├── main.js
│   │   └── vendor.js
│   ├── pug
│   │   ├── mixins
│   │   │   └── svg.pug
│   │   └── base.pug
│   ├── resources
│   │   └── fonts
│   │       └── .keep
│   ├── scss
│   │   ├── functions
│   │   │   └── _sprites.scss
│   │   ├── mixins
│   │   │   ├── _retina.scss
│   │   │   ├── _sprites.scss
│   │   │   └── _triangle.scss
│   │   ├── vendor
│   │   │   └── .keep
│   │   ├── _base.scss
│   │   ├── _fonts.scss
│   │   ├── _functions.scss
│   │   ├── _mixins.scss
│   │   ├── _sprites.hbs
│   │   ├── _sprites.scss
│   │   ├── _variables.scss
│   │   ├── _vendor.scss
│   │   └── main.scss
│   └── index.pug
├── .babelrc
├── .editorconfig
├── .eslintignore
├── .eslintrc
├── .gitignore
├── .npmrc
├── .pug-lintrc.json
├── .stylelintrc
├── bitbucket-pipelines.yml
├── gulpfile.babel.js
├── package.json
├── README.md
└── router-config.js
```

## `src`

В папке `src` хранятся исходные файлы проекта.

## `src/images`

Папка `images` предназначена для хранения изображений.
При сборке файлы из данной папки попадают в `build/images`.

## `src/images/sprites`

Папка `src/images/sprites` предназначена для хранения векторных (SVG) и растровых (PNG) иконок.

## `src/images/sprites/png`

Папка `src/images/sprites/png` предназначена для хранения растровых иконок.
При сборке файлы из данной папки объединяются в два спрайта: `build/images/sprites.png` и `build/images/sprites@2x.png`.

## `src/images/sprites/svg`

Папка `src/images/sprites/svg` предназначена для хранения векторных иконок.
При сборке файлы из данной папки объединяются в один спрайт: `build/images/sprites.svg`.

## `src/js`

Папка `src/js` предназначена для хранения скриптов.

## `src/js/vendor`

Папка `src/js/vendor` предназначена для хранения скриптов сторонних библиотек, которых нет в репозитории npm.

## `src/js/detect.js`

Файл `src/js/detect.js` предназначен для определения устройства, браузера и операционной системы пользователя.

## `src/js/globals.js`

Файл `src/js/globals.js` предназначен для хранения глобальных переменных.

## `src/js/main.js`

Файл `src/js/main.js` предназначен для хранения основной логики сайта.
При сборке данный файл попадает в `build/js`.

## `src/js/vendor.js`

Файл `src/js/vendor.js` предназначен для подключения скриптов сторонних библиотек.
При сборке данный файл попадет в `build/js`.

## `src/pug`

Папка `src/pug` предназначена для хранения шаблонов.

## `src/pug/mixins`

Папка `src/pug/mixins` предназначена для хранения Pug-миксинов.

## `src/pug/mixins/svg.pug`

В файле `src/pug/mixins/svg.pug` хранится Pug-миксин для подключения SVG-иконок.

## `src/pug/base.pug`

В файле `src/pug/base.pug` хранится базовый шаблон страниц сайта.

## `src/resources`

Папка `src/resources` предназначена для хранения различных файлов проекта.
При сборке файлы из данной папки попадают в `build`.

## `src/resources/fonts`

Папка `src/resources/fonts` предназначена для хранения шрифтов.
При сборке файлы из данной папки попадают в `build/fonts`.

## `src/scss`

Папка `src/scss` предназначена для хранения стилей.

## `src/scss/functions`

Папка `src/scss/functions` предназначена для хранения SCSS-функций.

## `src/scss/functions/_sprites.scss`

В файле `src/scss/functions/_sprites.scss` хранятся SCSS-функции для работы с PNG-спрайтами.

## `src/scss/mixins`

Папка `src/scss/mixins` предназначена для хранения SCSS-миксинов.

## `src/scss/mixins/_retina.scss`

В файле `src/scss/mixins/_retina.scss` хранится SCSS-миксин для работы с retina.

## `src/scss/mixins/_sprites.scss`

В файле `src/scss/mixins/_sprites.scss` хранятся SCSS-миксины для работы с PNG-спрайтами.

## `src/scss/mixins/_triangle.scss`

В файле `src/scss/mixins/_triangle.scss` хранится SCSS-миксин для создания CSS-треугольников.

## `src/scss/vendor`

Папка `src/scss/vendor` предназначена для хранения стилей сторонних библиотек, которых нет в репозитории npm.

## `src/scss/_base.scss`

Файл `src/scss/_base.scss` предназначен для хранения базовых стилей.

## `src/scss/_fonts.scss`

Файл `src/scss/_fonts.scss` предназначен для подключения шрифтов.

## `src/scss/_functions.scss`

Файл `src/scss/_functions.scss` предназначен для подключения функций из папки `src/scss/functions`.

## `src/scss/_mixins.scss`

Файл `src/scss/_mixins.scss` предназначен для подключения миксинов из папки `src/scss/mixins`.

## `src/scss/_sprites.hbs`

`src/scss/_sprites.hbs` — шаблон, на основе которого генерируется содержимое файла `src/scss/_sprites.scss`.

## `src/scss/_sprites.scss`

Файл `src/scss/_sprites.scss` предназначен для работы с PNG-спрайтами.
Содержимое данного файла автоматически генерируется на основе шаблона `src/scss/_sprites.hbs` и иконок из папки `src/images/sprites/png`.

## `src/scss/_variables.scss`

Файл `src/scss/_variables.scss` предназначен для хранения SCSS-переменных.

## `src/scss/_vendor.scss`

Файл `src/scss/_vendor.scss` предназначен для подключения стилей сторонних библиотек.

## `src/scss/main.scss`

Файл `src/scss/main.scss` предназначен для хранения основных стилей сайта.
При сборке данный файл преобразуется в CSS и сохраняется в `build/css` вместе с файлом `main.css.map`.

## `src/index.pug`

`src/index.pug` — шаблон главной страницы.
При сборке все Pug-файлы из папки `src` преобразуются в HTML и сохраняются в `build`.

## `.babelrc`

`.babelrc` — файл настроек JavaScript-транспайлера Babel.

## `.editorconfig`

`.editorconfig` — файл настроек редактора.

## `.eslintignore`

`.eslintignore` — файл настроек ESLint для игнорирования файлов.

## `.eslintrc`

`.eslintrc` — файл настроек ESLint.

## `.gitignore`

`.gitignore` — файл настроек Git для игнорирования файлов.

## `.npmrc`

`.npmrc` — файл настроек npm.

## `.pug-lintrc.json`

`.pug-lintrc` — файл настроек pug-lint.

## `.stylelintrc`

`.stylelintrc` — файл настроек stylelint.

## `bitbucket-pipelines.yml`

`bitbucket-pipelines.yml` — файл настроек Bitbucket Pipelines.

## `gulpfile.babel.js`

`gulpfile.babel.js` — основной файл сборки, содержащий Gulp-задачи.

## `package.json`

`package.json` — файл, содержащий базовую информацию о проекте и список требуемых библиотек.

## `README.md`

`README.md` — документация.

## `router-config.js`

`router-config.js` — файл настроек роутинга Browsersync (только для одностраничных приложений).
