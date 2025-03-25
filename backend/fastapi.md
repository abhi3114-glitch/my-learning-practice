# FastAPI

## Overview
FastAPI is a modern, fast Python web framework for building APIs with automatic OpenAPI documentation and type hints.

## Basic Setup
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = False

@app.get("/")
async def root():
    return {"message": "Hello World"}

@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}

@app.post("/items/")
async def create_item(item: Item):
    return item

# Run: uvicorn main:app --reload
```

## Path & Query Parameters
```python
@app.get("/users/{user_id}")
async def get_user(
    user_id: int,
    skip: int = 0,
    limit: int = 10,
    active: bool = True
):
    return {"user_id": user_id, "skip": skip, "limit": limit}
```

## Request Body
```python
from pydantic import BaseModel, Field
from typing import Optional, List

class User(BaseModel):
    name: str = Field(..., min_length=1)
    email: str
    age: Optional[int] = None
    tags: List[str] = []

    class Config:
        schema_extra = {
            "example": {
                "name": "John",
                "email": "john@example.com"
            }
        }

@app.post("/users/")
async def create_user(user: User):
    return user
```

## Dependency Injection
```python
from fastapi import Depends

async def get_db():
    db = Database()
    try:
        yield db
    finally:
        db.close()

@app.get("/users/")
async def get_users(db: Database = Depends(get_db)):
    return db.query(User).all()
```

## Error Handling
```python
from fastapi import HTTPException

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return items[item_id]
```

## Authentication
```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    user = get_user_from_token(token)
    return user
```

## Best Practices
1. Use **Pydantic models** for validation
2. Implement **dependency injection**
3. Use **async** functions
4. Add **type hints** everywhere
5. Structure with **routers**

## Resources
- FastAPI Documentation
