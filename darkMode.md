# Implementing Theming in shadcn UI: Next.js and Vite React

In this post, we’ll explore how to set up light and dark themes in shadcn UI for both Next.js and Vite React applications. We’ll cover the setup process, show how to toggle between themes, and discuss where to place the toggle button for best usability.


## Part 1: Setting Up Theming in Next.js

### Step 1: Install next-themes

We’ll use the next-themes package to enable dark mode switching in a Next.js project. Start by installing the package:

```bash
npm install next-themes
```

### Step 2: Create the Theme Provider

Create a theme-provider.tsx component to wrap around the application and manage theme states.

```typescript
// components/theme-provider.tsx
"use client";

import * as React from "react";
import { ThemeProvider as NextThemesProvider } from "next-themes";
import { type ThemeProviderProps } from "next-themes/dist/types";

export function ThemeProvider({ children, ...props }: ThemeProviderProps) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>;
}
```

### Step 3: Wrap the Root Layout

In the root layout file (app/layout.tsx), wrap the ThemeProvider around the application content. This sets the theme globally.

```typescript
// app/layout.tsx
import { ThemeProvider } from "@/components/theme-provider";

export default function RootLayout({ children }) {
  return (
    <html lang="en" suppressHydrationWarning>
      <head />
      <body>
        <ThemeProvider attribute="class" defaultTheme="system" enableSystem disableTransitionOnChange>
          {children}
        </ThemeProvider>
      </body>
    </html>
  );
}
```

### Explanation of Key Props

- attribute="class": Adds the theme class (e.g., dark or light) to the html tag.
- defaultTheme="system": Sets the theme based on the user’s system preferences.
- enableSystem: Enables automatic theme switching based on system settings.
- disableTransitionOnChange: Prevents transition effects when switching themes.

Best Place for the Toggle Button: Placing the toggle button in a fixed location, such as a header or settings dropdown, ensures it’s accessible on all pages.

### Step 4: Implement the Mode Toggle

Now, let’s create a toggle button using a dropdown menu to switch between light, dark, and system themes.

```typescript
"use client"

import * as React from "react"
import { Moon, MoonIcon, Sun } from "lucide-react"
import { useTheme } from "next-themes"

import { Button } from "@/components/ui/button"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"

export function ModeToggle() {
  const { setTheme } = useTheme()

  return (
    <DropdownMenu>
      <DropdownMenuTrigger asChild>
        <Button variant="outline" size="icon">
          <Sun className="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
          <Moon className="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
          <span className="sr-only">Toggle theme</span>
        </Button>
      </DropdownMenuTrigger>
      <DropdownMenuContent align="end">
        <DropdownMenuItem onClick={() => setTheme("light")}>
          Light
        </DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("dark")}>
          Dark
        </DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("system")}>
          System
        </DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  )
}

```

### Explanation of setTheme("system")

The setTheme("system") option allows the theme to follow the user’s operating system preferences. This is especially useful if the user wants their app theme to match their system’s light/dark mode automatically.

### Customizable Parts

  - Button Styles: Modify the Button component style, like variant and size, to match your design.
  - Icon Transitions: Adjust the transition classes for a smooth icon change effect.
  - Themes: You can customize the colors, typography, and other aspects in Tailwind’s config or by adjusting CSS variables for each theme.


## Part 2: Setting Up Theming in Vite React

For Vite React, we’ll follow a similar structure, but with a custom context setup for the theme provider.

### Step 1: Create the Theme Provider

Create a theme-provider.tsx file to handle theme state management.

```typescript
// components/theme-provider.tsx
import * as React from "react";
import { useState, useEffect, createContext, useContext } from "react";

interface ThemeContextType {
  theme: string;
  setTheme: (theme: string) => void;
}

const ThemeProviderContext = createContext<ThemeContextType | undefined>(undefined);

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState(localStorage.getItem("vite-ui-theme") || "dark");

  useEffect(() => {
    localStorage.setItem("vite-ui-theme", theme);
    document.documentElement.className = theme;
  }, [theme]);

  return (
    <ThemeProviderContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeProviderContext.Provider>
  );
};

export const useTheme = () => {
  const context = useContext(ThemeProviderContext);
  if (!context) throw new Error("useTheme must be used within a ThemeProvider");
  return context;
};
```

### Explanation of Code Inside ThemeProvider
- ThemeProviderContext: Manages the theme state and makes it accessible throughout the app.
- useState for Theme: Reads the theme from localStorage initially, ensuring the selected theme persists across sessions.
- useEffect Hook: Syncs the theme with localStorage and applies it to the document’s root element (document.documentElement), allowing easy CSS-based theme changes.
- useTheme Hook: Provides a custom hook to access and set the theme from anywhere in the app.

### Step 2: Wrap the App Component
In App.tsx, wrap the entire app with the ThemeProvider.

```typescript
// App.tsx
import { ThemeProvider } from "@/components/theme-provider";

function App() {
  return (
    <ThemeProvider>
      <div> {/* App content here */} </div>
    </ThemeProvider>
  );
}

export default App;
```

### Step 3: Add a Mode Toggle

Create a mode-toggle.tsx component to switch themes.

```typescript
// components/mode-toggle.tsx
import { useTheme } from "@/components/theme-provider";
import { Button } from "@/components/ui/button";
import { Moon, Sun } from "lucide-react";
import { DropdownMenu, DropdownMenuContent, DropdownMenuItem, DropdownMenuTrigger } from "@/components/ui/dropdown-menu";

export function ModeToggle() {
  const { theme, setTheme } = useTheme();

  return (
    <DropdownMenu>
      <DropdownMenuTrigger asChild>
        <Button variant="outline" size="icon">
          <Sun className={`h-5 w-5 ${theme === "dark" ? "hidden" : ""}`} />
          <Moon className={`h-5 w-5 ${theme === "dark" ? "" : "hidden"}`} />
          <span className="sr-only">Toggle theme</span>
        </Button>
      </DropdownMenuTrigger>
      <DropdownMenuContent align="end">
        <DropdownMenuItem onClick={() => setTheme("light")}>Light</DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("dark")}>Dark</DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  );
}
```

This setup provides a complete theming solution for both Next.js and Vite React, allowing users to toggle between light and dark modes effortlessly.





















