# Работа с изображениями

Изображения следует хранить в папке `src/images`.
При запуске задачи `images` файлы из папки `src/images` копируются в `build/images`.

```text
ninelines-template
├── build
│   └── images
└── src
    └── images
```

Для оптимизации изображений можно использовать задачу `optimize:images`.

> `optimize:images` оптимизирует только исходные файлы из папки `src/images`!

Предварительно оптимизированные изображения рекомендуется хранить в папке `src/resources/images`.
В таком случае при запуске задачи `optimize:images` данные файлы не будут затронуты.

```text
ninelines-template
└── src
    └── resources
        └── images
```

## Работа с PNG-спрайтами

Работа с PNG-спрайтами строится следующим образом:

1. Берем две версии иконки — обычную и retina (увеличенную в два раза).
   Сохраняем в `src/images/sprites/png`:

   ```text
   ninelines-template
   └── src
       └── images
           └── sprites
               └── png
                   ├── phone.png
                   └── phone@2x.png
   ```

2. Запускаем задачу `sprites:png` (если уже запущен `gulp watch` или `gulp`, то данный шаг можно пропустить):

   ```bash
   gulp sprites:png
   ```

3. Генератор оптимизирует и объединяет иконки в спрайты:

   ```text
   ninelines-template
   └── build
       └── images
           ├── sprites.png
           └── sprites@2x.png
   ```

   На основе предзаданного шаблона `src/scss/_sprites.hbs` генерируется файл `src/scss/_sprites.scss`, содержащий вспомогательную информацию о получившихся спрайтах:

   ```text
   ninelines-template
   └── src
       └── scss
           ├── _sprites.hbs
           └── _sprites.scss
   ```

   Для каждой иконки создается CSS-класс в формате `.sprite-[name]`.
   В нашем случае получим класс `.sprite-phone`.

   В сборке также содержится ряд SCSS-функций и миксин для работы со спрайтами.

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

   Или в SCSS (с помощью миксин):

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
   ninelines-template
   └── src
       └── images
           └── sprites
               └── svg
                   └── phone.svg
   ```

2. Запускаем задачу `sprites:svg` (если уже запущен `gulp watch` или `gulp`, то данный шаг можно пропустить):

   ```bash
   gulp sprites:svg
   ```

3. Генератор оптимизирует и объединяет иконки в один спрайт:

   ```text
   ninelines-template
   └── build
       └── images
           └── sprites.svg
   ```

   В сборке содержится Pug-миксин для подключения SVG-спрайтов.<br>
   `src/pug/mixins/svg.pug`:

   ```jade
    mixin svg(name)
       svg&attributes(attributes)
           use(xlink:href=`${baseDir}images/sprites.svg#${name}`)
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
