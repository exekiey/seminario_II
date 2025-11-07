## 1. Qué funciones se pueden usar en los scripts de Unity para llevar a cabo traslaciones, rotaciones y escalados.
```
Traslación: transform.position = ..., transform.Translate(Vector3).

Rotación: transform.rotation = Quaternion.Euler(x,y,z),

transform.Rotate(...)

Escalado: transform.localScale = ...
```
## 2. ¿Cómo trasladarías la cámara 2 metros en cada uno de los ejes y luego la rotas
30º alrededor del eje Y?. Rota la cámara alrededor del eje Y 30ª y desplázala 2 metros en cada uno de los ejes. ¿Obtendrías el mismo resultado en ambos casos?. Justifica el resultado
### Caso 1

```
transform.position += new Vector3(2f,2f,2f);

transform.rotation = Quaternion.Euler(0f,30f,0f) * transform.rotation;
```
### Caso 2
```
transform.rotation = Quaternion.Euler(0f,30f,0f) * transform.rotation;

transform.position += new Vector3(2f,2f,2f);
```
En nuestro caso el resultado no es el mismo porque la dirección de los ejes de traslación se modifica al rotarlo.
## 3. Sitúa la esfera de radio 1 en el campo de visión de la cámara y configura un volumen de vista que la recorte parcialmente.
```
camera.transform.position = Vector3.zero;

sphere.transform.position = camera.transform.forward * 4f;

sphere.transform.localScale = Vector3.one * 2f;

camera.nearClipPlane = 3.5f;
```
## 4. Sitúa la esfera de radio 1 en el campo de visión de la cámara y configura el volumen de vista para que la deje fuera de la vista.
```
sphere.transform.position = camera.transform.forward * 0.5f;

camera.nearClipPlane = 1f;
```
## 5. ¿Cómo puedes aumentar el ángulo de la cámara?. Qué efecto tiene disminuir el ángulo de la cámara.
```
Camera.main.fieldOfView += 10f;
Reducirlo hace zoom. Aumentarlo hace zoom-out.
```
## 6. Es correcta la siguiente afirmación: Para realizar la proyección al espacio 2D, en el inspector de la cámara, cambiaremos el valor de projection, asignándole el valor de orthographic
Sí, al activar orthographic la cámara usa proyección ortográfica.
## 7. Especifica las rotaciones que se han indicado en los ejercicios previos con la utilidad quaternion.
### Ejercicio 1:
```
transform.rotation = new Quaternion(0f, 0.3826834f, 0f, 0.9238795f);
```
### Ejercicio 2:
```
transform.rotation = new Quaternion(0f, 0.2588190f, 0f, 0.9659258f);
```
## 8. ¿Cómo puedes averiguar la matriz de proyección en perspectiva que se ha usado para proyectar la escena al último frame renderizado?.
```
Matrix4x4 perspectiva = Camera.main.projectionMatrix;
Debug.Log(perspectiva);
```
## 9. ¿Cómo puedes averiguar la matriz de proyección en perspectiva ortográfica que se ha usado para proyectar la escena al último frame renderizado?.
```
Camera.main.orthographic = true;
Matrix4x4 perspectiva = Camera.main.projectionMatrix;
Debug.Log(perspectiva);
```
## 10. ¿Cómo puedes obtener la matriz de transformación entre el sistema de coordenadas local y el mundial?.
```
Matrix4x4 localToWorld = transform.localToWorldMatrix;
```
Matrix4x4 worldToLocal = transform.worldToLocalMatrix;
## 11. Cómo puedes obtener la matriz para cambiar al sistema de referencia de vista.
```
Matrix4x4 vista = Camera.main.worldToCameraMatrix;
Matrix4x4 nueva = vista * transform.localToWorldMatrix;
```
## 12. Especifica la matriz de la proyección usada en un instante de la ejecución del ejercicio 1 de la práctica 1.
```
Debug.Log(Camera.main.projectionMatrix);

1.48058 0.00000 0.00000 0.00000
0.00000 1.73205 0.00000 0.00000
0.00000 0.00000 -1.00060 -0.60018
0.00000 0.00000 -1.00000 0.00000
```
## 13. Especifica la matriz de modelo y vista de la escena del ejercicio 1 de la práctica 1.
```
Matrix4x4 M = transform.localToWorldMatrix;

1.00000 0.00000 0.00000 0.00000
0.00000 1.00000 0.00000 0.00000
0.00000 0.00000 1.00000 0.00000
0.00000 0.00000 0.00000 1.00000
Matrix4x4 V = Camera.main.worldToCameraMatrix;

1.00000 0.00000 0.00000 0.00000
0.00000 1.00000 0.00000 0.00000
0.00000 0.00000 -1.00000 0.00000
0.00000 0.00000 0.00000 1.00000
```
## 14. Aplica una rotación en el start de uno de los objetos de la escena y muestra la
matriz de cambio al sistema de referencias mundial.
0.93872 -0.04322 0.34197 0.00000
0.05233 0.99848 -0.01745 0.00000
-0.34069 0.03428 0.93955 0.00000
0.00000 0.00000 0.00000 1.00000
## 15. ¿Cómo puedes calcular las coordenadas del sistema de referencia de un objeto con las siguientes propiedades del Transform:?
```
Position (3, 1, 1), Rotation (45, 0, 45)
Matrix4x4 m = Matrix4x4.TRS(new Vector3(3, 1, 1), Quaternion.Euler(45, 0, 45), Vector3.one);
```
## 16. Crea una escena en Unity con los siguientes elementos: cámara principal, planobase (como suelo) y tres cubos de distinto color (rojo, verde, azul) colocados enposiciones distintas en el espacio. Realiza un pequeño script de depuración junto a la cámara que permita visualizar en consola o en pantalla las matrices de transformación (Model, View, Projection) y sus resultados sobre un vértice de cada cubo.
0
```
1.00000 0.00000 0.00000 1.49700
0.00000 1.00000 0.00000 0.84000
0.00000 0.00000 1.00000 -1.83837
0.00000 0.00000 0.00000 1.00000
1.00000 0.00000 0.00000 0.00000
0.00000 1.00000 0.00000 0.00000
0.00000 0.00000 -1.00000 0.00000
0.00000 0.00000 0.00000 1.00000
1.79103 0.00000 0.00000 0.00000
0.00000 1.73205 0.00000 0.00000
0.00000 0.00000 -1.00060 -0.60018
0.00000 0.00000 -1.00000 0.00000
(0.50, 0.50, 0.50)
(2.00, 1.34, -1.34)
(2.00, -0.13, -7.01)
(3.58, -0.23, 7.02)
```
1
```
1.00000 0.00000 0.00000 -0.22751
0.00000 1.00000 0.00000 0.84000
0.00000 0.00000 1.00000 -3.76000
0.00000 0.00000 0.00000 1.00000
1.00000 0.00000 0.00000 0.00000
0.00000 1.00000 0.00000 0.00000
0.00000 0.00000 -1.00000 0.00000
0.00000 0.00000 0.00000 1.00000
1.79103 0.00000 0.00000 0.00000
0.00000 1.73205 0.00000 0.00000
0.00000 0.00000 -1.00060 -0.60018
0.00000 0.00000 -1.00000 0.00000
(0.50, 0.50, 0.50)
(0.27, 1.34, -3.26)
(0.27, -0.13, -5.09)
(0.49, -0.23, 5.09)
```
2
```
1.00000 0.00000 0.00000 -0.22751
0.00000 1.00000 0.00000 0.84000
0.00000 0.00000 1.00000 -1.83837
0.00000 0.00000 0.00000 1.00000
1.00000 0.00000 0.00000 0.00000
0.00000 1.00000 0.00000 0.00000
0.00000 0.00000 -1.00000 0.00000
0.00000 0.00000 0.00000 1.00000
1.79103 0.00000 0.00000 0.00000
0.00000 1.73205 0.00000 0.00000
0.00000 0.00000 -1.00060 -0.60018
0.00000 0.00000 -1.00000 0.00000
(0.50, 0.50, 0.50)
(0.27, 1.34, -1.34)
(0.27, -0.13, -7.01)
(0.49, -0.23, 7.02)
```
## 17. Dibujar en un programa de dibujo el recorrido de las coordenadas de un vértice específico del cubo rojo: <br> Local → World → Camera/View → Clip → NDC → Viewport. Indicar cómo cambia su valor en cada espacio. Aplicar la transformación manualmente a un punto (por ejemplo, el vértice (0.5, 0.5, 0.5)) y registrar los resultados paso a paso.
```
(0.50, 0.50, 0.50)
(0.27, 1.34, -1.34)
(0.27, -0.13, -7.01)
(0.49, -0.23, 6.42, 7.01)
(0.07, -0.03, 0.92)
(0.53, 0.48, 0.92)
```
## 18. Mover o rotar uno de los cubos y mostrar cómo cambian los valores de su matriz
de modelo. Rotar la cámara y mostrar cómo se modifica la matriz de vista.
Cambiar entre proyección ortográfica y perspectiva y comparar las diferencias
numéricas en la matriz de proyección.
```
MODEL:
1.00000 0.00000 0.00000 1.49700
0.00000 1.00000 0.00000 0.84000
0.00000 0.00000 1.00000 -1.83837
0.00000 0.00000 0.00000 1.00000
VIEW:
1.00000 0.00000 0.00000 0.00000
0.00000 1.00000 0.00000 -1.47000
0.00000 0.00000 -1.00000 -8.35000
0.00000 0.00000 0.00000 1.00000
PROJ:
1.79103 0.00000 0.00000 0.00000
0.00000 1.73205 0.00000 0.00000
0.00000 0.00000 -1.00060 -0.60018
0.00000 0.00000 -1.00000 0.00000
```
Movemos y rotamos el cubo
```
MODEL:
0.87662 0.00000 -0.48118 0.87248
0.00000 1.00000 0.00000 0.84000
0.48118 0.00000 0.87662 -0.79579
0.00000 0.00000 0.00000 1.00000
```
Rotamos la cámara
```
VIEW:
0.83200 0.00000 0.55478 4.63241
0.00000 1.00000 0.00000 -1.47000
0.55478 0.00000 -0.83200 -6.94718
0.00000 0.00000 0.00000 1.00000
```
Cambiamos proyección
```
PROJ:
0.20681 0.00000 0.00000 0.00000
0.00000 0.20000 0.00000 0.00000
0.00000 0.00000 -0.00200 -1.00060
0.00000 0.00000 0.00000 1.00000
```
