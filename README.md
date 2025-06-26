
# Full-Stack ERP Software with `next.js 15`

This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

It includes integration of **Dark Mode support** using [shadcn/ui](https://ui.shadcn.com) and [`next-themes`](https://github.com/pacocoursey/next-themes).

---

## 🚀 Getting Started

First, install dependencies and start the development server:

```bash
npm install
npm run dev
```

Or use:

```bash
yarn dev
# or
pnpm dev
# or
bun dev
```

Open your browser and visit:  
👉 [http://localhost:3000](http://localhost:3000)

---

## 📂 Project Structure

- Main editable page: `app/page.js`
- Font Optimization: Uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) for [Geist](https://vercel.com/font)

---

## 🌗 Dark Mode Setup with `shadcn/ui`

### 1. Install `next-themes`
```bash
npm install next-themes
```

### 2. Create a Theme Provider

**`components/theme-provider.jsx`**
```jsx
"use client"

import * as React from "react"
import { ThemeProvider as NextThemesProvider } from "next-themes"

export function ThemeProvider({ children, ...props }) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
```

### 3. Add `ThemeProvider` in your `RootLayout`

```tsx
import { ThemeProvider } from "@/components/theme-provider"

export default function RootLayout({ children }) {
  return (
    <html lang="en" suppressHydrationWarning>
      <head />
      <body>
        <ThemeProvider
          attribute="class"
          defaultTheme="system"
          enableSystem
          disableTransitionOnChange
        >
          {children}
        </ThemeProvider>
      </body>
    </html>
  )
}
```
###### **`suppressHydrationWarning`**
```
The "suppressHydrationWarning" prop is an escape hatch provided by the React DOM package to silence hydration warnings in specific cases where developers are aware of the unavoidable hydration mismatch errors and have deemed them harmless.
```

###### **`suppressHydrationWarning`**
```
**`"disableTransitionOnChange"`** helps to prevent annoying animations or flickers when you switch between light and dark modes.
```

### 4. You can use it directly in header or wherever you want just paste the code there. But here i created a new component named as **`components/ui/mode-toggle.jsx`**.

**`components/ui/mode-toggle.jsx`**
```jsx
"use client"

import * as React from "react"
import { Moon, Sun } from "lucide-react"
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
          <Sun className="h-5 w-5 rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
          <Moon className="absolute h-5 w-5 rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
          <span className="sr-only">Toggle theme</span>
        </Button>
      </DropdownMenuTrigger>
      <DropdownMenuContent align="end">
        <DropdownMenuItem onClick={() => setTheme("light")}>Light</DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("dark")}>Dark</DropdownMenuItem>
        <DropdownMenuItem onClick={() => setTheme("system")}>System</DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  )
}
```

### 5. Use `<ModeToggle />` in Your `Header` or `navbar`. Here I am using it in my **`components/site-header.jsx`**. 

**Example: `components/site-header.jsx`**
```tsx
import { Button } from "@/components/ui/button"
import { Separator } from "@/components/ui/separator"
import { SidebarTrigger } from "@/components/ui/sidebar"
import { ModeToggle } from "./ui/mode-toggle"

export function SiteHeader() {
  return (
    <header className="flex items-center gap-2 border-b px-4 h-14">
      <SidebarTrigger />
      <Separator orientation="vertical" className="mx-2 h-4" />
      <h1 className="text-base font-medium">Documents</h1>
      <div className="ml-auto flex items-center gap-2">
        <ModeToggle />
        <Button variant="ghost" asChild size="sm" className="hidden sm:flex">
          <a
            href="https://github.com/shadcn-ui/ui/tree/main/apps/v4/app/(examples)/dashboard"
            rel="noopener noreferrer"
            target="_blank"
          >
            GitHub
          </a>
        </Button>
      </div>
    </header>
  )
}
```

---

## 📚 Learn More

- [Next.js Documentation](https://nextjs.org/docs)  
- [Learn Next.js (official tutorial)](https://nextjs.org/learn)  
- [shadcn/ui Documentation](https://ui.shadcn.com/docs) 
- [Dark Mode Tutorial](https://ui.shadcn.com/docs/dark-mode/next)
- [next-themes GitHub](https://github.com/pacocoursey/next-themes)  

---

## 🛠️ Tech Stack

- **Next.js (App Router)**
- **shadcn/ui (Dark mode + UI components)**
- **Tailwind CSS**
- **next-themes**

---

Made with ❤️ by Vikas
