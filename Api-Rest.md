# Guia d’APIs REST (amb `curl` i JavaScript)

## 1) Què és una API REST

Una **API REST** (Representational State Transfer) és una interfície que permet que **dues aplicacions es comuniquin mitjançant HTTP**, utilitzant:
- **URLs** per identificar recursos (ex: `/posts/1`)
- **mètodes HTTP** per indicar l’acció (GET, POST, PUT/PATCH, DELETE)
- **JSON** com a format habitual d’intercanvi de dades

Mètodes més comuns:
- **GET** → obtenir dades  
- **POST** → crear dades  
- **PUT / PATCH** → modificar dades  
- **DELETE** → eliminar dades  

---

## 2) HTTP Request: estructura

Un **HTTP Request** és el missatge que envia el client (navegador, `curl`, una app…) al servidor.

### Estructura

```
MÈTODE + PATH + VERSIÓ HTTP
Headers...
(línia en blanc)
Body (opcional)
```

### Exemple (GET)

```
GET /posts/1 HTTP/1.1
Host: jsonplaceholder.typicode.com
Accept: application/json
```

### Exemple (POST)

```
POST /posts HTTP/1.1
Host: jsonplaceholder.typicode.com
Content-Type: application/json
Accept: application/json

{
  "title": "Hola API",
  "body": "Aquest és un post de prova",
  "userId": 1
}
```

---

## 3) HTTP Response: estructura

Un **HTTP Response** és el missatge que retorna el servidor.

### Estructura

```
VERSIÓ HTTP + CODI D’ESTAT
Headers...
(línia en blanc)
Body (opcional)
```

### Exemple (200 OK)

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "title": "...",
  "body": "..."
}
```

### Codis habituals

| Codi | Significat |
|----|----|
| 200 | OK |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 500 | Internal Server Error |

---

## 4) `curl`

`curl` és una eina de línia d’ordres per fer peticions HTTP.

Opcions útils:
- `-X` mètode HTTP
- `-H` headers
- `-d` body
- `-i` mostrar headers de resposta

---

## 5) Exemple GET `/posts/1`

### Amb `curl`

```bash
curl -i https://jsonplaceholder.typicode.com/posts/1
```

### Amb JavaScript (`get-post-1.html`)

```html
<script>
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(r => r.json())
  .then(d => console.log(d));
</script>
```

---

## 6) Exemple POST `/posts`

### Amb `curl`

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"Hola API","body":"Post de prova","userId":1}'
```

### Amb JavaScript (`post-create.html`)

```html
<script>
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {'Content-Type':'application/json'},
  body: JSON.stringify({
    title:'Hola API',
    body:'Post de prova',
    userId:1
  })
})
.then(r => r.json())
.then(d => console.log(d));
</script>
```
