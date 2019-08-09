# Использование БЭМ методологии

Что такое БЭМ и всю информацио о методологии можно прочесть [здесь](https://ru.bem.info/methodology/).

* Используется стиль именования [«Two Dashes»](https://ru.bem.info/methodology/naming-convention/#%D1%81%D1%82%D0%B8%D0%BB%D1%8C-two-dashes).

* Название блока должно быть логически понятным: header, footer, nav, sidebar, content, list и т.п.

* Элемент - составная часть блока. Не должен использоваться вне блока и не должен являться частью другого элемента.

* Модификатор не должен использоваться самостоятельно.

* Допустимы модификаторы со значениями, но желательно использовать в очень редких случаях.

* Допустимо использование миксов.

* В идеале, каждый блок должен представлять из себя независимый компонент. Такой компонент позволяет без труда использовать его много раз в повторяющихся местах сайта, быстро и безболезненно редактировать и дополнять его, а также переносить из проекта в проект (универсальный компонент).

**Неправильно:**

```jade
.header--fixed
  .header__top
    button.header__top__burger
    a.header__top__logo(href="#")
    
  .header__bottom
    .header__nav
      .header__nav__item
        a.header__nav__item__link(href="#")
      .header__nav__item--active
        a.header__nav__item--active__link(href="#")
      .header__nav__item
        a.header__nav__item__link(href="#")
```

**Правильно:**

```jade
header.header.header--fixed
  .header__top
    button.header__burger(type="button")
    a.header__logo(href="#")
    
  .header__bottom
    nav.nav
      .nav__item
        a.nav__link(href="#")
      .nav__item.nav__item--active
        a.nav__link(href="#")
      .nav__item
        a.nav__link(href="#")
```

**Правильно:**

```jade
header.header.is-fixed
  .header__top
    button.header__burger(type="button")
    a.header__logo(href="#")
    
  .header__bottom
    nav.nav
      .nav__item
        a.nav__link(href="#")
      .nav__item.nav__item.is-active
        a.nav__link(href="#")
      .nav__item
        a.nav__link(href="#")
```
