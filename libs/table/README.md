# RCKIT – Table

> @rckit/table – RCKIT – Table – React table component with sorting, pagination, search, and infinite scroll support

[![LSK logo](https://badgen.net/badge/icon/MADE%20BY%20LSK?icon=zeit\&label\&color=red\&labelColor=red)](https://github.com/lskjs)
[![NPM version](https://badgen.net/npm/v/@rckit/table)](https://www.npmjs.com/package/@rckit/table)
[![NPM downloads](https://badgen.net/npm/dt/@rckit/table)](https://www.npmjs.com/package/@rckit/table)
[![NPM Dependency count](https://badgen.net/bundlephobia/dependency-count/@rckit/table)](https://bundlephobia.com/result?p=@rckit/table)
[![Have TypeScript types](https://badgen.net/npm/types/@rckit/table)](https://www.npmjs.com/package/@rckit/table)
[![Have tree shaking](https://badgen.net/bundlephobia/tree-shaking/@rckit/table)](https://bundlephobia.com/result?p=@rckit/table)
[![NPM Package size](https://badgen.net/bundlephobia/minzip/@rckit/table)](https://bundlephobia.com/result?p=@rckit/table)
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
    *   [Defining Columns](#defining-columns)
    *   [Using with Data Array](#using-with-data-array)
    *   [Using with Query Hook](#using-with-query-hook)
    *   [Infinite Scroll](#infinite-scroll)
    *   [Search Functionality](#search-functionality)
    *   [Sorting](#sorting)
    *   [Pagination](#pagination)
    *   [Custom Components](#custom-components)
    *   [Filters](#filters)
*   [📚 API Reference](#-api-reference)
    *   [Table](#table)
    *   [TableProps](#tableprops)
    *   [QueryListParams](#querylistparams)
    *   [TableColumn](#tablecolumn)
    *   [Custom Components](#custom-components-1)
*   [🔧 Configuration](#-configuration)
*   [📖 License](#-license)
*   [👥 Contributors](#-contributors)
*   [👏 Contributing](#-contributing)
*   [📮 Any questions? Always welcome :)](#-any-questions-always-welcome-)

# ⌨️ Install

```sh
# pnpm
pnpm add @rckit/table

# yarn
yarn add @rckit/table

# npm
npm i @rckit/table
```

# 📖 Features

- 📊 **Powerful table component** built on top of `@tanstack/react-table`
- 🔍 **Built-in search** with debounced input
- ↕️ **Column sorting** with support for single and multi-column sorting
- 📄 **Pagination** with customizable page size
- ♾️ **Infinite scroll** support for large datasets
- 🔄 **Refresh functionality** with loading states
- 🎨 **Customizable components** - replace any part of the table UI
- 🎯 **Type-safe** - full TypeScript support
- 🌲 **Tree-shakeable** - optimized bundle size
- 🎛️ **Filter support** - optional filter panel integration

# 🚀 Usage

## Basic Setup

Import and use the `Table` component with your data and columns:

```tsx
import React, { useState } from 'react';
import { Table } from '@rckit/table';
import type { ColumnDef } from '@tanstack/react-table';

interface User {
  id: number;
  name: string;
  email: string;
}

function MyTable() {
  const [params, setParams] = useState({
    limit: 10,
    offset: 0,
  });

  const columns: ColumnDef<User>[] = [
    {
      accessorKey: 'name',
      header: 'Name',
      enableSorting: true,
    },
    {
      accessorKey: 'email',
      header: 'Email',
      enableSorting: true,
    },
  ];

  const data = [
    { id: 1, name: 'John Doe', email: 'john@example.com' },
    { id: 2, name: 'Jane Smith', email: 'jane@example.com' },
  ];

  return (
    <Table
      data={data}
      columns={columns}
      count={data.length}
      limit={10}
      initialState={params}
      onChange={setParams}
    />
  );
}
```

## Defining Columns

Define columns using `@tanstack/react-table` column definitions:

```tsx
import type { ColumnDef } from '@tanstack/react-table';

const columns: ColumnDef<User>[] = [
  {
    accessorKey: 'id',
    header: 'ID',
    enableSorting: false,
  },
  {
    accessorKey: 'name',
    header: 'Name',
    enableSorting: true,
    width: 200,
  },
  {
    accessorKey: 'email',
    header: 'Email',
    enableSorting: true,
    cell: ({ getValue }) => (
      <a href={`mailto:${getValue()}`}>{getValue()}</a>
    ),
  },
];
```

## Using with Data Array

Pass data directly as an array:

```tsx
<Table
  data={users}
  columns={columns}
  count={users.length}
  limit={10}
  initialState={{ limit: 10, offset: 0 }}
  onChange={setParams}
/>
```

## Using with Query Hook

Use with React Query or similar data fetching libraries:

```tsx
import { useQuery } from '@tanstack/react-query';

function UsersTable() {
  const [params, setParams] = useState({
    limit: 10,
    offset: 0,
    search: '',
    sort: '',
  });

  const query = useQuery({
    queryKey: ['users', params],
    queryFn: () => fetchUsers(params),
  });

  return (
    <Table
      query={query}
      columns={columns}
      initialState={params}
      onChange={setParams}
    />
  );
}
```

## Infinite Scroll

Enable infinite scroll by providing a query with `fetchNextPage`:

```tsx
import { useInfiniteQuery } from '@tanstack/react-query';

function InfiniteUsersTable() {
  const [params, setParams] = useState({
    limit: 10,
    offset: 0,
  });

  const query = useInfiniteQuery({
    queryKey: ['users', params],
    queryFn: ({ pageParam = 0 }) => fetchUsers({ ...params, offset: pageParam }),
    getNextPageParam: (lastPage, pages) => {
      if (lastPage.items.length < params.limit) return undefined;
      return pages.length * params.limit;
    },
  });

  return (
    <Table
      query={query}
      columns={columns}
      initialState={params}
      onChange={setParams}
    />
  );
}
```

## Search Functionality

The table includes built-in search with debounced input:

```tsx
<Table
  data={data}
  columns={columns}
  search={params.search}
  initialState={params}
  onChange={(prev) => setParams({ ...prev, search: value })}
/>
```

The search component automatically:
- Debounces input (500ms delay)
- Shows loading state during fetch
- Provides refresh button
- Clears search value

## Sorting

Enable sorting on columns and handle sort changes:

```tsx
const [params, setParams] = useState({
  limit: 10,
  offset: 0,
  sort: '', // Can be string, array, or object
});

// Single column sort
const columns: ColumnDef<User>[] = [
  {
    accessorKey: 'name',
    header: 'Name',
    enableSorting: true,
  },
];

// Handle sort changes
<Table
  data={data}
  columns={columns}
  initialState={params}
  onChange={(prev) => {
    setParams({
      ...prev,
      sort: newSortValue,
      offset: 0, // Reset to first page on sort
    });
  }}
/>
```

### Multi-Column Sorting

Enable multi-column sorting:

```tsx
<Table
  data={data}
  columns={columns}
  enableMultiSort={true}
  initialState={params}
  onChange={setParams}
/>
```

### Sort Parameter Formats

The `sort` parameter supports multiple formats:

```tsx
// String format
sort: '-name' // descending
sort: 'name'  // ascending

// Array format
sort: ['name', '-email']

// Object format
sort: { name: false, email: true } // false = asc, true = desc

// QueryListSort1Param format
sort: [{ id: 'name', desc: false }, { id: 'email', desc: true }]
```

## Pagination

Control pagination with `limit` and `offset`:

```tsx
const [params, setParams] = useState({
  limit: 10,
  offset: 0,
});

<Table
  data={data}
  columns={columns}
  count={totalCount}
  limit={params.limit}
  initialState={params}
  onChange={(prev) => {
    setParams({
      ...prev,
      offset: limit * selectedPage,
    });
  }}
/>
```

## Custom Components

Replace any part of the table with custom components:

```tsx
const CustomMessage = ({ type }) => (
  <div>Custom {type} message</div>
);

const CustomPagination = ({ pageCount, onPageChange }) => (
  <div>Custom pagination</div>
);

<Table
  data={data}
  columns={columns}
  components={{
    Message: CustomMessage,
    Pagination: CustomPagination,
    Search: CustomSearch,
    Filter: CustomFilter,
  }}
  initialState={params}
  onChange={setParams}
/>
```

## Filters

Add a custom filter component:

```tsx
const UserFilter = ({ value, onSubmit }) => {
  const [filters, setFilters] = useState(value || {});

  return (
    <form onSubmit={(e) => {
      e.preventDefault();
      onSubmit(filters);
    }}>
      <input
        value={filters.role || ''}
        onChange={(e) => setFilters({ ...filters, role: e.target.value })}
        placeholder="Filter by role"
      />
      <button type="submit">Apply</button>
    </form>
  );
};

<Table
  data={data}
  columns={columns}
  components={{
    Filter: UserFilter,
  }}
  initialOpenFilter={false}
  initialState={params}
  onChange={setParams}
/>
```

# 📚 API Reference

## Table

Main table component that renders a fully-featured data table.

### Props

```typescript
interface TableProps<T = {}> {
  // Data sources (use either data or query)
  data?: {
    items?: Array<Record<string, unknown>>;
    pages?: Array<Record<string, unknown>>;
    count?: number;
  };
  query?: any; // React Query or similar query object
  
  // Pagination
  count?: number;
  limit?: number;
  
  // Required props
  columns: ColumnDef[];
  onChange: Dispatch<SetStateAction<QueryListParams<T>>>;
  initialState: QueryListParams<T>;
  
  // Optional features
  enableMultiSort?: boolean;
  initialOpenFilter?: boolean;
  search?: string;
  components?: {
    Pagination?: ITablePagination;
    Message?: ITableMessage;
    Search?: ITableSearch;
    Filter?: ITableFilter;
  };
  debug?: boolean;
}
```

### Usage

```tsx
<Table
  data={data}
  columns={columns}
  count={totalCount}
  limit={10}
  initialState={{ limit: 10, offset: 0 }}
  onChange={setParams}
/>
```

**Features:**
- Automatically handles loading and empty states
- Supports both array data and query-based data fetching
- Integrates with infinite scroll when query provides `fetchNextPage`
- Manages sorting, pagination, and search state
- Provides customizable UI components

## TableProps

TypeScript interface for table component props.

```typescript
interface TableProps<T = {}> {
  data?: {
    items?: Array<Record<string, unknown>>;
    pages?: Array<Record<string, unknown>>;
    count?: number;
  };
  query?: any;
  count?: number;
  limit?: number;
  onChange: Dispatch<SetStateAction<QueryListParams<T>>>;
  initialState: QueryListParams<T>;
  enableMultiSort?: boolean;
  initialOpenFilter?: boolean;
  columns: any[];
  search?: string;
  components?: {
    Pagination?: ITablePagination;
    Message?: ITableMessage;
    Search?: ITableSearch;
    Filter?: ITableFilter;
  };
  debug?: boolean;
}
```

## QueryListParams

TypeScript interface for query parameters.

```typescript
interface QueryListParams<T = {}> {
  limit?: number;
  offset?: number;
  filter?: T;
  search?: string;
  sort?: QueryListSortParam;
  count?: boolean;
}
```

### Fields

- `limit` - Number of items per page
- `offset` - Number of items to skip (for pagination)
- `filter` - Custom filter object
- `search` - Search query string
- `sort` - Sort configuration (see Sort Parameter Formats)
- `count` - Whether to include total count in response

## TableColumn

Extended column definition with width support.

```typescript
type TableColumn<TData, TValue> = ColumnDef<TData, TValue> & {
  width?: string | number | null;
};
```

Extends `@tanstack/react-table`'s `ColumnDef` with optional `width` property.

## Custom Components

### ITablePagination

```typescript
type ITablePagination = (props: {
  pageCount: number;
  initialPage: number;
  onPageChange: ({ selected }: { selected: number }) => void;
}) => React.ReactElement;
```

### ITableMessage

```typescript
interface TableMessageProps {
  type?: 'empty' | 'loading';
  title?: string;
  subtitle?: string;
}

type ITableMessage = (props: TableMessageProps) => React.ReactElement;
```

### ITableSearch

```typescript
interface TableSearchProps {
  placeholder?: string;
  onChange: (value: string) => void;
  open: () => void;
  hasFilter?: boolean;
  search?: string;
  isFetching?: boolean;
  showRefresh?: boolean;
  refresh: () => void;
}

type ITableSearch = (props: TableSearchProps) => React.ReactElement;
```

### ITableFilter

```typescript
interface TableFilterProps<T = any> {
  value?: T;
  onSubmit: (value: T) => any;
}

type ITableFilter = (props: TableFilterProps) => React.ReactElement;
```

# 🔧 Configuration

The package requires the following dependencies:

- `react` - React library (peer dependency)
- `@tanstack/react-table` - Table library (peer dependency)
- `react-infinite-scroll-component` - Infinite scroll support
- `use-debounce` - Debounced search input
- `clsx` - Class name utility
- `@rckit/icons` - Icon components
- `@rckit/debug` - Debug utilities
- `@lsk4/algos` - Algorithm utilities
- `@lsk4/env` - Environment detection

### Data Format

The table accepts data in multiple formats:

**Array format:**
```typescript
data = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }]
```

**Query response format:**
```typescript
data = {
  items: [{ id: 1, name: 'John' }],
  count: 100
}
```

**Infinite query format:**
```typescript
data = {
  pages: [
    { items: [{ id: 1 }], count: 100 },
    { items: [{ id: 2 }], count: 100 }
  ]
}
```

### Query Object

When using `query` prop, the table expects:

```typescript
{
  data: any; // Current data
  isFetching: boolean; // Loading state
  fetchNextPage?: () => void; // For infinite scroll
  hasNextPage?: boolean; // For infinite scroll
  fetchPreviousPage?: () => void; // For infinite scroll
  hasPreviousPage?: boolean; // For infinite scroll
  isFetchingNextPage?: boolean; // For infinite scroll
  isFetchingPreviousPage?: boolean; // For infinite scroll
  refetch: () => void; // Refresh function
}
```

### Sort Normalization

The table automatically normalizes sort parameters. Supported formats:

- **String**: `'name'` (asc) or `'-name'` (desc)
- **Array**: `['name', '-email']`
- **Object**: `{ name: false, email: true }` (false = asc, true = desc)
- **QueryListSort1Param**: `[{ id: 'name', desc: false }]`

### Styling

The table uses CSS classes with the `rctbl_` prefix. You can override styles by targeting these classes:

- `rctbl_root__wrapper` - Main wrapper
- `rctbl_root__tableWrapper` - Table container
- `rctbl_tablesearch__wrapper` - Search wrapper
- `rctbl_tablepagination__container` - Pagination container
- `rctbl_tablemessage__wrapper` - Message wrapper
- `rctbl_tbody__td` - Table cell

### Browser Compatibility

This package requires modern browser features:
- ES6+ JavaScript
- CSS Grid/Flexbox for layout
- React 18+

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
3.  Commit your changes (`git commit -am 'feat(table): Add some fooBar'`)
4.  Push to the branch (`git push origin feature/fooBar`)
5.  Create a new Pull Request

# 📮 Any questions? Always welcome :)

*   [Email](mailto:hi@isuvorov.com)
*   [LSK.news – Telegram channel](https://t.me/lskjs)
*   [Спроси нас в телеграме ;)](https://t.me/lskjschat)
