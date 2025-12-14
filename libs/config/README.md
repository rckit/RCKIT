# RCKIT – Config

> @rckit/config – RCKIT – Config – React configuration management with localStorage persistence

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/config)](https://www.npmjs.com/package/@rckit/config)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/config)](https://www.npmjs.com/package/@rckit/config)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/config)](https://bundlephobia.com/result?p=@rckit/config)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/config)](https://www.npmjs.com/package/@rckit/config)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/config)](https://bundlephobia.com/result?p=@rckit/config)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/config)](https://bundlephobia.com/result?p=@rckit/config)
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
    *   [Using AppConfig Provider](#using-appconfig-provider)
    *   [Accessing Configuration](#accessing-configuration)
    *   [Updating Configuration](#updating-configuration)
    *   [Custom Configuration](#custom-configuration)
*   [📚 API Reference](#-api-reference)
    *   [AppConfig](#appconfig)
    *   [useAppConfig](#useappconfig)
    *   [AppConfigType](#appconfigtype)
    *   [defaultAppConfig](#defaultappconfig)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/config

# yarn
yarn add @rckit/config

# npm
npm i @rckit/config
```

# 📖 Features

- ⚙️ **React configuration management** with Context API
- 💾 **localStorage persistence** - configuration persists across page reloads
- 🎨 **Theme support** - built-in light/dark theme management
- 🐛 **Debug mode** - toggle debug mode with automatic dev environment detection
- 🔄 **Reactive updates** - configuration changes trigger component re-renders
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🎯 **Simple API** - easy-to-use hook-based interface
- 🌲 **Tree-shakeable** - optimized bundle size

# 🚀 Usage

## Basic Setup

Wrap your application with the `AppConfig` provider:

```tsx
import React from 'react';
import { AppConfig } from '@rckit/config';

function App() {
  return (
    <AppConfig>
      <YourApp />
    </AppConfig>
  );
}
```

## Using AppConfig Provider

The `AppConfig` component provides configuration context to all child components and automatically persists configuration to localStorage.

```tsx
import React from 'react';
import { AppConfig } from '@rckit/config';

function Root() {
  return (
    <AppConfig>
      <div>
        <Header />
        <Main />
        <Footer />
      </div>
    </AppConfig>
  );
}
```

## Accessing Configuration

Use the `useAppConfig` hook to access and update configuration:

```tsx
import React from 'react';
import { useAppConfig } from '@rckit/config';

function MyComponent() {
  const { isDebug, theme, setAppConfig } = useAppConfig();

  return (
    <div>
      <p>Debug mode: {isDebug ? 'ON' : 'OFF'}</p>
      <p>Current theme: {theme}</p>
    </div>
  );
}
```

## Updating Configuration

Update configuration using the `setAppConfig` function:

```tsx
import React from 'react';
import { useAppConfig } from '@rckit/config';

function ThemeToggle() {
  const { theme, setAppConfig } = useAppConfig();

  const toggleTheme = () => {
    setAppConfig((prev) => ({
      ...prev,
      theme: prev.theme === 'light' ? 'dark' : 'light',
    }));
  };

  return (
    <button onClick={toggleTheme}>
      Switch to {theme === 'light' ? 'dark' : 'light'} mode
    </button>
  );
}
```

### Updating Specific Fields

```tsx
import React from 'react';
import { useAppConfig } from '@rckit/config';

function DebugToggle() {
  const { isDebug, setAppConfig } = useAppConfig();

  const toggleDebug = () => {
    setAppConfig((prev) => ({
      ...prev,
      isDebug: !prev.isDebug,
    }));
  };

  return (
    <button onClick={toggleDebug}>
      {isDebug ? 'Disable' : 'Enable'} Debug Mode
    </button>
  );
}
```

### Updating Multiple Fields

```tsx
import React from 'react';
import { useAppConfig } from '@rckit/config';

function SettingsPanel() {
  const { setAppConfig } = useAppConfig();

  const applySettings = (newTheme: 'light' | 'dark', debug: boolean) => {
    setAppConfig({
      theme: newTheme,
      isDebug: debug,
    });
  };

  return (
    <div>
      <button onClick={() => applySettings('dark', true)}>
        Dark + Debug
      </button>
      <button onClick={() => applySettings('light', false)}>
        Light + No Debug
      </button>
    </div>
  );
}
```

## Custom Configuration

The default configuration includes `isDebug` and `theme` fields. The `isDebug` field automatically defaults to `true` in development environments (detected via `@lsk4/env`).

### Default Configuration

```typescript
{
  isDebug: isDev,  // Automatically true in development
  theme: 'light'
}
```

### Using Configuration in Components

```tsx
import React from 'react';
import { useAppConfig } from '@rckit/config';

function ThemedComponent() {
  const { theme } = useAppConfig();

  return (
    <div className={`app app--${theme}`}>
      <h1>My Application</h1>
      {theme === 'dark' && <p>Dark mode is active</p>}
    </div>
  );
}
```

### Conditional Rendering Based on Config

```tsx
import React from 'react';
import { useAppConfig } from '@rckit/config';

function DebugPanel() {
  const { isDebug } = useAppConfig();

  if (!isDebug) {
    return null;
  }

  return (
    <div className="debug-panel">
      <h2>Debug Information</h2>
      <pre>{JSON.stringify(window.location, null, 2)}</pre>
    </div>
  );
}
```

# 📚 API Reference

## AppConfig

React context provider component that manages application configuration.

### Props

```typescript
interface AppConfigProps {
  children: React.ReactNode;
}
```

### Usage

```tsx
<AppConfig>
  <YourApp />
</AppConfig>
```

**Features:**
- Provides configuration context to all child components
- Persists configuration to localStorage with key `'appConfig'`
- Automatically restores configuration from localStorage on mount
- Updates all consuming components when configuration changes

## useAppConfig

React hook to access and update application configuration.

### Returns

```typescript
interface AppConfigContextProps {
  isDebug: boolean;
  theme: 'light' | 'dark';
  setAppConfig: Dispatch<SetStateAction<AppConfigType>>;
}
```

### Usage

```tsx
const { isDebug, theme, setAppConfig } = useAppConfig();
```

**Returns:**
- `isDebug` - Boolean indicating if debug mode is enabled
- `theme` - Current theme ('light' or 'dark')
- `setAppConfig` - Function to update configuration (supports both direct value and updater function)

**Examples:**

```tsx
// Direct value update
setAppConfig({ isDebug: true, theme: 'dark' });

// Functional update
setAppConfig((prev) => ({ ...prev, theme: 'light' }));
```

**Note:** Must be used within an `AppConfig` provider. Will throw an error if used outside the provider context.

## AppConfigType

TypeScript interface defining the configuration structure.

```typescript
interface AppConfigType {
  isDebug: boolean;
  theme: 'light' | 'dark';
}
```

### Fields

- `isDebug` - Boolean flag for debug mode
- `theme` - Theme preference, either `'light'` or `'dark'`

## defaultAppConfig

Default configuration object used when no stored configuration is found.

```typescript
const defaultAppConfig: AppConfigType = {
  isDebug: isDev,  // From @lsk4/env
  theme: 'light',
};
```

**Behavior:**
- Used as initial value when localStorage is empty
- `isDebug` automatically set based on environment (development vs production)
- `theme` defaults to `'light'`

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `use-local-storage-state` - localStorage state management hook
- `@lsk4/env` - Environment detection utilities

### localStorage Key

Configuration is stored in localStorage under the key: `'appConfig'`

### Environment Detection

The `isDebug` field in the default configuration is automatically set based on the environment:
- **Development**: `isDebug = true` (when `isDev` from `@lsk4/env` is true)
- **Production**: `isDebug = false` (when `isDev` from `@lsk4/env` is false)

### Persistence

- Configuration is automatically saved to localStorage whenever `setAppConfig` is called
- Configuration is automatically restored from localStorage when the `AppConfig` provider mounts
- If no stored configuration exists, the default configuration is used

### Browser Compatibility

This package uses the `localStorage` API, which is supported in all modern browsers. For older browser support, ensure you have appropriate polyfills.

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
3.  Commit your changes (`git commit -am 'feat(config): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
