# Vite

## Overview
Vite is a next-generation frontend build tool that provides a faster and leaner development experience.

## Getting Started

```bash
# Create new project
npm create vite@latest my-app -- --template react-ts

# Templates: vanilla, vue, react, preact, lit, svelte
# Add -ts for TypeScript variant

cd my-app
npm install
npm run dev
```

## Configuration

```javascript
// vite.config.ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  
  // Dev server
  server: {
    port: 3000,
    open: true,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
      },
    },
  },
  
  // Build options
  build: {
    outDir: 'dist',
    sourcemap: true,
    minify: 'terser',
  },
  
  // Path aliases
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
      '@components': path.resolve(__dirname, './src/components'),
    },
  },
  
  // Environment variables
  define: {
    'process.env': process.env,
  },
});
```

## Environment Variables

```env
# .env
VITE_API_URL=http://localhost:8080

# .env.production
VITE_API_URL=https://api.example.com
```

```typescript
// Usage (must prefix with VITE_)
const apiUrl = import.meta.env.VITE_API_URL;
const mode = import.meta.env.MODE;  // 'development' or 'production'
const isProd = import.meta.env.PROD;
const isDev = import.meta.env.DEV;
```

## Features

### Hot Module Replacement (HMR)
```typescript
// Automatic with React/Vue plugins
// Manual HMR:
if (import.meta.hot) {
  import.meta.hot.accept('./module.js', (newModule) => {
    // Handle update
  });
}
```

### CSS
```typescript
// Import CSS
import './style.css';

// CSS Modules
import styles from './component.module.css';
<div className={styles.container}>

// PostCSS (auto-detected from postcss.config.js)
// Sass/SCSS (install sass)
import './style.scss';
```

### Static Assets
```typescript
// Import as URL
import imgUrl from './image.png';

// Import as string (raw)
import content from './file.txt?raw';

// Import as worker
import Worker from './worker.js?worker';
```

### JSON
```typescript
// Import entire JSON
import data from './data.json';

// Named imports
import { name, version } from './package.json';
```

## Plugins

```javascript
// vite.config.ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import legacy from '@vitejs/plugin-legacy';
import compression from 'vite-plugin-compression';

export default defineConfig({
  plugins: [
    react(),
    legacy({
      targets: ['defaults', 'not IE 11'],
    }),
    compression({
      algorithm: 'gzip',
    }),
  ],
});
```

## Build Optimization

```javascript
// vite.config.ts
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          utils: ['lodash', 'date-fns'],
        },
      },
    },
    chunkSizeWarningLimit: 1000,
  },
});
```

## Scripts

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint src --ext .ts,.tsx"
  }
}
```

## Best Practices

1. Use **path aliases** for cleaner imports
2. Configure **proxy** for API development
3. Use **environment variables** for config
4. Enable **sourcemaps** in production
5. Use **code splitting** for large apps
6. Leverage **pre-bundling** for dependencies

## Resources
- Vite Documentation
- Awesome Vite (plugins list)
- Vite GitHub Discussions
