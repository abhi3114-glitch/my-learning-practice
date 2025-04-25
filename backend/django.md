# Django

## Overview
Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design.

## Project Structure
```
myproject/
├── manage.py
├── myproject/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── myapp/
    ├── models.py
    ├── views.py
    ├── urls.py
    └── templates/
```

## Models
```python
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['-created_at']
```

## Views
```python
from django.http import JsonResponse
from django.views import View

class UserView(View):
    def get(self, request):
        users = User.objects.all()
        return JsonResponse(list(users.values()), safe=False)

    def post(self, request):
        data = json.loads(request.body)
        user = User.objects.create(**data)
        return JsonResponse({'id': user.id}, status=201)
```

## Django REST Framework
```python
from rest_framework import serializers, viewsets

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = '__all__'

class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer
```

## Best Practices
1. Use **Django ORM** for database operations
2. Implement **class-based views**
3. Use **Django REST Framework** for APIs
4. Apply **migrations** carefully

## Resources
- Django Documentation
- Django REST Framework
