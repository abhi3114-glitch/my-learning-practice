# Next.js

## Overview
Next.js is a React framework for production that provides hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more.

## Core Concepts

### Project Structure (App Router - Next.js 13+)
```
app/
├── layout.tsx        # Root layout
├── page.tsx          # Home page
├── loading.tsx       # Loading UI
├── error.tsx         # Error UI
├── not-found.tsx     # 404 page
├── api/
│   └── route.ts      # API routes
├── dashboard/
│   ├── layout.tsx    # Nested layout
│   └── page.tsx
└── blog/
    └── [slug]/
        └── page.tsx  # Dynamic route
```

### Routing
```tsx
// app/page.tsx - Home page (/)
export default function Home() {
  return <h1>Home</h1>;
}

// app/about/page.tsx - About page (/about)
export default function About() {
  return <h1>About</h1>;
}

// app/blog/[slug]/page.tsx - Dynamic route
export default function BlogPost({ params }: { params: { slug: string } }) {
  return <h1>Post: {params.slug}</h1>;
}

// app/shop/[...slug]/page.tsx - Catch-all route
export default function Shop({ params }: { params: { slug: string[] } }) {
  return <h1>Path: {params.slug.join('/')}</h1>;
}
```

### Layouts
```tsx
// app/layout.tsx - Root layout
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <nav>Navigation</nav>
        {children}
        <footer>Footer</footer>
      </body>
    </html>
  );
}

// app/dashboard/layout.tsx - Nested layout
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <div className="dashboard">
      <Sidebar />
      <main>{children}</main>
    </div>
  );
}
```

### Data Fetching

#### Server Components (default)
```tsx
// This runs on the server
async function getData() {
  const res = await fetch('https://api.example.com/data', {
    cache: 'no-store',  // Dynamic data
    // cache: 'force-cache',  // Static (default)
    // next: { revalidate: 60 },  // ISR
  });
  return res.json();
}

export default async function Page() {
  const data = await getData();
  return <div>{data.title}</div>;
}
```

#### Client Components
```tsx
'use client';

import { useState, useEffect } from 'react';

export default function ClientComponent() {
  const [data, setData] = useState(null);
  
  useEffect(() => {
    fetch('/api/data')
      .then(res => res.json())
      .then(setData);
  }, []);
  
  return <div>{data?.title}</div>;
}
```

### API Routes
```ts
// app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const users = await getUsers();
  return NextResponse.json(users);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await createUser(body);
  return NextResponse.json(user, { status: 201 });
}

// app/api/users/[id]/route.ts
export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await getUser(params.id);
  if (!user) {
    return NextResponse.json({ error: 'Not found' }, { status: 404 });
  }
  return NextResponse.json(user);
}
```

### Server Actions
```tsx
// app/actions.ts
'use server';

import { revalidatePath } from 'next/cache';

export async function createPost(formData: FormData) {
  const title = formData.get('title');
  const content = formData.get('content');
  
  await db.post.create({ data: { title, content } });
  
  revalidatePath('/posts');
}

// app/posts/new/page.tsx
import { createPost } from '../actions';

export default function NewPost() {
  return (
    <form action={createPost}>
      <input name="title" required />
      <textarea name="content" required />
      <button type="submit">Create</button>
    </form>
  );
}
```

### Metadata
```tsx
// Static metadata
export const metadata = {
  title: 'My App',
  description: 'Description of my app',
  openGraph: {
    title: 'My App',
    description: 'Description',
    images: ['/og-image.png'],
  },
};

// Dynamic metadata
export async function generateMetadata({ params }) {
  const post = await getPost(params.slug);
  return {
    title: post.title,
    description: post.excerpt,
  };
}
```

### Loading & Error States
```tsx
// app/dashboard/loading.tsx
export default function Loading() {
  return <div className="skeleton">Loading...</div>;
}

// app/dashboard/error.tsx
'use client';

export default function Error({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

### Middleware
```ts
// middleware.ts (root level)
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // Check auth
  const token = request.cookies.get('token');
  
  if (!token && request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*', '/api/:path*'],
};
```

### Image Optimization
```tsx
import Image from 'next/image';

export default function Gallery() {
  return (
    <Image
      src="/hero.jpg"
      alt="Hero image"
      width={800}
      height={600}
      priority  // Load immediately
      placeholder="blur"
      blurDataURL="..."
    />
  );
}
```

### Environment Variables
```env
# .env.local
DATABASE_URL=postgres://...
NEXT_PUBLIC_API_URL=https://api.example.com
```

```tsx
// Server-side only
const dbUrl = process.env.DATABASE_URL;

// Client-side (must have NEXT_PUBLIC_ prefix)
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

## Best Practices

1. Use **Server Components** by default
2. Add `'use client'` only when necessary
3. Use **Server Actions** for mutations
4. Implement **loading.tsx** and **error.tsx**
5. Optimize images with **next/image**
6. Use **route groups** for organization
7. Leverage **ISR** for dynamic but cacheable content

## Resources
- Next.js Documentation
- Vercel Examples
- Lee Robinson's Blog
