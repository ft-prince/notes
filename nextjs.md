Next.js Cheat List
===

[![NPM version](https://img.shields.io/npm/v/next.svg?style=flat)](https://www.npmjs.com/package/next)
[![Downloads](https://img.shields.io/npm/dm/next.svg?style=flat)](https://www.npmjs.com/package/next)
[![Repo Dependents](https://badgen.net/github/dependents-repo/vercel/next.js)](https://github.com/vercel/next.js/network/dependents)
[![Github repo](https://badgen.net/badge/icon/Github?icon=github&label)](https://github.com/vercel/next.js)

This is a quick reference cheat sheet containing an API reference list and some examples for [Next.js](https://nextjs.org/)
<!--rehype:style=padding-top: 12px;-->

getting Started
----

### Create project

```shell
npx create-next-app@latest
# or
yarn create next-app
# or
pnpm create next-app
```

Or create a [TypeScript](./typescript.md) project

```shell
npx create-next-app@latest --typescript
# or
yarn create next-app --typescript
# or
pnpm create next-app --typescript
```

Run `npm run dev` or `yarn dev` or `pnpm dev` to start the development server on <http://localhost:3000>

### Add home page

Populate `pages/index.js` with the following content:

```jsx
function HomePage() {
  return <div>Welcome to Next.js!</div>
}

export default HomePage
```

`Next.js` is built around the concept of pages. Pages are `React` components exported from `.js`, `.jsx`, `.ts` or `.tsx` files in the `pages` directory

### getServerSideProps
<!--rehype:wrap-class=row-span-2-->

```jsx
function Page({ data }) {
  // Render data...
}

// This will be called on every request
export async function getServerSideProps() {
  // Get data from external API
  const res = await fetch(`https://.../data`)
  const data = await res.json()

  // Pass data to the page through props
  return { props: { data } }
}

export default Page
```

If you export a function called `getServerSideProps` (server-side rendering) from a page, `Next.js` will pre-render the page on every request using the data returned by `getServerSideProps`

- When you request this page directly, `getServerSideProps` is run on request and the page will be pre-rendered using the returned props
- When you request this page on the client page transition via `next/link` or `next/router`, `Next.js` sends an API request to the server and the server runs `getServerSideProps`

### getStaticPaths
<!--rehype:wrap-class=row-span-2-->

```jsx
// pages/posts/[id].js
export async function getStaticPaths() {
  // Don't prerender any static pages when this is true (in preview environment) (faster build, but slower initial page load)
  if (process.env.SKIP_BUILD_STATIC_GENERATION) {
    return {
      paths: [],
      fallback: 'blocking',
    }
  }

  // Call the external API endpoint to get the posts
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // Get the path we want to pre-render based on the post. In the production environment, pre-render all pages.
  // (Slower build, but faster initial page load)
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }))

  // { fallback: false } indicates that other routes should 404
  return { paths, fallback: false }
}
```

If the page has dynamic routing and uses `getStaticProps`, you need to define a list of paths to be statically generated

- Data comes from headless CMS
- Data comes from database
- Data comes from file system
- Data can be cached publicly (not user specific)
- Pages must be pre-rendered (for SEO) and very fast - `getStaticProps` generates HTML and JSON files, both of which can be cached by the CDN to improve performance

### getStaticProps
<!--rehype:wrap-class=row-span-2-->

```jsx
// Posts will be populated by getStaticProps() at build time
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}

// This function is called during server-side build.
// It's not called on the client side, so you can even do database queries directly.
export async function getStaticProps() {
  // Call the external API endpoint to get the posts. You can use any data fetching library
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // By returning { props: { posts } }, the Blog component will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  }
}

export default Blog
```

Called when building on the server side

### Incremental static regeneration
<!--rehype:wrap-class=row-span-2-->

```jsx
function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  )
}

// This function is called during server-side build
// It may be called again on the serverless function if revalidation is enabled and a new request comes in
export async function getStaticProps() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    props: {
      posts,
    },
    // Next.js will try to regenerate the page:
    // - when a request comes in
    // - at most once every 10 seconds
    revalidate: 10, // within a moment
  }
}

// This function is called during server-side build
// If the path has not been generated yet, it may be called again on the serverless function
export async function getStaticPaths() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // Get the path we want to pre-render based on the post
  const paths = posts.map((post) => ({
    params: { id: post.id },
  }))

  // We will only prerender these paths at build time
  // { fallback: blocking } If the path does not exist, the server will render the page on demand
  return { paths, fallback: 'blocking' }
}

export default Blog
```

- Any requests to the page after the initial request and before 10 seconds will also be cached and instant
- After the 10 second window, the next request will still show the cached (stale) page
- Next.js triggers page regeneration in the background
- Once the page is successfully generated, Next.js will invalidate the cache and display the updated page. If the background regeneration fails, the old page will remain unchanged

### Use useEffect client data acquisition

```jsx
import { useState, useEffect } from 'react'

function Profile() {
  const [data, setData] = useState(null)
  const [isLoading, setLoading] = useState(false)

  useEffect(() => {
    setLoading(true)
    fetch('/api/profile-data')
      .then((res) => res.json())
      .then((data) => {
        setData(data)
        setLoading(false)
      })
  }, [])

  if (isLoading) return <p>Loading...</p>
  if (!data) return <p>No profile data</p>

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.bio}</p>
    </div>
  )
}
```

### Use SWR to obtain client data

```jsx
import useSWR from 'swr'

const fetcher = (...args) => fetch(...args).then((res) => res.json())

function Profile() {
  const { data, error } = useSWR('/api/profile-data', fetcher)

  if (error) return <div>Failed to load</div>
  if (!data) return <div>Loading...</div>

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.bio}</p>
    </div>
  )
}
```

### Static file service

Next.js can serve static files, such as images, in a folder named `public` in the root directory. Your code can then reference files in `public` starting from the base URL (`/`)

```jsx
import Image from 'next/image'

function Avatar() {
  return (
    <Image
      src="/me.png"
      alt="me"
      width="64"
      height="64"
    />
  )
}

export default Avatar
```

### Supported browsers and features

Next.js supports modern browsers with zero configuration

- Chrome 64+
- Edge 79+
- Firefox 67+
- Opera 51+
-Safari 12+
<!--rehype:className=cols-3-->

Next.js supports configuring `Browserslist` in `package.json` file

```js
{
  "browserslist": [
    "chrome 64",
    "edge 79",
    "firefox 67",
    "opera 51",
    "safari 12"
  ]
}
```

Built-in CSS support
---

### Add global style sheet
<!--rehype:wrap-class=row-span-2-->

If it does not exist, create a `pages/_app.js` file. Then, import the `styles.css` file

```jsx
import '../styles.css';

// This default export is required in the new "pages/_app.js" file
export default function MyApp({
  Component, pageProps
}) {
  return <Component {...pageProps} />
}
```

For example, consider the following stylesheet named `styles.css`

```css
body {
  font-family:
    'SF Pro Text', 'SF Pro Icons',
    'Helvetica Neue', 'Helvetica',
    'Arial', sans-serif;
  margin: 0 auto;
}
```

### Import styles from node_modules

For global stylesheets, such as `bootstrap` or `nprogress`, you should import the file in `pages/_app.js`

```jsx
// pages/_app.js
import 'bootstrap/dist/css/bootstrap.css'

export default function MyApp({
  Component, pageProps
}) {
  return <Component {...pageProps} />
}
```

Starting with <red>Next.js 9.5.4</red>, importing CSS files from `node_modules` is allowed anywhere in your application

### Add component-level CSS (CSS Modules)
<!--rehype:wrap-class=row-span-2-->

You don't need to worry about .error {} with any other `.css` or `.module.css` files! It will be generated `hash` name

```css
.error {
  color: white;
  background-color: red;
}
```

Then, create `components/Button.js`, import and use the above CSS file:

```jsx
import styles from './Button.module.css'

export function Button() {
  return (
    <button
      type="button"
      // Please note the "error" class
      // How it is accessed as a property of the imported "styles" object
      className={styles.error}
    >
      Destroy
    </button>
  )
}
```

### Sass support

Next.js allows you to import Sass using the `.scss` and `.sass` extensions, and component-level `Sass` can be used through CSS modules and the `.module.scss` or `.module.sass` extensions

```shell
$ npm install --save-dev sass
```

Before using Next.js' built-in `Sass` support, be sure to <pur>install `sass`</pur>

### Custom Sass options
<!--rehype:wrap-class=col-span-2-->

Configuring the `Sass` compiler is done using `sassOptions` in `next.config.js`. For example add `includePaths`:

```js
const path = require('path')

module.exports = {
  sassOptions: {
    includePaths:
        [path.join(__dirname, 'styles')],
  },
}
```

#### Sass Variables

```sass
/* variables.module.scss */
$primary-color: #64ff00;

:export {
  primaryColor: $primary-color;
}
```

Import `variables.module.scss` in `pages/_app.js`

```jsx
import variables from '../styles/variables.module.scss'

export default function MyApp({ Component, pageProps }) {
  return (
    <Layout color={variables.primaryColor}>
      <Component {...pageProps} />
    </Layout>
  )
}
```

### CSS-in-JS

The simplest one is inline styles:

```jsx
function HiThere() {
  return (
    <p style={{ color: 'red' }}>hi here</p>
  )
}

export default HiThere
```

The component using [styled-jsx](https://github.com/vercel/styled-jsx) is as follows:

```jsx
function HelloWorld() {
  return (
    <div>
      Hello world
      <p>scoped!</p>
      <style jsx>{`
        p { color: blue; }
        div { background: red; }
        @media (max-width: 600px) {
          div { background: blue; }
        }
      `}</style>
      <style global jsx>{`
        body { background: black; }
      `}</style>
    </div>
  )
}

export default HelloWorld
```

Of course, you can also use [styled-components](./styled-components.md)

Layouts
---

### Basic example

```jsx
// components/layout.js
import Navbar from './navbar'
import Footer from './footer'

export default function Layout({ children }) {
  return (
    <>
      <Navbar />
      <main>{children}</main>
      <Footer />
    </>
  )
}
```

### Single shared layout with custom application

```jsx
// pages/_app.js
import Layout from '../components/layout'

export default function MyApp({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  )
}
```

### Using TypeScript
<!--rehype:wrap-class=row-span-2-->

```jsx
// pages/index.tsx
import type { ReactElement } from 'react'
import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'
import type { NextPageWithLayout } from './_app'

const Page: NextPageWithLayout = () => {
  return <p>hello world</p>
}

Page.getLayout = function getLayout(page: ReactElement) {
  return (
    <Layout>
      <NestedLayout>{page}</NestedLayout>
    </Layout>
  )
}

export default Page
```

```jsx
// pages/_app.tsx

import type { ReactElement, ReactNode } from 'react'
import type { NextPage } from 'next'
import type {AppProps} from 'next/app'

export type NextPageWithLayout<P = {}, IP = P> = NextPage<P, IP> & {
  getLayout?: (page: ReactElement) => ReactNode
}

type AppPropsWithLayout = AppProps & {
  Component: NextPageWithLayout
}

export default function MyApp({ Component, pageProps }: AppPropsWithLayout) {
  // Use the layout defined at the page level if available
  const getLayout = Component.getLayout ?? ((page) => page)

  return getLayout(<Component {...pageProps} />)
}
```

### Layout per page

```jsx
// pages/index.js
import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'

export default function Page() {
  return (
    /** Your content */
  )
}

Page.getLayout = function getLayout(page) {
  return (
    <Layout>
      <NestedLayout>{page}</NestedLayout>
    </Layout>
  )
}
```

```jsx
// pages/_app.js
export default function MyApp({ Component, pageProps }) {
  // Use the layout defined at the page level if available
  const getLayout = Component.getLayout || ((page) => page)
  return getLayout(<Component {...pageProps} />)
}
```

### Data request

```jsx
// components/layout.js
import useSWR from 'swr'
import Navbar from './navbar'
import Footer from './footer'

export default function Layout({ children }) {
  const { data, error } = useSWR('/api/navigation', fetcher)
  if (error) return <div>Failed to load</div>
  if (!data) return <div>Loading...</div>
  return (
    <>
      <Navbar links={data.links} />
      <main>{children}</main>
      <Footer />
    </>
  )
}
```

Image optimization
---

### Local pictures

```jsx
import Image from 'next/image'
import profilePic from '../public/me.png'

function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src={profilePic}
        alt="Picture of the author"
        // width={500} automatically provided
        // height={500} automatically provided
        // blurDataURL="data:..." automatically provided
        // placeholder="blur" // Optional blur processing when loading
      />
      <p>Welcome to my homepage!</p>
    </>
  )
}
```

### Remote picture

```jsx
import Image from 'next/image'

export default function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src="/me.png"
        alt="Picture of the author"
        width={500}
        height={500}
      />
      <p>Welcome to my homepage!</p>
    </>
  )
}
```

To use a remote image, the `src` attribute should be a `URL` string, which can be relative or absolute

### Priority

You should add the priority attribute to the image that will become the Largest Contentful Paint (LCP) element for every page. Doing so allows Next.js to specifically prioritize which images to load (e.g. via preload tags or priority hints), significantly increasing LCP

```jsx
import Image from 'next/image'

export default function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src="/me.png"
        alt="Picture of the author"
        width={500}
        height={500}
        priority
      />
      <p>Welcome to my homepage!</p>
    </>
  )
}
```

Optimize fonts
---

### Google Fonts
<!--rehype:wrap-class=row-span-2-->

Automatically host any Google font. Fonts are included in the deployment and served from the same domain as your deployment. The browser will not send any requests to Google

```jsx
// pages/_app.js
import { Inter } from '@next/font/google'

// If loading a variable font, no need to specify font weight
const inter = Inter({ subsets: ['latin'] })

export default function MyApp({
  Component, pageProps
}) {
  return (
    <main className={inter.className}>
      <Component {...pageProps} />
    </main>
  )
}
```

### Specify thickness
<!--rehype:wrap-class=row-span-2-->

If you can't use variable fonts, you need to specify the weight:

```jsx {5}
// pages/_app.js
import { Roboto } from '@next/font/google'

const roboto = Roboto({
  weight: '400',
  subsets: ['latin'],
})

export default function MyApp({
  Component, pageProps
}) {
  return (
    <main className={roboto.className}>
      <Component {...pageProps} />
    </main>
  )
}
```

### Array specifies multiple weights or styles

```jsx
const roboto = Roboto({
  weight: ['400', '700'],
  style: ['normal', 'italic'],
  subsets: ['latin'],
})
```

### Apply fonts in \<head>

```jsx
// pages/_app.js
import { Inter } from '@next/font/google'
const inter = Inter({ subsets: ['latin'] })
export default function MyApp({ Component, pageProps }) {
  return (
    <>
      <style jsx global>{`
        html {
          font-family: ${inter.style.fontFamily};
        }
      `}</style>
      <Component {...pageProps} />
    </>
  )
}
```

### Single page use

```jsx
// pages/index.js
import { Inter } from '@next/font/google'

const inter = Inter({ subsets: ['latin'] })

export default function Home() {
  return (
    <div className={inter.className}>
      <p>Hello World</p>
    </div>
  )
}
```

### Specify a subset

```jsx
// pages/_app.js
const inter = Inter({ subsets: ['latin'] })
```

Use all fonts globally in `next.config.js`

```js
// next.config.js
module.exports = {
  experimental: {
    fontLoaders: [
      {
        loader: '@next/font/google',
        options: { subsets: ['latin'] }
      },
    ],
  },
}
```

If both are configured, the subset from the function call is used

### Local font
<!--rehype:wrap-class=row-span-2-->

```jsx
// pages/_app.js
import localFont from '@next/font/local'

// Font files can be located within "pages"
const myFont = localFont({
  src: './my-font.woff2'
})

export default function MyApp({
  Component, pageProps
}) {
  return (
    <main className={myFont.className}>
      <Component {...pageProps} />
    </main>
  )
}
```

If you want to use multiple files for a single font family, `src` can be an array:

```jsx
const roboto = localFont({
  src: [
    {
      path: './Roboto-Regular.woff2',
      weight: '400',
      style: 'normal',
    },
    {
      path: './Roboto-Italic.woff2',
      weight: '400',
      style: 'italic',
    },
    {
      path: './Roboto-Bold.woff2',
      weight: '700',
      style: 'normal',
    },
    {
      path: './Roboto-BoldItalic.woff2',
      weight: '700',
      style: 'italic',
    },
  ],
})
```

### Using Tailwind CSS
<!--rehype:wrap-class=col-span-2-->

```jsx
// pages/_app.js
import { Inter } from '@next/font/google'
const inter = Inter({
  subsets: ['latin'],
  variable: '--font-inter',
});
export default function MyApp({ Component, pageProps }) {
  return (
    <main className={`${inter.variable} font-sans`}>
      <Component {...pageProps} />
    </main>
  )
}
```

Finally, add the CSS variables to your Tailwind CSS configuration:

```jsx
// tailwind.config.js
const { fontFamily } = require('tailwindcss/defaultTheme')

module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ['var(--font-inter)', ...fontFamily.sans],
      },
    },
  },
  plugins: [],
}
```

Optimize Scripts
---

### Page script

```jsx
import Script from 'next/script'

export default function Dashboard() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
      />
    </>
  )
}
```

### App Script
<!--rehype:wrap-class=row-span-2-->

To load third-party scripts for all routes, import `next/script` and include the script directly in `pages/_app.js`

```jsx
import Script from 'next/script'

export default function MyApp({
  Component, pageProps
}) {
  return (
    <>
      <Script
        src="https://example.com/script.js"
      />
      <Component {...pageProps} />
    </>
  )
}
```

### Offload script to Web Worker (experimental)
<!--rehype:wrap-class=row-span-2-->

This strategy is still experimental and can only be used if the `nextScriptWorkers` flag is enabled in `next.config.js`:

```js
module.exports = {
  experimental: {
    nextScriptWorkers: true,
  },
}
```

Once setup, defining `strategy="worker"` will automatically instantiate `Partytown` in your application and offload the script to the network worker

```jsx
import Script from 'next/script'

export default function Home() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        strategy="worker"
      />
    </>
  )
}
```

### Other attributes

```jsx
import Script from 'next/script'

export default function Page() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        id="example-script"
        nonce="XUENAJFW"
        data-test="script"
      />
    </>
  )
}
```

### Inline script
<!--rehype:wrap-class=col-span-2-->

```jsx
<Script id="show-banner">
  {`document.getElementById('banner').classList.remove('hidden')`}
</Script>
```

```jsx
<Script
  id="show-banner"
  dangerouslySetInnerHTML={{
    __html: `document.getElementById('banner').classList.remove('hidden')`,
  }}
/>
```

### Execute additional code

```jsx
import Script from 'next/script'

export default function Page() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        onLoad={() => {
          console.log('Script has loaded')
        }}
      />
    </>
  )
}
```

ESLint
---

### Integrate ESLint

```json
"scripts": {
  "lint": "next lint"
}
```

Then run `npm run lint` or `yarn lint`:

```shell
yarn lint
# You will see a prompt like this:
#
# ? How do you want to configure ESLint?
#
# ❯ Basic configuration + Core Web Vitals rule set (recommended)
# basic configuration
#None
```

### Strict

Strict strict configuration: including basic ESLint configuration of Next.js and more strict [Core Web Vitals rule set](https://nextjs.org/docs/basic-features/eslint#core-web-vitals)

```js
{
  "extends": "next/core-web-vitals"
}
```

Base basic configuration: including basic ESLint configuration of Next.js

```js
{
  "extends": "next"
}
```

Create a `.eslintrc.json` file containing the selected configuration in the root directory of the project

### Custom settings

```js
{
  "extends": "next",
  "settings": {
    "next": {
      "rootDir": "packages/my-app/"
    }
  }
}
```

`rootDir` can be a path (relative or absolute), a glob (i.e. "`packages/*/`"), or an array of paths and/or `glob`

### Check custom directories and files
<!--rehype:wrap-class=row-span-2-->

```js
module.exports = {
  eslint: {
    dirs: ['pages', 'utils'],
  },
}
```

Run `ESLint` only on the "`pages`" and "`utils`" directories during a production build (`next build`), or use the command

```bash
$ next lint --dir pages --dir utils --file bar.js
```
<!--rehype:className=wrap-text-->

### Disable rules
<!--rehype:wrap-class=row-span-2-->

You can change them directly using the `rules` attribute in `.eslintrc`:

```js
{
  "extends": "next",
  "rules": {
    "react/no-unescaped-entities": "off",
    "@next/next/no-page-custom-font": "off"
  }
}
```

Modify or disable any rules provided by supported plugins (`react`, `react-hooks`, `next`)

### Core Web Vitals

```js
{
  "extends": "next/core-web-vitals"
}
```

### Prettier

```bash
npm install -S eslint-config-prettier
# or
yarn add --dev eslint-config-prettier
```

---

```js
{
  "extends": ["next", "prettier"]
}
```

### lint-staged
<!--rehype:wrap-class=col-span-2-->

```js
const path = require('path')

const buildEslintCommand = (filenames) =>
  `next lint --fix --file ${filenames
    .map((f) => path.relative(process.cwd(), f))
    .join(' --file ')}`;

module.exports = {
  '*.{js,jsx,ts,tsx}': [buildEslintCommand],
}
```

Content is added to the `.lintstagedrc.js` file in the project root directory to specify the `--file` flag

TypeScript
---

### create-next-app

```bash
npx create-next-app@latest --ts
# or
yarn create next-app --typescript
# or
pnpm create next-app --ts
```

### Static generation and server-side rendering
<!--rehype:wrap-class=col-span-2 row-span-2-->

```tsx
import { GetStaticProps, GetStaticPaths, GetServerSideProps } from 'next'
export const getStaticProps: GetStaticProps = async (context) => {
  // ...
}
export const getStaticPaths: GetStaticPaths = async () => {
  // ...
}
export const getServerSideProps: GetServerSideProps = async (context) => {
  // ...
}
```

### Add ts configuration to existing project

```bash
touchtsconfig.json
```

You can also provide a relative path to the `tsconfig.json` file by setting the `typescript.tsconfigPath` property in the `next.config.js` file

### API routing
<!--rehype:wrap-class=row-span-2-->

```tsx
import type {
  NextApiRequest, NextApiResponse
} from 'next'

export default (
  req: NextApiRequest,
  res: NextApiResponse
) => {
  res.status(200).json({ name:'John Doe' })
}
```

You can also type response data:

```tsx
import type {
  NextApiRequest, NextApiResponse
} from 'next'

type Data = {
  name: string
}

export default (
  req: NextApiRequest,
  res: NextApiResponse<Data>
) => {
  res.status(200).json({ name:'John Doe' })
}
```

### Custom application

Use the built-in type `AppProps` and change the file name to `./pages/_app.tsx` as follows:

```tsx
import type {AppProps} from 'next/app'

export default function MyApp({
  Component, pageProps
}: AppProps) {
  return <Component {...pageProps} />
}
```

### Type checking next.config.js

```tsx
// @ts-check
/**
 * @type {import('next').NextConfig}
 **/
const nextConfig = {
  /*Configuration options go here*/
}

module.exports = nextConfig
```

### Ignore TypeScript errors

```tsx {3}
module.exports = {
  typescript: {
    ignoreBuildErrors: true,
  },
}
```

Dangerously allowing production builds to complete successfully even if your project has type errors

environment variables
---

### Load environment variables

Load environment variables from `.env.local` into `process.env`

```ini
DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

Use environment variables

```js
// pages/index.js
export async function getStaticProps() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
  })
  // ...
}
```

### Automatically expand variables in .env* files

```bash
# .env
HOSTNAME=localhost
PORT=8080
HOST=http://$HOSTNAME:$PORT
```

If you try to use a variable with `$` in the actual value, you need to escape it like this: `\$`

```bash
# .env
A=abc

# becomes "preabc"
WRONG=pre$A

# becomes "pre$A"
CORRECT=pre\$A
```

### Expose environment variables to the browser

In order to expose a variable to the browser, you must prefix the variable with `NEXT_PUBLIC_`

```bash
NEXT_PUBLIC_ANALYTICS_ID=abcdefghijk
```

`NEXT_PUBLIC_ANALYTICS_ID` can be used here because it is prefixed with `NEXT_PUBLIC_`

```jsx
// pages/index.js
import setupAnalyticsService from '../lib/my-analytics-service'

//
// It will be converted to `setupAnalyticsService('abcdefghijk')` at build time
setupAnalyticsService(process.env.NEXT_PUBLIC_ANALYTICS_ID)

function HomePage() {
  return <h1>Hello World</h1>
}

export default HomePage
```

routing
---

### introduce
<!--rehype:wrap-class=row-span-2-->

The router will automatically route the file named `index` to the root of the directory

:-- | --
:-- | --
`pages/index.js` | <pur>`/`</pur>
`pages/blog/index.js` | <pur>`/blog`</pur>

The router supports nested files. If you create a nested folder structure, files will be automatically routed in the same way

:-- | --
:-- | --
`pages/blog/first-post.js` | <pur>`/blog/first-post`</pur>
`pages/dashboard/settings/username.js` | <pur>`/dashboard/settings/username`</pur>
<!--rehype:className=style-list-->

dynamic routing

:-- | --
:-- | --
`pages/blog/[slug].js` | <pur>`/blog/:slug`</pur> (<yel>`/blog/hello-world`</yel>)
`pages/[username]/settings.js` | <pur>`/:username/settings`</pur> (<yel>`/foo/settings`</yel>)
`pages/post/[...all].js` | <pur>`/post/*`</pur> (<yel>`/post/2020/id/title`</yel>)
<!--rehype:className=style-list-->

### Pages with dynamic routing

If you create a file called `pages/posts/[pid].js` then it will be accessible at `posts/1`, `posts/2` etc.

```jsx
import { useRouter } from 'next/router'

const Post = () => {
  const router = useRouter()
  const { pid } = router.query

  return <p>Post: {pid}</p>
}

export default Post
```

Use `useRouter` to get the dynamic routing parameter `pid`

### Links between pages
<!--rehype:wrap-class=row-span-2-->

```jsx
import Link from 'next/link'

export default function Home() {
  return (
    <ul>
      <li>
        <Link href="/">Home</Link>
      </li>
      <li>
        <Link href="/about">About us</Link>
      </li>
      <li>
        <Link href="/blog/hello-world">
          blog post
        </Link>
      </li>
    </ul>
  )
}
```

---

:-- | --
:-- | --
`/` | <pur>`pages/index.js`</pur>
`/about` | <pur>`pages/about.js`</pur>
`/blog/hello-world` | <pur>`pages/blog/[slug].js`</pur>

### Link to dynamic path

```jsx
import Link from 'next/link'

export default function Posts({ posts }) {
  return (
    <Link href={`/blog/${encodeURIComponent(post.slug)}`}>
      title
    </Link>
  )
}
```

### URL object

```jsx
import Link from 'next/link'

export default function Posts({ posts }) {
  return (
    <Link
      href={{
        pathname: '/blog/[slug]',
        query: { slug: posts.slug },
      }}
    >
      title
    </Link>
  )
}
```

### Dynamic routing
<!--rehype:wrap-class=row-span-2-->

Consider the following page `pages/post/[pid].js`:

```jsx
import { useRouter } from 'next/router'

const Post = () => {
  const router = useRouter()
  const { pid } = router.query

  return <p>Post: {pid}</p>
}

export default Post
```

Client navigation to dynamic routes is handled by `next/link`

```jsx
import Link from 'next/link'

export default function Home() {
  return (
    <div>
      <Link href="/post/abc">
        Go to pages/post/[pid].js
      </Link>
      <Link href="/post/abc?foo=bar">
        Also go to pages/post/[pid].js
      </Link>
      <Link href="/post/abc/a-comment">
        Go to pages/post/[pid]/[comment].js
      </Link>
    </div>
  )
}
```

### Multiple dynamic routes

Works the same way. The page `pages/post/[pid]/[comment].js` will match the route `/post/abc/a-comment` and its query object will be:

```js
{ "pid": "abc", "comment": "a-comment" }
```

### Capture all routes

Dynamic routing can be extended to capture all paths by adding three dots (`...`) within brackets, `pages/post/[...slug].js` matches `/post/a` and also ` /post/a/b`, `/post/a/b/c`, etc.

```js
// /post/a
{ "slug": ["a"] }

// /post/a/b
{ "slug": ["a", "b"] }
```

### Optional capture all routes

Using `[[...slug]]`, `pages/post/[[...slug]].js` will match `/post`, `/post/a`, `/post/a/b` wait

```js
// GET `/post` (empty object)
{ }
// `GET /post/a` (single-element array)
{ "slug": ["a"] }
// `GET /post/a/b` (multi-element array)
{ "slug": ["a", "b"] }
```

### Event execution adjustment page

```jsx
import { useRouter } from 'next/router'

export default function ReadMore() {
  const router = useRouter()

  return (
    <button
      onClick={() => router.push('/about')}
    >
      Click here to read more
    </button>
  )
}
```

### Shallow routing
<!--rehype:wrap-class=col-span-2-->

```jsx
import { useEffect } from 'react'
import { useRouter } from 'next/router'

//The current URL is "/"
export default function Page() {
  const router = useRouter()

  useEffect(() => {
    //Always navigate after first render
    router.push('/?counter=10', undefined, { shallow: true })
  }, [])

  useEffect(() => {
    // counter has changed!
  }, [router.query.counter])
}
```

#### Precautions

Shallow routing only works on URL changes in the current page. For example, let's say we have another page called `pages/about.js` and you run the following command:

```jsx
router.push('/?counter=10', '/about?counter=10', { shallow: true })
```

Since this is a new page, it unloads the current page, loads the new page and waits for the data to be fetched, even if we ask for shallow routing

See also
---

- [Next.js Documentation](https://nextjs.org/docs/getting-started)
