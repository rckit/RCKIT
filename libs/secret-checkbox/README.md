# RCKIT – Secret Checkbox

> @rckit/secret-checkbox – RCKIT – Secret Checkbox – React checkbox component that requires multiple clicks to toggle

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/secret-checkbox)](https://www.npmjs.com/package/@rckit/secret-checkbox)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/secret-checkbox)](https://www.npmjs.com/package/@rckit/secret-checkbox)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/secret-checkbox)](https://bundlephobia.com/result?p=@rckit/secret-checkbox)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/secret-checkbox)](https://www.npmjs.com/package/@rckit/secret-checkbox)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/secret-checkbox)](https://bundlephobia.com/result?p=@rckit/secret-checkbox)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/secret-checkbox)](https://bundlephobia.com/result?p=@rckit/secret-checkbox)
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
    *   [Custom Click Count](#custom-click-count)
    *   [Controlled Component](#controlled-component)
    *   [Uncontrolled Component](#uncontrolled-component)
    *   [With HTML Attributes](#with-html-attributes)
*   [📚 API Reference](#-api-reference)
    *   [SecretCheckbox](#secretcheckbox)
    *   [SecretCheckboxProps](#secretcheckboxprops)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/secret-checkbox

# yarn
yarn add @rckit/secret-checkbox

# npm
npm i @rckit/secret-checkbox
```

# 📖 Features

- 🔒 **Secret toggle** - requires multiple clicks to change state (prevents accidental toggles)
- 🎯 **Configurable click count** - customize how many clicks are required (default: 5)
- 🎛️ **Controlled & uncontrolled** - supports both controlled and uncontrolled usage patterns
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🎨 **Standard HTML input** - accepts all standard HTML input attributes
- 🌲 **Tree-shakeable** - optimized bundle size
- ⚡ **Lightweight** - minimal dependencies, only React

# 🚀 Usage

## Basic Usage

The simplest way to use `SecretCheckbox` is as an uncontrolled component:

```tsx
import React from 'react';
import { SecretCheckbox } from '@rckit/secret-checkbox';

function MyComponent() {
  const handleChange = (value: boolean) => {
    console.log('Checkbox toggled:', value);
  };

  return (
    <div>
      <label>
        <SecretCheckbox onChange={handleChange} />
        Enable secret feature
      </label>
    </div>
  );
}
```

**Note:** By default, the checkbox requires **5 clicks** before it toggles its state. This prevents accidental changes.

## Custom Click Count

You can customize the number of clicks required using the `count` prop:

```tsx
import React from 'react';
import { SecretCheckbox } from '@rckit/secret-checkbox';

function MyComponent() {
  return (
    <div>
      {/* Requires 3 clicks */}
      <label>
        <SecretCheckbox count={3} />
        Easy toggle (3 clicks)
      </label>

      {/* Requires 10 clicks */}
      <label>
        <SecretCheckbox count={10} />
        Hard toggle (10 clicks)
      </label>
    </div>
  );
}
```

## Controlled Component

Use the `value` prop to control the checkbox state:

```tsx
import React, { useState } from 'react';
import { SecretCheckbox } from '@rckit/secret-checkbox';

function ControlledExample() {
  const [checked, setChecked] = useState(false);

  return (
    <div>
      <label>
        <SecretCheckbox
          value={checked}
          onChange={setChecked}
          count={3}
        />
        Delete all data (requires 3 clicks)
      </label>
      <p>Current state: {checked ? 'Enabled' : 'Disabled'}</p>
    </div>
  );
}
```

## Uncontrolled Component

When used without the `value` prop, the component manages its own state:

```tsx
import React from 'react';
import { SecretCheckbox } from '@rckit/secret-checkbox';

function UncontrolledExample() {
  const handleChange = (value: boolean) => {
    if (value) {
      console.log('Dangerous action enabled!');
    }
  };

  return (
    <label>
      <SecretCheckbox
        onChange={handleChange}
        count={7}
      />
      Enable dangerous mode
    </label>
  );
}
```

## With HTML Attributes

`SecretCheckbox` accepts all standard HTML input attributes:

```tsx
import React from 'react';
import { SecretCheckbox } from '@rckit/secret-checkbox';

function WithAttributes() {
  return (
    <div>
      <label>
        <SecretCheckbox
          id="secret-feature"
          name="secretFeature"
          className="custom-checkbox"
          disabled={false}
          aria-label="Secret feature toggle"
          count={5}
        />
        Secret Feature
      </label>
    </div>
  );
}
```

### Real-world Example: Dangerous Action Confirmation

```tsx
import React, { useState } from 'react';
import { SecretCheckbox } from '@rckit/secret-checkbox';

function DangerousActionForm() {
  const [confirmed, setConfirmed] = useState(false);

  const handleSubmit = () => {
    if (confirmed) {
      // Perform dangerous action
      console.log('Action confirmed and executed');
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          <SecretCheckbox
            value={confirmed}
            onChange={setConfirmed}
            count={7}
          />
          I understand this action cannot be undone (click 7 times)
        </label>
      </div>
      <button type="submit" disabled={!confirmed}>
        Delete Account
      </button>
    </form>
  );
}
```

# 📚 API Reference

## SecretCheckbox

React component that renders a checkbox requiring multiple clicks to toggle.

### Props

```typescript
interface SecretCheckboxProps extends React.HtmlHTMLAttributes<HTMLInputElement> {
  count?: number;
  value?: boolean;
  onChange?: (value: boolean) => void;
}
```

### Props Details

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `count` | `number` | `5` | Number of clicks required before the checkbox toggles |
| `value` | `boolean` | `undefined` | Controlled value. When provided, the component is controlled |
| `onChange` | `(value: boolean) => void` | `undefined` | Callback fired when the checkbox state changes (after required clicks) |
| `...props` | `React.HtmlHTMLAttributes<HTMLInputElement>` | - | All standard HTML input attributes (id, className, disabled, etc.) |

### Behavior

- **Click counting**: The component counts clicks internally. Only after the required number of clicks (specified by `count`) is reached, the checkbox state changes.
- **State reset**: If the `value` prop changes externally (in controlled mode), the click counter resets to 0.
- **Uncontrolled mode**: When `value` is not provided, the component manages its own internal state.
- **Controlled mode**: When `value` is provided, the component is fully controlled and the click counter resets when `value` changes.

### Usage

```tsx
// Uncontrolled
<SecretCheckbox onChange={(value) => console.log(value)} />

// Controlled
<SecretCheckbox value={checked} onChange={setChecked} />

// Custom click count
<SecretCheckbox count={10} onChange={handleChange} />

// With HTML attributes
<SecretCheckbox
  id="my-checkbox"
  className="custom-class"
  disabled={false}
  count={5}
  onChange={handleChange}
/>
```

## SecretCheckboxProps

TypeScript interface for the component props.

```typescript
type SecretCheckboxProps = React.HtmlHTMLAttributes<HTMLInputElement> & {
  count?: number;
  value?: boolean;
  onChange?: (value: boolean) => void;
};
```

**Extends:** `React.HtmlHTMLAttributes<HTMLInputElement>` - All standard HTML input element attributes are supported.

# 🔧 Configuration

## Dependencies

The package requires the following dependencies:

- `react` - React library (peer dependency)

## Default Behavior

- **Default click count**: `5` clicks are required by default
- **Initial state**: When used uncontrolled, the checkbox starts as `unchecked` (false)
- **State persistence**: The component does not persist state across page reloads. Use external state management if persistence is needed.

## Click Counter Reset

The click counter automatically resets in the following scenarios:

1. **After successful toggle**: Once the required number of clicks is reached and the checkbox toggles, the counter resets to 0
2. **On value prop change**: In controlled mode, when the `value` prop changes externally, the counter resets to 0
3. **On component remount**: If the component unmounts and remounts, the counter resets

## Browser Compatibility

This package uses standard React features and HTML input elements, which are supported in all modern browsers that support React.

## Performance Considerations

- The component uses React hooks (`useState`, `useEffect`) for state management
- Click counting is handled internally with minimal overhead
- The component re-renders only when the internal state changes or when props change

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
3.  Commit your changes (`git commit -am 'feat(secret-checkbox): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
