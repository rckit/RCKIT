# RCKIT – Breadcrumbs

> @rckit/breadcrumbs – RCKIT – Breadcrumbs – React breadcrumbs component with menu integration

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/breadcrumbs)](https://www.npmjs.com/package/@rckit/breadcrumbs)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/breadcrumbs)](https://www.npmjs.com/package/@rckit/breadcrumbs)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/breadcrumbs)](https://bundlephobia.com/result?p=@rckit/breadcrumbs)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/breadcrumbs)](https://www.npmjs.com/package/@rckit/breadcrumbs)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/breadcrumbs)](https://bundlephobia.com/result?p=@rckit/breadcrumbs)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/breadcrumbs)](https://bundlephobia.com/result?p=@rckit/breadcrumbs)
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
    *   [Using AppMenuConfig Provider](#using-appmenuconfig-provider)
    *   [Basic Breadcrumbs](#basic-breadcrumbs)
    *   [Automatic Breadcrumbs from Menu](#automatic-breadcrumbs-from-menu)
    *   [Custom Breadcrumbs Items](#custom-breadcrumbs-items)
    *   [Breadcrumbs with Title](#breadcrumbs-with-title)
    *   [Breadcrumbs with Actions](#breadcrumbs-with-actions)
    *   [Custom Divider](#custom-divider)
*   [📚 API Reference](#-api-reference)
    *   [AppBreadcrumbs](#appbreadcrumbs)
    *   [BreadcrumbItem](#breadcrumbitem)
    *   [AppMenuConfig](#appmenuconfig)
    *   [useAppMenuConfig](#useappmenuconfig)
    *   [MenuItem](#menuitem)
    *   [findBreadcrumbs](#findbreadcrumbs)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/breadcrumbs

# yarn
yarn add @rckit/breadcrumbs

# npm
npm i @rckit/breadcrumbs
```

# 📖 Features

- 🍞 **React breadcrumbs component** with Bootstrap integration
- 🔗 **Automatic breadcrumb generation** from menu structure
- 🎯 **Smart path detection** - automatically finds breadcrumb path based on active href
- 📱 **Responsive design** - mobile-friendly with adaptive layout
- 🎨 **Customizable dividers** - support for custom divider components
- 🔧 **Menu integration** - works seamlessly with AppMenuConfig context
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🌲 **Tree-shakeable** - optimized bundle size
- 🎛️ **Flexible API** - supports both automatic and manual breadcrumb configuration

# 🚀 Usage

## Basic Setup

Wrap your application with the `AppMenuConfig` provider to enable menu-based breadcrumbs:

```tsx
import React from 'react';
import { AppMenuConfig } from '@rckit/breadcrumbs';

const menuItems = [
  {
    title: 'Home',
    href: '/',
  },
  {
    title: 'Products',
    href: '/products',
    items: [
      {
        title: 'Electronics',
        href: '/products/electronics',
      },
    ],
  },
];

function App() {
  return (
    <AppMenuConfig items={menuItems}>
      <YourApp />
    </AppMenuConfig>
  );
}
```

## Using AppMenuConfig Provider

The `AppMenuConfig` component provides menu configuration context to all child components. This enables automatic breadcrumb generation based on the menu structure.

```tsx
import React from 'react';
import { AppMenuConfig } from '@rckit/breadcrumbs';

function Root() {
  const menuItems = [
    { title: 'Dashboard', href: '/dashboard' },
    {
      title: 'Settings',
      href: '/settings',
      items: [
        { title: 'Profile', href: '/settings/profile' },
        { title: 'Security', href: '/settings/security' },
      ],
    },
  ];

  return (
    <AppMenuConfig items={menuItems}>
      <div>
        <Header />
        <Main />
        <Footer />
      </div>
    </AppMenuConfig>
  );
}
```

### Dynamic Menu Items

Menu items can also be provided as a function that receives context:

```tsx
import React from 'react';
import { AppMenuConfig } from '@rckit/breadcrumbs';

function Root() {
  const getMenuItems = (ctx: any) => {
    // Generate menu items based on context (user permissions, etc.)
    return [
      { title: 'Home', href: '/' },
      ...(ctx.isAdmin ? [{ title: 'Admin', href: '/admin' }] : []),
    ];
  };

  return (
    <AppMenuConfig items={getMenuItems}>
      <YourApp />
    </AppMenuConfig>
  );
}
```

## Basic Breadcrumbs

Use the `AppBreadcrumbs` component to display breadcrumbs:

```tsx
import React from 'react';
import { AppBreadcrumbs } from '@rckit/breadcrumbs';

function MyPage() {
  return (
    <div>
      <AppBreadcrumbs activeHref="/products/electronics" />
      <main>Page content</main>
    </div>
  );
}
```

## Automatic Breadcrumbs from Menu

When `AppMenuConfig` is set up, breadcrumbs are automatically generated based on the active href:

```tsx
import React from 'react';
import { AppBreadcrumbs } from '@rckit/breadcrumbs';

function ProductPage() {
  // Breadcrumbs will automatically show: Home > Products > Electronics
  // based on the menu structure and current route
  return (
    <div>
      <AppBreadcrumbs activeHref="/products/electronics" />
      <ProductDetails />
    </div>
  );
}
```

## Custom Breadcrumbs Items

You can provide custom breadcrumb items directly:

```tsx
import React from 'react';
import { AppBreadcrumbs } from '@rckit/breadcrumbs';

function CustomPage() {
  const customItems = [
    { title: 'Home', href: '/' },
    { title: 'Custom', href: '/custom' },
    { title: 'Current Page' },
  ];

  return (
    <div>
      <AppBreadcrumbs items={customItems} />
      <PageContent />
    </div>
  );
}
```

## Breadcrumbs with Title

Display a page title alongside breadcrumbs:

```tsx
import React from 'react';
import { AppBreadcrumbs } from '@rckit/breadcrumbs';

function ProductPage() {
  return (
    <div>
      <AppBreadcrumbs
        activeHref="/products/electronics"
        title="Electronics"
        showTitle={true}
      />
      <ProductDetails />
    </div>
  );
}
```

The title is automatically shown when:
- Only one breadcrumb item exists
- A custom title is provided
- Actions are present

## Breadcrumbs with Actions

Add action buttons to the breadcrumbs area:

```tsx
import React from 'react';
import { AppBreadcrumbs } from '@rckit/breadcrumbs';

function ProductPage() {
  return (
    <div>
      <AppBreadcrumbs
        activeHref="/products/electronics"
        title="Electronics"
        actions={
          <>
            <button>Edit</button>
            <button>Delete</button>
          </>
        }
      />
      <ProductDetails />
    </div>
  );
}
```

## Custom Divider

Customize the divider between breadcrumb items:

```tsx
import React from 'react';
import { BreadcrumbItem } from '@rckit/breadcrumbs';

function CustomBreadcrumbs() {
  const customDivider = <span> / </span>;

  return (
    <BreadcrumbItem href="/" divider={customDivider}>
      Home
    </BreadcrumbItem>
  );
}
```

# 📚 API Reference

## AppBreadcrumbs

Main component for displaying breadcrumbs navigation.

### Props

```typescript
interface AppBreadcrumbsProps {
  title?: string;
  activeHref?: string;
  actions?: React.ReactNode;
  items?: MenuItem[];
  showTitle?: boolean;
}
```

### Props Description

- `title` - Optional page title to display below breadcrumbs
- `activeHref` - Current page href used to automatically find breadcrumb path from menu
- `actions` - Optional React node (buttons, links, etc.) displayed on the right side
- `items` - Optional custom breadcrumb items (overrides automatic menu-based breadcrumbs)
- `showTitle` - Controls title visibility (default: auto-determined based on breadcrumbs length)

### Usage

```tsx
<AppBreadcrumbs
  activeHref="/products/electronics"
  title="Electronics"
  actions={<button>Edit</button>}
/>
```

**Features:**
- Automatically finds breadcrumb path from menu structure when `activeHref` is provided
- Responsive layout with mobile-friendly design
- Hides breadcrumbs when only one item exists (unless title or actions are present)
- Last breadcrumb item is not clickable (current page)

## BreadcrumbItem

Component for individual breadcrumb items.

### Props

```typescript
interface BreadcrumbItemProps {
  href?: string;
  divider?: React.ReactNode;
  showDivider?: boolean;
  children: React.ReactNode;
}
```

### Props Description

- `href` - Optional link URL (if not provided, item is rendered as plain text)
- `divider` - Custom divider component (default: ArrowRight icon)
- `showDivider` - Whether to show divider before item (default: true)
- `children` - Item label/content

### Usage

```tsx
<BreadcrumbItem href="/products" showDivider={true}>
  Products
</BreadcrumbItem>
```

## AppMenuConfig

React context provider component that manages menu configuration.

### Props

```typescript
interface AppMenuConfigProps {
  items?: MenuItem[] | ((ctx: any) => MenuItem[]);
  children: React.ReactNode;
}
```

### Props Description

- `items` - Menu items array or function that returns menu items based on context
- `children` - Child components that can access menu configuration

### Usage

```tsx
<AppMenuConfig items={menuItems}>
  <YourApp />
</AppMenuConfig>
```

**Features:**
- Provides menu configuration to all child components
- Supports both static and dynamic menu items
- Enables automatic breadcrumb generation

## useAppMenuConfig

React hook to access menu configuration and filtered menu items.

### Returns

```typescript
interface AppMenuConfigRes {
  items: MenuItem[];
  navItems: MenuItem[];
  cabinetItems: MenuItem[];
  adminItems: MenuItem[];
  profileItems: MenuItem[];
}
```

### Usage

```tsx
const { items, navItems, adminItems } = useAppMenuConfig();
```

**Returns:**
- `items` - All menu items
- `navItems` - Items with type 'nav'
- `cabinetItems` - Items with type 'cabinet'
- `adminItems` - Items with type 'admin'
- `profileItems` - Items with type 'profile'

**Note:** Must be used within an `AppMenuConfig` provider.

## MenuItem

TypeScript interface defining the menu item structure.

```typescript
interface MenuItem {
  type?: string | string[];
  types?: string | string[];
  title: string;
  href?: string;
  icon?: React.ReactNode;
  image?: string;
  parents?: MenuItem[];
  items?: MenuItem[];
  hidden?: boolean;
}
```

### Fields

- `type` - Single type or array of types for filtering (e.g., 'nav', 'admin', 'cabinet', 'profile')
- `types` - Alternative field for type definition
- `title` - Display title of the menu item
- `href` - URL path for the menu item
- `icon` - Optional React node for icon
- `image` - Optional image URL
- `parents` - Optional array of parent menu items (used for breadcrumb generation)
- `items` - Optional array of child menu items (nested structure)
- `hidden` - Optional flag to hide item from display

### Example

```typescript
const menuItem: MenuItem = {
  type: 'nav',
  title: 'Products',
  href: '/products',
  icon: <ProductIcon />,
  items: [
    {
      title: 'Electronics',
      href: '/products/electronics',
      parents: [{ title: 'Products', href: '/products' }],
    },
  ],
};
```

## findBreadcrumbs

Utility function to find breadcrumb path from menu items based on active href.

### Signature

```typescript
function findBreadcrumbs(items: MenuItem[], activeHref: string): MenuItem[]
```

### Parameters

- `items` - Array of menu items to search
- `activeHref` - Current page href to match against

### Returns

Array of menu items representing the breadcrumb path from root to active item.

### Usage

```typescript
import { findBreadcrumbs } from '@rckit/breadcrumbs';

const menuItems = [
  { title: 'Home', href: '/' },
  {
    title: 'Products',
    href: '/products',
    items: [{ title: 'Electronics', href: '/products/electronics' }],
  },
];

const breadcrumbs = findBreadcrumbs(menuItems, '/products/electronics');
// Returns: [{ title: 'Products', href: '/products' }, { title: 'Electronics', href: '/products/electronics' }]
```

**Behavior:**
- Recursively searches through nested menu items
- Returns full path including parents if specified
- Returns empty array if no match is found

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `react-bootstrap` - Bootstrap components for React (peer dependency)
- `@rckit/link` - Link component for navigation
- `@rckit/icons` - Icon components
- `@lsk4/env` - Environment detection utilities

### Menu Structure

Menu items should follow a hierarchical structure with nested `items` arrays:

```typescript
const menuItems: MenuItem[] = [
  {
    title: 'Home',
    href: '/',
  },
  {
    title: 'Products',
    href: '/products',
    items: [
      {
        title: 'Electronics',
        href: '/products/electronics',
        // Optional: explicitly define parents for breadcrumbs
        parents: [{ title: 'Products', href: '/products' }],
      },
    ],
  },
];
```

### Breadcrumb Generation Rules

1. **Automatic Path Detection**: When `activeHref` is provided, the component automatically searches the menu structure to find the matching item and builds the breadcrumb path.

2. **Parent Items**: If a menu item has a `parents` array, those items are included in the breadcrumb path.

3. **Nested Items**: The function recursively searches through nested `items` arrays to find matches.

4. **Display Logic**:
   - Breadcrumbs are shown when there are 2 or more items
   - Title is shown when there's only 1 breadcrumb item, or when explicitly provided
   - Last breadcrumb item is not clickable (represents current page)

### Responsive Behavior

The component includes built-in responsive styles:
- On mobile (max-width: 576px): Some elements can be hidden with `.hide-mobile` class
- On desktop (min-width: 575px): Some elements can be hidden with `.hide-desktop` class

### Custom Styling

The component uses Bootstrap's breadcrumb styles and includes custom CSS for:
- Breadcrumb item spacing
- Divider styling
- Responsive breakpoints

You can override styles using CSS variables:
- `--bs-breadcrumb-item-padding-x` - Horizontal padding for breadcrumb items
- `--bs-breadcrumb-divider-color` - Color for breadcrumb dividers

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
3.  Commit your changes (`git commit -am 'feat(breadcrumbs): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
