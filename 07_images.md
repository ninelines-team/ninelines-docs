# Работа с изображениями

Изображения следует хранить в папке `src/images`.
При запуске задачи `images` файлы из папки собираются, оптимизируются, и получившийся результат сохраняется в `build/images`.

```text
project-template
├── build
│   └── images
└── src
    ├── images
    └── resources
        └── images
```

Если изображений очень много, либо имеются файлы, обработка которых занимает значительное время, то их необходимо предварительно оптимизировать и сохранить в папке `src/resources/images`:

```text
project-template
└── src
    └── resources
        └── images
```

Оптимизированные изображения можно получить одним из следующих способов:

* Скопировать из `build/images`.
* С помощью графического редактора.
* С помощью онлайн-инструментов ([tinypng.com](https://tinypng.com), [optimizilla.com](http://optimizilla.com/ru/), [compressor.io](https://compressor.io/)).
* С помощью консольных утилит ([optipng](http://optipng.sourceforge.net/), [jpegoptim](https://ruhighload.com/post/Jpegoptim)).

После переноса файлов в `src/resources/images` неоптимизированные версии изображений из папки `src/images` можно удалить.

## Работа с PNG-спрайтами

Работа с PNG-спрайтами строится следующим образом:

1. Берем две версии иконки — обычную и retina (увеличенную в два раза).
   Сохраняем в `src/images/sprites/png`:

   ```text
   project-template
   └── src
       └── images
           └── sprites
               └── png
                   ├── phone.png
                   └── phone@2x.png
   ```

2. Запускаем задачу `pngSprites` (если уже запущен `gulp watch` или `gulp`, то данный шаг можно пропустить):

   ```bash
   gulp pngSprites
   ```

3. Генератор оптимизирует и объединяет иконки в спрайты:

   ```text
   project-template
   └── build
       └── images
           ├── sprites.png
           └── sprites@2x.png
   ```

   На основе предзаданного шаблона `src/scss/_sprites.hbs` генерируется файл `src/scss/_sprites.scss`, содержащий вспомогательную информацию о получившихся спрайтах:

   ```text
   project-template
   └── src
       └── scss
           ├── _sprites.hbs
           └── _sprites.scss
   ```

   Для каждой иконки создается CSS-класс в формате `.sprite-[name]`.
   В нашем случае получим класс `.sprite-phone`.

   В сборке также содержится ряд SCSS-функций и миксинов для работы со спрайтами.

   `src/scss/functions/_sprites.scss`:

   ```scss
   @function sprite($name, $size: normal)  { /* ... */ }
   @function sprite-width($name, $size: normal)  { /* ... */ }
   @function sprite-height($name, $size: normal)  { /* ... */ }
   @function sprite-image($name, $size: normal)  { /* ... */ }
   @function sprite-x($name, $size: normal)  { /* ... */ }
   @function sprite-y($name, $size: normal)  { /* ... */ }
   @function sprite-total-width($name, $size: normal)  { /* ... */ }
   @function sprite-total-height($name, $size: normal) { /* ... */ }
   ```

   `src/scss/mixins/_srites.scss`:

   ```scss
   @mixin sprite-width($name, $size: normal)  { /* ... */ }
   @mixin sprite-height($name, $size: normal)  { /* ... */ }
   @mixin sprite-background-image($name, $size: normal)  { /* ... */ }
   @mixin sprite-background-position($name, $size: normal)  { /* ... */ }
   @mixin sprite-background-size($name, $size: normal)  { /* ... */ }
   @mixin sprite-background($name, $size: normal)  { /* ... */ }
   @mixin sprite($name)  { /* ... */ }
   ```

4. Полученные спрайты можно использовать в Pug (с помощью классов):

   ```jade
   footer
       a(href="tel:+71234567890")
           span.sprite-phone
           | +7 (123) 456-78-90
   ```

   Или в SCSS (с помощью миксинов):

   ```scss
   footer {
       a {
           &::before {
               @include sprite("phone");

               content: "";
           }
       }
   }
   ```

## Работа с SVG-спрайтами

Принцип работы с SVG-спрайтами:

1. Получаем векторные иконки в формате `.svg` (либо заранее подготовленные, либо экспортируем с помощью редактора).
   Сохраняем в папку `src/images/sprites/svg`:

   ```text
   project-template
   └── src
       └── images
           └── sprites
               └── svg
                   └── phone.svg
   ```

2. Запускаем задачу `svgSprites` (если уже запущен `gulp watch` или `gulp`, то данный шаг можно пропустить):

   ```bash
   gulp svgSprites
   ```

3. Генератор оптимизирует и объединяет иконки в один спрайт:

   ```text
   project-template
   └── build
       └── images
           └── sprites.svg
   ```

   В сборке содержится Pug-миксин для подключения SVG-спрайтов.<br>
   `src/pug/mixins/svg.pug`:

   ```jade
   mixin svg(name)
       svg&attributes(attributes)
           use(xlink:href="/images/sprites.svg#" + name)
   ```

4. Подключаем иконку в Pug:

   ```jade
   footer
       a(href="tel:+71234567890")
           +svg("phone")
           | +7 (123) 456-78-90
   ```

   При необходимости иконку можно стилизовать:

   ```scss
   footer {
       a {
           svg {
               display: inline-block;
               vertical-align: middle;
               width: 30px;
               height: 30px;
               fill: $color-black;
           }
       }
   }
   ```

   Если цвет заливки или обводки не удается изменить с помощью CSS, то необходимо открыть SVG-файл иконки в редакторе и удалить соответствующие атрибуты (`fill`, `stroke`) из кода.
