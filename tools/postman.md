# Postman

Postman is an API development and testing platform.

## Features
- Create and save requests
- Environment variables
- Test scripts
- Collections
- Mock servers

## Test Scripts
```javascript
pm.test("Status is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has data", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('data');
});
```
