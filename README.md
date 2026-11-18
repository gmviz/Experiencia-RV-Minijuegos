
## PROYECTO: Interacción en Realidad Virtual - Minijuegos
Alumno: Guillermo Mata Vizcaíno

* **Enlace al recurso original (FAB):** [Detective Office - [https://www.fab.com/listings/82fea2b7-ffde-4a9f-9ec7-17faa7504477]
* **Pipeline de renderizado:** Forward Shading + Iluminación Estática Bakeada (Lumen desactivado).
>Para probar y utilizar este proyecto sin necesidad de gafas de Realidad Virtual físicas, es obligatorio ejecutar el archivo `LanzarConSimulador.bat` incluido en la carpeta

## 1. Comparativa Global de Rendimiento (Antes vs. Después)
Medidas sacadas en **VR Preview** desde el mismo `PlayerStart` fijo mediante `stat fps`, `stat unit`, `stat rhi` y la herramienta de auditoría `Statistics`:

| Métrica | Escena Inicial (`escena-inicial`) | Escena Optimizada (`main`) | Mejora / Diferencia |
| :--- | :---: | :---: | :---: |
| **FPS medios** | `118.76 FPS` | `120.00 FPS` *(tope del motor)* | Estable al máximo |
| **Tiempo de Fotograma (`Frame`)** | `8.41 ms` | `8.33 ms` | `-0.08 ms` |
| **Tiempo de CPU (`Game`)** | `5.87 ms` | `2.91 ms` | **`-50.4%` (`-2.96 ms`)** |
| **Tiempo de Render Thread (`Draw`)** | `3.43 ms` | `2.09 ms` | **`-39.1%` (`-1.34 ms`)** |
| **Tiempo de GPU (`GPU Time`)** | `5.00 ms` | `5.19 ms` | `+0.19 ms`  |
| **Draw Calls (`Draws`)** | `1,198` | `565` | **`-52.8%` (`-633 draws`)** |
| **Actores / Mallas en escena (`Count`)** | `2,274` | `40` | **`-98.2%`** |
| **Primitivas en vista (`Prims`)** | `414.8 K` | `2,936.5 K` | Mayor lote por *Merge Actors* |
| **Memoria de Texturas (`Current Memory`)** | `1,697.00 MB` | `384.38 MB` | **`-77.3%` (`-1,312.6 MB`)** |
| **Memoria de Texturas (`Fully Loaded`)** | `2,469.75 MB` | `537.56 MB` | **`-78.2%` (`-1,932.2 MB`)** |
| **RAM / VRAM total en ejecución** | `5.41 GB` / `2.22 GB` | `4.48 GB` / `1.74 GB` | **`-930 MB` RAM / `-480 MB` VRAM** |
| **Errores de iluminación dinámica** | 9 luces solapadas sin sombras | `0 errores` (Bakeada *Production*) | **100% eliminados** |


## 2. Comparativa Visual y de Estadísticas

### Rendimiento en tiempo real (`stat fps`, `stat unit`, `stat rhi`)

| Escena Inicial (`escena-inicial`) | Escena Optimizada (`main`) |
| :---: | :---: |
| ![Stats Antes](./Screenshots/01_stats_antes.png) | ![Stats Después](./Screenshots/01_stats_despues.png) |


### Auditoría de Geometría

| Antes (`2,274 actores`) | Después (`40 actores` tras Merge Actors) |
| :---: | :---: |
| ![Mallas Antes](./Screenshots/02_mallas_antes.png) | ![Mallas Después](./Screenshots/02_mallas_despues.png) |

### Auditoría de Texturas

| Antes (`1.69 GB` cargados en 4K) | Después (`384 MB` tras acotar resolución) |
| :---: | :---: |
| ![Texturas Antes](./Screenshots/03_texturas_antes.png) | ![Texturas Después](./Screenshots/03_texturas_despues.png) |
