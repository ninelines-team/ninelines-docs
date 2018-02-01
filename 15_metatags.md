# Работа с метатегами

В данном разделе приведен список основных метатегов `<meta>` и `<link>` с примерами.
Менее значащие или устаревшие метатеги намеренно не указаны.

## Базовые метатеги

Базовые метатеги задают основную информацию о сайте.

### `charset`

Задает кодировку страницы.

> Значение по умолчанию в сборке — `utf-8`.

Пример:

```jade
append vars
    - meta.charset = 'utf-8'
```

### `description`

Задает описание страницы.

> Оптимальная длинна описания — не больше 160 символов.

Пример:

```jade
append vars
    - meta.description = 'Описание страницы'
```

Или так:

```jade
prepend vars
    - description = 'Описание страницы'
```

При этом также будут определены значения `og:description` и `twitter:description`.

### `keywords`

Задает список ключевых слов.

Пример:

```jade
append vars
    - meta.keywords = ['список', 'ключевых', 'слов']
```

Или так:

```jade
append vars
    - meta.keywords = 'список, ключевых, слов'
```

### `title`

Задает заголовок страницы (`<title>`).

Пример:

```jade
prepend vars
    - title = 'Заголовок страницы'
```

При этом также будут определены значения `og:title` и `twitter:title`.

### `viewport`

Позволяет управлять отображением страницы на мобильных устройствах.

> Значение по умолчанию в сборке — `width=device-width`.

Пример:

```jade
append vars
    - meta.viewport = 'width=device-width, initial-scale=1'
```

### `icon`

Задает favicon сайта.

Пример:

```jade
append vars
    - link.icon = 'favicon.ico'
```

Также можно задать иконки разных размеров:

```jade
append vars
    - link.icon16x16 = 'favicon-16x16.png'
    - link.icon32x32 = 'favicon-32x32.png'
    - link.icon96x96 = 'favicon-96x96.png'
    - link.icon128x128 = 'favicon-128x128.png'
    - link.icon196x196 = 'favicon-196x196.png'
```

### `manifest`

Задает ссылку на `manifest.json`.

Пример:

```jade
append vars
    - link.manifest = 'manifest.json'
```

Манифест веб-приложения предоставляет информацию о приложении (такую как имя, авторство, иконку и описание) в формате JSON-файла.
Цель манифеста — установить веб-приложение на рабочий стол устройства, предоставляя более быстрый доступ.


## Метатеги Apple

Метатеги Apple задают дополнительную информацию для устройств на iOS (iPhone, iPad).

### `apple-mobile-web-app-capable`

Включает режим полноэкранного приложения iOS, в котором скрывается адресная строка и панель навигации.

Пример:

```jade
append vars
    - meta.appleMobileWebAppCapable = 'on'
```

### `apple-mobile-web-app-status-bar-style`

Задает стиль строки состояния в полноэкранном режиме iOS.

Пример:

```jade
append vars
    - meta.appleMobileWebAppCapable = 'on'
    - meta.appleMobileWebAppStatusBarStyle = 'black'
```

### `apple-mobile-web-app-title`

Задает заголовок для иконки запуска в iOS.

> Если не указано, то будет использоваться значение тега `<title>`.

Пример:

```jade
append vars
    - meta.appleMobileWebAppTitle = 'Название сайта'
```

### `apple-touch-icon`

Задает иконку сайта в iOS.

Пример:

```jade
append vars
    - link.appleTouchIcon = 'images/touch-icon.png'
```

Также можно задать иконки разных размеров:

```jade
append vars
    - link.appleTouchIcon40x40 = 'images/touch-icon-40x40.png'
    - link.appleTouchIcon57x57 = 'images/touch-icon-57x57.png'
    - link.appleTouchIcon58x58 = 'images/touch-icon-58x58.png'
    - link.appleTouchIcon60x60 = 'images/touch-icon-60x60.png'
    - link.appleTouchIcon72x72 = 'images/touch-icon-72x72.png'
    - link.appleTouchIcon76x76 = 'images/touch-icon-76x76.png'
    - link.appleTouchIcon80x80 = 'images/touch-icon-80x80.png'
    - link.appleTouchIcon87x87 = 'images/touch-icon-87x87.png'
    - link.appleTouchIcon114x114 = 'images/touch-icon-114x114.png'
    - link.appleTouchIcon120x120 = 'images/touch-icon-120x120.png'
    - link.appleTouchIcon144x144 = 'images/touch-icon-144x144.png'
    - link.appleTouchIcon152x152 = 'images/touch-icon-152x152.png'
    - link.appleTouchIcon167x167 = 'images/touch-icon-167x167.png'
    - link.appleTouchIcon180x180 = 'images/touch-icon-180x180.png'
    - link.appleTouchIcon1024x1024 = 'images/touch-icon-1024x1024.png'
```

### `apple-touch-icon-precomposed`

Задает precomposed-иконку в iOS.
Используется в том случае, если к иконке не нужно применять системные стили.

Пример:

```jade
append vars
    - link.appleTouchIconPrecomposed = 'images/touch-icon-precomposed.png'
```

Также можно задать иконки разных размеров:

```jade
append vars
    - link.appleTouchIconPrecomposed40x40 = 'images/touch-icon-precomposed-40x40.png'
    - link.appleTouchIconPrecomposed57x57 = 'images/touch-icon-precomposed-57x57.png'
    - link.appleTouchIconPrecomposed58x58 = 'images/touch-icon-precomposed-58x58.png'
    - link.appleTouchIconPrecomposed60x60 = 'images/touch-icon-precomposed-60x60.png'
    - link.appleTouchIconPrecomposed72x72 = 'images/touch-icon-precomposed-72x72.png'
    - link.appleTouchIconPrecomposed76x76 = 'images/touch-icon-precomposed-76x76.png'
    - link.appleTouchIconPrecomposed80x80 = 'images/touch-icon-precomposed-80x80.png'
    - link.appleTouchIconPrecomposed87x87 = 'images/touch-icon-precomposed-87x87.png'
    - link.appleTouchIconPrecomposed114x114 = 'images/touch-icon-precomposed-114x114.png'
    - link.appleTouchIconPrecomposed120x120 = 'images/touch-icon-precomposed-120x120.png'
    - link.appleTouchIconPrecomposed144x144 = 'images/touch-icon-precomposed-144x144.png'
    - link.appleTouchIconPrecomposed152x152 = 'images/touch-icon-precomposed-152x152.png'
    - link.appleTouchIconPrecomposed167x167 = 'images/touch-icon-precomposed-167x167.png'
    - link.appleTouchIconPrecomposed180x180 = 'images/touch-icon-precomposed-180x180.png'
    - link.appleTouchIconPrecomposed1024x1024 = 'images/touch-icon-precomposed-1024x1024.png'
```

### `mask-icon`

Задает маску для иконки закрепленного сайта в iOS.

Пример:

```jade
append vars
    - link.maskIcon.href = 'mask-icon.svg'
    - link.maskIcon.color = 'red'
```

## Метатеги Microsoft

Метатеги Microsoft задают дополнительную информацию для IE и Edge на Windows.

### `application-name`

Задает заголовок закрепленного сайта в IE11 и Edge.

> Если не указано, то будет использоваться значение тега `<title>`.

Пример:

```jade
append vars
    - meta.applicationName = 'Название сайта'
```

### `msapplication-TileColor`

Задает цвет плитки в Windows 10.

Пример:

```jade
append vars
    - meta.msapplicationTileColor = '#FF3300'
```

### `msapplication-TileImage`

Задает фоновое изображение плитки в Windows 10.

Пример:

```jade
append vars
    - meta.msapplicationTileImage = 'images/tile-image.png'
```

### `msapplication-square70x70logo`

Задает иконку малой плитки в Windows 10.

Пример:

```jade
append vars
    - meta.msapplicationSquare70x70logo = 'images/ms-logo-70x70.png'
```

### `msapplication-square150x150logo`

Задает иконку средней плитки в Windows 10.

Пример:

```jade
append vars
    - meta.msapplicationSquare150x150logo = 'images/ms-logo-150x150.png'
```

### `msapplication-wide310x150logo`

Задает иконку широкой плитки в Windows 10.

Пример:

```jade
append vars
    - meta.msapplicationSquare310x150logo = 'images/ms-logo-310x150.png'
```

### `msapplication-square310x310logo`

Задает иконку большой плитки в Windows 10.

Пример:

```jade
append vars
    - meta.msapplicationSquare310x310logo = 'images/ms-logo-310x310.png'
```

### `msapplication-notification`

Позволяет определить до пяти XML-файлов, которые будут опрашиваться с определенным интервалом.
Эти файлы могут содержать уведомления, отображаемые на плитке.

Пример:

```jade
append vars
    - meta.msapplicationNotification = 'frequency=30; polling-uri=notifications/feed-1.xml; polling-uri2=notifications/feed-2.xml'
```

### `X-UA-Compatible`

Позволяет управлять режимом совместимости браузеров IE8+.

> Значение по умолчанию в сборке — `IE=edge`.

Пример:

```jade
append vars
    - meta.XUACompatible = 'IE=edge'
```

## Метатеги Open Graph

Метатеги Open Graph задают дополнительную информацию, используемую социальными сетями (VK, Twitter, Google Plus, Одноклассники и так далее) для оформления публикаций.

### `og:url`

Задает адрес страницы в Open Graph.

> Требуется указывать полный URL.<br>
> Если значение не задано, то используется текущий адрес страницы.

Пример:

```jade
append vars
    - meta.ogUrl = 'http://example.com/'
```

### `og:locale`

Задает локаль страницы в Open Graph.

> Значение по умолчанию в сборке — `ru_RU`.

Пример:

```jade
append vars
    - meta.ogLocale = 'ru_RU'
```

### `og:title`

Задает заголовок страницы в Open Graph.

Пример:

```jade
append vars
    - meta.ogTitle = 'Заголовок страницы'
```

Или так:

```jade
append vars
    - title = 'Заголовок страницы'
```

### `og:description`

Задает описание страницы в Open Graph.

Пример:

```jade
prepend vars
    - meta.ogDescription = 'Описание страницы'
```

Или так:

```jade
prepend vars
    - description = 'Описание страницы'
```

### `og:image`

Задает изображение страницы в [Open Graph](http://ogp.me/).

> Требуется указывать полный URL.

Пример:

```jade
append vars
    - meta.ogImage = 'http://example.com/images/og-image.png'
```

Или так:

```jade
prepend vars
    - image = 'http://example.com/images/og-image.png'
```

## Метатеги Twitter

Метатеги Twitter задают дополнительную информацию, используемую для оформления Twitter-публикаций.

### `twitter:card`

Задает тип карточки Twitter.

> Значение по умолчанию в сборке — `summary_large_image`.

Пример:

```jade
append vars
    - meta.twitterCard = 'summary_large_image'
```

### `twitter:site`

Задает `@username` сайта в Twitter.

Пример:

```jade
append vars
    - meta.twitterSite = '@username'
```

### `twitter:creator`

Задает `@username` автора контента в Twitter.

Пример:

```jade
append vars
    - meta.twitterCreator = '@username'
```

### `twitter:title`

Задает заголовок страницы в Twitter.

Пример:

```jade
append vars
    - meta.twitterSite = 'Заголовок страницы'
```

Или так:

```jade
prepend vars
    - title = 'Заголовок страницы'
```

### `twitter:description`

Задает описание страницы в Twitter.

Пример:

```jade
append vars
    - meta.twitterDescription = 'Описание страницы'
```

Или так:

```jade
prepend vars
    - description = 'Описание страницы'
```

### `twitter:image`

Задает изображение страницы в Twitter.

> Требуется указывать полный URL.

Пример:

```jade
append vars
    - meta.twitterImage = 'http://example.com/images/twitter-image.png'
```

Или так:

```jade
prepend vars
    - image = 'http://example.com/images/twitter-image.png'
```
