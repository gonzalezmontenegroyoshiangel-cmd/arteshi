# Arteshi AutoBuilder — Fabric 1.21.11

**Estado: 0.1.0-alpha, código fuente para compilar y probar.** No es un mod estable ni se ha validado dentro del juego. Instálalo solamente si el servidor permite automatización.

## Funciones de esta primera versión

- Mod **solo del cliente**. No necesita permisos de administración ni plugin en el servidor.
- Tecla **B**: menú y selección del tipo de bloque detectado en el inventario.
- Mira un bloque y pulsa **J** para marcar la primera esquina; **K** para la segunda.
- Selección de volumen 3D: paredes (1 bloque de grosor), suelos y áreas volumétricas.
- Tres modos: `Rellenar vacíos`, `Reemplazar` (omite materiales ya correctos), `Excavar`.
- Recorrido automático mediante rutas A* sobre suelo firme, saltos de 1 bloque y evitación básica de agua/lava; sin vuelo, teletransporte o comandos administrativos.
- Colocación, rotura y cambio de ranura por interacciones normales con el servidor.
- Busca el material en las 36 ranuras del inventario y lo intercambia con la barra rápida cuando hace falta.
- Pausar con **V**, continuar/cancelar desde el menú. Límite inicial de **10,000** posiciones por trabajo.
- Protege bloques con entidades de bloque (cofres, shulkers, etc.), bedrock y bloques irrompibles.

## Para compilar en Windows

1. Instala **JDK 21**, no solo un JRE, y confirma `java -version`.
2. Instala **Gradle 9.x** desde https://gradle.org/install/ o usa el flujo de GitHub Actions incluido.
3. Desde la carpeta que contiene `build.gradle` ejecuta `gradle build`.
4. Si compila correctamente, toma el archivo sin `-sources` de `build/libs/`.
5. Colócalo en `.minecraft/mods/` con **Fabric Loader 1.21.11** y **Fabric API 0.141.6+1.21.11**.
6. Empieza probando en un mundo de un jugador creado para pruebas y luego en un servidor donde tengas permiso.

En GitHub: sube el proyecto a un repositorio, abre **Actions → Compilar AutoBuilder → Run workflow**. El artefacto compilado se publica al terminar si el proyecto pasa la compilación.

## Limitaciones actuales (muy importantes)

- Este archivo **no contiene un `.jar` compilado**. La máquina en que se creó el proyecto no pudo descargar dependencias Maven/Gradle para validar la compilación. Es posible que haya que ajustar firmas de la API de Minecraft para 1.21.11.
- El buscador de rutas **solo camina sobre terreno existente**. No construye puentes, andamios o escaleras de forma automática. Tampoco sabe abrir puertas, nadar, rodear un acantilado de tamaño ilimitado, ni resolver cualquier geometría 3D.
- No tiene sistema de reanudación persistente tras cerrar Minecraft; sí permite pausar/reanudar durante la misma sesión.
- No muestra un holograma ni contorno de la selección todavía.
- Para poner un bloque necesita una cara de soporte visible y un área alcanzable; llenar huecos suspendidos en el aire puede requerir andamios manuales.
- Los bloques orientables (escaleras, troncos, losas, etc.) se colocan con su orientación de juego normal. El planificador compara el tipo de bloque, no todos sus estados.
- Se detiene ante bloques con datos/inventarios, herramientas ausentes, materiales agotados, áreas no cargadas o situaciones que no puede resolver con seguridad. La protección del servidor puede negar las modificaciones.
- El movimiento/colocación automatizados pueden estar prohibidos por las reglas de algunos servidores. No intenta evitar anticheats o protecciones.
- No se garantiza compatibilidad con otros mods que controlen el movimiento o hagan modificaciones a cámara/controles.
- Empieza usando áreas pequeñas (3x3 a 5x5), materiales sólidos comunes y suelo plano.

## Archivos

- `AutoBuilderClient`: inicialización, teclas y puntos.
- `BuilderScreen`: GUI de selección de materiales y controles.
- `BuildConfig`: modos y región.
- `BuildEngine`: flujo de trabajo, inventario, ruptura y colocación.
- `PathNavigator`: búsqueda de ruta conservadora y movimiento.

MIT: código original de esta maqueta; Minecraft/Fabric/Fabric API son de sus respectivos autores.
