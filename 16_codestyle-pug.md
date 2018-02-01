# Синтаксис и форматирование

* Для отступов используется символ табуляции `\t`.

* Для переноса строк используется символ `\n` (LF).

* Не должно быть пробелов в конце строк.

* Максимальная длина строки — 120 символов.

* Между большими блоками кода следует оставлять одну пустую строку.

**Неправильно** (нет пустых строк):

```jade
.products
    .product
        img.product__image(src="images/products/1.png" alt="")
        .product__title
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 12345
    .product
        img.product__image(src="images/products/2.png" alt="")
        .product__title
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 45678
    .product
        img.product__image(src="images/products/3.png" alt="")
        .product__title
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 90123
.navigation
    a.navigation__link(href="/catalog?page=2")
        | Следующая страница
```

**Неправильно** (слишком много пустых строк):

```jade
.products

    .product
        img.product__image(src="images/products/1.png" alt="")

        .product__title
            | Название товара

        .product__description
            | Описание товара

        .product__price
            | 12345


    .product
        img.product__image(src="images/products/2.png" alt="")

        .product__title
            | Название товара

        .product__description
            | Описание товара

        .product__price
            | 45678


    .product
        img.product__image(src="images/products/3.png" alt="")

        .product__title
            | Название товара

        .product__description
            | Описание товара

        .product__price
            | 90123


.navigation
    a.navigation__link(href="/catalog?page=2")
        | Следующая страница
```

**Правильно:**

```jade
.products
    .product
        img.product__image(src="images/products/1.png" alt="")
        .product__title
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 12345

    .product
        img.product__image(src="images/products/2.png" alt="")
        .product__title
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 45678

    .product
        img.product__image(src="images/products/3.png" alt="")
        .product__title
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 90123

.navigation
    a.navigation__link(href="/catalog?page=2")
        | Следующая страница
```

# Однострочная вложенность

Как правило теги вкладываются друг на разных строках:

```jade
ul
    li
        a(href="/page/1")
            | 1
    li
        a(href="/page/2")
            | 2
    li
        a(href="/page/3")
            | 3
```

Но в случае, **если** строк в файле довольно много и их сокращение **увеличивает читаемость**, то допустимо
использовать однострочную запись:

```jade
ul
    li: a(href="/page/1") 1
    li: a(href="/page/2") 2
    li: a(href="/page/3") 3
```

В иных случаях не следует использовать такой способ записи.

# Самозакрывающиеся теги

Самозакрывающиеся теги (`img`, `meta`, `link`) определяются автоматически, поэтому не следует указывать это явно.

# Классы

Классы записываются сразу после тега:

```jade
ul.navigation
    li.navigation__item
```

Если у элемента не указан тег, то он принимается за `div` (по этой причине не следует явно указывать тег `div`):

```jade
.container
    .block
```

Будет преобразовано в:

```html
<div class="container">
    <div class="block"></div>
</div>
```

Атрибут `class` используется только в том случае, если он задается с помощью переменной или через условие:

```jade
- page = 'index'

.menu
    a.menu__item(class={'menu__item--active': page === 'index'} href='/')
        | Главная страница
    a.menu__item(class={'menu__item--active': page === 'catalog'} href='/catalog')
        | Каталог
    a.menu__item(class={'menu__item--active': page === 'contacts'} href='/contacts')
        | Контакты
```

# Идентификаторы

Идентификатор записывается после класса или тега.

**Неправильно:**

```jade
ul#top-menu.menu
```

**Правильно:**

```jade
ul.menu#top-menu

// или так
.menu#top-menu

// или так
#top-menu
```

Атрибут `id` используется только в случае, если он задается с помощью переменной.

# Атрибуты

Атрибуты записываются в круглых скобках после указания тега, класса и/или идентификатора.

```jade
form(action="/login.php" method="post")
    input(type="email" name="email" placeholder="E-mail")
    input(type="password" name="password" placeholder="Пароль")
    button(type="submit")
        | Войти
```

Не следует дублировать запись атрибутов.

**Неправильно:**

```jade
img(src="images/photo.jpg")(alt="")
```

**Правильно:**

```jade
img(src="images/photo.jpg" alt="")
```

# Кавычки

Для указания значения атрибутов используются двойные кавычки.

**Неправильно:**

```jade
input(type='text' name='name')
```

**Правильно:**

```jade
input(type="text" name="name")
```

# Разделение атрибутов

Атрибуты разделяются одним пробелом.

**Неправильно:**

```jade
img(src="images/logo.png", srcset="images/logo@2x.png 2x", alt="")
```

**Правильно:**

```jade
img(src="images/logo.png" srcset="images/logo@2x.png 2x" alt="")
```

# Нестандартные атрибуты

Атрибуты, в названии которых используются нестандартные символы (`(`, `)`, `[`, `]`, `:`, `@`) записываются в одинарных
кавычках.

**Неправильно:**

```jade
// Не скомпилируется
button(type="button" (click)="send()")
    | Отправить
```

```jade
button(type="button" v-on:click="send()")
    | Отправить
```

```jade
button(type="button" @click="send()")
    | Отправить
```

**Правильно:**

```jade
// Не скомпилируется
button(type="button" '(click)'="send()")
    | Отправить
```

```jade
button(type="button" 'v-on:click'="send()")
    | Отправить
```

```jade
button(type="button" '@click'="send()")
    | Отправить
```

# Многострочная запись атрибутов

Если атрибутов слишком много и/или длина строки превышает установленный предел, то следует записать каждый атрибут
в отдельной строке:

```jade
input(
    type="text"
    name="name"
    placeholder="Имя"
    maxlength="20"
    required
    autocomplete="on"
)
```

# Использование переменных в атбирутах

В значение атрибута можно передать переменную или любое JS-выражение:

```jade
img(src=`images/image-${image.number}.jpg` alt=image.description)
```

По умолчанию значения атрибутов экранируются.

```jade
.pagination(v-if="items.length > 5")
```

Будет преобразовано в:

```html
<div class="pagination" v-if="items.length &gt; 5"></div>
```

Отключить экранирование значения атрибута можно заменив `=` на `!=`.

```jade
.pagination(v-if!="items.length > 5")
```

Будет преобразовано в:

```html
<div class="pagination" v-if="items.length > 5"></div>
```

# JSON

JSON в атрибуте записывается в виде JS-объекта, а не строки.

**Неправильно:**

```jade
.slider(data-options="{autoplay: true, arrows: false, fade: true}")
```

**Правильно:**

```jade
.slider(data-options={
    autoplay: true,
    arrows: false,
    fade: true
})

// или так
.slider(
    data-options={
        autoplay: true,
        arrows: false,
        fade: true
    }
)
```

# Атрибут style

Атрибут style также при необходимости можно записать в виде JS-объекта.

```jade
.element(
    style={
        '-webkit-transform': 'rotate(45deg)',
        'transform': 'rotate(45deg)'
    }
)
```

# Использование `&attributes`

`&attributes` либо в миксинах, либо в том случае, если необходимо задать множество атрибутов элемента с помощью
переменной.

**Неправильно:**

```jade
a(href="/")&attributes({target: '_blank'})
    | На главную
```

**Правильно:**

```jade
a(href="/" target="_blank")
    | На главную
```

```jade
- attrs = {class: 'no-js', lang: 'ru'}

doctype html
html&attributes(attrs)
    head
    body
```

```jade
mixin button()
    button.button&attributes(attributes)
        block

+button().button--large(type="submit")
    | Войти
```

# Вывод текста

Текст следует выводить на следующей строке с помощью символа `|`.

**Неправильно:**

```jade
.product
    img.product__image(src="images/products/1.png" alt="")
    .product__title Название товара
    .product__description Описание товара
    .product__price 12345
```

**Правильно:**

```jade
.product
    img.product__image(src="images/products/1.png" alt="")
    .product__title
        | Название товара
    .product__description
        | Описание товара
    .product__price
        | 12345
```

В случае, **если** строк в файле довольно много и их сокращение **увеличивает читаемость**, то допустимо использовать
однострочную запись.

# Использование JS в Pug

Pug позволяет использовать JS в шаблонах:

```jade
// Однострочная запись
- title = 'Title'
- description = 'Description'

// Многострочная запись
-
    attrs = {
        class: 'no-js',
        lang: 'ru'
    }
```

Не следует использовать эту возможность для создания условий и циклов, так как в Pug уже имеются специальные
конструкции.

# Вывод переменных

Существует два варианта вывода переменных — экранированный и неэкранированный:

```jade
// Экранированный
.product
    .product__title= title
    .product__description= description
    .product__price= price

// Неэкранированный
.product
    .product__title!= title
    .product__description!= description
    .product__price!= price
```

# Вывод переменных в тексте

При необходимости вывести переменную в тексте следует воспользоваться конструкцией `#{}` (для экранированного вывода)
или `!{}` (для неэкранированного вывода):

```jade
.product
    .product__title
        | Название товара: #{title}
    .product__description
        | Описание: #{description}
    .product__price
        | Цена: !{price}р.
```

# Вывод элементов в тексте

Элементы в тексте записываются с помощью конструкции `#[]`.

**Неправильно:**

```jade
.product
    .product__title
        | <b>Название товара:</b><br>
        | <a href="/product/1">#{title}</a>
    .product__description
        | <b>Описание:</b><br>
        | #{description}
    .product__price
        | <b>Цена:</b><br>
        | !{price}р.
```

```jade
.product
    .product__title
        b Название товара:
        br
        a(href="/product/1") #{title}
    .product__description
        b Описание:
        br
        | #{description}
    .product__price
        b Цена:
        br
        | !{price}р.
```

**Правильно:**

```jade
.product
    .product__title
        | #[b Название товара:]#[br]
        | #[a(href="/product/1") #{title}]
    .product__description
        | #[b Описание:]#[br]
        | #{description}
    .product__price
        | #[b Цена:]#[br]
        | !{price}р.
```

После `#[br]` следует ставить перенос строки.

# Вывод кода

При необходимости записать `<script>` или `<style>` непосредственно в Pug, то можно воспользоваться следующей
конструкцией:

```jade
script.
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

    ga('create', 'UA-123456789-00', 'auto');
    ga('send', 'pageview');

style.
    img[href*="tns-counter"] {
        position: absolute;
        left: -9999px;
    }
```

# Управляющие конструкции

* `if` — используется для условий.

**Неправильно:**

```jade
- if (products.length) {
    .products
        // ...
- }
```

**Правильно:**

```jade
if products.length
    .products
        // ...
```

* `unless` — предназначена для условий, но не используется. Вместо нее следует использовать `if`.

* `case` — предназначена для условий. Практически не используется.

* `each` — предназначена для создания циклов.

**Неправильно:**

```jade
- for (var i = 0; i < products.length; i++) {
    - var product = products[i];
    .product
        .product__title= product.title
        .product__description= product.description
        .product__price= product.price
- }
```

**Правильно:**

```jade
each product in products
    .product
        .product__title= product.title
        .product__description= product.description
        .product__price= product.price
```

```jade
each i in Array.from(Array(10).keys())
    img(src=`images/frame-${i}.jpg` alt="")
```

* `while` — не используется.

# Наследование

Базовый шаблон (`base.pug`) не предназначен для редактирования. Не стоит в нем задавать значения переменных, подключать
какие-либо скрипты или стили, и уж тем более писать код страницы. На то он и базовый. В нем описывается самый основной
код страницы. Допустимо лишь подключать миксины в этом файле.

Если возникает необходимость изменить этот файл (подключить какие-то стили или скрипты, добавить шапку и подвал сайта),
то лучше создать другой базовый шаблон (например `custom-base.pug`) унаследованный от `base.pug` (а то и вовсе
написанный с нуля), и уже работать с этим файлом и наследовать страницы от него.

При переопределении блоков можно использовать сокращенную запись.

**Неправильно:**

```jade
block append content
    // ...
```

**Правильно:**

```jade
append content
    // ...
```

# Подключение файлов

Если страница состоит из нескольких независимых блоков, то каждый следует вынести в отдельный файл.

**Неправильно:**

```jade
.header
    // ...
.banner
    // ...
.container
    .sidebar
        // ...
    .content
        .filter
            // ...
        .products
            // ...
        .pagination
            // ...
.footer
    // ...
```

**Правильно:**

```jade
include pug/header
include pug/banner
.container
    include pug/sidebar
    .content
        include pug/filter
        include pug/products
        include pug/pagination
```

Если на странице используются какие-либо счетчики (Google Analytics, Яндекс Метрика и тому подобноее), то этот также
следует выносить в отдельный файл:

```jade
prepend scripts
    include pug/counters
```

При подключении Pug-файлов не нужно указывать расширение.

**Неправильно:**

```jade
include pug/header.pug
```

**Правильно:**

```jade
include pug/header
```

Подключать можно не только Pug, но и любые другие текстовые файлы. Например svg:

```jade
.header
    a.header__logo(href="/")
        include ../images/logo.svg
```

# Миксины

Если на сайте имеется какой-либо шаблонный блок или компонент (кнопка, карточка, статья), который встречается более
одного раза, то его следует вынести в отдельный миксин.

**Неправильно:**

```jade
.products
    .product
        a.product__image(href="/product/1")
            img(src="/images/image-1.jpg" alt="")
        a.product__title(href="/product/1")
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 12345
        a.product__link(href="/product/1")
            | Подробнее

    .product
        a.product__image(href="/product/2")
            img(src="/images/image-2.jpg" alt="")
        a.product__title(href="/product/2")
            | Название товара
        .product__description
            | Описание товара
        .product__price
            | 67890
        a.product__link(href="/product/2")
            | Подробнее
```

**Правильно:**

Создаем миксин в файле src/pug/mixins/product.pug

```jade
mixin product(options)
    .product&attributes(attributes)
        a.product__image(href=options.href)
            img(src=options.image alt="")
        a.product__title(href=options.href)= options.title
        .product__description= options.description
        .product__price= options.price
        a.product__link(href=options.href)
            | Подробнее
```

Подключаем миксин в `base.pug`:

```jade
include mixins/svg
include mixins/product
```

После можно использовать созданный миксин на любой странице:

```jade
.products
    +product({
        href: '/product/1',
        image: '/images/image-1.jpg',
        title: 'Название товара',
        description: 'Описание товара',
        price: 12345
    })

    +product({
        href: '/product/2',
        image: '/images/image-2.jpg',
        title: 'Название товара',
        description: 'Описание товара',
        price: 67890
    })
```

В миксин также можно передать содержимое (в основном используется при передаче большого количества контента, например
в статьях):

```jade
mixin article(title)
    article.article
        h1.article__title= title
        .article__content
            block

+article('Заголовок статьи')
    | Содержимое статьи
```

# Комментарии

Для комментариаев используется синтаксис `//` и `//-`:

```jade
// Однострочный комментарий, который попадет в html

//- Однострочный комментарий, который не попадет в html

//
    Многострочный комментарий,
    который попадет в html

//-
    Многострочный комментарий,
    который не попадет в html
```
