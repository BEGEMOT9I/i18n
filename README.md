# Nano Stores I18n

<img align="right" width="92" height="92" title="Nano Stores logo"
     src="https://nanostores.github.io/nanostores/logo.svg">

Tiny and flexible JS library to make your web application translatable.
Uses [Nano Stores] state manager and [JS Internationalization API].

* **Small.** Between 448 and 844 bytes (minified and gzipped).
  Zero dependencies.
* Works with **React**, **Preact**, **Vue**, **Svelte**, and plain JS.
* Supports **tree-shaking** and translation **on-demand download**.
* **Plain JSON** translations compatible with
  online translation services like [Weblate].
* Out of the box **TypeScript** support for translations.
* **Flexible variable translations**. You can change translation,
  for instance, depends on screen size.

```tsx
// components/post.jsx
import { params, count } from '@nanostores/i18n' // You can use own functions
import { useStore } from 'nanostores'
import { i18n, format } from '../stores/i18n.js'

export const messages = i18n({
  title: 'Post details',
  publishedAt: params<{ at: string }>('Was published at {date}')
  posts: count({
    one: '{count} comment',
    many: '{count} comments'
  })
})

export const Post = ({ author, comments, publishedAt }) => {
  const t = useStore(messages)
  const { time } = useStore(format)
  return <article>
    <h1>{t.title}</h1>
    <p>{t.publishedAt({ date: time(publishedAt) })}</p>
    <p>{t.comments(comments.length)}</p>
  </article>
}
```

```ts
// stores/i18n.js
import { createI18n, localeFrom, browser, formatter } from '@nanostores/i18n'
import availableLocales from './locales.js'
import localStoreLocale from './locale-store-locale.js'

export const locale = localeFrom(
  localStoreLocale,                        // Can be also locale from URL
  browser({ available: availableLocales }) // Browser’s locale autodetect
)

export const i18n = createI18n({
  get (locale) {
    return fetchJSON(`/translations/${locale}.json`)
  }
})

export const format = formatter(locale)
```

```js
// public/translations/ru.json
{
  "title": "Данные о публикации",
  "publishedAt": "Опубликован {date}",
  "comments": {
    "one": "{count} комментарий",
    "few": "{count} комментария",
    "many": "{count} комментариев",
  }
}
```

[JS Internationalization API]: https://hacks.mozilla.org/2014/12/introducing-the-javascript-internationalization-api/
[Nano Stores]: https://github.com/nanostores/nanostores
[Weblate]: https://weblate.org/ru/

<a href="https://evilmartians.com/?utm_source=nanostores-i18n">
  <img src="https://evilmartians.com/badges/sponsored-by-evil-martians.svg"
       alt="Sponsored by Evil Martians" width="236" height="54">
</a>


## Install

```sh
npm install nanostores @nanostores/i18n
```


## Usage

### Locale

*Under construction*

### Date & Number Format

*Under construction*

### Translations

*Under construction*

#### Pluralization

*Under construction*

#### Parameters

*Under construction*

### Custom Variable Translations

*Under construction*
