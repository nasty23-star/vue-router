# Установка %{#installation}%

<VueMasteryLogoLink></VueMasteryLogoLink>

## Пакетные менеджеры %{#Package-managers}%

Если у вас уже есть проект, использующий менеджер пакетов JavaScript, вы можете установить Vue Router из реестра npm:

::: code-group

```bash [npm]
npm install vue-router
```

```bash [yarn]
yarn add vue-router
```

```bash [pnpm]
pnpm add vue-router
```

```bash [bun]
bun add vue-router
```

```bash [deno]
deno add vue-router
```

:::

Если вы начинаете новый проект, вам может быть удобнее воспользоваться инструментом для создания структуры проекта [create-vue](https://github.com/vuejs/create-vue), который создает проект на основе Vite с возможностью включения Vue Router:

::: code-group

```bash [npm]
npm create vue@latest
```

```bash [yarn]
yarn create vue
```

```bash [pnpm]
pnpm create vue
```

```bash [bun]
bun create vue
```

:::

Вам будет предложено ответить на несколько вопросов о том, какой проект вы хотите создать. Если вы решите установить Vue Router, пример приложения также продемонстрирует некоторые из основных возможностей Vue Router.

Проекты, использующие менеджеры пакетов, обычно используют ES-модули для доступа к Vue Router, например, `import { createRouter } from 'vue-router'`.

## Прямое скачивание / CDN %{#direct-download-cdn}%

Если вы не хотите использовать сборщик, вы можете вместо этого загрузить Vue Router напрямую в браузер — либо через CDN, либо скачав соответствующие файлы и разместив их на своём сервере.

Vue Router предоставляет несколько готовых файлов для различных сценариев использования, аналогично Vue. Если вы ещё не знакомы с тем, как это устроено в Vue, рекомендуем сначала прочитать об этом.

- <https://vuejs.org/guide/quick-start.html#using-vue-from-cdn>

Vue Router поддерживает как сборки в формате **_ES-модулей_**, так и **_глобальные сборки_**. Мы рекомендуем по возможности использовать ES-модули.

Какой бы подход вы ни выбрали, важно фиксировать версии используемых библиотек, особенно в продакшене. Это означает, что в URL-адресах CDN следует указывать точную версию, которую вы хотите использовать, вместо того чтобы позволять CDN выбирать за вас последнюю версию.

Каждая сборка поставляется в версиях для разработки и для продакшена. Версии для разработки значительно больше по размеру, но содержат дополнительный код для облегчения отладки. В названиях продакшен-версий присутствует `.prod`.

### Использование ES-модулей %{#using ES modules}%

```html-vue
<script type="importmap">
  {
    "imports": {
      "vue": "https://unpkg.com/vue@{{ $frontmatter.packageVersions?.vue }}/dist/vue.esm-browser.js",
      "vue-router": "https://unpkg.com/vue-router@{{ $frontmatter.packageVersions?.['vue-router'] }}/dist/vue-router.esm-browser.js",
      "nostics": "https://unpkg.com/nostics@1/dist/index.mjs",
      "@vue/devtools-api": "https://unpkg.com/@vue/devtools-api@8/dist/vue-devtools-api.esm-browser.js"
    }
  }
</script>
<script type="module">
  import { createApp } from 'vue'
  import { createRouter } from 'vue-router'

  // ...
</script>
```

`@vue/devtools-api` нужен только при использовании сборки Vue Router для разработки. Его (импорт `@vue/devtools-api`) можно удалить при использовании продакшен-сборки `vue-router.esm-browser.prod.js`.

### Использование глобальной сборки %{#using the global build}%

```html-vue
<script src="https://unpkg.com/vue@{{ $frontmatter.packageVersions?.vue }}/dist/vue.global.js"></script>
<script src="https://unpkg.com/vue-router@{{ $frontmatter.packageVersions?.['vue-router'] }}/dist/vue-router.global.js"></script>
<script>
  const { createApp } = Vue
  const { createRouter } = VueRouter

  // ...
</script>
```
Соответствующая продакшен-сборка Vue Router называется `vue-router.global.prod.js`.
