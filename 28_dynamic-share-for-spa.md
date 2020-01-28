# Настройка динамических шерингов для SPA

С недавнего времени в сборку был добавлен новый файл `shareSettings.php`, в папку `resources`. В нем необходимо указывать все данные по шерингам. Во избежание ошибок при сборке, данный файл нельзя удалять из проекта. Он автоматически удаляется в конечном билде.

Теперь нет необходимости добавлять логику с корректировкой URL для `share.js`, создавать отдельный файл `share.php` и в нескольких местах менять данные шеринга. Достаточно один раз прописать все данные в `shareSettings.php`.

### базовый код файла shareSettings.php:

```php
$protocol = $_SERVER['PROTOCOL'] = isset($_SERVER['HTTPS']) && !empty($_SERVER['HTTPS']) ? 'https' : 'http';
$host = $protocol . '://' . $_SERVER['HTTP_HOST'];
$title = '';
$description = '';
$image = $host . '/images/';

// Uncomment the code below and fill in the pages if necessary
// $pages = [
//     '/page/1' => [
//         'title' => '',
//         'description' => '',
//         'image' => '/images/',
//     ],
// ];

$page = @$pages[$_SERVER['REQUEST_URI']];

if ($page) {
    $title = !is_null(@$page['title']) ? $page['title'] : $title;
    $description = !is_null(@$page['description']) ? $page['description'] : $description;
    $image = !is_null(@$page['image']) ? $host . $page['image'] : $image;
}
```

### пример кода с указанными данными для шеринга:

```php
$protocol = $_SERVER['PROTOCOL'] = isset($_SERVER['HTTPS']) && !empty($_SERVER['HTTPS']) ? 'https' : 'http';
$host = $protocol . '://' . $_SERVER['HTTP_HOST'];
$title = 'Базовый заголовок страницы';
$description = 'Базовое описание страницы';
$image = $host . '/images/share/main.jpg';

$pages = [
    '/article' => [
        'title' => 'Заголовок статьи',
        'description' => 'Описание статьи',
        'image' => '/images/share/article.jpg',
    ],
    '/test' => [
        'title' => 'Заголовок теста',
        'description' => 'Описание теста',
        'image' => '/images/share/test.jpg',
    ],
    '/test?result=1' => [
        'title' => 'Заголовок результатов теста №1',
        'description' => 'Описание результатов теста №1',
        'image' => '/images/share/test.jpg',
    ],
    '/test?result=2' => [
        'title' => 'Заголовок результатов теста №2',
        'description' => 'Описание результатов теста №2',
        'image' => '/images/share/test.jpg',
    ],
    '/product' => [
        'title' => 'Заголовок продуктовой страницы',
        'description' => 'Описание продуктовой страницы',
        'image' => '/images/share/product.jpg',
    ],
];

$page = @$pages[$_SERVER['REQUEST_URI']];

if ($page) {
    $title = !is_null(@$page['title']) ? $page['title'] : $title;
    $description = !is_null(@$page['description']) ? $page['description'] : $description;
    $image = !is_null(@$page['image']) ? $host . $page['image'] : $image;
}
```

---

Чтобы все данные из этого файла попали в разметку страницы при входе, необходимо обязательно внести небольшие изменения в корневой файл `index.pug`.

### пример кода для index.pug:

```jade
extends pug/base

prepend vars
    - title = '<?= htmlspecialchars($title) ?>'
    - description = '<?= htmlspecialchars($description) ?>'
    - image = '<?= htmlspecialchars($image) ?>'

append vars
    //- ...

block content
    //- ...
```

Теперь на локальном сервере во вкладке будет отображаться подобное - `<?= htmlspecialchars($title) ?>`. Не стоит пугаться, корректный заголовок (а также description и image) будут работать на тестовом, а также боевом серверах.

Это происходит по той причине, что `index.html`, который создается в результате обычного билда, просто не умеет читать php-код. А на сервер вместо `index.html` будет добавляться `index.php`, который прекрасно распознает все эти переменные.

---

Также в папке `resources` теперь хранится файл `.htaccess`, который также нельзя удалять и для него тоже настроено автоудаление, если сборка не запущена в режиме SPA. Этот файл содержит настройки для корректной работы сайта в режиме SPA.
