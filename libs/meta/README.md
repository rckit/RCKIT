# RCKIT – Meta

> @rckit/meta – RCKIT – Meta – React components and hooks for managing HTML meta tags and environment variables

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/meta)](https://www.npmjs.com/package/@rckit/meta)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/meta)](https://www.npmjs.com/package/@rckit/meta)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/meta)](https://bundlephobia.com/result?p=@rckit/meta)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/meta)](https://www.npmjs.com/package/@rckit/meta)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/meta)](https://bundlephobia.com/result?p=@rckit/meta)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/meta)](https://bundlephobia.com/result?p=@rckit/meta)
[![Package size](https://badgen.net//github/license/rckit/rckit)](https://github.com/rckit/rckit/blob/main/LICENSE)
[![Ask us in Telegram](https://img.shields.io/badge/Ask%20us%20in-Telegram-brightgreen.svg)](https://t.me/lskjschat)

<!-- template file="scripts/templates/preview.md" start -->

<!-- template end -->

***

<!-- # 📒 Table of contents  -->

# Table of contents

*   [⌨️ Install](#️-install)
*   [📖 Features](#-features)
*   [🚀 Usage](#-usage)
    *   [Basic Setup](#basic-setup)
    *   [Using HeadMeta Component](#using-headmeta-component)
    *   [Using useHeadMeta Hook](#using-useheadmeta-hook)
    *   [Using HeadEnv Component](#using-headenv-component)
    *   [Custom Meta Configuration](#custom-meta-configuration)
    *   [Open Graph Tags](#open-graph-tags)
    *   [Twitter Card Tags](#twitter-card-tags)
*   [📚 API Reference](#-api-reference)
    *   [HeadMeta](#headmeta)
    *   [useHeadMeta](#useheadmeta)
    *   [HeadEnv](#headenv)
    *   [Meta Interface](#meta-interface)
    *   [OpenGraph Interface](#opengraph-interface)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/meta

# yarn
yarn add @rckit/meta

# npm
npm i @rckit/meta
```

# 📖 Features

- 🏷️ **HTML meta tags management** - easy-to-use components and hooks for managing page metadata
- 🔍 **SEO optimization** - automatic generation of title, description, and Open Graph tags
- 🐦 **Twitter Card support** - built-in Twitter Card meta tags generation
- 🌐 **Open Graph support** - full Open Graph protocol implementation for social media sharing
- 🎯 **Title masking** - customizable title format with mask support (e.g., `%s | Site Name`)
- 🔧 **Environment variables** - inject environment variables into `window` object for client-side access
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🎨 **React-friendly** - designed for React applications with hooks and components
- 🌲 **Tree-shakeable** - optimized bundle size

# 🚀 Usage

## Basic Setup

Import and use the components in your React application:

```tsx
import React from 'react';
import { HeadMeta, HeadEnv } from '@rckit/meta';

function App() {
  return (
    <>
      <HeadEnv isDev={process.env.NODE_ENV === 'development'} />
      <HeadMeta title="Home Page" />
      <div>Your app content</div>
    </>
  );
}
```

## Using HeadMeta Component

The `HeadMeta` component automatically generates and renders all necessary meta tags based on the provided title:

```tsx
import React from 'react';
import { HeadMeta } from '@rckit/meta';

function HomePage() {
  return (
    <>
      <HeadMeta title="Welcome to Our Site" />
      <div>
        <h1>Home Page</h1>
      </div>
    </>
  );
}
```

### With Custom Description

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function AboutPage() {
  const metaElements = useHeadMeta({
    title: 'About Us',
    description: 'Learn more about our company and mission',
  });

  return (
    <>
      {metaElements}
      <div>
        <h1>About Us</h1>
      </div>
    </>
  );
}
```

## Using useHeadMeta Hook

The `useHeadMeta` hook gives you more control over meta tag generation and allows you to customize the output:

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function ProductPage() {
  const metaElements = useHeadMeta({
    title: 'Product Name',
    description: 'Product description for SEO',
    titleMask: '%s | My Store',
  });

  return (
    <>
      {metaElements}
      <div>
        <h1>Product Name</h1>
      </div>
    </>
  );
}
```

### Custom Title Mask

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function BlogPost() {
  const metaElements = useHeadMeta({
    title: 'My Blog Post',
    titleMask: '%s - Blog',
    description: 'This is a blog post about...',
  });

  return (
    <>
      {metaElements}
      <article>
        <h1>My Blog Post</h1>
        <p>Content...</p>
      </article>
    </>
  );
}
```

## Using HeadEnv Component

The `HeadEnv` component injects environment variables into the `window` object, making them accessible on the client side:

```tsx
import React from 'react';
import { HeadEnv } from '@rckit/meta';

function App() {
  return (
    <>
      <HeadEnv 
        isDev={process.env.NODE_ENV === 'development'}
        apiUrl={process.env.NEXT_PUBLIC_API_URL}
        version={process.env.NEXT_PUBLIC_VERSION}
      />
      <div>Your app</div>
    </>
  );
}
```

### Accessing Environment Variables

After using `HeadEnv`, you can access the variables in your client-side code:

```tsx
// In your client-side code
if (window.__DEV__) {
  console.log('Development mode');
}

const apiUrl = window.env?.apiUrl;
const isDev = window.env?.isDev;
```

## Custom Meta Configuration

### Full Meta Configuration

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function ArticlePage() {
  const metaElements = useHeadMeta({
    title: 'Article Title',
    titleMask: '%s | News Site',
    description: 'Article description for search engines',
    openGraph: {
      title: 'Custom OG Title',
      description: 'Custom OG description',
      url: 'https://example.com/article',
      type: 'article',
      image: 'https://example.com/article-image.jpg',
      locale: 'en_US',
      siteName: 'News Site',
    },
  });

  return (
    <>
      {metaElements}
      <article>
        <h1>Article Title</h1>
        <p>Content...</p>
      </article>
    </>
  );
}
```

## Open Graph Tags

Open Graph tags are automatically generated for better social media sharing:

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function ShareablePage() {
  const metaElements = useHeadMeta({
    title: 'Shareable Content',
    description: 'This page will look great when shared on social media',
    openGraph: {
      url: 'https://example.com/shareable',
      image: 'https://example.com/og-image.png',
      type: 'website',
    },
  });

  return (
    <>
      {metaElements}
      <div>Content to share</div>
    </>
  );
}
```

### Open Graph for Articles

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function NewsArticle() {
  const metaElements = useHeadMeta({
    title: 'Breaking News',
    description: 'Latest news update',
    openGraph: {
      type: 'article',
      url: 'https://example.com/news/breaking',
      image: 'https://example.com/news-image.jpg',
      locale: 'en_US',
    },
  });

  return (
    <>
      {metaElements}
      <article>News content...</article>
    </>
  );
}
```

## Twitter Card Tags

Twitter Card tags are automatically generated based on Open Graph data:

```tsx
import React from 'react';
import { useHeadMeta } from '@rckit/meta';

function TwitterCardPage() {
  const metaElements = useHeadMeta({
    title: 'Twitter Card Example',
    description: 'This will display nicely on Twitter',
    openGraph: {
      image: 'https://example.com/twitter-image.jpg',
      url: 'https://example.com/twitter-card',
    },
  });

  return (
    <>
      {metaElements}
      <div>Content with Twitter Card support</div>
    </>
  );
}
```

# 📚 API Reference

## HeadMeta

React component that renders meta tags based on the provided title.

### Props

```typescript
interface HeadMetaProps {
  title: string;
}
```

### Usage

```tsx
<HeadMeta title="Page Title" />
```

**Features:**
- Automatically generates title, description, Open Graph, and Twitter Card meta tags
- Uses default values for missing fields
- Applies title mask format (default: `%s | Kit4`)
- Returns React elements ready to be rendered in the document head

## useHeadMeta

React hook that generates meta tag elements based on the provided configuration.

### Parameters

```typescript
interface Meta {
  title?: string;
  titleMask?: string;
  description?: string;
  openGraph?: OpenGraph;
}
```

### Returns

Returns an array of React elements (`React.ReactElement[]`) containing:
- `<title>` element
- `<meta>` elements for description
- `<meta>` elements for Open Graph tags
- `<meta>` elements for Twitter Card tags

### Usage

```tsx
const metaElements = useHeadMeta({
  title: 'My Page',
  description: 'Page description',
});
```

**Default Values:**
- `title`: `'Kit4'` (if not provided)
- `titleMask`: `'%s | Kit4'` (if not provided)
- `description`: `'Kit4 description'` (if not provided)
- `lang`: `'en'` (default language)

**Open Graph Defaults:**
- `title`: Uses meta title if not specified
- `description`: Uses meta description if not specified
- `locale`: Uses default lang if not specified
- `url`: Empty string if not specified
- `type`: `'website'` if not specified
- `image`: Empty string if not specified
- `siteName`: Uses default title if not specified

**Twitter Card Defaults:**
- `card`: `'summary_large_image'`
- `site`: `'en'`
- Other fields inherit from Open Graph data

## HeadEnv

React component that injects environment variables into the `window` object via a script tag.

### Props

```typescript
interface HeadEnvProps {
  isDev: boolean;
  [key: string]: any;
}
```

### Usage

```tsx
<HeadEnv 
  isDev={process.env.NODE_ENV === 'development'}
  apiUrl="https://api.example.com"
  version="1.0.0"
/>
```

**Features:**
- Sets `window.__DEV__` to the boolean value of `isDev`
- Sets `window.env` to an object containing all provided props
- Injects a script tag into the document head
- All props are JSON-stringified and made available on the client side

**Generated Script:**
```javascript
window.__DEV__ = Boolean(true);
window.env = {"isDev": true, "apiUrl": "https://api.example.com", "version": "1.0.0"};
```

## Meta Interface

TypeScript interface for meta configuration.

```typescript
interface Meta {
  title?: string;
  titleMask?: string;
  description?: string;
  openGraph?: OpenGraph;
}
```

### Fields

- `title` - Page title (optional, defaults to `'Kit4'`)
- `titleMask` - Title format mask with `%s` placeholder (optional, defaults to `'%s | Kit4'`)
- `description` - Page description for meta tags (optional, defaults to `'Kit4 description'`)
- `openGraph` - Open Graph configuration object (optional)

## OpenGraph Interface

TypeScript interface for Open Graph configuration.

```typescript
interface OpenGraph {
  title?: string;
  description?: string;
  locale?: string;
  url?: string;
  type?: string;
  image?: string;
  siteName?: string;
}
```

### Fields

- `title` - Open Graph title (defaults to meta title if not provided)
- `description` - Open Graph description (defaults to meta description if not provided)
- `locale` - Locale code (e.g., `'en_US'`, defaults to meta lang)
- `url` - Canonical URL of the page
- `type` - Content type (e.g., `'website'`, `'article'`, defaults to `'website'`)
- `image` - URL to the Open Graph image
- `siteName` - Name of the site (defaults to default title)

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)

### Default Meta Values

The package uses the following default values:

```typescript
const defaultMeta = {
  title: 'Kit4',
  lang: 'en',
  titleMask: '%s | Kit4',
  description: 'Kit4 description',
};
```

### Title Mask Format

The `titleMask` supports a `%s` placeholder that will be replaced with the actual title:

- `'%s | Kit4'` → `'My Page | Kit4'` (if title is `'My Page'`)
- `'%s - Blog'` → `'Post Title - Blog'` (if title is `'Post Title'`)
- `'Kit4 - %s'` → `'Kit4 - My Page'` (if title is `'My Page'`)

### Meta Tags Generated

The hook generates the following meta tags:

1. **Standard Meta Tags:**
   - `<title>` - Page title
   - `<meta name="description" content="...">` - Page description

2. **Open Graph Tags:**
   - `<meta name="og:title" content="...">`
   - `<meta name="og:description" content="...">`
   - `<meta name="og:locale" content="...">`
   - `<meta name="og:url" content="...">`
   - `<meta name="og:type" content="...">`
   - `<meta name="og:image" content="...">`
   - `<meta name="og:site_name" content="...">`

3. **Twitter Card Tags:**
   - `<meta name="twitter:card" content="summary_large_image">`
   - `<meta name="twitter:site" content="...">`
   - `<meta name="twitter:title" content="...">`
   - `<meta name="twitter:description" content="...">`
   - `<meta name="twitter:image" content="...">`

### Environment Variables Injection

The `HeadEnv` component injects environment variables in a way that makes them accessible in client-side code:

- `window.__DEV__` - Boolean indicating development mode
- `window.env` - Object containing all environment variables passed as props

**Note:** Only non-empty values are included in the generated meta tags. Empty strings are filtered out.

### Browser Compatibility

This package uses standard React and HTML features, which are supported in all modern browsers. The `dangerouslySetInnerHTML` prop is used for environment variable injection, which is a standard React feature.

***

# 📖 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

# 👥 Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->

<!-- prettier-ignore-start -->

<!-- markdownlint-disable -->

<table>
  <tr>
    <td align="center"><a href="https://isuvorov.com"><img src="https://avatars2.githubusercontent.com/u/1056977?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Igor Suvorov</b></sub></a><br /><a href="rckit/rckit///commits?author=isuvorov" title="Code">💻</a> <a href="#design-isuvorov" title="Design">🎨</a> <a href="#ideas-isuvorov" title="Ideas, Planning, & Feedback">🤔</a></td>
  </tr>
</table>
<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

# 👏 Contributing

1.  Fork it (<https://github.com/rckit/rckit/fork>)
2.  Create your feature branch (`git checkout -b features/fooBar`)
3.  Commit your changes (`git commit -am 'feat(meta): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
