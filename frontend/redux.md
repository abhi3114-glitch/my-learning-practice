# Redux

## Overview
Redux is a predictable state container for JavaScript apps. It helps manage global application state with a unidirectional data flow.

## Core Concepts

### Principles
1. **Single source of truth** - One store for all state
2. **State is read-only** - Only actions can change state
3. **Pure reducers** - Changes made with pure functions

### Redux Toolkit (Modern Redux)

#### Store Setup
```typescript
// store/store.ts
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';
import userReducer from './userSlice';

export const store = configureStore({
  reducer: {
    counter: counterReducer,
    user: userReducer,
  },
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

#### Slices
```typescript
// store/counterSlice.ts
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface CounterState {
  value: number;
  status: 'idle' | 'loading' | 'failed';
}

const initialState: CounterState = {
  value: 0,
  status: 'idle',
};

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action: PayloadAction<number>) => {
      state.value += action.payload;
    },
    reset: () => initialState,
  },
});

export const { increment, decrement, incrementByAmount, reset } = counterSlice.actions;
export default counterSlice.reducer;
```

#### Async Thunks
```typescript
// store/userSlice.ts
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

interface User {
  id: number;
  name: string;
  email: string;
}

interface UserState {
  data: User | null;
  loading: boolean;
  error: string | null;
}

export const fetchUser = createAsyncThunk(
  'user/fetchUser',
  async (userId: number, { rejectWithValue }) => {
    try {
      const response = await fetch(`/api/users/${userId}`);
      if (!response.ok) throw new Error('Failed to fetch');
      return response.json();
    } catch (error) {
      return rejectWithValue(error.message);
    }
  }
);

const userSlice = createSlice({
  name: 'user',
  initialState: { data: null, loading: false, error: null } as UserState,
  reducers: {
    clearUser: (state) => {
      state.data = null;
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchUser.pending, (state) => {
        state.loading = true;
        state.error = null;
      })
      .addCase(fetchUser.fulfilled, (state, action) => {
        state.loading = false;
        state.data = action.payload;
      })
      .addCase(fetchUser.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload as string;
      });
  },
});
```

### Typed Hooks
```typescript
// store/hooks.ts
import { TypedUseSelectorHook, useDispatch, useSelector } from 'react-redux';
import type { RootState, AppDispatch } from './store';

export const useAppDispatch = () => useDispatch<AppDispatch>();
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;
```

### Provider Setup
```tsx
// App.tsx or _app.tsx
import { Provider } from 'react-redux';
import { store } from './store/store';

function App({ children }) {
  return (
    <Provider store={store}>
      {children}
    </Provider>
  );
}
```

### Using in Components
```tsx
import { useAppSelector, useAppDispatch } from './store/hooks';
import { increment, decrement, incrementByAmount } from './store/counterSlice';
import { fetchUser } from './store/userSlice';

function Counter() {
  const count = useAppSelector((state) => state.counter.value);
  const dispatch = useAppDispatch();
  
  return (
    <div>
      <span>{count}</span>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
      <button onClick={() => dispatch(incrementByAmount(5))}>+5</button>
    </div>
  );
}

function UserProfile({ userId }) {
  const { data: user, loading, error } = useAppSelector((state) => state.user);
  const dispatch = useAppDispatch();
  
  useEffect(() => {
    dispatch(fetchUser(userId));
  }, [userId, dispatch]);
  
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  if (!user) return null;
  
  return <div>{user.name}</div>;
}
```

### Selectors
```typescript
// store/selectors.ts
import { createSelector } from '@reduxjs/toolkit';
import { RootState } from './store';

const selectTodos = (state: RootState) => state.todos.items;
const selectFilter = (state: RootState) => state.todos.filter;

// Memoized selector
export const selectFilteredTodos = createSelector(
  [selectTodos, selectFilter],
  (todos, filter) => {
    switch (filter) {
      case 'completed':
        return todos.filter(t => t.completed);
      case 'active':
        return todos.filter(t => !t.completed);
      default:
        return todos;
    }
  }
);
```

### RTK Query
```typescript
// store/api.ts
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const api = createApi({
  reducerPath: 'api',
  baseQuery: fetchBaseQuery({ baseUrl: '/api' }),
  tagTypes: ['User', 'Post'],
  endpoints: (builder) => ({
    getUsers: builder.query<User[], void>({
      query: () => 'users',
      providesTags: ['User'],
    }),
    getUser: builder.query<User, number>({
      query: (id) => `users/${id}`,
      providesTags: (result, error, id) => [{ type: 'User', id }],
    }),
    createUser: builder.mutation<User, Partial<User>>({
      query: (body) => ({
        url: 'users',
        method: 'POST',
        body,
      }),
      invalidatesTags: ['User'],
    }),
  }),
});

export const { useGetUsersQuery, useGetUserQuery, useCreateUserMutation } = api;

// Usage in component
function UserList() {
  const { data: users, isLoading, error } = useGetUsersQuery();
  const [createUser] = useCreateUserMutation();
  
  if (isLoading) return <p>Loading...</p>;
  
  return (
    <ul>
      {users?.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

## Best Practices

1. Use **Redux Toolkit** (not vanilla Redux)
2. **Normalize state** for complex data
3. Use **selectors** for derived state
4. Keep **UI state local** when possible
5. Use **RTK Query** for data fetching
6. **Type everything** with TypeScript
7. Use **Redux DevTools** for debugging

## Resources
- Redux Toolkit Documentation
- Redux Style Guide
- Mark Erikson's Blog
