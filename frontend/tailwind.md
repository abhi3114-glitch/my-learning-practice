# Tailwind CSS

## Overview
Tailwind CSS is a utility-first CSS framework for rapidly building custom designs without leaving your HTML.

## Installation
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## Configuration
```javascript
// tailwind.config.js
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: '#3498db',
        secondary: '#2ecc71',
      },
      spacing: {
        '128': '32rem',
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
      },
    },
  },
  plugins: [],
};
```

## Core Utilities

### Layout
```html
<!-- Display -->
<div class="block">Block</div>
<div class="hidden">Hidden</div>
<div class="flex">Flexbox</div>
<div class="grid">Grid</div>

<!-- Container -->
<div class="container mx-auto px-4">Centered container</div>

<!-- Flexbox -->
<div class="flex flex-row justify-between items-center gap-4">
  <div class="flex-1">Item 1</div>
  <div class="flex-shrink-0">Item 2</div>
</div>

<!-- Grid -->
<div class="grid grid-cols-3 gap-4">
  <div class="col-span-2">Wide</div>
  <div>Normal</div>
</div>
```

### Spacing
```html
<!-- Padding -->
<div class="p-4">All sides</div>
<div class="px-4 py-2">Horizontal / Vertical</div>
<div class="pt-2 pr-4 pb-2 pl-4">Individual sides</div>

<!-- Margin -->
<div class="m-4">All sides</div>
<div class="mx-auto">Center horizontally</div>
<div class="mt-8 mb-4">Top and bottom</div>

<!-- Space between children -->
<div class="space-y-4">
  <div>Child 1</div>
  <div>Child 2</div>
</div>
```

### Typography
```html
<!-- Font size -->
<p class="text-xs">Extra small</p>
<p class="text-sm">Small</p>
<p class="text-base">Base</p>
<p class="text-lg">Large</p>
<p class="text-xl">Extra large</p>
<p class="text-2xl">2XL</p>

<!-- Font weight -->
<p class="font-light">Light</p>
<p class="font-normal">Normal</p>
<p class="font-medium">Medium</p>
<p class="font-semibold">Semibold</p>
<p class="font-bold">Bold</p>

<!-- Text alignment -->
<p class="text-left">Left</p>
<p class="text-center">Center</p>
<p class="text-right">Right</p>

<!-- Text color -->
<p class="text-gray-500">Gray text</p>
<p class="text-blue-600">Blue text</p>
```

### Colors & Backgrounds
```html
<!-- Background -->
<div class="bg-white">White BG</div>
<div class="bg-gray-100">Light gray</div>
<div class="bg-blue-500">Blue</div>
<div class="bg-gradient-to-r from-blue-500 to-purple-500">Gradient</div>

<!-- Opacity -->
<div class="bg-black bg-opacity-50">Semi-transparent</div>
<div class="bg-black/50">Same with slash syntax</div>
```

### Sizing
```html
<!-- Width -->
<div class="w-full">Full width</div>
<div class="w-1/2">50%</div>
<div class="w-64">16rem</div>
<div class="max-w-md">Max width</div>

<!-- Height -->
<div class="h-screen">Viewport height</div>
<div class="h-64">16rem</div>
<div class="min-h-screen">Min viewport height</div>
```

### Borders & Shadows
```html
<!-- Borders -->
<div class="border">1px border</div>
<div class="border-2">2px border</div>
<div class="border-gray-300">Gray border</div>
<div class="rounded">Small radius</div>
<div class="rounded-lg">Large radius</div>
<div class="rounded-full">Circle</div>

<!-- Shadows -->
<div class="shadow">Default shadow</div>
<div class="shadow-md">Medium shadow</div>
<div class="shadow-lg">Large shadow</div>
<div class="shadow-xl">XL shadow</div>
```

### Responsive Design
```html
<!-- Mobile first -->
<div class="w-full md:w-1/2 lg:w-1/3">
  Full on mobile, half on tablet, third on desktop
</div>

<!-- Breakpoints: sm (640px), md (768px), lg (1024px), xl (1280px), 2xl (1536px) -->
<div class="text-sm md:text-base lg:text-lg">Responsive text</div>

<div class="flex flex-col md:flex-row">Stacked on mobile, row on tablet+</div>
```

### States
```html
<!-- Hover -->
<button class="bg-blue-500 hover:bg-blue-700">Hover me</button>

<!-- Focus -->
<input class="border focus:ring-2 focus:ring-blue-500 focus:outline-none">

<!-- Active -->
<button class="active:scale-95">Press me</button>

<!-- Group hover -->
<div class="group">
  <p class="group-hover:text-blue-500">Changes on parent hover</p>
</div>

<!-- Dark mode -->
<div class="bg-white dark:bg-gray-800 text-black dark:text-white">
  Adapts to dark mode
</div>
```

### Transitions & Animations
```html
<!-- Transitions -->
<button class="transition duration-300 ease-in-out hover:scale-105">
  Smooth hover
</button>

<!-- Transform -->
<div class="transform hover:scale-110 hover:rotate-3">Transform</div>

<!-- Built-in animations -->
<div class="animate-spin">Spinning</div>
<div class="animate-pulse">Pulsing</div>
<div class="animate-bounce">Bouncing</div>
```

## Component Examples

### Button
```html
<button class="px-4 py-2 bg-blue-500 text-white rounded-lg 
               hover:bg-blue-600 active:bg-blue-700 
               transition duration-200 font-medium">
  Click me
</button>
```

### Card
```html
<div class="bg-white rounded-xl shadow-lg p-6 max-w-sm">
  <h3 class="text-xl font-bold mb-2">Card Title</h3>
  <p class="text-gray-600">Card description goes here.</p>
</div>
```

### Input
```html
<input type="text" 
       class="w-full px-4 py-2 border border-gray-300 rounded-lg
              focus:ring-2 focus:ring-blue-500 focus:border-transparent
              outline-none transition">
```

## Best Practices

1. Use **@apply** sparingly in CSS files
2. Extract **component classes** for repeated patterns
3. Use **arbitrary values** when needed: `w-[137px]`
4. Configure **theme** in tailwind.config.js
5. Use **plugins** for complex utilities
6. Enable **JIT mode** (default in v3)
7. Purge **unused styles** in production

## Resources
- Tailwind CSS Documentation
- Tailwind UI (component library)
- Headless UI (unstyled components)
