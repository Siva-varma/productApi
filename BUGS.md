# Bugs / Issues Notes

## 1. Product API request body error

Error received:
```json
{
  "success": false,
  "message": "Cannot destructure property 'name' of 'req.body' as it is undefined."
}
```

### Root cause
The controller tries to access values from `req.body`, but the request body is not being parsed correctly.

### Required fix
Add this middleware in the Express app:
```js
app.use(express.urlencoded({ extended: true }));
```