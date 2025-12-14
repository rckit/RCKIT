# RCKIT – Auth

> @rckit/auth – RCKIT – Auth – React authentication management with session persistence

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/auth)](https://www.npmjs.com/package/@rckit/auth)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/auth)](https://www.npmjs.com/package/@rckit/auth)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/auth)](https://bundlephobia.com/result?p=@rckit/auth)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/auth)](https://www.npmjs.com/package/@rckit/auth)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/auth)](https://bundlephobia.com/result?p=@rckit/auth)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/auth)](https://bundlephobia.com/result?p=@rckit/auth)
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
    *   [Using AppSession Provider](#using-appsession-provider)
    *   [Accessing Session](#accessing-session)
    *   [Accessing User](#accessing-user)
    *   [Updating Session](#updating-session)
    *   [Logging Out](#logging-out)
    *   [Route Protection](#route-protection)
    *   [Authentication Forms](#authentication-forms)
    *   [Authentication Queries](#authentication-queries)
*   [📚 API Reference](#-api-reference)
    *   [AppSession](#appsession)
    *   [useAppSession](#useappsession)
    *   [useAppUser](#useappuser)
    *   [useAuthGuard](#useauthguard)
    *   [Authentication Forms](#authentication-forms-1)
    *   [Authentication Queries](#authentication-queries-1)
    *   [Types](#types)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/auth

# yarn
yarn add @rckit/auth

# npm
npm i @rckit/auth
```

# 📖 Features

- 🔐 **React authentication management** with Context API
- 💾 **localStorage persistence** - session persists across page reloads
- 🔄 **Automatic session refresh** - session automatically refreshes when expired
- 🛡️ **Route protection** - built-in guard hooks for role-based access control
- 📝 **Ready-to-use forms** - pre-built authentication forms (login, signup, OTP, etc.)
- 🌐 **API integration** - complete set of authentication query functions
- 👤 **User management** - easy access to current user and session data
- 📦 **Type-safe** - full TypeScript support with type definitions
- 🎯 **Simple API** - easy-to-use hook-based interface
- 🌲 **Tree-shakeable** - optimized bundle size

# 🚀 Usage

## Basic Setup

Wrap your application with the `AppSession` provider:

```tsx
import React from 'react';
import { AppSession } from '@rckit/auth';

function App() {
  return (
    <AppSession>
      <YourApp />
    </AppSession>
  );
}
```

## Using AppSession Provider

The `AppSession` component provides authentication context to all child components and automatically manages session state with localStorage persistence.

```tsx
import React from 'react';
import { AppSession } from '@rckit/auth';

function Root() {
  return (
    <AppSession>
      <div>
        <Header />
        <Main />
        <Footer />
      </div>
    </AppSession>
  );
}
```

**Features:**
- Automatically fetches session on mount
- Persists session to localStorage with key `'appSession'`
- Automatically refreshes session when expired
- Shows loading screen during session operations
- Updates all consuming components when session changes

## Accessing Session

Use the `useAppSession` hook to access session data and methods:

```tsx
import React from 'react';
import { useAppSession } from '@rckit/auth';

function MyComponent() {
  const { session, sessionStatus, updateSession, clearSession } = useAppSession();

  return (
    <div>
      <p>Session status: {sessionStatus}</p>
      {session?.user && (
        <p>Logged in as: {session.user.email}</p>
      )}
    </div>
  );
}
```

## Accessing User

Use the `useAppUser` hook to access current user information:

```tsx
import React from 'react';
import { useAppUser } from '@rckit/auth';

function UserProfile() {
  const user = useAppUser();

  if (!user) {
    return <div>Not logged in</div>;
  }

  return (
    <div>
      <h1>{user.title}</h1>
      <p>Email: {user.email}</p>
      <p>Role: {user.role}</p>
      {user.isAdmin && <p>Admin privileges</p>}
    </div>
  );
}
```

## Updating Session

Update session using the `updateSession` function:

```tsx
import React from 'react';
import { useAppSession } from '@rckit/auth';
import { fetchAuthLogin } from '@rckit/auth';

function LoginButton() {
  const { updateSession } = useAppSession();

  const handleLogin = async () => {
    try {
      const { session } = await fetchAuthLogin({
        email: 'user@example.com',
        password: 'password123',
      });
      updateSession(session);
    } catch (error) {
      console.error('Login failed:', error);
    }
  };

  return <button onClick={handleLogin}>Login</button>;
}
```

### Updating Session with Redirect

Use `updateSessionWithRedirect` to update session and redirect to a specific path:

```tsx
import React from 'react';
import { useAppSession } from '@rckit/auth';
import { useRouter } from 'next/router';

function LoginHandler() {
  const { updateSessionWithRedirect } = useAppSession();
  const router = useRouter();

  const handleLogin = async (session) => {
    await updateSessionWithRedirect(session, router, '/dashboard');
  };

  return <button onClick={handleLogin}>Login and Redirect</button>;
}
```

## Logging Out

Clear session using the `clearSession` function:

```tsx
import React from 'react';
import { useAppSession } from '@rckit/auth';

function LogoutButton() {
  const { clearSession } = useAppSession();

  const handleLogout = async () => {
    await clearSession();
  };

  return <button onClick={handleLogout}>Logout</button>;
}
```

## Route Protection

Use the `useAuthGuard` hook to protect routes based on user roles:

```tsx
import React, { useEffect } from 'react';
import { useAuthGuard } from '@rckit/auth';
import { useRouter } from 'next/router';

function AdminPage() {
  const router = useRouter();
  const redirectUrl = useAuthGuard(router, { role: 'admin' });

  if (redirectUrl) {
    return null; // Redirecting...
  }

  return <div>Admin content</div>;
}
```

### Available Role Options

- `'user'` - Requires user or admin role (default)
- `'admin'` - Requires admin role only
- `'guestOnly'` - Requires user to be logged out

### Custom Redirect

```tsx
import { useAuthGuard } from '@rckit/auth';

function ProtectedPage() {
  const router = useRouter();
  useAuthGuard(router, {
    role: 'user',
    redirect: '/custom-login',
  });

  return <div>Protected content</div>;
}
```

## Authentication Forms

The package provides ready-to-use authentication forms:

### Login Form

```tsx
import React from 'react';
import { AuthLoginForm, fetchAuthLogin, useAppSession } from '@rckit/auth';

function LoginPage() {
  const { updateSessionWithRedirect } = useAppSession();
  const router = useRouter();

  const handleSubmit = async (values) => {
    const { session } = await fetchAuthLogin(values);
    await updateSessionWithRedirect(session, router, '/dashboard');
  };

  return <AuthLoginForm onSubmit={handleSubmit} />;
}
```

### Signup Form

```tsx
import React from 'react';
import { AuthSignupForm, fetchAuthSignup, useAppSession } from '@rckit/auth';

function SignupPage() {
  const { updateSessionWithRedirect } = useAppSession();
  const router = useRouter();

  const handleSubmit = async (values) => {
    const { session } = await fetchAuthSignup(values);
    await updateSessionWithRedirect(session, router, '/dashboard');
  };

  return <AuthSignupForm onSubmit={handleSubmit} />;
}
```

### Other Forms

- `AuthOtpForm` - OTP verification form
- `AuthWebappForm` - Web app authentication form
- `AuthRestoreForm` - Password restore request form
- `AuthResetPasswordForm` - Password reset form

## Authentication Queries

The package provides query functions for all authentication operations:

```tsx
import {
  fetchAuthLogin,
  fetchAuthSignup,
  fetchAuthLogout,
  fetchAuthSession,
  fetchAuthOtp,
  fetchAuthRestore,
  fetchAuthResetPassword,
  fetchAuthWebapp,
} from '@rckit/auth';

// Login
const { session, otp } = await fetchAuthLogin({
  email: 'user@example.com',
  password: 'password123',
});

// Signup
const { session } = await fetchAuthSignup({
  email: 'user@example.com',
  password: 'password123',
  tos: true,
});

// Logout
await fetchAuthLogout();

// Get session
const { session } = await fetchAuthSession({});

// Verify OTP
const { session } = await fetchAuthOtp({
  code: '123456',
});

// Request password restore
await fetchAuthRestore({
  email: 'user@example.com',
});

// Reset password
await fetchAuthResetPassword({
  token: 'reset-token',
  password: 'newpassword123',
});
```

# 📚 API Reference

## AppSession

React context provider component that manages authentication session.

### Props

```typescript
interface AppSessionProps {
  children: React.ReactNode;
}
```

### Usage

```tsx
<AppSession>
  <YourApp />
</AppSession>
```

**Features:**
- Provides session context to all child components
- Persists session to localStorage with key `'appSession'`
- Automatically fetches session on mount
- Automatically refreshes session when expired (5 minutes in production, 1 minute in development)
- Shows loading screen during session operations
- Updates all consuming components when session changes

## useAppSession

React hook to access and manage authentication session.

### Returns

```typescript
interface AppSessionContextProps {
  sessionId?: string;
  session?: Session;
  sessionStatus?: 'init' | 'loading' | 'fetched';
  sessionInitedAt?: number;
  sessionLoadingAt?: number;
  sessionFetchedAt?: number;
  updateSession: (session?: Session) => Promise<void>;
  updateSessionWithRedirect: (
    session: Session | null,
    router: Router,
    path?: string | string[]
  ) => Promise<void>;
  clearSession: () => Promise<void>;
  setAppSession: Dispatch<SetStateAction<AppSessionType>>;
}
```

### Usage

```tsx
const {
  session,
  sessionStatus,
  updateSession,
  updateSessionWithRedirect,
  clearSession,
} = useAppSession();
```

**Returns:**
- `session` - Current session object (contains user data)
- `sessionId` - Current session ID
- `sessionStatus` - Current status: `'init'`, `'loading'`, or `'fetched'`
- `sessionInitedAt` - Timestamp when session was initialized
- `sessionLoadingAt` - Timestamp when session loading started
- `sessionFetchedAt` - Timestamp when session was last fetched
- `updateSession` - Function to update session (optionally fetches from server if no session provided)
- `updateSessionWithRedirect` - Function to update session and redirect
- `clearSession` - Function to clear session and logout
- `setAppSession` - Direct state setter (advanced usage)

**Note:** Must be used within an `AppSession` provider. Will throw an error if used outside the provider context.

## useAppUser

React hook to access current user information.

### Returns

```typescript
interface User {
  _id: string;
  email: string;
  role: string;
  companyId: string;
  isAdmin: boolean;
  title: string;
  avatar?: string;
}
```

### Usage

```tsx
const user = useAppUser();

if (!user) {
  return <div>Not logged in</div>;
}

// user.isAdmin - boolean indicating admin role
// user.title - user display name (name or email)
// user.avatar - user avatar URL
```

**Returns:**
- `null` if user is not logged in
- User object with additional computed fields:
  - `isAdmin` - Boolean indicating if user has admin role
  - `title` - Display name (falls back to email)
  - `avatar` - User avatar URL

## useAuthGuard

React hook to protect routes based on user roles.

### Parameters

```typescript
type UseAuthGuardOptions = {
  role?: 'user' | 'admin' | 'guestOnly';
  redirect?: string;
};

useAuthGuard(
  router: Router,
  options?: UseAuthGuardOptions
): string | null
```

### Usage

```tsx
const redirectUrl = useAuthGuard(router, { role: 'admin' });
```

**Parameters:**
- `router` - Router object with `asPath` and `push` method (e.g., Next.js router)
- `options.role` - Required role: `'user'` (default), `'admin'`, or `'guestOnly'`
- `options.redirect` - Custom redirect path (optional)

**Returns:**
- `null` if access is allowed
- Redirect URL string if redirect is needed

**Behavior:**
- Automatically redirects unauthorized users
- Adds return URL parameter (`?r=...`) for login redirects
- Default redirects:
  - Admin access denied: `/cabinet/forbidden`
  - User access denied: `/auth/login`
  - Guest-only access denied: `/cabinet`

## Authentication Forms

### AuthLoginForm

Login form component with email and password fields.

```typescript
interface AuthLoginFormProps {
  onSubmit: (values: AuthLoginFormValues) => Promise<void>;
}

interface AuthLoginFormValues {
  email: string;
  password: string;
}
```

### AuthSignupForm

Signup form component with email, password, and terms of service checkbox.

```typescript
interface AuthSignupFormProps {
  onSubmit: (values: AuthSignupFormValues) => Promise<void>;
}

interface AuthSignupFormValues {
  email: string;
  password: string;
  tos: boolean;
}
```

### AuthOtpForm

OTP verification form component.

### AuthWebappForm

Web app authentication form component.

### AuthRestoreForm

Password restore request form component.

### AuthResetPasswordForm

Password reset form component.

## Authentication Queries

All query functions accept an optional `ApiClientOptions` parameter:

```typescript
interface ApiClientOptions {
  apiClient?: ApiClient;
}
```

### fetchAuthLogin

Login with email and password.

```typescript
interface AuthLoginParams {
  email: string;
  password: string;
}

interface AuthLoginResponse {
  otp?: Otp;
  session: Session;
}

fetchAuthLogin(
  params: AuthLoginParams,
  options?: ApiClientOptions
): Promise<AuthLoginResponse>
```

### fetchAuthSignup

Sign up new user.

```typescript
interface AuthSignupParams {
  email: string;
  password: string;
  tos: boolean;
}

fetchAuthSignup(
  params: AuthSignupParams,
  options?: ApiClientOptions
): Promise<{ session: Session }>
```

### fetchAuthLogout

Logout current user.

```typescript
fetchAuthLogout(
  options?: ApiClientOptions
): Promise<Record<string, unknown>>
```

### fetchAuthSession

Get current session.

```typescript
interface AuthSessionParams {}

interface AuthSessionResponse {
  data: {
    session?: Session;
  };
}

fetchAuthSession(
  params: AuthSessionParams,
  options?: ApiClientOptions
): Promise<AuthSessionResponse>
```

### fetchAuthOtp

Verify OTP code.

```typescript
interface AuthOtpParams {
  code: string;
}

fetchAuthOtp(
  params: AuthOtpParams,
  options?: ApiClientOptions
): Promise<{ session: Session }>
```

### fetchAuthRestore

Request password restore.

```typescript
interface AuthRestoreParams {
  email: string;
}

fetchAuthRestore(
  params: AuthRestoreParams,
  options?: ApiClientOptions
): Promise<boolean>
```

### fetchAuthResetPassword

Reset password with token.

```typescript
interface AuthResetPasswordParams {
  token: string;
  password: string;
}

fetchAuthResetPassword(
  params: AuthResetPasswordParams,
  options?: ApiClientOptions
): Promise<void>
```

### fetchAuthWebapp

Authenticate via web app.

```typescript
interface AuthWebappParams {
  // Web app specific parameters
}

fetchAuthWebapp(
  params: AuthWebappParams,
  options?: ApiClientOptions
): Promise<{ session: Session }>
```

## Types

### User

```typescript
interface User {
  _id: string;
  email: string;
  role: string;
  companyId: string;
}
```

### Session

```typescript
interface Session {
  _id: string;
  user?: User;
}
```

### Otp

```typescript
interface Otp {
  _id: string;
}
```

### Router

```typescript
type Router = {
  asPath: string;
  push: (url: string) => void;
};
```

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `react-bootstrap` - Bootstrap components (peer dependency)
- `use-local-storage-state` - localStorage state management hook (peer dependency)
- `@rckit/api-client` - API client for making requests
- `@rckit/form` - Form components and hooks
- `@rckit/link` - Link component
- `@rckit/debug` - Debug utilities
- `@lsk4/algos` - Algorithm utilities
- `@lsk4/env` - Environment detection
- `@lsk4/err` - Error handling
- `@lsk4/log` - Logging utilities

### localStorage Key

Session is stored in localStorage under the key: `'appSession'`

### Session Expiration

Session automatically refreshes when expired:
- **Development**: 1 minute
- **Production**: 5 minutes

### API Endpoints

The package expects the following API endpoints:

- `POST /api/auth/login` - User login
- `POST /api/auth/signup` - User signup
- `POST /api/auth/logout` - User logout
- `POST /api/auth/session` - Get current session
- `POST /api/auth/otp` - Verify OTP
- `POST /api/auth/resetPassword/request` - Request password restore
- `POST /api/auth/resetPassword` - Reset password
- `POST /api/auth/webapp` - Web app authentication

### Custom API Client

You can provide a custom API client to query functions:

```tsx
import { fetchAuthLogin } from '@rckit/auth';
import { createApiClient } from '@rckit/api-client';

const customApiClient = createApiClient({
  baseURL: 'https://api.example.com',
});

const { session } = await fetchAuthLogin(
  { email: 'user@example.com', password: 'password' },
  { apiClient: customApiClient }
);
```

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
3.  Commit your changes (`git commit -am 'feat(auth): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
