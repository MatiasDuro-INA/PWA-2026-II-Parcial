# Parcial: Playlist — de HTML a React

## Objetivo

Pasar la pantalla de álbum y playlist de [playlist-vanilla.html](./src/components/Playlist/playlist-vanilla.html), hecha en HTML, CSS y JavaScript puro, a componentes de React.

Abrí el archivo en el navegador y probalo antes de empezar:
- **♡ Favorito** marca y desmarca el álbum (cambia a **♥ En favoritos**).
- **+ Agregar** suma la canción a "Mi playlist". Una vez agregada, su botón pasa a decir **✓ Agregada** y queda deshabilitado, así no se puede agregar dos veces.
- En "Mi playlist", la **✕** quita esa canción. Al quitarla, su botón de arriba vuelve a habilitarse.
- **Vaciar playlist** quita todas las canciones.
- Si la playlist está vacía se muestra "Tu playlist está vacía." y no aparece el botón de vaciar.
- Arriba se ve cuántas canciones hay en la playlist.

## Cómo arrancar

```bash
npm install
npm run dev
```

## Material

- [playlist-vanilla.html](./src/components/Playlist/playlist-vanilla.html): la pantalla original.
- [playlist-react.css](./src/components/Playlist/playlist-react.css): los estilos listos para importar desde React.
- En [App.jsx](./src/App.jsx) ya está el objeto `album` con todos los datos, incluido el array `canciones`. **No hay que escribir ningún dato a mano en el componente**: todo sale de ese objeto.

## Consignas

Resolvé los puntos en orden. Van de más fácil a más difícil.

1. **Crear la estructura (0,5 pts).** En `src/components/Playlist/` creá `Playlist.jsx` con un componente `Playlist` que devuelva el HTML del álbum convertido a JSX. Todavía no hace falta que funcione nada. Mostralo en `App.jsx`.

2. **Pasar los estilos (0,5 pts).** Importá `playlist-react.css` en el componente. Acordate de cambiar `class` por `className`.

3. **Pasarle los datos desde App (1 pt).** Pasale el objeto `album` por props a `Playlist`:
   ```jsx
   <Playlist album={album} />
   ```
   Mostrá título, artista, género, año e imagen usando las props. El `alt` de la imagen tiene que ser el título.

4. **Canciones con `map` (1 pt).** Las canciones del álbum no pueden estar escritas a mano: generá los `<li>` recorriendo `album.canciones` con `map`. Usá el `id` de cada canción como `key`.

5. **Favorito (0,5 pts).** Agregá un estado booleano `esFavorito`. El botón alterna entre `♡ Favorito` y `♥ En favoritos`, y cuando está marcado tiene además la clase `marcado` (`btn-favorito marcado`).

6. **Agregar a la playlist (1,5 pts).** Agregá un estado `playlist` que empiece como un array vacío (`[]`). Al hacer clic en **+ Agregar**, sumá esa canción al array. Arriba mostrá cuántas hay (🎵 Mi playlist: N canciones).

   Pista: no se puede usar `push` sobre el estado. Hay que crear un array nuevo con el spread (`[...playlist, cancion]`).

7. **Mostrar la playlist (1 pt).** Debajo de "Mi playlist", mostrá las canciones del estado con `map`, cada una con su nombre y un botón `✕` (`btn-quitar`).
   - Si la playlist está vacía, mostrá `<p className="vacia">Tu playlist está vacía.</p>` en lugar de la lista.

8. **No repetir canciones (1 pt).** Si una canción ya está en la playlist, su botón tiene que decir `✓ Agregada` y estar `disabled`. Si no está, dice `+ Agregar`.

   Pista: `some` o `find` sirven para saber si un elemento está en un array.

9. **Quitar de la playlist (1 pt).** Al hacer clic en `✕`, sacá esa canción del array. Usá `filter`.

10. **Vaciar la playlist (0,5 pts).** Agregá el botón **Vaciar playlist** (`btn-vaciar`), que deja el estado en `[]`. Solo se muestra cuando hay al menos una canción.

11. **Componentizar la fila de canción (0,5 pts).** Creá el componente `FilaCancion` en su propio archivo, dentro de `src/components/Playlist/`. Muestra una canción del álbum con su botón. Recibe la canción, si ya está agregada y una función para agregarla:
    ```jsx
    <FilaCancion
      cancion={cancion}
      agregada={...}
      onAgregar={...}
    />
    ```
    El estado **sigue viviendo en `Playlist`**, no adentro de `FilaCancion`.

12. **Componentizar la playlist (1 pt).** Creá el componente `MiPlaylist` en su propio archivo, dentro de `src/components/Playlist/`. Recibe el array de canciones y las funciones para quitar una canción y vaciar la lista. Tiene que seguir funcionando todo lo de los puntos 7, 9 y 10. Elegí vos los nombres de las props.

**Total: 10 puntos.**

## Condiciones

- Prohibido usar `document.getElementById`, `querySelector`, `addEventListener` o `innerHTML`. Todo se resuelve con estado, props y eventos de React (`onClick`).
- Prohibido modificar el estado directamente (`push`, `splice`, `playlist[0] = ...`). Siempre se crea un array nuevo.
- Ningún dato del álbum (título, artista, canciones) puede estar escrito a mano en los componentes.
- El proyecto tiene que levantar con `npm run dev` sin errores en la consola.
- Se aprueba con 6 puntos.
