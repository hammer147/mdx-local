# Using MDX in Next.js 13 with TailwindCSS

[guide from Next.js](https://beta.nextjs.org/docs/guides/mdx)

## 1. Install dependencies

```bash
npm i @next/mdx @types/mdx
```

## 2. Create mdx-components.tsx in the root of your application

```tsx
import type { MDXComponents } from 'mdx/types'

// This file allows you to provide custom React components
// to be used in MDX files. You can import and use any
// React component you want, including components from
// other libraries.

// This file is required to use MDX in `app` directory.
export function useMDXComponents(components: MDXComponents): MDXComponents {
  return {
    // Allows customizing built-in components, e.g. to add styling.
    // h1: ({ children }) => <h1 style={{ fontSize: "100px" }}>{children}</h1>,
    ...components
  }
}
```

## 3. Update next.config.js

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    appDir: true,
    mdxRs: true
  }
}

const withMDX = require('@next/mdx')()
module.exports = withMDX(nextConfig)
```

## 4. Create a new hello.mdx file in the `app` directory

```mdx
# Hello, Next.js!

You can import and use React components in MDX files.
```

## 5. Import the MDX file in a page

```tsx
import HelloWorld from './hello.mdx'

export default function Page() {
  return <HelloWorld />
}
```

## 6. TailwindCSS

1. [install tailwindcss](https://tailwindcss.com/docs/guides/nextjs)
2. install prettier plugin

    ```bash
    npm i -D prettier prettier-plugin-tailwindcss
    ```

3. install typography plugin

    ```bash
    npm i -D @tailwindcss/typography
    ```

4. update tailwind.config.js

    ```js
    /** @type {import('tailwindcss').Config} */

    module.exports = {
    content: ['./src/**/*.{js,ts,jsx,tsx,mdx}', './mdx-components.tsx'],
    theme: {
    extend: {}
    },
    plugins: [require('@tailwindcss/typography')]
    }
    ```

5. add prose class to mdx
  
    ```mdx
    # Hello, Next.js!
    
    You can import and use React components in MDX files.

    export default ({ children }) => <div className='prose'>{children}</div>
    ```
