# Работа со стилями

В сборке используется препроцессор [SCSS](http://sass-lang.com/) и PostCSS-плагин [Autoprefixer](https://autoprefixer.github.io/ru/).

Стили размещаются в папке `src/scss`:

```text
project-template
└── src
    └── scss
        ├── functions
        │   └── _sprites.scss
        ├── mixins
        │   ├── _retina.scss
        │   ├── _sprites.scss
        │   └── _triangle.scss
        ├── vendor
        │   └── .keep
        ├── _base.scss
        ├── _fonts.scss
        ├── _functions.scss
        ├── _mixins.scss
        ├── _sprites.hbs
        ├── _sprites.scss
        ├── _variables.scss
        ├── _vendor.scss
        └── main.scss
```

За сборку и преобразование SCSS в CSS отвечает задача `scss`:

```bash
gulp scss
```

После выполнения команды в папке `build/css` появятся файлы `main.css` и `main.css.map`:

```text
project-template
└── build
    └── css
        ├── main.css
        └── main.css.map
```

## Правила написания кода

### БЭМ

Для именования классов рекомендуется использовать [БЭМ-нотацию](https://ru.bem.info/methodology/naming-convention/).

```scss
.block {
    &__element {
        &--modificator {
            // ...
        }
    }
}
```

### Классы состояний

Классы состояний рекомендуется записывать кратко:

```scss
.is-active {
    // ...
}

.is-current {
    // ...
}

.is-open {
    // ...
}

.is-hidden {
    // ...
}
```

### Порядок CSS-свойств

CSS-свойства следует записывать в определенном порядке. Порядок задан в файле `.stylelintrc` (ключ `order/properties-order`).
Проверить правильность порядка свойств можно с помощью линтера:

```bash
gulp lintScss
```

### Переменные

В файл `src/scss/_variables.scss` следует выносить лишь основные переменные:

* `font-family` для шрифтов. Пример:

  ```scss
  $font-family-roboto: Roboto, sans-serif;
  $font-family-pt-serif: PT Serif, serif;
  ```

* Цвета. Пример:

  ```scss
  $color-aqua-deep: #005741;
  $color-black: #000;
  $color-white: #fff;
  ```

  Для именования цветов можно пользоваться [данным сервисом](http://chir.ag/projects/name-that-color/).

Переменные, используемые лишь в одном блоке или компоненте следует записывать в том же файле, где они используются.

### `@mixin` и `@extend`

Повторяющиеся участки кода (20-30 строк и более), отличающиеся лишь значениями, следует выносить в отдельные миксины.

Не рекомендуется использовать директиву `@extend`. Вместо неё следует воспользоваться `@mixin`.

### Вендорные префиксы

В SCSS-коде не должно присутствовать вендорных префиксов. Они автоматически расставляются в процессе сборки.

**Неправильно**:

```scss
input {
    -webkit-transition: border-color 0.3s;
    transition: border-color 0.3s;

    &::-webkit-input-placeholder {
        color: #000;
    }

    &:-moz-placeholder {
        color: #000;
    }

    &::-moz-placeholder {
        color: #000;
    }

    &:-ms-input-placeholder {
        color: #000;
    }

    &::placeholder {
        color: #000;
    }
}
```

**Правильно**:

```scss
input {
    transition: border-color 0.3s;

    &::placeholder {
        color: #000;
    }
}
```

## Использование линтера

В сборку интегрирован линтер [stylelint](https://stylelint.io/).
Файл настроек — `.stylelintrc`.
Данный линтер позволяет поддерживать SCSS-код в соответствии с заданным регламентом.

Проверка осуществляется с помощью задачи `lintScss`:

```bash
gulp lintScss
```

Пример использования:

```scss
.block {
  &__element {
    display: inline-block
  }
  border-radius: 0px;
  height: 30px;
  width:30px;
}
```

Результаты проверки:

```text
2:3     ⚠  Expected indentation of 1 tab (indentation) [stylelint]
3:5     ⚠  Expected indentation of 2 tabs (indentation) [stylelint]
3:25    ⚠  Expected a trailing semicolon (declaration-block-trailing-semicolon) [stylelint]
4:3     ⚠  Expected indentation of 1 tab (indentation) [stylelint]
5:3     ⚠  Expected indentation of 1 tab (indentation) [stylelint]
5:3     ⚠  Expected declaration to come before rule (order/order) [stylelint]
5:3     ⚠  Expected empty line before declaration (declaration-empty-line-before) [stylelint]
5:19    ⚠  Unexpected unit (length-zero-no-unit) [stylelint]
6:3     ⚠  Expected indentation of 1 tab (indentation) [stylelint]
7:3     ⚠  Expected indentation of 1 tab (indentation) [stylelint]
7:3     ⚠  Expected "width" to come before "height" (order/properties-order) [stylelint]
7:9     ⚠  Expected single space after ":" with a single-line declaration (declaration-colon-space-after) [stylelint]
```

Исправленный код:

```scss
.block {
    border-radius: 0;
    width:30px;
    height: 30px;

    &__element {
        display: inline-block
    }
}
```
