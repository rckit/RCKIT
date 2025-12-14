# RCKIT – Link

> @rckit/link – RCKIT – Link – React link and image components with router integration support

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/link)](https://www.npmjs.com/package/@rckit/link)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/link)](https://www.npmjs.com/package/@rckit/link)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/link)](https://bundlephobia.com/result?p=@rckit/link)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/link)](https://www.npmjs.com/package/@rckit/link)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/link)](https://bundlephobia.com/result?p=@rckit/link)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/link)](https://bundlephobia.com/result?p=@rckit/link)
[![Package size](https://badgen.net//github/license/rckit/rckit)](https://github.com/rckit/rckit/blob/main/LICENSE)
[![Ask us in Telegram](https://img.shields.io/badge/Ask%20us%20in-Telegram-brightblue.svg)](https://t.me/lskjschat)

<!-- template file="scripts/templates/preview.md" start -->

<!-- template end -->

***

<!-- # 📒 Table of contents  -->

# Table of contents

*   [⌨️ Install](#️-install)
*   [📖 Features](#-features)
*   [🚀 Usage](#-usage)
    *   [Basic Setup](#basic-setup)
    *   [Using ComponentProvider](#using-componentprovider)
    *   [Using Link Component](#using-link-component)
    *   [Using Image Component](#using-image-component)
    *   [Router Integration](#router-integration)
    *   [Next.js Integration](#nextjs-integration)
    *   [React Router Integration](#react-router-integration)
*   [📚 API Reference](#-api-reference)
    *   [ComponentProvider](#componentprovider)
    *   [Link](#link)
    *   [Image](#image)
    *   [ComponentContext](#componentcontext)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/link

# yarn
yarn add @rckit/link

# npm
npm i @rckit/link
```

# 📖 Features

- 🔗 **Router-agnostic Link component** - works with any routing library or plain HTML
- 🖼️ **Flexible Image component** - supports custom image components (e.g., Next.js Image)
- 🎯 **Context-based configuration** - easily swap components via context provider
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🌲 **Tree-shakeable** - optimized bundle size
- ⚡ **Zero dependencies** - lightweight and fast
- 🔄 **Fallback support** - gracefully falls back to native HTML elements when no custom components provided

# 🚀 Usage

## Basic Setup

Use `Link` and `Image` components directly without any provider for standard HTML behavior:

```tsx
import React from 'react';
import { Link, Image } from '@rckit/link';

function App() {
  return (
    <div>
      <Link href="/about">About Us</Link>
      <Image src="/logo.png" alt="Logo" />
    </div>
  );
}
```

## Using ComponentProvider

Wrap your application with `ComponentProvider` to use custom router components:

```tsx
import React from 'react';
import { ComponentProvider, Link, Image } from '@rckit/link';
import { Link as NextLink, Image as NextImage } from 'next/link';

function App() {
  return (
    <ComponentProvider
      Router={null}
      Link={NextLink}
      Image={NextImage}
    >
      <YourApp />
    </ComponentProvider>
  );
}
```

## Using Link Component

The `Link` component automatically uses the custom Link from context or falls back to a standard `<a>` tag:

```tsx
import React from 'react';
import { Link } from '@rckit/link';

function Navigation() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/about">About</Link>
      <Link href="/contact">Contact</Link>
    </nav>
  );
}
```

### Link with Additional Props

All standard anchor tag props are supported:

```tsx
import React from 'react';
import { Link } from '@rckit/link';

function ExternalLink() {
  return (
    <Link
      href="https://example.com"
      target="_blank"
      rel="noopener noreferrer"
    >
      External Link
    </Link>
  );
}
```

## Using Image Component

The `Image` component automatically uses the custom Image from context or falls back to a standard `<img>` tag:

```tsx
import React from 'react';
import { Image } from '@rckit/link';

function Profile() {
  return (
    <div>
      <Image
        src="/avatar.jpg"
        alt="User Avatar"
        width={100}
        height={100}
      />
    </div>
  );
}
```

### Image with Additional Props

All standard image tag props are supported:

```tsx
import React from 'react';
import { Image } from '@rckit/link';

function Gallery() {
  return (
    <div>
      <Image
        src="/photo1.jpg"
        alt="Photo 1"
        width={800}
        height={600}
        loading="lazy"
      />
    </div>
  );
}
```

## Router Integration

### Next.js Integration

Integrate with Next.js Link and Image components:

```tsx
import React from 'react';
import { ComponentProvider, Link, Image } from '@rckit/link';
import NextLink from 'next/link';
import NextImage from 'next/image';

function App({ Component, pageProps }) {
  return (
    <ComponentProvider
      Router={null}
      Link={NextLink}
      Image={NextImage}
    >
      <Component {...pageProps} />
    </ComponentProvider>
  );
}

// In your components
function MyComponent() {
  return (
    <div>
      <Link href="/about">About</Link>
      <Image src="/logo.png" alt="Logo" width={200} height={100} />
    </div>
  );
}
```

### React Router Integration

Integrate with React Router's Link component:

```tsx
import React from 'react';
import { ComponentProvider, Link } from '@rckit/link';
import { Link as RouterLink } from 'react-router-dom';

function App() {
  return (
    <ComponentProvider
      Router={null}
      Link={RouterLink}
      Image="img"
    >
      <YourApp />
    </ComponentProvider>
  );
}

// In your components
function Navigation() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```

### Custom Router Integration

You can integrate with any routing library:

```tsx
import React from 'react';
import { ComponentProvider, Link } from '@rckit/link';
import { Link as CustomRouterLink } from 'your-router-library';

function App() {
  return (
    <ComponentProvider
      Router={null}
      Link={CustomRouterLink}
      Image="img"
    >
      <YourApp />
    </ComponentProvider>
  );
}
```

# 📚 API Reference

## ComponentProvider

React context provider that allows you to inject custom Link and Image components.

### Props

```typescript
interface ComponentProviderProps {
  children: React.ReactNode;
  Router?: any;
  Link?: React.ComponentType<any> | string;
  Image?: React.ComponentType<any> | string;
}
```

### Usage

```tsx
<ComponentProvider
  Router={null}
  Link={NextLink}
  Image={NextImage}
>
  <YourApp />
</ComponentProvider>
```

**Features:**
- Provides component context to all child components
- Allows overriding default Link and Image components
- Falls back to native HTML elements (`'a'` and `'img'`) if not provided
- `Router` prop is reserved for future use

## Link

React component that renders a link using the custom Link from context or a standard anchor tag.

### Props

```typescript
type LinkProps = React.HTMLProps<HTMLAnchorElement>;
```

All standard HTML anchor element props are supported, including:
- `href` - Link destination
- `target` - Link target (e.g., `'_blank'`)
- `rel` - Link relationship
- `className` - CSS class name
- And all other standard anchor tag attributes

### Usage

```tsx
<Link href="/about">About Us</Link>
```

**Behavior:**
- Uses `components.Link` from context if available
- Falls back to standard `<a>` tag if no custom Link provided
- Supports all standard anchor tag props and events

## Image

React component that renders an image using the custom Image from context or a standard img tag.

### Props

```typescript
type ImageProps = React.HTMLProps<HTMLImageElement>;
```

All standard HTML image element props are supported, including:
- `src` - Image source URL
- `alt` - Alternative text
- `width` - Image width
- `height` - Image height
- `loading` - Loading strategy (`'lazy'`, `'eager'`)
- `className` - CSS class name
- And all other standard image tag attributes

### Usage

```tsx
<Image src="/logo.png" alt="Logo" width={200} height={100} />
```

**Behavior:**
- Uses `components.Image` from context if available
- Falls back to standard `<img>` tag if no custom Image provided
- Supports all standard image tag props and events

## ComponentContext

React context that stores the component configuration.

```typescript
const ComponentContext = createContext({
  Router: null,
  Link: 'a',
  Image: 'img',
});
```

**Default Values:**
- `Router` - `null` (reserved for future use)
- `Link` - `'a'` (standard anchor tag)
- `Image` - `'img'` (standard image tag)

**Note:** This context is primarily used internally. Use `ComponentProvider` to configure components rather than accessing the context directly.

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)

### Component Override

You can override the default components by providing them through `ComponentProvider`:

```tsx
<ComponentProvider
  Link={CustomLink}
  Image={CustomImage}
>
  {/* Your app */}
</ComponentProvider>
```

### Fallback Behavior

If no custom components are provided, the components fall back to native HTML elements:
- `Link` → `<a>`
- `Image` → `<img>`

This ensures the components work out of the box without any configuration.

### Type Safety

The package provides full TypeScript support. All components accept standard HTML element props, ensuring type safety when using custom router components.

### Browser Compatibility

This package uses standard React patterns and is compatible with all modern browsers that support React.

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
3.  Commit your changes (`git commit -am 'feat(link): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
