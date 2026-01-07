# Getting started with Speed Insights

This guide will help you get started with using Vercel Speed Insights on your project, showing you how to enable it, add the package to your project, deploy your app to Vercel, and view your data in the dashboard.

To view instructions on using the Vercel Speed Insights in your project for your framework, use the **Choose a framework** dropdown on the right (at the bottom in mobile view).

## Prerequisites

- A Vercel account. If you don't have one, you can [sign up for free](https://vercel.com/signup).
- A Vercel project. If you don't have one, you can [create a new project](https://vercel.com/new).
- The Vercel CLI installed. If you don't have it, you can install it using the following command:
  ```bash
  # Using pnpm
  pnpm i vercel
  
  # Using yarn
  yarn i vercel
  
  # Using npm
  npm i vercel
  
  # Using bun
  bun i vercel
  ```

## Getting Started

### Enable Speed Insights in Vercel

On the [Vercel dashboard](/dashboard), select your Project followed by the **Speed Insights** tab. You can also select the button below to be taken there. Then, select **Enable** from the dialog.

> **💡 Note:** Enabling Speed Insights will add new routes (scoped at `/_vercel/speed-insights/*`) after your next deployment.

### Add `@vercel/speed-insights` to your project

Using the package manager of your choice, add the `@vercel/speed-insights` package to your project:

```bash
# Using pnpm
pnpm i @vercel/speed-insights

# Using yarn
yarn i @vercel/speed-insights

# Using npm
npm i @vercel/speed-insights

# Using bun
bun i @vercel/speed-insights
```

> **Note:** When using the HTML implementation, there is no need to install the `@vercel/speed-insights` package.

### Add the `SpeedInsights` component to your app

#### For Vite + React Applications

The `SpeedInsights` component is a wrapper around the tracking script, offering more seamless integration with React.

Add the following component to your main app file:

```tsx filename="src/App.tsx"
import { SpeedInsights } from '@vercel/speed-insights/react';

function App() {
  return (
    <>
      {/* Your app components */}
      <SpeedInsights />
    </>
  );
}

export default App;
```

```jsx filename="src/App.jsx"
import { SpeedInsights } from '@vercel/speed-insights/react';

function App() {
  return (
    <>
      {/* Your app components */}
      <SpeedInsights />
    </>
  );
}

export default App;
```

#### Alternative Frameworks

**For Next.js (Pages Router):**
```tsx filename="pages/_app.tsx"
import type { AppProps } from 'next/app';
import { SpeedInsights } from '@vercel/speed-insights/next';

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <>
      <Component {...pageProps} />
      <SpeedInsights />
    </>
  );
}

export default MyApp;
```

**For Next.js (App Router):**
```tsx filename="app/layout.tsx"
import { SpeedInsights } from "@vercel/speed-insights/next";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <head>
        <title>Next.js</title>
      </head>
      <body>
        {children}
        <SpeedInsights />
      </body>
    </html>
  );
}
```

**For Remix:**
```tsx filename="app/root.tsx"
import { SpeedInsights } from '@vercel/speed-insights/remix';

export default function App() {
  return (
    <html lang="en">
      <body>
        {/* ... */}
        <SpeedInsights />
      </body>
    </html>
  );
}
```

**For SvelteKit:**
```ts filename="src/routes/+layout.ts"
import { injectSpeedInsights } from "@vercel/speed-insights/sveltekit";

injectSpeedInsights();
```

**For Vue:**
```vue filename="src/App.vue"
<script setup lang="ts">
import { SpeedInsights } from '@vercel/speed-insights/vue';
</script>

<template>
  <SpeedInsights />
</template>
```

**For Nuxt:**
```vue filename="layouts/default.vue"
<script setup lang="ts">
import { SpeedInsights } from '@vercel/speed-insights/vue';
</script>

<template>
  <SpeedInsights />
</template>
```

**For Astro:**
```astro filename="BaseHead.astro"
---
import SpeedInsights from '@vercel/speed-insights/astro';
const { title, description } = Astro.props;
---
<title>{title}</title>
<meta name="title" content={title} />
<meta name="description" content={description} />

<SpeedInsights />
```

Optionally, you can remove sensitive information from the URL by adding a `speedInsightsBeforeSend` function:

```astro filename="BaseHead.astro"
---
import SpeedInsights from '@vercel/speed-insights/astro';
const { title, description } = Astro.props;
---
<title>{title}</title>
<meta name="title" content={title} />
<meta name="description" content={description} />

<script is:inline>
  function speedInsightsBeforeSend(data){
    console.log("Speed Insights before send", data)
    return data;
  }
</script>
<SpeedInsights />
```

**For HTML (Static):**
```html filename="index.html"
<script>
  window.si = window.si || function () { (window.siq = window.siq || []).push(arguments); };
</script>
<script defer src="/_vercel/speed-insights/script.js"></script>
```

**For Other Frameworks:**
```ts filename="main.ts"
import { injectSpeedInsights } from "@vercel/speed-insights";

injectSpeedInsights();
```

### Deploy your app to Vercel

You can deploy your app to Vercel's global [CDN](/docs/cdn) by running the following command from your terminal:

```bash
vercel deploy
```

Alternatively, you can [connect your project's git repository](/docs/git#deploying-a-git-repository), which will enable Vercel to deploy your latest pushes and merges to main.

Once your app is deployed, it's ready to begin tracking performance metrics.

> **💡 Note:** If everything is set up correctly, you should be able to find the `/_vercel/speed-insights/script.js` script inside the body tag of your page.

### View your data in the dashboard

Once your app is deployed, and users have visited your site, you can view the data in the dashboard.

To do so, go to your [dashboard](/dashboard), select your project, and click the **Speed Insights** tab.

After a few days of visitors, you'll be able to start exploring your metrics. For more information on how to use Speed Insights, see [Using Speed Insights](/docs/speed-insights/using-speed-insights).

Learn more about how Vercel supports [privacy and data compliance standards](/docs/speed-insights/privacy-policy) with Vercel Speed Insights.

## Next steps

Now that you have Vercel Speed Insights set up, you can explore the following topics to learn more:

- [Learn how to use the `@vercel/speed-insights` package](/docs/speed-insights/package)
- [Learn about metrics](/docs/speed-insights/metrics)
- [Read about privacy and compliance](/docs/speed-insights/privacy-policy)
- [Explore pricing](/docs/speed-insights/limits-and-pricing)
- [Troubleshooting](/docs/speed-insights/troubleshooting)
