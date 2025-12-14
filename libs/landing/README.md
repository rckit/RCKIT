# RCKIT – Landing

> @rckit/landing – RCKIT – Landing – React components for building landing page sections

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/landing)](https://www.npmjs.com/package/@rckit/landing)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/landing)](https://www.npmjs.com/package/@rckit/landing)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/landing)](https://bundlephobia.com/result?p=@rckit/landing)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/landing)](https://www.npmjs.com/package/@rckit/landing)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/landing)](https://bundlephobia.com/result?p=@rckit/landing)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/landing)](https://bundlephobia.com/result?p=@rckit/landing)
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
    *   [With Background Image](#with-background-image)
    *   [Full Height Section](#full-height-section)
    *   [Top Section](#top-section)
    *   [Using Container](#using-container)
    *   [Complete Landing Page Example](#complete-landing-page-example)
*   [📚 API Reference](#-api-reference)
    *   [LandingSection](#landingsection)
    *   [LandingSectionContainer](#landingsectioncontainer)
    *   [LandingSectionProps](#landingsectionprops)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/landing

# yarn
yarn add @rckit/landing

# npm
npm i @rckit/landing
```

# 📖 Features

- 🎨 **Landing page sections** - ready-to-use section components for landing pages
- 🖼️ **Background images** - support for background images with overlay effects
- 📐 **Bootstrap integration** - built on react-bootstrap for responsive layouts
- 🎯 **Flexible layout** - full-height sections, top sections, and custom containers
- 🎭 **Decorative elements** - built-in decorative triangles and overlays
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🌲 **Tree-shakeable** - optimized bundle size

# 🚀 Usage

## Basic Usage

Create a simple landing section:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function MyLanding() {
  return (
    <LandingSection>
      <h1>Welcome to Our Landing Page</h1>
      <p>This is a beautiful landing section</p>
    </LandingSection>
  );
}
```

## With Background Image

Add a background image to your section:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function HeroSection() {
  return (
    <LandingSection backgroundImage="/images/hero-bg.jpg">
      <h1>Hero Section</h1>
      <p>With beautiful background image</p>
    </LandingSection>
  );
}
```

## Full Height Section

Create a full-height section:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function FullHeightHero() {
  return (
    <LandingSection full>
      <h1>Full Height Section</h1>
      <p>This section takes the full viewport height</p>
    </LandingSection>
  );
}
```

## Top Section

Add top padding/margin to a section:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function TopSection() {
  return (
    <LandingSection top>
      <h1>Top Section</h1>
      <p>This section has top spacing</p>
    </LandingSection>
  );
}
```

## Using Container

Use the built-in container component for centered content:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function CenteredSection() {
  return (
    <LandingSection>
      <LandingSection.Container>
        <h1>Centered Content</h1>
        <p>This content is centered using Bootstrap grid</p>
      </LandingSection.Container>
    </LandingSection>
  );
}
```

## Complete Landing Page Example

Build a complete landing page with multiple sections:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function LandingPage() {
  return (
    <>
      {/* Hero Section */}
      <LandingSection full backgroundImage="/images/hero.jpg">
        <LandingSection.Container>
          <h1>Welcome to Our Product</h1>
          <p>Amazing features await you</p>
          <button>Get Started</button>
        </LandingSection.Container>
      </LandingSection>

      {/* Features Section */}
      <LandingSection top>
        <LandingSection.Container>
          <h2>Features</h2>
          <div>
            <h3>Feature 1</h3>
            <p>Description of feature 1</p>
          </div>
          <div>
            <h3>Feature 2</h3>
            <p>Description of feature 2</p>
          </div>
        </LandingSection.Container>
      </LandingSection>

      {/* CTA Section */}
      <LandingSection backgroundImage="/images/cta-bg.jpg">
        <LandingSection.Container>
          <h2>Ready to Get Started?</h2>
          <button>Sign Up Now</button>
        </LandingSection.Container>
      </LandingSection>
    </>
  );
}
```

### Combining Props

You can combine multiple props for more complex layouts:

```tsx
import React from 'react';
import { LandingSection } from '@rckit/landing';

function ComplexSection() {
  return (
    <LandingSection 
      full 
      top 
      backgroundImage="/images/complex-bg.jpg"
      className="custom-section"
    >
      <LandingSection.Container>
        <h1>Complex Section</h1>
        <p>Full height, top spacing, background image, and custom class</p>
      </LandingSection.Container>
    </LandingSection>
  );
}
```

# 📚 API Reference

## LandingSection

Main component for creating landing page sections with decorative elements and background support.

### Props

```typescript
interface LandingSectionProps {
  children?: React.ReactNode;
  full?: boolean;
  top?: boolean;
  className?: string;
  backgroundImage?: string;
}
```

### Props Description

- `children` - React node to render inside the section
- `full` - If `true`, the section will take full viewport height
- `top` - If `true`, adds top spacing to the section
- `className` - Additional CSS classes to apply to the section
- `backgroundImage` - URL of the background image to display

### Usage

```tsx
<LandingSection full top backgroundImage="/bg.jpg" className="my-section">
  <h1>Content</h1>
</LandingSection>
```

**Features:**
- Renders a `<section>` element with decorative elements
- Automatically adds background image with overlay if `backgroundImage` is provided
- Includes decorative triangles at the bottom
- Supports custom className for additional styling
- All standard HTML section attributes are supported via spread props

**Built-in Elements:**
- `bg-cover` - Background image container
- `bg-overlay` - Overlay for background images
- `bg-triangle` - Decorative triangles (left and right)

## LandingSectionContainer

Container component for centering content using Bootstrap grid system.

### Props

```typescript
interface LandingSectionContainerProps {
  children: React.ReactNode;
}
```

### Usage

```tsx
<LandingSection>
  <LandingSection.Container>
    <h1>Centered Content</h1>
  </LandingSection.Container>
</LandingSection>
```

**Features:**
- Uses Bootstrap `Container` and `Row` components
- Centers content with `justify-content-center` and `align-items-center`
- Uses responsive column classes (`col-md-8 col-lg-7`)
- Accessible via `LandingSection.Container` static property

**Note:** This component requires `react-bootstrap` to be installed and properly configured.

## LandingSectionProps

TypeScript type definition for LandingSection component props.

```typescript
type LandingSectionProps = React.PropsWithChildren<{
  full?: boolean;
  top?: boolean;
  className?: string;
  backgroundImage?: string;
}>;
```

### Type Fields

- `full` - Optional boolean for full-height sections
- `top` - Optional boolean for top spacing
- `className` - Optional string for custom CSS classes
- `backgroundImage` - Optional string URL for background image
- `children` - React children (inherited from `React.PropsWithChildren`)

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `react-bootstrap` - Bootstrap components for React (peer dependency)
- `@lsk4/algos` - Utility functions (internal dependency)

### Bootstrap Setup

This package uses `react-bootstrap` components (`Container`, `Row`, `Col`). Make sure you have Bootstrap CSS included in your project:

```tsx
// In your main entry file
import 'bootstrap/dist/css/bootstrap.min.css';
```

### CSS Classes

The component uses the following CSS classes that should be defined in your stylesheet:

- `.section` - Base section styling
- `.section-top` - Top section spacing
- `.section-full` - Full height section
- `.bg-cover` - Background image container
- `.bg-overlay` - Background overlay
- `.bg-triangle` - Decorative triangle base
- `.bg-triangle-light` - Light triangle variant
- `.bg-triangle-bottom` - Triangle at bottom
- `.bg-triangle-left` - Triangle on left
- `.bg-triangle-right` - Triangle on right

### Styling

You can customize the appearance by:

1. Adding custom CSS classes via the `className` prop
2. Overriding the default CSS classes in your stylesheet
3. Using CSS-in-JS solutions to style the components

### Browser Compatibility

This package uses standard React and Bootstrap components, which are supported in all modern browsers. For older browser support, ensure you have appropriate polyfills for:

- CSS Grid (used by Bootstrap)
- Flexbox (used by Bootstrap)
- ES6+ JavaScript features

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
3.  Commit your changes (`git commit -am 'feat(landing): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
