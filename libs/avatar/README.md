# RCKIT – Avatar

> @rckit/avatar – RCKIT – Avatar – React avatar component with automatic placeholder generation

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/avatar)](https://www.npmjs.com/package/@rckit/avatar)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/avatar)](https://www.npmjs.com/package/@rckit/avatar)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/avatar)](https://bundlephobia.com/result?p=@rckit/avatar)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/avatar)](https://www.npmjs.com/package/@rckit/avatar)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/avatar)](https://bundlephobia.com/result?p=@rckit/avatar)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/avatar)](https://bundlephobia.com/result?p=@rckit/avatar)
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
    *   [Basic Usage](#basic-usage)
    *   [With Image Source](#with-image-source)
    *   [Without Image (Placeholder)](#without-image-placeholder)
    *   [Custom Sizes](#custom-sizes)
    *   [Square Avatar](#square-avatar)
    *   [Custom Image Component](#custom-image-component)
    *   [Using User Data](#using-user-data)
*   [📚 API Reference](#-api-reference)
    *   [Avatar](#avatar)
    *   [AvatarPlaceholder](#avatarplaceholder)
    *   [AvatarProps](#avatarprops)
    *   [defaultAvatarColors](#defaultavatarcolors)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/avatar

# yarn
yarn add @rckit/avatar

# npm
npm i @rckit/avatar
```

# 📖 Features

- 🖼️ **Image avatar support** - display user avatars from image URLs
- 🎨 **Automatic placeholder generation** - generates colorful placeholders with user initials
- 🎲 **Deterministic colors** - consistent color assignment based on user ID
- 📏 **Flexible sizing** - support for size, height, and width props
- ⭕ **Round/square shapes** - toggle between circular and square avatars
- 🔄 **Fallback handling** - automatic fallback to placeholder when image is missing
- 🎯 **Type-safe** - full TypeScript support with type definitions
- 🌲 **Tree-shakeable** - optimized bundle size
- 🧩 **Customizable** - replace image component with custom implementation

# 🚀 Usage

## Basic Usage

The simplest way to use the Avatar component:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function UserProfile() {
  return (
    <div>
      <Avatar name="John Doe" />
    </div>
  );
}
```

## With Image Source

When you have an image URL, the Avatar component will display it:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function UserProfile() {
  return (
    <div>
      <Avatar 
        src="https://example.com/avatar.jpg" 
        name="John Doe"
        size={64}
      />
    </div>
  );
}
```

**Note:** If the image fails to load or `src` is not provided, the component automatically falls back to a placeholder with user initials.

## Without Image (Placeholder)

When no image source is provided, the Avatar component automatically generates a colorful placeholder with user initials:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function UserList() {
  return (
    <div>
      <Avatar name="John Doe" size={48} />
      <Avatar email="jane@example.com" size={48} />
      <Avatar title="Admin User" size={48} />
    </div>
  );
}
```

The placeholder will:
- Extract initials from `name`, `email`, or `title` props
- Generate a consistent color based on the user's `id` or `_id`
- Display up to 2 initials in uppercase

## Custom Sizes

Control avatar size using `size`, `height`, or `width` props:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function SizesExample() {
  return (
    <div>
      <Avatar name="Small" size={32} />
      <Avatar name="Medium" size={64} />
      <Avatar name="Large" size={128} />
      <Avatar name="Custom" width={100} height={50} />
    </div>
  );
}
```

**Size priority:**
- If `size` is provided, it's used for both width and height
- If `height` or `width` are provided, they override `size`
- Default size is `64px` if none are specified

## Square Avatar

By default, avatars are round. To make them square, set `round={false}`:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function SquareAvatars() {
  return (
    <div>
      <Avatar name="Round" round={true} size={64} />
      <Avatar name="Square" round={false} size={64} />
    </div>
  );
}
```

## Custom Image Component

Replace the default image component using the `as` prop:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';
import { CustomImage } from './CustomImage';

function CustomAvatar() {
  return (
    <Avatar 
      src="https://example.com/avatar.jpg"
      name="John Doe"
      as={CustomImage}
      size={64}
    />
  );
}
```

You can also use native HTML elements:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function NativeAvatar() {
  return (
    <Avatar 
      src="https://example.com/avatar.jpg"
      name="John Doe"
      as="img"
      size={64}
    />
  );
}
```

## Using User Data

The Avatar component can extract user information from various props:

```tsx
import React from 'react';
import { Avatar } from '@rckit/avatar';

function UserCard({ user }) {
  return (
    <div>
      <Avatar 
        src={user.avatarUrl}
        name={user.fullName}
        email={user.email}
        id={user.id}
        size={80}
      />
      <h3>{user.fullName}</h3>
    </div>
  );
}
```

**Initials extraction priority:**
1. `name` - Full name (e.g., "John Doe" → "JD")
2. `email` - Email address (e.g., "john@example.com" → "JE")
3. `title` - Title or display name
4. Falls back to "?" if none are provided

**Color generation:**
- Colors are deterministically generated based on `id` or `_id`
- If no ID is provided, a random ID is generated
- The same ID will always produce the same color combination

# 📚 API Reference

## Avatar

Main avatar component that displays user avatars with automatic placeholder fallback.

### Props

```typescript
interface AvatarProps extends React.ImgHTMLAttributes<HTMLImageElement> {
  as?: React.ElementType | string;
  src?: string;
  id?: string;
  _id?: string;
  title?: string;
  name?: string;
  email?: string;
  size?: number;
  height?: number;
  width?: number;
  round?: boolean;
  children?: React.ReactNode;
}
```

### Usage

```tsx
<Avatar 
  src="https://example.com/avatar.jpg"
  name="John Doe"
  size={64}
/>
```

**Behavior:**
- If `src` is provided, displays the image with placeholder as background
- If `src` is not provided, displays only the placeholder
- Automatically extracts initials from `name`, `email`, or `title`
- Generates consistent colors based on `id` or `_id`
- Supports all standard HTML image attributes

## AvatarPlaceholder

Standalone placeholder component that generates colorful avatars with user initials.

### Props

Same as `AvatarProps` (excluding `src` and `as`).

### Usage

```tsx
import { AvatarPlaceholder } from '@rckit/avatar';

<AvatarPlaceholder 
  name="John Doe"
  size={64}
/>
```

**Features:**
- Generates initials from user data
- Assigns colors based on user ID
- Supports custom styling via `style` prop
- Can be used independently or as fallback

## AvatarProps

TypeScript interface defining all available props for Avatar components.

```typescript
type AvatarProps = React.ImgHTMLAttributes<HTMLImageElement> & {
  as?: React.ElementType | string;
  src?: string;
  id?: string;
  _id?: string;
  title?: string;
  name?: string;
  email?: string;
  size?: number;
  height?: number;
  width?: number;
  round?: boolean;
  children?: React.ReactNode;
};
```

### Props Description

- `as` - Custom component or HTML element to use for image rendering (default: `Image` from `@rckit/link`)
- `src` - Image URL for the avatar
- `id` / `_id` - User identifier for deterministic color generation
- `title` - Display title (used for initials if name/email not available)
- `name` - User's full name (primary source for initials)
- `email` - User's email address (secondary source for initials)
- `size` - Size in pixels (applies to both width and height)
- `height` - Height in pixels (overrides size)
- `width` - Width in pixels (overrides size)
- `round` - Whether to display as circle (default: `true`)
- `children` - Additional content to render inside the avatar container
- All standard HTML image attributes are also supported

## defaultAvatarColors

Array of color combinations used for placeholder generation.

```typescript
const defaultAvatarColors = [
  ['#FF6633', '#FFB399'],  // Orange/Peach
  ['#FF33FF', '#FFFF99'],  // Magenta/Yellow
  ['#00B3E6', '#E6B333'],  // Blue/Gold
  ['#3366E6', '#999966'],  // Blue/Gray
  ['#99FF99', '#B399FF'],  // Green/Purple
];
```

Each entry is a tuple of `[textColor, backgroundColor]`.

**Color Selection:**
- Colors are selected based on the sum of character codes in the user's ID
- The same ID will always produce the same color combination
- If no ID is provided, a random ID is generated

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `@lsk4/algos` - Utility functions (for `omit`)
- `@rckit/link` - Link and Image components (workspace dependency)

### Image Component

By default, the Avatar component uses `Image` from `@rckit/link`. You can replace it using the `as` prop:

```tsx
<Avatar as={CustomImage} src="..." />
```

### Placeholder Generation

The placeholder generation algorithm:

1. **Initials extraction:**
   - Removes non-alphanumeric characters
   - Converts to uppercase
   - Splits by spaces
   - Takes first letter of each word
   - Limits to 2 characters

2. **Color assignment:**
   - Calculates numeric ID from string ID (sum of character codes)
   - Uses modulo operation to select from `defaultAvatarColors` array
   - Ensures consistent color for the same ID

3. **Font size:**
   - Automatically calculated as `height / 2.5`
   - Ensures readable text size for any avatar size

### Styling

The Avatar component uses inline styles for positioning and layout. You can override styles using the `style` prop:

```tsx
<Avatar 
  name="John Doe"
  style={{ border: '2px solid blue' }}
/>
```

### CSS Classes

When `round={true}`, the image component receives the `rounded-circle` class (Bootstrap convention). You may need to ensure this class is available in your CSS framework or define it yourself.

### Browser Compatibility

This package uses standard React and DOM APIs, which are supported in all modern browsers. For older browser support, ensure you have appropriate polyfills for:
- ES6 features (if using older build tools)
- CSS flexbox (for placeholder alignment)

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
3.  Commit your changes (`git commit -am 'feat(avatar): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
