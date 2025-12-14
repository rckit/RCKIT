# RCKIT – Debug

> @rckit/debug – RCKIT – Debug – React debug components with visual highlighting

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/debug)](https://www.npmjs.com/package/@rckit/debug)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/debug)](https://www.npmjs.com/package/@rckit/debug)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/debug)](https://bundlephobia.com/result?p=@rckit/debug)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/debug)](https://www.npmjs.com/package/@rckit/debug)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/debug)](https://bundlephobia.com/result?p=@rckit/debug)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/debug)](https://bundlephobia.com/result?p=@rckit/debug)
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
    *   [Using Debug Component](#using-debug-component)
    *   [Displaying JSON Data](#displaying-json-data)
    *   [Conditional Debug Rendering](#conditional-debug-rendering)
    *   [Custom Debug Elements](#custom-debug-elements)
    *   [Using Zebra Component](#using-zebra-component)
*   [📚 API Reference](#-api-reference)
    *   [Debug](#debug)
    *   [Zebra](#zebra)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/debug

# yarn
yarn add @rckit/debug

# npm
npm i @rckit/debug
```

# 📖 Features

- 🐛 **Debug component** - conditionally render debug information based on app config
- 🎨 **Visual highlighting** - zebra-striped background pattern for easy visual identification
- 📊 **JSON display** - automatically format and display JSON data with syntax highlighting
- ⚙️ **Config integration** - automatically respects `isDebug` flag from `@rckit/config`
- 🎯 **Flexible rendering** - render as any HTML element or React component
- 🔄 **Conditional display** - show/hide debug content based on custom conditions
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🌲 **Tree-shakeable** - optimized bundle size

# 🚀 Usage

## Basic Setup

The `Debug` component requires the `AppConfig` provider from `@rckit/config`. Make sure your app is wrapped with it:

```tsx
import React from 'react';
import { AppConfig } from '@rckit/config';
import { Debug } from '@rckit/debug';

function App() {
  return (
    <AppConfig>
      <YourApp />
    </AppConfig>
  );
}
```

## Using Debug Component

The `Debug` component automatically shows content only when debug mode is enabled (via `@rckit/config`):

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function MyComponent() {
  const data = { name: 'John', age: 30 };

  return (
    <div>
      <h1>My Component</h1>
      <Debug>
        <p>This will only show in debug mode</p>
        <p>Data: {data.name}</p>
      </Debug>
    </div>
  );
}
```

## Displaying JSON Data

Use the `json` prop to automatically format and display JSON data:

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function DataComponent() {
  const user = {
    id: 1,
    name: 'John Doe',
    email: 'john@example.com',
    preferences: {
      theme: 'dark',
      notifications: true,
    },
  };

  return (
    <div>
      <h1>User Profile</h1>
      <Debug json={user} />
    </div>
  );
}
```

### Compact JSON Format

By default, JSON is pretty-printed. To display compact format, set `pretty={false}`:

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function CompactDebug() {
  const data = { a: 1, b: 2, c: 3 };

  return (
    <Debug json={data} pretty={false} />
  );
}
```

## Conditional Debug Rendering

Override the default debug mode check with a custom condition:

```tsx
import React, { useState } from 'react';
import { Debug } from '@rckit/debug';

function ConditionalComponent() {
  const [showDetails, setShowDetails] = useState(false);

  return (
    <div>
      <button onClick={() => setShowDetails(!showDetails)}>
        Toggle Details
      </button>
      <Debug condition={showDetails}>
        <p>This shows when showDetails is true, regardless of debug mode</p>
      </Debug>
    </div>
  );
}
```

### Always Show Debug Content

To always show debug content regardless of debug mode:

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function AlwaysVisible() {
  return (
    <Debug condition={true}>
      <p>This is always visible</p>
    </Debug>
  );
}
```

### Never Show Debug Content

To hide debug content even in debug mode:

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function NeverVisible() {
  return (
    <Debug condition={false}>
      <p>This will never be visible</p>
    </Debug>
  );
}
```

## Custom Debug Elements

Use the `as` prop to render the debug component as a different HTML element:

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function CustomElement() {
  const data = { message: 'Debug info' };

  return (
    <div>
      <Debug as="section" json={data}>
        <h2>Debug Section</h2>
      </Debug>
      <Debug as="span">Inline debug info</Debug>
    </div>
  );
}
```

### Using Custom React Components

You can also render debug content inside custom React components:

```tsx
import React from 'react';
import { Debug } from '@rckit/debug';

function CustomCard({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

function App() {
  return (
    <Debug as={CustomCard}>
      <p>Debug content in a custom card component</p>
    </Debug>
  );
}
```

## Using Zebra Component

The `Zebra` component provides visual highlighting with a diagonal striped pattern. It's used internally by `Debug` but can also be used standalone:

```tsx
import React from 'react';
import { Zebra } from '@rckit/debug';

function HighlightedContent() {
  return (
    <Zebra>
      <p>This content has a zebra-striped background</p>
    </Zebra>
  );
}
```

### Customizing Zebra Appearance

Customize colors, border, and other visual properties:

```tsx
import React from 'react';
import { Zebra } from '@rckit/debug';

function CustomZebra() {
  return (
    <Zebra
      color="#ff0000"
      border={3}
      colors={['#ff000022', '#ff000044']}
      padding={20}
      height={300}
    >
      <p>Custom styled zebra component</p>
    </Zebra>
  );
}
```

### Zebra as Different Elements

Render zebra as any HTML element:

```tsx
import React from 'react';
import { Zebra } from '@rckit/debug';

function ZebraExamples() {
  return (
    <div>
      <Zebra as="section" padding={10}>
        <h2>Zebra Section</h2>
      </Zebra>
      <Zebra as="span" border={1}>
        Inline zebra
      </Zebra>
    </div>
  );
}
```

# 📚 API Reference

## Debug

React component for conditionally displaying debug information with visual highlighting.

### Props

```typescript
interface DebugProps {
  as?: React.ElementType;
  children?: any;
  json?: any;
  pretty?: boolean;
  condition?: boolean | null;
  [key: string]: any; // Additional props passed to the underlying element
}
```

### Props Details

- `as` - HTML element type or React component to render as (default: `'pre'` for JSON, `'div'` for children)
- `children` - React children to display when not using `json` prop
- `json` - Object to display as formatted JSON
- `pretty` - Whether to pretty-print JSON (default: `true`)
- `condition` - Override debug mode check. If `null` or `undefined`, uses `isDebug` from `@rckit/config`. If `true`, always shows. If `false`, never shows.

### Usage

```tsx
<Debug json={data} />
<Debug condition={isDev}>Debug content</Debug>
<Debug as="section" condition={true}>Always visible</Debug>
```

**Behavior:**
- Automatically checks `isDebug` from `@rckit/config` when `condition` is not provided
- Returns `null` (renders nothing) when condition is `false`
- Uses `Zebra` component internally for visual highlighting
- When `json` prop is provided, renders as `<pre>` element by default
- When `children` are provided, renders as `<div>` element by default

## Zebra

React component that provides visual highlighting with a diagonal striped background pattern.

### Props

```typescript
interface ZebraProps {
  as?: React.ElementType;
  children?: any;
  color?: string;
  border?: number;
  colors?: string[];
  padding?: number;
  height?: number;
  [key: string]: any; // Additional props passed to the underlying element
}
```

### Props Details

- `as` - HTML element type or React component to render as (default: `'div'`)
- `children` - React children to display
- `color` - Color for the dashed border outline (default: `'#fcfcfc77'`)
- `border` - Width of the dashed border in pixels (default: `2`, set to `0` to disable)
- `colors` - Array of two colors for the striped pattern (default: `['#fcfcfc77', '#eeeeee77']`)
- `padding` - CSS padding value (number in pixels)
- `height` - Maximum height in pixels

### Usage

```tsx
<Zebra>Content with zebra stripes</Zebra>
<Zebra color="#ff0000" border={3} colors={['#ff000022', '#ff000044']}>
  Custom styled content
</Zebra>
```

**Behavior:**
- Creates a diagonal repeating linear gradient using the two colors from `colors` array
- Applies a dashed outline border when `border > 0` and `color` is provided
- All additional props are spread to the underlying element
- Default colors are semi-transparent for subtle visual indication

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `@rckit/config` - Configuration management (for `isDebug` flag)
- `@lsk4/env` - Environment detection utilities (transitive dependency)

### Integration with @rckit/config

The `Debug` component automatically integrates with `@rckit/config`:

- Checks the `isDebug` flag from `useAppConfig()` hook
- Only renders content when `isDebug === true` (unless overridden by `condition` prop)
- Requires `AppConfig` provider to be present in the component tree

### Default Styling

The `Debug` component uses the following default styling:

- **Background**: Diagonal striped pattern with colors `['#00000000', '#fbba2111']`
- **Border**: No border (`border={0}`)
- **Element**: `<pre>` for JSON, `<div>` for children

The `Zebra` component uses:

- **Background**: Diagonal striped pattern with colors `['#fcfcfc77', '#eeeeee77']`
- **Border**: 2px dashed outline with color `#fcfcfc77`

### Browser Compatibility

This package uses standard React features and CSS properties:
- `repeating-linear-gradient` - supported in all modern browsers
- `outline` with dashed style - supported in all modern browsers

For older browser support, ensure you have appropriate polyfills.

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
3.  Commit your changes (`git commit -am 'feat(debug): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
