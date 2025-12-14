# RCKIT – Icons

> @rckit/icons – RCKIT – Icons – React icon components library based on react-icons

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/icons)](https://www.npmjs.com/package/@rckit/icons)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/icons)](https://www.npmjs.com/package/@rckit/icons)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/icons)](https://bundlephobia.com/result?p=@rckit/icons)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/icons)](https://www.npmjs.com/package/@rckit/icons)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/icons)](https://bundlephobia.com/result?p=@rckit/icons)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/icons)](https://bundlephobia.com/result?p=@rckit/icons)
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
    *   [Using Icons in Components](#using-icons-in-components)
    *   [Icon Props](#icon-props)
    *   [Styling Icons](#styling-icons)
    *   [Available Icon Categories](#available-icon-categories)
*   [📚 API Reference](#-api-reference)
    *   [UI Icons](#ui-icons)
    *   [Social Media Icons](#social-media-icons)
    *   [Brand Icons](#brand-icons)
    *   [Icon Component Props](#icon-component-props)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/icons

# yarn
yarn add @rckit/icons

# npm
npm i @rckit/icons
```

# 📖 Features

- 🎨 **Comprehensive icon library** - 80+ pre-configured React icon components
- 📦 **Based on react-icons** - built on top of the popular react-icons library
- 🎯 **Simple API** - clean, consistent naming convention for all icons
- 🌲 **Tree-shakeable** - import only the icons you need
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🎨 **Customizable** - all icons accept standard React props (size, color, className, etc.)
- 🔄 **Consistent naming** - predictable PascalCase component names
- 🚀 **Zero configuration** - works out of the box

# 🚀 Usage

## Basic Usage

Import and use icons directly in your components:

```tsx
import React from 'react';
import { Alert, Check, Search, Plus } from '@rckit/icons';

function MyComponent() {
  return (
    <div>
      <Alert size={24} />
      <Check size={24} color="green" />
      <Search size={20} />
      <Plus size={16} />
    </div>
  );
}
```

## Using Icons in Components

Icons are React components that can be used anywhere in your JSX:

```tsx
import React from 'react';
import { Bell, BellFill, BellSlash } from '@rckit/icons';

function NotificationButton({ hasNotifications, isMuted, onClick }) {
  const Icon = isMuted ? BellSlash : hasNotifications ? BellFill : Bell;
  
  return (
    <button onClick={onClick}>
      <Icon size={20} />
      Notifications
    </button>
  );
}
```

## Icon Props

All icons accept standard React component props, including:

- `size` - Icon size (number, in pixels)
- `color` - Icon color (string, CSS color value)
- `className` - CSS class name
- `style` - Inline styles object
- All other standard HTML/SVG attributes

```tsx
import React from 'react';
import { Gear, Moon, Sun } from '@rckit/icons';

function SettingsIcon({ theme }) {
  return (
    <Gear 
      size={24} 
      color={theme === 'dark' ? '#fff' : '#000'}
      className="settings-icon"
      style={{ marginRight: 8 }}
    />
  );
}

function ThemeToggle({ theme, onToggle }) {
  const Icon = theme === 'dark' ? Sun : Moon;
  
  return (
    <button onClick={onToggle}>
      <Icon size={20} />
      Switch to {theme === 'dark' ? 'light' : 'dark'} mode
    </button>
  );
}
```

## Styling Icons

Icons can be styled using CSS classes or inline styles:

```tsx
import React from 'react';
import { Trash, Pencil, Copy } from '@rckit/icons';
import './ActionButtons.css';

function ActionButtons() {
  return (
    <div className="action-buttons">
      <button className="btn-icon">
        <Pencil size={16} className="icon-edit" />
        Edit
      </button>
      <button className="btn-icon">
        <Copy size={16} className="icon-copy" />
        Copy
      </button>
      <button className="btn-icon btn-icon--danger">
        <Trash size={16} className="icon-delete" />
        Delete
      </button>
    </div>
  );
}
```

### CSS Example

```css
.btn-icon {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
}

.icon-edit {
  color: #0066cc;
}

.icon-copy {
  color: #666;
}

.icon-delete {
  color: #dc3545;
}

.btn-icon--danger .icon-delete {
  color: #fff;
}
```

## Available Icon Categories

The library includes icons organized into several categories:

- **UI Icons** - Common interface elements (arrows, check, cross, etc.)
- **Social Media** - Social platform icons (Twitter, Instagram, Telegram, etc.)
- **Brand Icons** - Company and product logos (Apple, Google Play, etc.)
- **Action Icons** - User actions (edit, delete, copy, etc.)
- **Status Icons** - Status indicators (alert, info, check, etc.)

# 📚 API Reference

## UI Icons

Common user interface icons:

```tsx
import {
  Alert,
  AlertFill,
  ArrowDown,
  ArrowLeft,
  ArrowRight,
  ArrowUp,
  Bell,
  BellFill,
  BellSlash,
  Blocked,
  Bot,
  Calendar,
  Check,
  Clock,
  ClockFill,
  Code,
  Comments,
  Copy,
  Cross,
  CrossCircle,
  Dot,
  Dots,
  Duplicate,
  Eye,
  EyeClosed,
  FileMedia,
  Filter,
  Flame,
  Gear,
  Grabber,
  Graph,
  Hourglass,
  Image,
  Info,
  Iterations,
  Key,
  Lab,
  Moon,
  Note,
  Paperclip,
  Paste,
  Pencil,
  People,
  Person,
  Plug,
  Plus,
  Refresh,
  Ruby,
  Search,
  Send,
  Share,
  SidebarCollapse,
  SidebarExpand,
  Skip,
  SortAsc,
  SortDesc,
  Stopwatch,
  Sun,
  Tag,
  Terminal,
  Tools,
  Trash,
} from '@rckit/icons';
```

## Social Media Icons

Social media platform icons with both outline and filled variants:

```tsx
import {
  // Telegram
  Telegram,
  TelegramFill,
  
  // YouTube
  YouTube,
  YouTubeFill,
  
  // Instagram
  Instagram,
  InstagramFill,
  
  // Twitter
  Twitter,
  TwitterFill,
  
  // TikTok
  TikTok,
  TikTokFill,
  
  // Discord
  Discord,
  DiscordFill,
  
  // WhatsApp
  WhatsApp,
  WhatsAppFill,
  
  // Twitch
  Twitch,
  TwitchFill,
  
  // Slack
  Slack,
  SlackFill,
} from '@rckit/icons';
```

## Brand Icons

Brand and product logos:

```tsx
import {
  // Apple
  Apple,
  AppleFill,
  AppStore,
  AppStoreFill,
  
  // Google Play
  GooglePlay,
  GooglePlayFill,
} from '@rckit/icons';
```

## Icon Component Props

All icon components accept the following props (inherited from react-icons):

```typescript
interface IconProps {
  size?: string | number;        // Icon size (default: '1em')
  color?: string;                // Icon color (default: 'currentColor')
  className?: string;             // CSS class name
  style?: React.CSSProperties;    // Inline styles
  title?: string;                 // Accessibility title
  // ... all other standard SVG/HTML attributes
}
```

### Example with All Props

```tsx
import React from 'react';
import { Search } from '@rckit/icons';

function SearchIcon() {
  return (
    <Search
      size={24}
      color="#333"
      className="search-icon"
      style={{ marginRight: 8 }}
      title="Search"
      aria-label="Search icon"
    />
  );
}
```

# 🔧 Configuration

The package is built on top of [react-icons](https://react-icons.github.io/react-icons/), which provides access to thousands of icons from popular icon libraries.

### Dependencies

- `react` - React library (peer dependency)
- `react-icons` - Icon library (dev dependency, bundled in the package)

### Icon Sources

Icons are sourced from various icon libraries via react-icons:
- **Go** (Github Octicons) - UI icons
- **Pi** (Phosphor Icons) - Modern interface icons
- And other icon sets available in react-icons

### Tree Shaking

The package supports tree shaking, so you can import only the icons you need:

```tsx
// ✅ Good - only imports what you need
import { Search, Check } from '@rckit/icons';

// ❌ Avoid - imports everything
import * as Icons from '@rckit/icons';
```

### Bundle Size

The package is optimized for minimal bundle size. Each icon is individually exportable, allowing bundlers to include only the icons you actually use in your application.

### Browser Compatibility

Icons are rendered as SVG elements, which are supported in all modern browsers. For older browser support, ensure you have appropriate polyfills.

### TypeScript Support

Full TypeScript support is included. All icons are properly typed and will provide IntelliSense in your IDE.

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
3.  Commit your changes (`git commit -am 'feat(icons): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
