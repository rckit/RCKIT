# RCKIT – API Client

> @rckit/api-client – RCKIT – API Client – HTTP client for React applications based on axios

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/api-client)](https://www.npmjs.com/package/@rckit/api-client)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/api-client)](https://www.npmjs.com/package/@rckit/api-client)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/api-client)](https://bundlephobia.com/result?p=@rckit/api-client)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/api-client)](https://www.npmjs.com/package/@rckit/api-client)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/api-client)](https://bundlephobia.com/result?p=@rckit/api-client)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/api-client)](https://bundlephobia.com/result?p=@rckit/api-client)
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
    *   [Creating Custom API Client](#creating-custom-api-client)
    *   [Using Default API Client](#using-default-api-client)
    *   [Making HTTP Requests](#making-http-requests)
    *   [Updating Client Configuration](#updating-client-configuration)
    *   [Error Handling](#error-handling)
    *   [Server-Side Usage](#server-side-usage)
*   [📚 API Reference](#-api-reference)
    *   [createApiClient](#createapiclient)
    *   [apiClient](#apiclient)
    *   [ApiClient](#apiclient-1)
    *   [ApiClientOptions](#apiclientoptions)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/api-client

# yarn
yarn add @rckit/api-client

# npm
npm i @rckit/api-client
```

# 📖 Features

- 🌐 **HTTP client** based on axios with enhanced features
- 🔐 **Automatic credentials** - `withCredentials` enabled by default for cookie-based authentication
- 📝 **Request/Response logging** - automatic logging of requests and responses in debug mode
- 🛡️ **Error handling** - enhanced error handling with structured error codes and messages
- 🔄 **Dynamic configuration** - update client configuration at runtime
- 🖥️ **SSR support** - optimized for server-side rendering with different headers
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🎯 **Simple API** - easy-to-use interface compatible with axios
- 🌲 **Tree-shakeable** - optimized bundle size

# 🚀 Usage

## Basic Setup

Import and use the default API client or create your own:

```tsx
import { apiClient } from '@rckit/api-client';

// Make a GET request
const data = await apiClient.get('/api/users');
```

## Creating Custom API Client

Create a custom API client with a specific base URL:

```tsx
import { createApiClient } from '@rckit/api-client';

const customApiClient = createApiClient({
  baseURL: 'https://api.example.com',
});

// Use the custom client
const users = await customApiClient.get('/users');
```

## Using Default API Client

The package exports a default `apiClient` instance that you can use directly:

```tsx
import apiClient from '@rckit/api-client';
// or
import { apiClient } from '@rckit/api-client';

// GET request
const response = await apiClient.get('/api/data');

// POST request
const result = await apiClient.post('/api/users', {
  name: 'John Doe',
  email: 'john@example.com',
});

// PUT request
await apiClient.put('/api/users/1', { name: 'Jane Doe' });

// DELETE request
await apiClient.delete('/api/users/1');
```

## Making HTTP Requests

The API client supports all standard HTTP methods:

```tsx
import { apiClient } from '@rckit/api-client';

// GET with query parameters
const users = await apiClient.get('/api/users', {
  params: { page: 1, limit: 10 },
});

// POST with data
const newUser = await apiClient.post('/api/users', {
  name: 'John',
  email: 'john@example.com',
});

// PUT request
const updated = await apiClient.put('/api/users/1', {
  name: 'John Updated',
});

// PATCH request
const patched = await apiClient.patch('/api/users/1', {
  email: 'newemail@example.com',
});

// DELETE request
await apiClient.delete('/api/users/1');
```

### Request with AbortSignal

Cancel requests using AbortSignal:

```tsx
import { apiClient } from '@rckit/api-client';

const controller = new AbortController();

// Start request
const promise = apiClient.get('/api/data', {
  signal: controller.signal,
});

// Cancel if needed
controller.abort();
```

## Updating Client Configuration

Update the client configuration dynamically using the `update` method:

```tsx
import { apiClient } from '@rckit/api-client';

// Update base URL
apiClient.update((defaults) => ({
  ...defaults,
  baseURL: 'https://new-api.example.com',
}));

// Update headers
apiClient.update((defaults) => ({
  ...defaults,
  headers: {
    ...defaults.headers,
    Authorization: 'Bearer new-token',
  },
}));

// Update timeout
apiClient.update((defaults) => ({
  ...defaults,
  timeout: 5000,
}));
```

### Updating Authentication Token

```tsx
import { apiClient } from '@rckit/api-client';

function setAuthToken(token: string) {
  apiClient.update((defaults) => ({
    ...defaults,
    headers: {
      ...defaults.headers,
      Authorization: `Bearer ${token}`,
    },
  }));
}

// Use it
setAuthToken('your-jwt-token');
```

## Error Handling

The API client automatically handles errors and throws structured error objects:

```tsx
import { apiClient } from '@rckit/api-client';
import { Err } from '@lsk4/err';

try {
  const data = await apiClient.get('/api/users');
} catch (error) {
  // Error is automatically wrapped in Err
  const code = Err.getCode(error);
  const message = Err.getMessage(error);
  
  console.error('Request failed:', code, message);
  
  if (code === 'ERR_CANCELED') {
    console.log('Request was canceled');
  }
}
```

### Handling Different Error Types

```tsx
import { apiClient } from '@rckit/api-client';
import { Err } from '@lsk4/err';

async function fetchUser(id: string) {
  try {
    return await apiClient.get(`/api/users/${id}`);
  } catch (error) {
    const code = Err.getCode(error);
    
    switch (code) {
      case 'ERR_CANCELED':
        console.log('Request canceled');
        break;
      case 'ERR_NETWORK':
        console.error('Network error');
        break;
      case '404':
        console.error('User not found');
        break;
      default:
        console.error('Unknown error:', Err.getMessage(error));
    }
    
    throw error;
  }
}
```

## Server-Side Usage

When using on the server, you must provide a `baseURL`:

```tsx
import { createApiClient } from '@rckit/api-client';

// Server-side
const serverApiClient = createApiClient({
  baseURL: process.env.API_URL || 'https://api.example.com',
});

// The client will automatically use appropriate headers for server-side requests
const data = await serverApiClient.get('/api/data');
```

**Note:** If `baseURL` is not provided on the server, the client will throw an error to prevent misconfiguration.

# 📚 API Reference

## createApiClient

Function to create a new API client instance.

### Parameters

```typescript
interface CreateApiClientOptions {
  baseURL?: string;
}
```

- `baseURL` (optional) - Base URL for all requests. Required on server-side.

### Returns

Returns an `ApiClient` instance (extends `AxiosInstance`).

### Usage

```tsx
const apiClient = createApiClient({ baseURL: 'https://api.example.com' });
```

**Features:**
- Creates an axios instance with enhanced error handling
- Automatically enables `withCredentials` for cookie-based authentication
- Sets appropriate headers for server-side rendering
- Includes request/response interceptors for logging and error handling
- Provides `update` method for dynamic configuration changes

## apiClient

Default API client instance exported from the package.

### Type

```typescript
const apiClient: ApiClient;
```

### Usage

```tsx
import { apiClient } from '@rckit/api-client';

const data = await apiClient.get('/api/data');
```

**Note:** The default instance is created without a `baseURL`. You should either:
- Use `createApiClient` with a `baseURL` for your use case
- Update the default instance using `apiClient.update()` method

## ApiClient

Extended axios instance interface with additional methods.

### Type

```typescript
interface ApiClient extends AxiosInstance {
  update(cb: (arg: AxiosInstance['defaults']) => AxiosInstance['defaults']): void;
}
```

### Methods

#### update

Updates the client configuration dynamically.

**Parameters:**
- `cb` - Callback function that receives current defaults and returns new defaults

**Returns:** `void`

**Example:**

```tsx
apiClient.update((defaults) => ({
  ...defaults,
  baseURL: 'https://new-api.example.com',
  headers: {
    ...defaults.headers,
    Authorization: 'Bearer token',
  },
}));
```

### Axios Methods

The `ApiClient` extends `AxiosInstance`, so it supports all standard axios methods:

- `get(url, config?)` - GET request
- `post(url, data?, config?)` - POST request
- `put(url, data?, config?)` - PUT request
- `patch(url, data?, config?)` - PATCH request
- `delete(url, config?)` - DELETE request
- `head(url, config?)` - HEAD request
- `options(url, config?)` - OPTIONS request
- `request(config)` - Generic request method

## ApiClientOptions

Options type for API client usage (used in hooks and utilities).

```typescript
interface ApiClientOptions {
  apiClient?: ApiClient;
  signal?: AbortSignal;
  pageParam?: number;
}
```

### Fields

- `apiClient` (optional) - Custom API client instance to use instead of default
- `signal` (optional) - AbortSignal for canceling requests
- `pageParam` (optional) - Page parameter for pagination

# 🔧 Configuration

The package requires the following dependencies:

- `axios` - HTTP client library
- `@lsk4/algos` - Utility functions (for `omitNull`)
- `@lsk4/env` - Environment detection utilities
- `@lsk4/err` - Error handling utilities
- `@lsk4/log` - Logging utilities

### Default Configuration

The API client is created with the following default settings:

- `withCredentials: true` - Enables sending cookies with cross-origin requests
- Server-side headers: `{ Accept: 'application/json', 'Accept-Encoding': 'identity' }`
- Client-side: No special headers by default

### Logging

The client automatically logs requests and responses:

- **Debug mode** (development): Logs all requests and responses at debug/trace level
- **Production mode**: Logs errors only
- Request logging includes: URL, params, and data
- Response logging includes: URL and response data
- Error logging includes: Error code, URL, and error message

### Error Handling

- All errors are automatically wrapped in `Err` from `@lsk4/err`
- Server error responses are extracted from `err.response.data`
- Canceled requests are logged as warnings, not errors
- Error codes are extracted and logged for debugging

### Server-Side Requirements

When using on the server (detected via `@lsk4/env`):

- `baseURL` is **required** - the client will throw an error if not provided
- Special headers are automatically set for server-side requests
- Credentials are still sent by default

### Browser Compatibility

This package uses standard Web APIs and axios, which are supported in all modern browsers. For older browser support, ensure you have appropriate polyfills for:
- `AbortSignal` (for request cancellation)
- `Promise` (for async/await)

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
3.  Commit your changes (`git commit -am 'feat(api-client): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
