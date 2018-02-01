# Подключение сторонних библиотек

Библиотеки подключаются с помощью npm.
При установке следует указывать ключ `--save` или `--save-dev`.

Пример:

```bash
npm install --save jquery
npm install --save-dev gulp
```

`--save` указывается для библиотек, код которых попадает в итоговую сборку (папку `build`) и будет использоваться на сайте.<br>
`--save-dev` указывается для библиотек, которые используются только для сборки.

После установки необходимо подключить нужные файлы библиотеки:

* скрипты — в `src/js/vendor.js` (рекомендуется подключать неминифицированные файлы).
* стили — в `src/scss/_vendor.scss`.
* изображения — в `src/images`.
* любые другие файлы — в `src/resources`.

Полный пример, описывающий установку библиотеки fancybox:

1. Установка:

   ```bash
   npm install --save fancybox
   ```

2. Подключение скриптов в файл `src/js/vendor.js`:

   ```js
   // @include('../../node_modules/fancybox/dist/js/jquery.fancybox.js')
   ```

3. Подключение стилей в файл `src/scss/_vendor.scss`:

   ```scss
   $fancybox-image-url: "../images";

   @import "../../node_modules/fancybox/dist/scss/jquery.fancybox";
   ```

4. Копирование изображений в `src/images`:

   ```text
   project-template
   └── src
       ├── images
       │   ├── blank.gif
       │   ├── fancybox_loading.gif
       │   ├── fancybox_loading@2x.gif
       │   ├── fancybox_overlay.png
       │   ├── fancybox_sprite.png
       │   ├── fancybox_sprite@2x.png
       │   └── ...
       └── ...
   ```

Если библиотека отсутствует в npm, либо её нужно модифицировать, то файлы следует скачать и закинуть в папки `src/js/vendor` и `src/scss/vendor`.
