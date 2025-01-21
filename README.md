# Prueba Técnica Front-End: Landing Page con Vue 3

## Instrucciones para ejecutar el proyecto

1. **Clonar el repositorio:**

Para comenzar, clona este repositorio en tu máquina local usando el siguiente comando:

```bash
git clone https://github.com/IliasVilux/TPH-Prueba-Tecnica-Ilias-Otsman.git
```

2. **Instalar las dependencias:**

Navega al directorio del proyecto y ejecuta el siguiente comando para instalar todas las dependencias necesarias:

```bash
cd TPH-Prueba-Tecnica-Ilias-Otsman
npm install
```

3. **Levantar el servidor de desarrollo:**

Una vez que las dependencias estén instaladas, puedes levantar el servidor de desarrollo con el siguiente comando:

```bash
npm run dev
```

¡Y listo! Deberías poder ver la Landing Page en funcionamiento accediendo al link que aparezca, generalmente `http://localhost:5173/`.

---

## Decisiones Técnicas

### 1. **Gestión de la Autenticación**

- **Peticiones HTTP:** Para gestionar las solicitudes hacia la API de Reqres, utilicé **Axios** debido a su simplicidad.
- **Manejo de Errores:** En caso de error en la autenticación, el mensaje de error se almacena en una variable reactiva, que luego es utilizada para mostrar feedback al usuario mediante un condicional en la interfaz.
- **Almacenamiento del Token:** Si la petición es exitosa, el token devuelto por la API se almacena tanto en una store creada con **Pinia** como en el **localStorage**. Esto garantiza persistencia de datos y facilita la gestión del estado global de la aplicación.

### 2. **Estructura del Proyecto y Componentización**

- La aplicación está dividida en **tres vistas principales**:
  - **Home:** La landing page que incluye el header, la sección principal (hero), posibles secciones informativas, que dependiendo del proyecto, necesitará de un componente independiente, y el footer. Cada una de estas partes es un componente independiente (`Header`, `Hero`, `Footer`) para garantizar un código modular y reutilizable.
  - **Login y Register:** Inicialmente diseñé componentes separados para cada formulario, pero al notar que las credenciales y las respuestas de la API eran similares, creé un componente mutuo llamado **`AuthForm`**. Este componente recibe una propiedad para identificar el tipo de formulario (login o register), ajustando dinámicamente los textos y comportamientos. Al enviar el formulario, emite un evento hacia la vista correspondiente con las credenciales ingresadas.

### 3. **Estilo y Maquetación**

- **Bootstrap:** Opté por **Bootstrap** como framework CSS para agilizar el desarrollo, asegurar la responsividad y mantener un diseño limpio.
- **Animaciones Personalizadas:** Para mejorar la experiencia de usuario, creé animaciones específicas y las mantuve separadas del archivo principal de estilos en un archivo SCSS dedicado. Esta separación asegura que el código sea más organizado y fácil de mantener.
- **Transiciones:** Utilicé el componente nativo de Vue, **`<transition>`**, para manejar transiciones suaves entre las vistas de la aplicación, proporcionando una experiencia de navegación más fluida.

### 4. **Validaciones y Manejo de Formularios**

- Implementé validaciones en los formularios para asegurar que los campos requeridos sean ingresados correctamente:
  - En el formulario de registro, verifico que el correo sea válido y que la contraseña tenga al menos seis caracteres.
  - En el formulario de login, verifico que el correo y la contraseña sean obligatorios antes de enviar la solicitud.
