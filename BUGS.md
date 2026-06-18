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


## 2. File upload mismatch

### Issue
The README says the API supports file uploads, but the route setup does not show any upload middleware for handling files.

### Why it matters
If the request is sent as `multipart/form-data`, the server must use a file parser such as `multer`.

### Expected behavior
For file uploads, the API should process `req.files` in the controller and route.

---

## 3. Wrong field name used in code

### Issue
The project uses `catageory` (misspelled), but the README uses `category`.

### Example mismatch
- README says: `category`
- Code uses: `catageory`

### Impact
Requests may not match the expected field name depending on how the code is written.

---

## 4. Query parameter mismatch

### Issue
The README examples show filtering using `?category=...`, but the controller reads `req.query.catageory`.

### Impact
The query filter may not work correctly unless the exact misspelled key is used.

---

## 5. Incorrect response documentation for DELETE

### Issue
The README shows a `204` response with a JSON body.

### Important note
A `204` response normally means no response body should be sent.

---

## 6. Status code examples are inconsistent

### Issue
The README says some responses are `200` for POST-like actions, but the actual code uses `201` for creation responses.

### Impact
The documented status codes should match the implementation.

---

## 7. CORS mention is not verified in code

### Issue
The README says CORS is configured, but no CORS middleware is shown in the app setup.

### Impact
The documentation may claim support that is not actually implemented.

---

## 8. `multipart/form-data` vs JSON confusion

### Issue
The README mixes JSON examples and file upload examples, but the backend behavior is not fully consistent between them.

### Impact
This causes confusion while testing the API.

---

## 9. Missing explicit upload handling in route

### Issue
The product route does not show any middleware for handling files.

### Impact
If the request includes images, the route is not properly configured for them.

---

## 10. Data flow docs are too detailed / may not match implementation

### Issue
The README includes long architecture flow sections that describe upload middleware and behavior not fully present in the route setup.

### Impact
The docs may mislead developers about how the API actually works.

---

## 11. ImageKit configuration is incomplete

### Issue
The ImageKit client setup only provides `privateKey` and does not include the required `publicKey` and `urlEndpoint` values.

### Impact
The upload/authentication flow may fail or behave inconsistently.

---

## 12. Image files are being validated before upload

### Issue
The validator expects image objects with `url` and `id`, but the request is sending raw Multer files.

### Impact
The API throws `Each image must include url and id` even when the file upload request is correct.

---
