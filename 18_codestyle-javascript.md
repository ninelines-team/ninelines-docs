# Синтаксис и форматирование

* Для отступов используется символ табуляции `\t`.

* Для переноса строк используется символ `\n` (LF).

* Не должно быть пробелов в конце строк.

* Максимальная длина строки — 120 символов.

* Всегда ставится `;`.

**Неправильно:**

```js
$('form').on('submit', (event) => {
    let $form = $(event.currentTarget)

    event.preventDefault()

    if (validate($form)) {
        $.post($form.attr('action'))
            .done(() => {
                showSuccessModal()
            })
            .fail(() => {
                showErrorModal()
            })
    }
})
```

**Правильно:**

```js
$('form').on('submit', (event) => {
    let $form = $(event.currentTarget);

    event.preventDefault();

    if (validate($form)) {
        $.post($form.attr('action'))
            .done(() => {
                showSuccessModal();
            })
            .fail(() => {
                showErrorModal();
            });
    }
})
```

* Используется строгое сравнение `===` и `!==` (вместо `==` и `!=`).

**Неправильно:**

```js
$('.test__button').on('click', () => {
    if (test.currentQuestionIndex == test.questions.length - 1) {
        test.finish();
    }

    test.answer();
});
```

**Правильно:**

```js
$('.test__button').on('click', () => {
    if (test.currentQuestionIndex === test.questions.length - 1) {
        test.finish();
    }

    test.answer();
});
```

* Не должно быть неиспользуемых переменных.

**Неправильно:**

```js
let dx = event.clientX - start.clientX;
let dy = event.clientY - start.clientY;

$slider.css({
    '-webkit-transform': `translate(${dx}px, 0)`,
    'transform': `translate(${dx}px, 0)`,
});
```

**Правильно:**

```js
let dx = event.clientX - start.clientX;

$slider.css({
    '-webkit-transform': `translate(${dx}px, 0)`,
    'transform': `translate(${dx}px, 0)`,
});
```

* Переменные объявляются на отдельных строках.

**Неправильно:**

```js
function showPage($page) {
    let $currentPage = $('.page--current'),
        $header = $('.header'),
        $footer = $('.footer');

    new TimelineMax()
        .to([
            $header,
            $footer,
            $currentPage,
        ], 1, {
            opacity: 0,
            onComplete() {
                $currentPage.removeClass('page--current');
            },
        })
        .from([
            $header,
            $footer,
            $page,
        ], 1, {
            clearProps: 'all',
            onStart() {
                $page.addClass('page--current');
            },
        });
}
```

**Правильно:**

```js
function showPage($page) {
    let $currentPage = $('.page--current');
    let $header = $('.header');
    let $footer = $('.footer');

    new TimelineMax()
        .to([
            $header,
            $footer,
            $currentPage,
        ], 1, {
            opacity: 0,
            onComplete() {
                $currentPage.removeClass('page--current');
            },
        })
        .from([
            $header,
            $footer,
            $page,
        ], 1, {
            clearProps: 'all',
            onStart() {
                $page.addClass('page--current');
            },
        });
}
```

* Не следует сокращать названия переменных и функций.

**Неправильно:**

```js
$('.js-scroll').on('click', (e) => {
    let $l = $(e.currentTarget);
    let h = $l.attr('href');
    let t = $(h).offset().top;

    $('html, body').animate({
        scrollTop: t,
    }, 500);
});
```

**Правильно:**

```js
$('.js-scroll').on('click', (event) => {
    let $link = $(event.currentTarget);
    let href = $link.attr('href');
    let top = $(href).offset().top;

    $('html, body').animate({
        scrollTop: top,
    }, 500);
});
```

* После определения переменных следует оставлять пустую строку.

**Неправильно:**

```js
$('form').on('submit', (event) => {
    let $form = $(event.currentTarget);
    let $button = $form.find('submit');
    event.preventDefault();
    $button.prop('disabled', true);
    submitForm($form);
});
```

**Правильно:**

```js
$('form').on('submit', (event) => {
    let $form = $(event.currentTarget);
    let $button = $form.find('submit');

    event.preventDefault();
    $button.prop('disabled', true);
    submitForm($form);
});
```

* Операторы в выражениях отделяются одним пробелом.

**Неправильно:**

```js
function sum(a, b) {
    return a+b;
}
```

**Правильно:**

```js
function sum(a, b) {
    return a + b;
}
```

* Перед `return` следует оставлять пустую строку.

**Неправильно:**

```js
function getQueryParam(key) {
    let params = location.search.slice(1).split('&');

    for (let param of params) {
        param = param.split('&');

        if (param[0] === key) {
            return param[1];
        }
    }
    return null;
}
```

**Правильно:**

```js
function getQueryParam(key) {
    let params = location.search.slice(1).split('&');

    for (let param of params) {
        param = param.split('&');

        if (param[0] === key) {
            return param[1];
        }
    }

    return null;
}
```

* Многострочные конструкции и выражения отделяются пустой строкой.

**Неправильно:**

```js
function f() {
    console.log('f');
}
function g() {
    console.log('g');
}
let timer = {
    start() {
        this.stop();
        this.intervalId = setInterval(() => {
            console.log('Tick');
        }, 1000);
    },
    stop() {
        clearInterval(this.intervalId);
    },
};
if (x > 5) {
    x = 0;
}
if (!items.length) {
    items.push(42);
}
switch (number) {
    case 4:
        console.log('a');
        break;
    case 5:
        console.log('b');
        break;
    case 1:
        console.log('c');
        break;
    default:
        console.log('d');
        break;
}
for (let i = 0; i < 10; i++) {
    y *= i;
}
$('.button').on('click', (event) => {
    event.preventDefault();
    run();
});
```

**Правильно:**

```js
function f() {
    console.log('f');
}

function g() {
    console.log('g');
}

let timer = {
    start() {
        this.stop();

        this.intervalId = setInterval(() => {
            console.log('Tick');
        }, 1000);
    },

    stop() {
        clearInterval(this.intervalId);
    },
};

if (x > 5) {
    x = 0;
}

if (!items.length) {
    items.push(42);
}

switch (number) {
    case 4:
        console.log('a');
        break;

    case 5:
        console.log('b');
        break;

    case 1:
        console.log('c');
        break;

    default:
        console.log('d');
        break;
}

for (let i = 0; i < 10; i++) {
    y *= i;
}

$('.button').on('click', (event) => {
    event.preventDefault();
    run();
});
```

* Не более одной пустой строки подряд.

**Неправильно:**

```js
$('.js-scroll-to').on('click', (event) => {
    event.preventDefault();
    scrollTo(event.currentTarget.href);
});


$('.js-close').on('click', (event) => {
    $(event.currentTarget).parent().removeClass('is-open');
});
```

**Правильно:**

```js
$('.js-scroll-to').on('click', (event) => {
    event.preventDefault();
    scrollTo(event.currentTarget.href);
});

$('.js-close').on('click', (event) => {
    $(event.currentTarget).parent().removeClass('is-open');
});
```

* Не следует использовать однострочную запись `if` без фигурных скобок.

**Неправильно:**

```js
function resizeItems() {
    if (!items.length) return;

    items.forEach((item) => {
        item.resize();
    });
}
```

**Правильно:**

```js
function resizeItems() {
    if (!items.length) {
        return;
    }

    items.forEach((item) => {
        item.resize();
    });
}
```

* Для строк используются одинарные кавычки.

**Неправильно:**

```js
let name = "John Doe"
```

**Правильно:**

```js
let name = 'John Doe';
```

# ES6 возможности

* Используются шаблонные строки вместо конкатенации.

**Неправильно:**

```js
function getDateTime() {
    let now = new Date();
    let year = now.getFullYear().toString().padStart(2, '0');
    let month = (now.getMonth() + 1).toString().padStart(2, '0');
    let day = now.getDate().toString().padStart(2, '0');
    let hours = now.getHours().toString().padStart(2, '0');
    let minutes = now.getMinutes().toString().padStart(2, '0');

    return year + '.' + month + '.' + day + ' ' + hours + ':' + minutes; 
}
```

**Правильно:**

```js
function getDateTime() {
    let now = new Date();
    let year = now.getFullYear().toString().padStart(2, '0');
    let month = (now.getMonth() + 1).toString().padStart(2, '0');
    let day = now.getDate().toString().padStart(2, '0');
    let hours = now.getHours().toString().padStart(2, '0');
    let minutes = now.getMinutes().toString().padStart(2, '0');

    return `${year}.${month}.${day} ${hours}:${minutes}`; 
}
```

* Используется `let` вместо `var`.

**Неправильно:**

```js
var name = 'John';
var surname = 'Doe';
var fullname = `${name} ${surname}`;
```

**Правильно:**

```js
let name = 'John';
let surname = 'Doe';
let fullname = `${name} ${surname}`;
```

**Правильно:**

```js
```

* Используются стрелочные функции вместо анонимных.

**Неправильно:**

```js
$('form').on('submit', function (event) {
    event.preventDefault();
    submitForm(this);
});
```

**Правильно:**

```js
$('form').on('submit', (event) => {
    event.preventDefault();
    submitForm(event.currentTarget);
});
```

* Следует использовать сокращенную запись ключей объекта.

**Неправильно:**

```js
function getObjectPosition(object) {
    let $offset = $(object).offset();
    let x = $offset.top;
    let y = $offset.left;
    
    return {
        x: x,
        y: y,
    };
}
```

**Правильно:**

```js
function getObjectPosition(object) {
    let $offset = $(object).offset();
    let x = $offset.top;
    let y = $offset.left;
    
    return {
        x,
        y,
    };
}
```

* Следует использовать сокращенную запись методов объекта.

**Неправильно:**

```js
TweenMax.from($element, 1, {
    opacity: 0,
    clearProps: 'all',
    onStart: () => {
        $element.removeClass('is-hidden');
    },
});
```

**Правильно:**

```js
TweenMax.from($element, 1, {
    opacity: 0,
    clearProps: 'all',
    onStart() {
        $element.removeClass('is-hidden');
    },
});
```
