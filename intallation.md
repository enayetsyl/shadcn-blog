# Getting Started with shadcn UI: Installation Guide for Next.js, Vite, and Remix

Welcome back! In this second blog of our shadcn UI series, we’ll walk through setting up shadcn UI in three popular frameworks: Next.js, Vite, and Remix. While shadcn UI works seamlessly with JavaScript, our examples will use TypeScript for additional type safety and development ease.


## Installation for Next.js

### Step 1: Create a New Next.js Project

If you’re starting from scratch, create a new Next.js project by running:

```bash
npx create-next-app@latest my-shadcn-app --typescript
```

Or, if you already have an existing project, navigate to your project folder.

### Step 2: Install shadcn UI

Initialize shadcn UI in your Next.js project by running:

```bash
npx shadcn@latest init
```

This will prompt you to configure settings for components.json. Here are the options:

- Style: Choose your base style (e.g., New York).
- Color: Select a base color, like Zinc.
- CSS Variables: Opt to use CSS variables by choosing "yes" for more flexibility in theming.

### Shortcut: Use the -d flag for default settings:

```bash
npx shadcn@latest init -d
```

## Installation for Vite

### Step 1: Create a New Vite Project

Set up a Vite project with TypeScript support

```bash
npm create vite@latest my-shadcn-app --template react-ts
```

Navigate to your project folder:

```bash
cd my-shadcn-app
```

### Step 2: Install Tailwind CSS

Install Tailwind and its dependencies, then configure it:

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Add Tailwind’s directives to your main CSS file (usually src/index.css):

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Update the tailwind.config.js content path:

```javascript
module.exports = {
  content: ["./index.html", "./src/**/*.{ts,tsx,js,jsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

### Step 3: Initialize shadcn UI

Run the following to initialize shadcn UI:

```bash
npx shadcn@latest init
```

### Shortcut: To bypass prompts, use the -d flag as we did in Next.js:

```bash
npx shadcn@latest init -d
```

After initializing the project and setting up Tailwind, you’ll need to adjust a few files to make sure your TypeScript setup works seamlessly with shadcn UI.

### Step 4: Edit tsconfig.json and tsconfig.app.json
Vite projects often use two TypeScript configuration files for more granular control.

1. Edit tsconfig.json

Add baseUrl and paths properties to configure module resolution:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

2. Edit tsconfig.app.json
 
In tsconfig.app.json, add the same baseUrl and paths properties:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

### Step 5: Update vite.config.ts
Add the following to vite.config.ts to set up an alias for @ to reference the src directory:

```typescript
import path from "path";
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

This setup helps Vite and TypeScript resolve paths using @/ as an alias for the src directory, making imports easier and reducing the risk of errors.

## Installation for Remix

### Step 1: Create a New Remix Project

Create a new Remix project with:

```bash
npx create-remix@latest my-shadcn-app
```

Navigate to the project directory

```bash
cd my-shadcn-app
```

### Step 2: Install Tailwind CSS

Install Tailwind CSS and add it to your Remix project

```bash
npm install -D tailwindcss@latest autoprefixer@latest
```

Update your postcss.config.js to include Tailwind:

```javascript
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

Link your tailwind.css in app/root.tsx:

```typescript
import styles from "./tailwind.css?url";

export const links: LinksFunction = () => [
  { rel: "stylesheet", href: styles },
];
```

### Step 3: Initialize shadcn UI

Set up shadcn UI with:

```bash
npx shadcn@latest init
```

Configure the components as per your preferences. You’ll encounter similar prompts for style, color, and CSS variables as in the Next.js setup.

### Shortcut: For a quicker setup

```bash
npx shadcn@latest init -d
```

With this setup, you’re ready to start building modern, responsive UIs with shadcn across your Next.js, Vite, and Remix projects. Each installation process is straightforward, and the optional -d flag simplifies the setup further by applying default configurations.

In the next post, we’ll explore components.json and how it enables customizability in shadcn UI. Stay tuned!







































