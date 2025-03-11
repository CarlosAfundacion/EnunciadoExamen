
# **Ampliación del Proyecto Android Studio – Recuperación segunda evaluación**  

### **Requisitos de implementación**  

Deberás implementar las siguientes mejoras en la aplicación móvil desarrollada en **Android Studio con Firebase** siempre siguienddo el **MVVM**:  

### **1. Filtrado de elementos en DashboardFragment**  
 **Requisito**: Mostrar en **DashboardFragment** únicamente los elementos que **no han sido marcados como favoritos**.  
 **Tareas**:  
- Modificar el `DashboardRepository` para que filtre los datos obtenidos de Firebase y **excluya los elementos marcados como favoritos por el usuario actual**.  
- Vincular este filtrado en el **DashboardViewModel**.  
- Actualizar el `RecyclerView` en **DashboardFragment** para que solo muestre los elementos que no están en favoritos.  
- Modificar la consulta a Firebase para que excluya los elementos cuyo `id` esté dentro de la lista de favoritos del usuario.  
- En el adaptador del `RecyclerView`, asegurarse de que la lista se actualiza correctamente cuando los datos cambian.  

---
### **2. Eliminacion de todos los favoritos desdeel `NavigationDrawer`**
 **Requisito**:  Al pulsar en la opción `Limpiar Favoritos` se eliminará toda la lista de favoritos asociada al usuario.

 **Tareas**:  

 - Crear un método en el repository que elimine el nodo `favoritos` asociado al usuario.
 - Cargar DashboardFragment``con todos los elementos.
---
### **3. Almacenamiento del usuario en SharedPreferences**  
 **Requisito**: Guardar en **SharedPreferences** el usuario autenticado para evitar que tenga que iniciar sesión de nuevo cada vez que se reinicie la app.  
 **Tareas**:  
- Al hacer **login**, almacenar en `SharedPreferences` el **UID del usuario autenticado**.  
- Al abrir la aplicación, si hay un **usuario almacenado**, redirigirlo directamente a la `MainActivity` con el `NavigationDrawer`, **evitando la pantalla de login**.  
- Implementar la funcionalidad de **logout**, asegurándose de que al cerrar sesión se elimine el usuario almacenado en `SharedPreferences`.  

 **Ayuda de implementación**:  
- **Guardar usuario al hacer login**  
```java
SharedPreferences sharedPref = getSharedPreferences("AppConfig", Context.MODE_PRIVATE);
SharedPreferences.Editor editor = sharedPref.edit();
editor.putString("userId", FirebaseAuth.getInstance().getCurrentUser().getUid());
editor.apply();
```
- **Comprobar si hay usuario almacenado al abrir la app** (en `LoginActivity` o en `SplashScreenActivity` si la tienes):  
```java
SharedPreferences sharedPref = getSharedPreferences("AppConfig", Context.MODE_PRIVATE);
String userId = sharedPref.getString("userId", null);

if (userId != null) {
    // Usuario autenticado previamente, redirigir a MainActivity
    startActivity(new Intent(this, MainActivity.class));
    finish();
}
```
- **Eliminar usuario de SharedPreferences al cerrar sesión** (en la función de logout de `MainActivity`):  
```java
FirebaseAuth.getInstance().signOut();
SharedPreferences sharedPref = getSharedPreferences("AppConfig", Context.MODE_PRIVATE);
sharedPref.edit().remove("userId").apply(); // Eliminar usuario guardado
startActivity(new Intent(this, LoginActivity.class));
finish();
```

---

### **3. Entregables**  
 **Repositorio GitHub:**  
- Subir el código a la rama `ampliacion`.  
- Realizar commits atómicos con el prefijo **"Ampliación: [Descripción del cambio]"**.  
- Mergear la rama `ampliacion` con `main` al finalizar.  

 **Vídeo demostrativo:**  
Grabar un vídeo mostrando:  
1. **Inicio de sesión y almacenamiento del usuario en SharedPreferences**.  
2. **Filtrado correcto en DashboardFragment** (los favoritos no aparecen).
3. **Eliminación de todos los favoritos desde el NavigationDrawer** 
4. **Reinicio de la aplicación sin cierre de sesión** (acceso directo a `MainActivity`).  
5. **Logout y eliminación de la sesión guardada** (requiere volver a iniciar sesión).  

📌 **Subida a Classroom:**  
- Enlace al repositorio GitHub.  
- Archivo ZIP con el proyecto de Android Studio.  
- Vídeo demostrativo.  

---

### **Criterios de Evaluación**  
- ✅ **Filtrado correcto en `DashboardFragment`** (exclusión de favoritos).  
- ✅ **Uso de `SharedPreferences` para el usuario**.  
- ✅ **Redirección automática a `MainActivity` si hay sesión guardada**.  
- ✅ **Logout funcional y eliminación de usuario de `SharedPreferences`**.  
- ✅ **Código limpio, organizado en MVVM y con commits bien documentados**.  

