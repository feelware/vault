# Queries

## Hall

```
/books
/book/:id
/lists
/list/:id
/reviews
/review/:id
/user/:id/reviews
/user/:id/lists
/search
/signin
/signup
/lends
/settings
```

### `/books`

![](utilities/attachments/Pasted%20image%2020241102190444.png)
#### Obtener los tags más preferidos por el usuario

- Seleccionar `n` registros de la tabla `User_Tag` con mayor `mean_rating`, donde `user_id` es la id del usuario.

#### Obtener los libros más populares (paginado)

- Incluir id, título, autor (id, nombre) y cover_url de cada uno de los libros.
- Opcionalmente, filtrar solo aquellos libros que coincidan con los tags preferidos del usuario.

### `/book/:id`

![](utilities/attachments/Pasted%20image%2020241103105632.png)

#### Obtener información completa sobre cierto libro

![](utilities/attachments/Pasted%20image%2020241103121626.png)

- Incluir rating, título, autores (id y nombre), fecha de publicación, sinopsis, tags (id y nombre).

#### Obtener reviews de cierto libro (paginado)

![](utilities/attachments/Pasted%20image%2020241103143209.png)

- Incluir id, título, contenido, autor (id, nombre y profile_picture_url) y total de likes.

#### Registrar un nuevo préstamo de cierto libro a cierto usuario

![](utilities/attachments/Pasted%20image%2020241103121921.png)

- Revisar que el usuario no tenga un préstamo activo para dicho libro.
- Revisar que el usuario no tenga más préstamos activos del límite establecido.
- Añadir un nuevo registro a la tabla `Order`
- Disminuir `available_copies` en 1

#### Obtener todas las listas creadas por cierto usuario

![](utilities/attachments/Pasted%20image%2020241103114708.png)

#### Añadir libro a lista

#### Quitar libro de lista

#### Cambiar nombre de lista

![](utilities/attachments/Pasted%20image%2020241103121204.png)

#### Crear nueva lista

- Darle un nombre por defecto (`Lista {{id}}`)

#### Añadir nueva review

![](utilities/attachments/Pasted%20image%2020241103121822.png)
![](utilities/attachments/Pasted%20image%2020241103121954.png)

- Añadir nuevo registro a la tabla `Review`
- Actualizar rating promedio del libro (`Document`)
- Actualizar rating promedio de cada tag (`Tag`)
- Actualizar rating promedio de cada tag en relación al usuario (`User_Tag`)
- El título debe tener un límite de caracteres.

### `/lists`

![](utilities/attachments/Pasted%20image%2020241103125745.png)

#### Obtener todas las listas (paginado)

- Incluir id, nombre, autor (id, autor y profile_picture_url), cover_url de 6 primeros libros, total de libros y total de likes.
- Opcionalmente, filtrar solo aquellos libros que coincidan con los tags preferidos del usuario.

### `/list/:id`

![](utilities/attachments/Pasted%20image%2020241103143413.png)
![](utilities/attachments/Pasted%20image%2020241103143424.png)

#### Obtener todos los libros de cierta lista (paginado)

- Incluir id, título, autor (id, nombre) y cover_url de cada uno de los libros.

#### Cambiar privacidad de lista (pública/privada)

#### Eliminar lista
