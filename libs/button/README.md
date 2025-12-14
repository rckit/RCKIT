# RCKIT – Button

> @rckit/button – RCKIT – Button – React button component with icon support and responsive text hiding

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/button)](https://www.npmjs.com/package/@rckit/button)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/button)](https://www.npmjs.com/package/@rckit/button)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/button)](https://bundlephobia.com/result?p=@rckit/button)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/button)](https://www.npmjs.com/package/@rckit/button)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/button)](https://bundlephobia.com/result?p=@rckit/button)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/button)](https://bundlephobia.com/result?p=@rckit/button)
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
    *   [Basic Usage](#basic-usage)
    *   [Icon Button](#icon-button)
    *   [Button with Text](#button-with-text)
    *   [Responsive Text Hiding](#responsive-text-hiding)
    *   [Button Variants](#button-variants)
    *   [Button Sizes](#button-sizes)
    *   [Custom Styling](#custom-styling)
*   [📚 API Reference](#-api-reference)
    *   [IconButton](#iconbutton)
    *   [IconButtonProps](#iconbuttonprops)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/button

# yarn
yarn add @rckit/button

# npm
npm i @rckit/button
```

# 📖 Features

- 🎨 **Icon support** - easily add icons to buttons
- 📱 **Responsive design** - automatic text hiding on mobile devices
- 🎯 **Type-safe** - full TypeScript support with type definitions
- 🔧 **Flexible** - extends all react-bootstrap Button props
- 🎨 **Customizable** - supports custom styling via style prop
- 🌲 **Tree-shakeable** - optimized bundle size
- ⚡ **Lightweight** - minimal overhead over react-bootstrap Button

# 🚀 Usage

## Basic Usage

Import and use the `IconButton` component:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';

function MyComponent() {
  return (
    <IconButton icon={<span>🚀</span>}>
      Launch
    </IconButton>
  );
}
```

## Icon Button

Create a button with an icon:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';
import { FaSave } from 'react-icons/fa';

function SaveButton() {
  return (
    <IconButton 
      icon={<FaSave />}
      variant="primary"
      onClick={() => console.log('Saved!')}
    >
      Save
    </IconButton>
  );
}
```

## Button with Text

The `IconButton` component supports both icon and text content:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';
import { FaDownload } from 'react-icons/fa';

function DownloadButton() {
  return (
    <IconButton 
      icon={<FaDownload />}
      variant="success"
    >
      Download File
    </IconButton>
  );
}
```

## Responsive Text Hiding

Use the `autohide` prop to automatically hide button text on small screens while keeping the icon visible:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';
import { FaSearch } from 'react-icons/fa';

function SearchButton() {
  return (
    <IconButton 
      icon={<FaSearch />}
      autohide
      variant="outline-primary"
    >
      Search
    </IconButton>
  );
}
```

With `autohide={true}`, the text "Search" will be hidden on mobile devices (using Bootstrap's `d-none d-sm-inline` classes) but the icon will remain visible.

## Button Variants

All react-bootstrap button variants are supported:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';
import { FaCheck, FaTimes, FaInfo } from 'react-icons/fa';

function VariantButtons() {
  return (
    <div>
      <IconButton icon={<FaCheck />} variant="primary">Primary</IconButton>
      <IconButton icon={<FaCheck />} variant="secondary">Secondary</IconButton>
      <IconButton icon={<FaCheck />} variant="success">Success</IconButton>
      <IconButton icon={<FaCheck />} variant="danger">Danger</IconButton>
      <IconButton icon={<FaCheck />} variant="warning">Warning</IconButton>
      <IconButton icon={<FaCheck />} variant="info">Info</IconButton>
      <IconButton icon={<FaCheck />} variant="light">Light</IconButton>
      <IconButton icon={<FaCheck />} variant="dark">Dark</IconButton>
      <IconButton icon={<FaCheck />} variant="link">Link</IconButton>
    </div>
  );
}
```

## Button Sizes

All react-bootstrap button sizes are supported:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';
import { FaStar } from 'react-icons/fa';

function SizeButtons() {
  return (
    <div>
      <IconButton icon={<FaStar />} size="lg">Large</IconButton>
      <IconButton icon={<FaStar />} size="sm">Small</IconButton>
    </div>
  );
}
```

## Custom Styling

You can customize the button styling using the `style` prop:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';
import { FaHeart } from 'react-icons/fa';

function CustomButton() {
  return (
    <IconButton 
      icon={<FaHeart />}
      style={{
        borderRadius: '20px',
        padding: '10px 20px',
      }}
    >
      Like
    </IconButton>
  );
}
```

The component uses flexbox layout with a gap between icon and text, which can be customized via CSS variables:

```tsx
import React from 'react';
import { IconButton } from '@rckit/button';

function CustomGapButton() {
  return (
    <IconButton 
      icon={<span>⭐</span>}
      style={{
        gap: '8px', // Override default gap
      }}
    >
      Star
    </IconButton>
  );
}
```

# 📚 API Reference

## IconButton

React component that extends react-bootstrap's Button with icon support and responsive text hiding.

### Props

```typescript
interface IconButtonProps extends ButtonProps {
  icon: React.ReactNode;
  autohide?: boolean;
}
```

### Usage

```tsx
<IconButton 
  icon={<YourIcon />}
  autohide={false}
  variant="primary"
  size="lg"
  onClick={handleClick}
>
  Button Text
</IconButton>
```

**Features:**
- Extends all `ButtonProps` from react-bootstrap
- Automatically applies flexbox layout with proper alignment
- Icon and text are properly spaced using CSS gap
- Icon size is normalized to `1em` to match text size
- Supports responsive text hiding via `autohide` prop

## IconButtonProps

TypeScript interface defining the props for the IconButton component.

```typescript
type IconButtonProps = ButtonProps & {
  icon: React.ReactNode;
  autohide?: boolean;
};
```

### Props

#### `icon` (required)

- **Type:** `React.ReactNode`
- **Description:** The icon element to display in the button. Can be any React node (SVG, icon component, emoji, etc.)

#### `autohide` (optional)

- **Type:** `boolean`
- **Default:** `false`
- **Description:** When `true`, the button text will be hidden on mobile devices (screens smaller than `sm` breakpoint) using Bootstrap's `d-none d-sm-inline` classes. The icon will remain visible.

#### Other Props

All props from react-bootstrap's `ButtonProps` are supported, including:
- `variant` - Button style variant ('primary', 'secondary', 'success', etc.)
- `size` - Button size ('lg', 'sm')
- `disabled` - Disable the button
- `onClick` - Click handler
- `type` - Button type ('button', 'submit', 'reset')
- `className` - Additional CSS classes
- `style` - Custom inline styles
- And all other standard button props

### Examples

```tsx
// Basic icon button
<IconButton icon={<FaSave />}>Save</IconButton>

// Icon only (no children)
<IconButton icon={<FaClose />} />

// With autohide for mobile
<IconButton icon={<FaSearch />} autohide>Search</IconButton>

// With all react-bootstrap props
<IconButton 
  icon={<FaDownload />}
  variant="success"
  size="lg"
  disabled={isLoading}
  onClick={handleDownload}
>
  Download
</IconButton>
```

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `react-bootstrap` - Bootstrap components for React (peer dependency)

### Layout

The component uses flexbox layout with the following default styles:
- `display: 'inline-flex'`
- `alignItems: 'center'`
- `gap: 'var(--bs-btn-padding-y)'` (uses Bootstrap's button padding as gap)

### Icon Styling

Icons are wrapped in a `<span>` with `fontSize: '1em'` to ensure they match the text size.

### Responsive Behavior

When `autohide` is enabled, the text uses Bootstrap's responsive utility classes:
- `d-none` - Hidden by default (mobile)
- `d-sm-inline` - Visible from small breakpoint and up

This ensures the button remains functional on mobile devices while saving space by hiding text.

### Browser Compatibility

This package depends on react-bootstrap, which supports all modern browsers. The flexbox layout and CSS gap property are supported in:
- Chrome 84+
- Firefox 63+
- Safari 14.1+
- Edge 84+

For older browser support, ensure you have appropriate polyfills or use a CSS-in-JS solution that handles fallbacks.

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
3.  Commit your changes (`git commit -am 'feat(button): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
