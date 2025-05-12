# Supabase

## Overview
Supabase is an open-source Firebase alternative providing PostgreSQL database, authentication, storage, and realtime subscriptions.

## Client Setup
```javascript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(
  'https://your-project.supabase.co',
  'your-anon-key'
);
```

## Database Operations
```javascript
// Select
const { data, error } = await supabase
  .from('users')
  .select('*')
  .eq('active', true)
  .order('created_at', { ascending: false })
  .limit(10);

// Insert
const { data, error } = await supabase
  .from('users')
  .insert({ name: 'John', email: 'john@example.com' })
  .select();

// Update
const { data, error } = await supabase
  .from('users')
  .update({ name: 'Jane' })
  .eq('id', 1);

// Delete
const { error } = await supabase
  .from('users')
  .delete()
  .eq('id', 1);
```

## Authentication
```javascript
// Sign up
const { user, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
});

// Sign in
const { user, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
});

// OAuth
await supabase.auth.signInWithOAuth({ provider: 'google' });

// Sign out
await supabase.auth.signOut();
```

## Realtime
```javascript
const subscription = supabase
  .channel('changes')
  .on('postgres_changes', 
    { event: '*', schema: 'public', table: 'messages' },
    (payload) => console.log(payload)
  )
  .subscribe();
```

## Storage
```javascript
const { data, error } = await supabase.storage
  .from('avatars')
  .upload('user-1.png', file);

const { data } = supabase.storage
  .from('avatars')
  .getPublicUrl('user-1.png');
```

## Best Practices
1. Use **Row Level Security (RLS)**
2. Enable **realtime** only when needed
3. Use **storage policies**

## Resources
- Supabase Documentation
