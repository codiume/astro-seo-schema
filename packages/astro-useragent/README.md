# 🚀 Astro UserAgent

[![version][version-badge]][npm]
[![downloads][downloads-badge]][npm]
[![github actions][github-actions-badge]][github-actions]
[![typescript][typescript-badge]][typescript]
[![makepr][makepr-badge]][makepr]

Astro Useragent is a simple helper for parsing `user-agent` header strings for browser matching inside your Astro API routes / Pages, when using [SSR Mode][astro-ssr]

> **Note**
>
> Due to the nature of Astro being an SSG by trade, This package only works when used with astro in [SSR Mode][astro-ssr].

## 📦 Installation

First, install the `astro-useragent` package using your package manager. (If you aren’t sure which package manager you’re using, run the first command.)

```bash
# Using NPM
npm install astro-useragent
# Using Yarn
yarn add astro-useragent
# Using PNPM
pnpm install astro-useragent
```

## 🥑 Usage

### Usage with Astro pages

To parse a `useragent` string inside any of your top level Astro pages, import `useUserAgent` and then use it inside the frontmatter section:

```jsx
---
import { useUserAgent } from "astro-useragent";

const uaString = Astro.request.headers.get('user-agent');
const { isMobile } = useUserAgent(uaString);
---

<div>
    <p>{ ua.source }</p>
    { ua.isMobile ? (
    <MobileContent />
    ) : (
    <DesktopContent />
    ) }
</div>
```

> **Note**
>
> Read more about Astro request headers here: [Astro Docs](https://docs.astro.build/en/guides/server-side-rendering/#astrorequestheaders)

### Usage with Astro API routes

`useUserAgent` can also be used inside your API routes, to perfom some logic based on client browser.

In the example below, an API route is used to redirect a user to a diffrent mobile page is he is using a mobile client, otherwise serve the normal content.

```javascript
import { useUserAgent } from 'astro-useragent';

export async function get({ request }) {
  const uaString = request.headers.get('user-agent');
  const { isMobile } = useUserAgent(uaString);

  if (isMobile) {
    return Response.redirect('mobile.example.com', 307);
  }

  return new Response(JSON.stringify({ data: [...] }), {
    status: 200
  });
}
```

> **Note**
>
> Read more about Astro API routes here: [Astro Docs](https://docs.astro.build/en/guides/server-side-rendering/#api-routes)

### Parsed object interface

The parsed `UserAgent` object will have the following interface:

```typescript
export interface UserAgent {
  readonly source: string; // original user agent string.
  readonly deviceType: string | null;
  readonly deviceVendor: string | null;
  readonly os: string;
  readonly osVersion: number;
  readonly browser: string;
  readonly browserVersion: number;
  readonly engine: string;
  readonly engineVersion: number;
  readonly isIphone: boolean;
  readonly isIpad: boolean;
  readonly isMobile: boolean;
  readonly isTablet: boolean;
  readonly isDesktop: boolean;
  readonly isChrome: boolean;
  readonly isFirefox: boolean;
  readonly isSafari: boolean;
  readonly isIE: boolean;
  readonly isEdge: boolean;
  readonly isOpera: boolean;
  readonly isMac: boolean;
  readonly isChromeOS: boolean;
  readonly isWindows: boolean;
  readonly isIos: boolean;
  readonly isAndroid: boolean;
}
```

## Changelog

Please see the [Changelog](CHANGELOG.md) for more information on what has changed recently.

## Acknowledgements

`astro-useragent` is _heavily_ inspired by [next-useragent][next-useragent] and all the amazing work the [Tsuyoshi Tokuda][tokuda109] and the comunity is doing developing it.

[astro-ssr]: https://docs.astro.build/en/guides/server-side-rendering
[npm]: https://npmjs.com/package/astro-useragent
[next-useragent]: https://github.com/tokuda109/next-useragent
[tokuda109]: https://github.com/tokuda109

<!-- Readme Badges -->

[version-badge]: https://img.shields.io/npm/v/astro-useragent.svg
[downloads-badge]: https://img.shields.io/npm/dt/astro-useragent
[github-actions]: https://github.com/codiume/orbit/actions
[github-actions-badge]: https://github.com/codiume/orbit/actions/workflows/node.js.yml/badge.svg
[typescript]: https://www.typescriptlang.org/dt/search?search=astro-useragent
[typescript-badge]: https://img.shields.io/npm/types/astro-useragent
[makepr]: https://makeapullrequest.com
[makepr-badge]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square?style=flat
