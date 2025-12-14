# RCKIT – Form

> @rckit/form – RCKIT – Form – React form components and hooks built on react-hook-form and react-bootstrap

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/form)](https://www.npmjs.com/package/@rckit/form)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/form)](https://www.npmjs.com/package/@rckit/form)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/form)](https://bundlephobia.com/result?p=@rckit/form)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/form)](https://www.npmjs.com/package/@rckit/form)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/form)](https://bundlephobia.com/result?p=@rckit/form)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/form)](https://bundlephobia.com/result?p=@rckit/form)
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
    *   [Basic Form Setup](#basic-form-setup)
    *   [Using useSmartForm Hook](#using-usesmartform-hook)
    *   [Form Components](#form-components)
    *   [FormButton Component](#formbutton-component)
    *   [FormError Component](#formerror-component)
    *   [FormItem Component](#formitem-component)
    *   [Complete Form Example](#complete-form-example)
*   [📚 API Reference](#-api-reference)
    *   [useSmartForm](#usesmartform)
    *   [FormButton](#formbutton)
    *   [FormError](#formerror)
    *   [FormItem](#formitem)
    *   [useFormButtonState](#useformbuttonstate)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/form

# yarn
yarn add @rckit/form

# npm
npm i @rckit/form
```

# 📖 Features

- 🎯 **Smart form handling** - Enhanced react-hook-form with automatic error handling
- 🚀 **Async submission** - Built-in support for async form submission with error catching
- 🎨 **Bootstrap integration** - Seamless integration with react-bootstrap components
- 🔘 **Smart button states** - FormButton automatically shows progress, error, and success states
- ⚠️ **Error display** - FormError component for displaying form and field errors
- 📦 **Type-safe** - Full TypeScript support with type definitions
- 🎯 **Simple API** - Easy-to-use components and hooks
- 🌲 **Tree-shakeable** - Optimized bundle size

# 🚀 Usage

## Basic Form Setup

Create a form using `useSmartForm` hook and form components:

```tsx
import React from 'react';
import { Form } from 'react-bootstrap';
import { useSmartForm, FormButton, FormError, FormItem } from '@rckit/form';

interface FormData {
  email: string;
  password: string;
}

function LoginForm() {
  const { register, onSmartSubmit, formState } = useSmartForm<FormData>({
    onSubmit: async (values) => {
      // Your async submission logic
      await loginUser(values);
    },
  });

  return (
    <Form onSubmit={onSmartSubmit}>
      <FormItem id="email" label="Email" required>
        <Form.Control {...register('email', { required: true })} type="email" />
      </FormItem>
      
      <FormItem id="password" label="Password" required>
        <Form.Control {...register('password', { required: true })} type="password" />
      </FormItem>
      
      <FormError formState={formState} />
      <FormButton formState={formState}>Login</FormButton>
    </Form>
  );
}
```

## Using useSmartForm Hook

The `useSmartForm` hook extends `react-hook-form`'s `useForm` with automatic error handling:

```tsx
import { useSmartForm } from '@rckit/form';

function MyForm() {
  const { register, onSmartSubmit, formState } = useSmartForm({
    onSubmit: async (values) => {
      // This will automatically catch errors and set them in formState
      await submitForm(values);
    },
    defaultValues: {
      name: '',
      email: '',
    },
  });

  return (
    <form onSubmit={onSmartSubmit}>
      {/* Your form fields */}
    </form>
  );
}
```

### Error Handling

Errors thrown in `onSubmit` are automatically caught and displayed:

```tsx
const { onSmartSubmit, formState } = useSmartForm({
  onSubmit: async (values) => {
    try {
      const response = await fetch('/api/submit', {
        method: 'POST',
        body: JSON.stringify(values),
      });
      
      if (!response.ok) {
        throw new Error('Submission failed');
      }
    } catch (error) {
      // Error is automatically caught and set to formState.errors.root
      throw error;
    }
  },
});
```

## Form Components

### FormButton Component

`FormButton` automatically displays different states based on form submission status:

```tsx
import { FormButton } from '@rckit/form';

function MyForm() {
  const { formState } = useSmartForm({ /* ... */ });

  return (
    <FormButton formState={formState}>
      Submit Form
    </FormButton>
  );
}
```

**Button States:**
- **Default**: Shows "Submit" text with primary variant
- **Progress**: Shows "Submitting..." text, button is disabled
- **Error**: Shows "Error" text with danger variant (auto-resets after 2 seconds)
- **Success**: Shows "Success" text with success variant (auto-resets after 2 seconds)

### FormError Component

Display form errors using the `FormError` component:

```tsx
import { FormError } from '@rckit/form';

function MyForm() {
  const { formState } = useSmartForm({ /* ... */ });

  return (
    <>
      {/* Display root-level errors */}
      <FormError formState={formState} />
      
      {/* Display field-specific errors */}
      <FormError formState={formState} name="email" />
    </>
  );
}
```

### FormItem Component

Wrap form fields with `FormItem` for consistent styling and error display:

```tsx
import { FormItem } from '@rckit/form';
import { Form } from 'react-bootstrap';

function MyForm() {
  const { register, formState } = useSmartForm({ /* ... */ });

  return (
    <FormItem
      id="email"
      label="Email Address"
      description="Enter your email address"
      required
      error={formState.errors.email?.message}
    >
      <Form.Control
        {...register('email', { required: 'Email is required' })}
        type="email"
      />
    </FormItem>
  );
}
```

## Complete Form Example

Here's a complete example combining all components:

```tsx
import React from 'react';
import { Form } from 'react-bootstrap';
import { useSmartForm, FormButton, FormError, FormItem } from '@rckit/form';

interface ContactFormData {
  name: string;
  email: string;
  message: string;
}

function ContactForm() {
  const { register, onSmartSubmit, formState } = useSmartForm<ContactFormData>({
    onSubmit: async (values) => {
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(values),
      });
      
      if (!response.ok) {
        throw new Error('Failed to send message');
      }
      
      alert('Message sent successfully!');
    },
    defaultValues: {
      name: '',
      email: '',
      message: '',
    },
  });

  return (
    <Form onSubmit={onSmartSubmit}>
      <FormItem
        id="name"
        label="Name"
        required
        error={formState.errors.name?.message}
      >
        <Form.Control
          {...register('name', { required: 'Name is required' })}
          type="text"
        />
      </FormItem>

      <FormItem
        id="email"
        label="Email"
        required
        error={formState.errors.email?.message}
      >
        <Form.Control
          {...register('email', {
            required: 'Email is required',
            pattern: {
              value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i,
              message: 'Invalid email address',
            },
          })}
          type="email"
        />
      </FormItem>

      <FormItem
        id="message"
        label="Message"
        description="Enter your message here"
        required
        error={formState.errors.message?.message}
      >
        <Form.Control
          {...register('message', {
            required: 'Message is required',
            minLength: {
              value: 10,
              message: 'Message must be at least 10 characters',
            },
          })}
          as="textarea"
          rows={5}
        />
      </FormItem>

      <FormError formState={formState} />
      <FormButton formState={formState}>Send Message</FormButton>
    </Form>
  );
}
```

# 📚 API Reference

## useSmartForm

Enhanced form hook that wraps `react-hook-form`'s `useForm` with automatic error handling.

### Type

```typescript
function useSmartForm<T extends FieldValues>({
  onSubmit: (values: T) => Promise<any>;
  ...useFormProps: UseFormProps<T>;
}): UseFormReturn<T> & {
  onSmartSubmit: (e?: React.BaseSyntheticEvent) => Promise<void>;
}
```

### Parameters

- `onSubmit` - Async function that handles form submission. Errors thrown will be automatically caught and set to `formState.errors.root`
- `...useFormProps` - All props from `react-hook-form`'s `useForm` hook (e.g., `defaultValues`, `mode`, `resolver`, etc.)

### Returns

Returns all properties from `react-hook-form`'s `useForm` hook plus:

- `onSmartSubmit` - Enhanced submit handler that wraps `handleSubmit` with automatic error catching

### Usage

```tsx
const {
  register,
  handleSubmit,
  formState,
  setError,
  clearErrors,
  onSmartSubmit,
  ...other
} = useSmartForm({
  onSubmit: async (values) => {
    await submitForm(values);
  },
});
```

**Features:**
- Automatically catches errors from `onSubmit` and sets them to `formState.errors.root`
- Prevents multiple simultaneous submissions (`isSubmitting` check)
- Clears errors before each submission attempt
- Logs errors using `@lsk4/log`

## FormButton

Button component that automatically displays form submission states.

### Props

```typescript
interface FormButtonProps extends React.ComponentProps<typeof ReactBootstrapButton> {
  formState: FormState<any>;
  children?: React.ReactNode;
}
```

### Usage

```tsx
<FormButton formState={formState}>Submit</FormButton>
```

**Behavior:**
- **Default state**: Shows children or "Submit" text, primary variant
- **Progress state**: Shows "Submitting..." text, button disabled (when `formState.isSubmitting` is true)
- **Error state**: Shows "Error" text, danger variant (when form has errors after submission, auto-resets after 2 seconds)
- **Success state**: Shows "Success" text, success variant (when `formState.isSubmitSuccessful` is true, auto-resets after 2 seconds)

## FormError

Component for displaying form errors.

### Props

```typescript
interface FormErrorProps {
  formState: FormState<any>;
  name?: string; // Default: 'root'
}
```

### Usage

```tsx
// Display root-level errors
<FormError formState={formState} />

// Display field-specific errors
<FormError formState={formState} name="email" />
```

**Features:**
- Displays error message from `formState.errors[name]?.message`
- Shows empty line (`<br />`) if no error exists
- Styled with Bootstrap danger text classes

## FormItem

Wrapper component for form fields with label, description, and error display.

### Props

```typescript
interface FormItemProps {
  id: string;
  label?: string | ReactNode;
  description?: string | ReactNode | number;
  required?: boolean;
  error?: string | ReactNode | number;
  children: React.ReactNode;
}
```

### Usage

```tsx
<FormItem
  id="email"
  label="Email Address"
  description="Enter your email"
  required
  error={formState.errors.email?.message}
>
  <Form.Control {...register('email')} />
</FormItem>
```

**Features:**
- Wraps field in `Form.Group` from react-bootstrap
- Displays label with required indicator (red asterisk)
- Shows description text if provided
- Displays error message below the field
- Provides `form-control-wrap` div for field styling

## useFormButtonState

Hook that determines button state based on form state.

### Type

```typescript
function useFormButtonState(
  formState: FormState<any>,
  options?: { timeout?: number } // Default: 2000ms
): 'success' | 'error' | 'progress' | null
```

### Parameters

- `formState` - Form state from `react-hook-form`
- `options.timeout` - Timeout in milliseconds for auto-resetting success/error states (default: 2000)

### Returns

Returns the current button state:
- `'progress'` - When form is submitting
- `'error'` - When form has errors after submission
- `'success'` - When form submission was successful
- `null` - Default state

### Usage

```tsx
const buttonStatus = useFormButtonState(formState, { timeout: 3000 });
```

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `react-bootstrap` - Bootstrap components for React (peer dependency)
- `react-hook-form` - Form state management library (peer dependency)
- `@lsk4/env` - Environment detection utilities
- `@lsk4/err` - Error handling utilities
- `@lsk4/log` - Logging utilities

### Error Handling

Errors thrown in the `onSubmit` function are automatically:
- Caught and logged using `@lsk4/log`
- Converted to error messages using `Err.getMessage()`
- Set to `formState.errors.root.message`
- Displayed when using `<FormError formState={formState} />`

### Button State Timeout

Success and error states in `FormButton` automatically reset to default after 2 seconds. This timeout can be customized by using `useFormButtonState` directly:

```tsx
const buttonStatus = useFormButtonState(formState, { timeout: 5000 });
```

### Form Validation

This package uses `react-hook-form` for validation. All validation rules and options from `react-hook-form` are supported:

```tsx
register('email', {
  required: 'Email is required',
  pattern: {
    value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i,
    message: 'Invalid email address',
  },
  minLength: {
    value: 5,
    message: 'Email must be at least 5 characters',
  },
});
```

### Integration with react-bootstrap

All components are designed to work seamlessly with `react-bootstrap`:
- `FormButton` uses `react-bootstrap`'s `Button` component
- `FormItem` uses `react-bootstrap`'s `Form.Group`, `Form.Label`, and `Form.Text` components
- Form controls should use `react-bootstrap`'s `Form.Control` component

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
3.  Commit your changes (`git commit -am 'feat(form): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
