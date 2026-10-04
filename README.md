# Labor.io — Maquetado mobile

Maquetado de la versión mobile de Labor.io.
Las pantallas maquetadas son:

- Inicio de sesión y registro (login.html y register.html)
- Busqueda de oportunidades (offers.html)
- Home (index.html)

## Primer uso

1. Clonar el repositorio.
2. Abrir **la carpeta del repositorio** en VS Code (File > Open Folder).
3. Instalar las extensiones recomendadas cuando VS Code lo sugiera.
4. En la terminal de VS Code, ejecutar:

```
   npm install
```

5. Verificar que en la barra inferior aparezca "Watching..." (Live Sass Compiler).

## Reglas del equipo

- `css/main.css` se genera solo: **nunca editarlo a mano**.
- Cada uno trabaja en su rama y en sus archivos.
- Cambios en `_variables.scss`, `_layout.scss` o `main.scss`: avisar al grupo porfi.
- Rutas siempre relativas, nunca empezando con `/`.
  - Desde `index.html`: `css/main.css`
  - Desde `pages/`: `../css/main.css`
- Conflicto en `main.css`: resolver el SCSS, guardar `main.scss` y commitear el CSS regenerado.

## Ramas

| Rama          | Archivos                                                |
| ------------- | ------------------------------------------------------- |
| `page/home`   | `index.html`, `_home.scss`                              |
| `page/auth`   | `pages/login.html`, `pages/register.html`, `_auth.scss` |
| `page/offers` | `pages/offers.html`, `_offers.scss`                     |
