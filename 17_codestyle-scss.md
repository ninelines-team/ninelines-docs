# Синтаксис и форматирование

* Для отступов используется символ табуляции `\t`.

* Для переноса строк используется символ `\n` (LF).

* Не должно быть пробелов в конце строк.

* Максимальная длина строки — 120 символов.

* `!important` используется только для того, чтобы перебить значение `style`-атрибута.

* В коде не должно быть вендорных префиксов. (есть исключения)

**Неправильно:**

```scss
a {
    -webkit-transition: color 0.3s;
    -moz-transition: color 0.3s;
    transition: color 0.3s;
}
```

**Правильно:**

```scss
a {
    transition: color 0.3s;
}
```

Вендорные префиксы допустимы только в том случае, если вариант без префикса отсутствует.

```scss
@mixin retina {
    @media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
        @content;
    }
}
```

* Селекторы, свойства, `@`-правила, названия переменных, миксин, функций, `#`-цвета — все записывается в нижнем
регистре.

**Неправильно:**

```scss
$Color-Cod-Gray: #1A1A1A;

.Form {
    INPUT {
        color: $Color-Cod-Gray;
    }
}
```

**Правильно:**

```scss
$color-cod-gray: #1a1a1a;

.form {
    input {
        color: $color-cod-gray;
    }
}
```

* CSS-правила отделяются друг от друга пустой строкой.

**Неправильно:**

```scss
.header {
    position: relative;
    margin: 0 auto;
    padding: 15px;
    max-width: 1000px;
    background: url("../images/header.jpg") 50% 50% no-repeat;
    @include retina {
        background-image: url("../images/header@2x.jpg");
    }
    @media (min-width: 1000px) {
        padding-top: 30px;
        padding-bottom: 30px;
    }
}
```

**Правильно:**

```scss
.header {
    position: relative;
    margin: 0 auto;
    padding: 15px;
    max-width: 1000px;
    background: url("../images/header.jpg") 50% 50% no-repeat;

    @include retina {
        background-image: url("../images/header@2x.jpg");
    }

    @media (min-width: 1000px) {
        padding-top: 30px;
        padding-bottom: 30px;
    }
}
```

* Не должно быть более одной пустой строки подряд.

**Неправильно:**

```scss
.button {
    display: inline-block;


    &::before {
        content: "";
    }
}
```

**Правильно:**

```scss
.button {
    display: inline-block;

    &::before {
        content: "";
    }
}
```

* Между свойствами не должно быть пустых строк.

**Неправильно:**

```scss
.button {
    display: inline-block;

    border: solid 1px $color-black;
    border-radius: 4px;

    padding: 5px 10px;

    font-family: $font-family-roboto;
    font-weight: 300;
    font-size: 16px;
    line-height: 1.5;

    text-align: center;
    text-decoration: none;

    cursor: pointer;
}
```

**Правильно:**

```scss
.button {
    display: inline-block;
    border: solid 1px $color-black;
    border-radius: 4px;
    padding: 5px 10px;
    font-family: $font-family-roboto;
    font-weight: 300;
    font-size: 16px;
    line-height: 1.5;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
}
```

* При перечислении селекторов каждый записывается на отдельной строке.

**Неправильно:**

```scss
.prev, .next {
    position: absolute;
    top: 50%;
}
```

**Правильно:**

```scss
.prev,
.next {
    position: absolute;
    top: 50%;
}
```

* Перед `{` ставится один пробел, а после — один перенос строки.

**Неправильно:**

```scss
.header{
    position: relative;
}

.banner  {
    max-width: 1000px;
}

.footer
{
    margin-top: 15px;
}

.container {

    margin: 0 auto;
}
```

**Правильно:**

```scss
.header {
    position: relative;
}

.banner {
    max-width: 1000px;
}

.footer {
    margin-top: 15px;
}

.container {
    margin: 0 auto;
}
```

* Перед `}` не должно быть пустых строк.

**Неправильно:**

```scss
a {
    text-decoration: none; }

p {
    margin: 15px 0;

}
```

**Правильно:**

```scss
a {
    text-decoration: none;
}

p {
    margin: 15px 0;
}
```

* Перед `:` и `,` не должно быть пробелов, а после ставится один пробел.

**Неправильно:**

```scss
.container {
    padding  :  0 15px;
    max-width:  1000px;
    background: none;
}

.button {
    box-shadow: inset 0 0 2px 1px $color-black ,0 5px 4px 0 rgba($color-black, 0.25);
    transition: color 0.3s , opacity 0.3s;
}
```

**Правильно:**

```scss
.container {
    padding: 0 15px;
    max-width: 1000px;
    background: none;
}

.button {
    box-shadow: inset 0 0 2px 1px $color-black, 0 5px 4px 0 rgba($color-black, 0.25);
    transition: color 0.3s, opacity 0.3s;
}
```

* После открывающей и до закрывающей скобки не должно быть пробелов.

**Неправильно:**

```scss
a[ href ] {
    color: darken( $color-blue, 10% );
    cursor: pointer;
}
```

**Правильно:**

```scss
a[href] {
    color: darken($color-blue, 10%);
    cursor: pointer;
}
```

* Перед и после операторов (`+`, `-`, `*`, `/`) и комбинаторов (`+`, `>`, `~`) ставится один пробел.

**Неправильно:**

```scss
.sidebar {
    width: calc((100%- 30px)/2);

    >a {
        display: block;
    }
}
```

**Правильно:**

```scss
.sidebar {
    width: calc((100% - 30px) / 2);

    > a {
        display: block;
    }
}
```

* Строки записываются в двойных кавычках.

**Неправильно:**

```scss
li {
    list-style: none;

    &::before {
        content: '';
        display: inline-block;
        vertical-align: middle;
        width: 10px;
        height: 10px;
        background-image: url(../images/point.png);
    }
}
```

**Правильно:**

```scss
li {
    list-style: none;

    &::before {
        content: "";
        display: inline-block;
        vertical-align: middle;
        width: 10px;
        height: 10px;
        background-image: url("../images/point.png");
    }
}
```

* Пути записываются в двойных кавычках.

**Неправильно:**

```scss
@import 'vendor/player';

.button-play {
    background: url(../images/play.png) 50% 50% no-repeat;
}
```

**Правильно:**

```scss
@import "vendor/player";

.button-play {
    background: url("../images/play.png") 50% 50% no-repeat;
}
```

* Значения атрибутов записываются в двойных кавычках.

**Неправильно:**

```scss
a[target=_blank]::after {
    content: "";
    display: inline-block;
    width: 15px;
    height: 15px;
    background-image: url("../images/new-page.png");
}
```

**Правильно:**

```scss
a[target="_blank"]::after {
    content: "";
    display: inline-block;
    width: 15px;
    height: 15px;
    background-image: url("../images/new-page.png");
}
```

* Названия шрифтов записываются в двойных кавычках, за исключением ключевых слов.

**Неправильно:**

```scss
$font-family-roboto: Roboto, sans-serif;

.button {
    font-family: $font-family-roboto;
}
```

**Правильно:**

```scss
$font-family-roboto: "Roboto", sans-serif;

.button {
    font-family: $font-family-roboto;
}
```

* Псевдоэлементы записываются с помощью `::`.

**Неправильно:**

```scss
.list {
    &__item {
        &:before {
            content: "";
            display: inline-block;
            vertical-align: middle;
            border-radius: 50%;
            width: 8px;
            height: 8px;
            background-color: currentColor;
        }
    }
}
```

**Правильно:**

```scss
.list {
    &__item {
        &::before {
            content: "";
            display: inline-block;
            vertical-align: middle;
            border-radius: 50%;
            width: 8px;
            height: 8px;
            background-color: currentColor;
        }
    }
}
```

* Не должно быть дублирующихся свойств.

**Неправильно:**

```scss
.button {
    display: inline-block;
    border: solid 1px $color-black;
    border-radius: 4px;
    padding: 5px;
    font-family: $font-family-roboto;
    font-weight: 300;
    font-size: 16px;
    line-height: 1.5;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
    border: none;
}
```

**Правильно:**

```scss
.button {
    display: inline-block;
    border: none;
    border-radius: 4px;
    padding: 5px;
    font-family: $font-family-roboto;
    font-weight: 300;
    font-size: 16px;
    line-height: 1.5;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
}
```

* `font-weight` записывается в числовом формате.

**Неправильно:**

```scss
b {
    font-weight: bold;
}
```

**Правильно:**

```scss
b {
    font-weight: 700;
}
```

* У нулевых значений не указываются единицы измерений (кроме времени).

**Неправильно:**

```scss
.button {
    margin: 0px auto;
    padding: 5px 0px 6px;
}
```

**Правильно:**

```scss
.button {
    margin: 0 auto;
    padding: 5px 0 6px;
}
```

* Для чисел в интервале `(-1, 1)` указывается ведущий ноль.

**Неправильно:**

```scss
a {
    transition: color .3s;
}
```

**Правильно:**

```scss
a {
    transition: color 0.3s;
}
```

* Вместо именованных цветов используется `#`-запись.

**Неправильно:**

```scss
$color-black: black;
```

**Правильно:**

```scss
$color-black: #000;
```

* Для записи `#`-цвета следует использовать сокращенный вариант, если это возможно.

**Неправильно:**

```scss
$color-black: #000000;
```

**Правильно:**

```scss
$color-black: #000;
```

* При записи `rgba`-цвета задается `#`-значением или переменной.

**Неправильно:**

```scss
.overlay {
    background-color: rgba(0, 0, 0, 0.5);
}
```

**Правильно:**

```scss
.overlay {
    background-color: rgba($color-black, 0.5);
}
```

# `@extend`

Вместо директивы `@extend` следует использовать `@mixin`.

# Порядок правил

* CSS-переменные.
* `$`-переменные.
* `@include` без контента
* Свойства
* `&::before`
* `&::after`
* Различные селекторы
* `&:link`
* `&:visited`
* `&:focus`
* `&:hover`
* `&:active`
* `&:first-child`
* `&:last-child`
* `&:nth-child()`
* `&[attr]`
* `&.modifier`
* `&--modifier`
* `@include` с контентом
* `@media`

# Порядок свойств

* `all`
* `print-color-adjust`
* `appearance`
* `counter-increment`
* `counter-reset`
* `content`
* `quotes`
* `position`
* `left`
* `right`
* `top`
* `bottom`
* `z-index`
* `display`
* `columns`
* `column-width`
* `column-count`
* `column-fill`
* `column-gap`
* `column-rule`
* `column-rule-style`
* `column-rule-width`
* `column-rule-color`
* `column-span`
* `break-after`
* `break-before`
* `break-inside`
* `page-break-after`
* `page-break-before`
* `page-break-inside`
* `orphans`
* `widows`
* `flex`
* `flex-grow`
* `flex-shrink`
* `flex-basis`
* `flex-flow`
* `flex-direction`
* `flex-wrap`
* `place-content`
* `place-items`
* `place-self`
* `align-content`
* `align-items`
* `align-self`
* `justify-content`
* `justify-items`
* `justify-self`
* `order`
* `clear`
* `float`
* `grid`
* `grid-area`
* `grid-auto-columns`
* `grid-auto-flow`
* `grid-auto-rows`
* `grid-column`
* `grid-column-end`
* `grid-column-gap`
* `grid-column-start`
* `grid-gap`
* `grid-row`
* `grid-row-end`
* `grid-row-gap`
* `grid-row-start`
* `grid-template`
* `grid-template-areas`
* `grid-template-columns`
* `grid-template-rows`
* `list-style`
* `list-style-type`
* `list-style-position`
* `list-style-image`
* `caption-side`
* `empty-cells`
* `table-layout`
* `vertical-align`
* `clip-path`
* `mask`
* `mask-clip`
* `mask-composite`
* `mask-image`
* `mask-mode`
* `mask-origin`
* `mask-position`
* `mask-position-x`
* `mask-position-y`
* `mask-repeat`
* `mask-repeat-x`
* `mask-repeat-y`
* `mask-size`
* `mask-type`
* `shape-image-threshold`
* `shape-margin`
* `shape-outside`
* `contain`
* `overflow`
* `overflow-x`
* `overflow-y`
* `overflow-anchor`
* `overflow-wrap`
* `margin`
* `margin-top`
* `margin-right`
* `margin-bottom`
* `margin-left`
* `margin-before`
* `margin-end`
* `margin-after`
* `margin-start`
* `margin-collapse`
* `margin-top-collapse`
* `margin-bottom-collapse`
* `margin-before-collapse`
* `margin-after-collapse`
* `outline`
* `outline-style`
* `outline-width`
* `outline-color`
* `outline-offset`
* `outline-radius`
* `outline-radius-topleft`
* `outline-radius-topright`
* `outline-radius-bottomright`
* `outline-radius-bottomleft`
* `border`
* `border-style`
* `border-width`
* `border-color`
* `border-top`
* `border-top-style`
* `border-top-width`
* `border-top-color`
* `border-right`
* `border-right-style`
* `border-right-width`
* `border-right-color`
* `border-bottom`
* `border-bottom-style`
* `border-bottom-width`
* `border-bottom-color`
* `border-left`
* `border-left-style`
* `border-left-width`
* `border-left-color`
* `border-before`
* `border-before-style`
* `border-before-width`
* `border-before-color`
* `border-end`
* `border-end-style`
* `border-end-width`
* `border-end-color`
* `border-after`
* `border-after-style`
* `border-after-width`
* `border-after-color`
* `border-start`
* `border-start-style`
* `border-start-width`
* `border-start-color`
* `border-collapse`
* `border-image`
* `border-image-source`
* `border-image-slice`
* `border-image-width`
* `border-image-outset`
* `border-image-repeat`
* `border-radius`
* `border-top-left-radius`
* `border-top-right-radius`
* `border-bottom-right-radius`
* `border-bottom-left-radius`
* `border-spacing`
* `padding`
* `padding-top`
* `padding-right`
* `padding-bottom`
* `padding-left`
* `padding-before`
* `padding-end`
* `padding-after`
* `padding-start`
* `width`
* `height`
* `min-width`
* `min-height`
* `max-width`
* `max-height`
* `box-decoration-break`
* `box-shadow`
* `box-sizing`
* `src`
* `font`
* `font-family`
* `font-weight`
* `font-style`
* `font-display`
* `font-feature-settings`
* `font-kerning`
* `font-smoothing`
* `font-stretch`
* `font-synthesis`
* `font-variant`
* `font-variant-alternates`
* `font-variant-caps`
* `font-variant-east-asian`
* `font-variant-ligatures`
* `font-variant-numeric`
* `font-variant-position`
* `font-size`
* `font-size-adjust`
* `unicode-bidi`
* `unicode-range`
* `line-break`
* `line-height`
* `letter-spacing`
* `word-break`
* `word-spacing`
* `word-wrap`
* `white-space`
* `hyphens`
* `tab-size`
* `text-align`
* `text-align-last`
* `text-combine-upright`
* `text-decoration`
* `text-decoration-style`
* `text-decoration-line`
* `text-decoration-color`
* `text-decoration-skip`
* `text-emphasis`
* `text-emphasis-style`
* `text-emphasis-color`
* `text-emphasis-position`
* `text-fill-color`
* `text-indent`
* `text-justify`
* `text-orientation`
* `text-overflow`
* `text-rendering`
* `text-security`
* `text-shadow`
* `text-size-adjust`
* `text-stroke`
* `text-stroke-width`
* `text-stroke-color`
* `text-transform`
* `text-underline-position`
* `direction`
* `writing-mode`
* `ruby-align`
* `ruby-position`
* `color`
* `caret-color`
* `tap-highlight-color`
* `d`
* `x`
* `y`
* `cx`
* `cy`
* `r`
* `rx`
* `ry`
* `fill`
* `fill-opacity`
* `fill-rule`
* `stroke`
* `stroke-dasharray`
* `stroke-dashoffset`
* `stroke-linecap`
* `stroke-linejoin`
* `stroke-miterlimit`
* `stroke-opacity`
* `stroke-width`
* `alignment-baseline`
* `baseline-shift`
* `dominant-baseline`
* `clip-rule`
* `color-interpolation`
* `color-interpolation-filters`
* `color-rendering`
* `flood-color`
* `flood-opacity`
* `lighting-color`
* `marker`
* `marker-end`
* `marker-mid`
* `marker-start`
* `paint-order`
* `shape-rendering`
* `stop-color`
* `stop-opacity`
* `text-anchor`
* `offset`
* `offset-position`
* `offset-path`
* `offset-distance`
* `offset-anchor`
* `offset-rotate`
* `background`
* `background-image`
* `background-position`
* `background-position-x`
* `background-position-y`
* `background-size`
* `background-repeat`
* `background-repeat-x`
* `background-repeat-y`
* `background-origin`
* `background-clip`
* `background-attachment`
* `background-color`
* `background-blend-mode`
* `image-orientation`
* `image-rendering`
* `object-fit`
* `object-position`
* `opacity`
* `visibility`
* `filter`
* `isolation`
* `mix-blend-mode`
* `zoom`
* `backface-visibility`
* `perspective`
* `perspective-origin`
* `perspective-origin-x`
* `perspective-origin-y`
* `transform`
* `transform-box`
* `transform-origin`
* `transform-origin-x`
* `transform-origin-y`
* `transform-origin-z`
* `transform-style`
* `transition`
* `transition-property`
* `transition-duration`
* `transition-delay`
* `transition-timing-function`
* `animation`
* `animation-name`
* `animation-duration`
* `animation-delay`
* `animation-timing-function`
* `animation-iteration-count`
* `animation-direction`
* `animation-fill-mode`
* `animation-play-state`
* `will-change`
* `cursor`
* `pointer-events`
* `touch-action`
* `user-drag`
* `user-focus`
* `user-select`
* `user-zoom`
* `resize`
* `scroll-behavior`
* `scroll-snap-coordinate`
* `scroll-snap-destination`
* `scroll-snap-type`
* `scroll-snap-type-x`
* `scroll-snap-type-y`
