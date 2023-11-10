# Algoritmos de optimización

 2023/11/03

 En la optimización, tenemos un objetivo, llamado función objetivo, que queremos maximizar o minimizar. Sin embargo, esta optimización debe cumplir con ciertas restricciones. Estas restricciones pueden ser ecuaciones o desigualdades que definen el espacio en el que debemos encontrar la mejor solución.

Fecha de desarrollo: [[1967]]

## [[Interior point]] method

Los métodos Interior-point (métodos de punto interior) son algoritmos para resolver problemas de programación lineal y programación cuadrática, así como problemas de programación semidefinida y convexa en general. Estos algoritmos son especialmente efectivos para resolver problemas en los que se busca encontrar la mejor solución dentro de un conjunto de restricciones y objetivos dados. 


**1. Problemas que resuelven los métodos Interior-point:**

Los métodos Interior-point son especialmente útiles para resolver problemas de optimización convexa. Los problemas convexos son aquellos en los que la función objetivo y las restricciones son funciones convexas. Estos algoritmos pueden manejar varios tipos de problemas, como:

- [[Programación lineal]]: Maximizar o minimizar una función lineal sujeta a restricciones lineales.
- [[Programación cuadrática]]: Maximizar o minimizar una función cuadrática sujeta a restricciones lineales.
- [[Programación semidefinida]]: Maximizar o minimizar una función lineal sujeta a restricciones semidefinidas lineales.

**2. Cómo funcionan los métodos Interior-point:**

Estos métodos funcionan de manera iterativa. Comienzan desde un punto interior del conjunto factible (una solución que cumple todas las restricciones) y se mueven gradualmente hacia el óptimo a lo largo de las direcciones que reducen la función objetivo mientras mantienen las restricciones satisfechas. Esto se hace mediante la resolución de sistemas de ecuaciones lineales y cuadráticas en cada iteración.

**3. Ventajas de los métodos Interior-point:**

- [[Eficiencia]]: Los métodos Interior-point pueden converger rápidamente para problemas convexos, a menudo en un número de iteraciones relativamente bajo.
- [[Precisión]]: Pueden encontrar soluciones con alta precisión, lo que los hace adecuados para aplicaciones en las que se requiere una alta calidad de solución.
- [[Aplicaciones]] amplias: Se utilizan en una amplia gama de aplicaciones, desde la planificación de la producción hasta la ingeniería financiera y el diseño de redes.

**4. Cuándo usar los métodos Interior-point:**

Los métodos Interior-point son útiles cuando tienes un problema de optimización convexa que necesita ser resuelto con alta precisión. Algunos ejemplos de situaciones en las que podrías utilizarlos incluyen:

- Planificación de [[producción]]: Optimizar la asignación de recursos para maximizar la producción y minimizar los costos.
- [[Finanzas]]: Encontrar la asignación óptima de activos en una cartera de inversión sujeta a restricciones de riesgo.
- Ingeniería: Diseñar sistemas de comunicación o redes de transporte eficientes.
- [[Logística]]: Planificar rutas de transporte para minimizar el tiempo y los costos.

En resumen, los métodos Interior-point son algoritmos poderosos para resolver problemas de optimización convexa, y son ideales cuando necesitas encontrar la mejor solución dentro de un conjunto de restricciones y objetivos dados con alta precisión.

## Ejemplo de uso

Vamos a usar el método Interior-point para maximizar el rendimiento esperado de una cartera de activos financieros, sujeto a [[restricciones]] de riesgo. Supongamos que tienes una lista de activos financieros con diferentes rendimientos esperados y [volatilidades], y deseas asignar una cantidad de dinero a cada activo de manera que se maximice el rendimiento esperado, pero sin superar un nivel de riesgo determinado.

```python
from scipy.optimize import linprog
import numpy as np

# Datos de los activos financieros (rendimiento esperado y volatilidad)
rendimientos = np.array([0.1, 0.12, 0.15, 0.09])
volatilidades = np.array([0.2, 0.25, 0.3, 0.18])

# Número de activos
num_activos = len(rendimientos)

# Matriz de covarianza (representa las relaciones entre los activos)
covarianza = np.array([[0.04, 0.02, 0.01, 0.03],
                       [0.02, 0.09, 0.04, 0.05],
                       [0.01, 0.04, 0.16, 0.08],
                       [0.03, 0.05, 0.08, 0.12]])

# Parámetros de restricción
nivel_de_riesgo = 0.1  # Máximo nivel de riesgo permitido
cantidad_disponible = 1000000  # Cantidad total de dinero disponible para invertir

# Coeficientes de la función objetivo (maximizar el rendimiento)
c = -rendimientos

# Coeficientes de las restricciones (matriz A)
A = np.vstack((covarianza, -np.eye(num_activos)))

# Lados derechos de las restricciones (vector b)
b = np.hstack((nivel_de_riesgo, np.zeros(num_activos)))

# Límites de las variables (cantidad invertida en cada activo)
x_bounds = [(0, cantidad_disponible) for _ in range(num_activos)]

# Resolver el problema de optimización de la cartera de inversión
res = linprog(c, A_ub=A, b_ub=b, bounds=x_bounds, method='interior-point')

# Imprimir la asignación óptima de activos
print("Asignación óptima de activos:")
for i, cantidad in enumerate(res.x):
    print(f"Activo {i+1}: {cantidad:.2f} unidades")

# Calcular el rendimiento esperado de la cartera
rendimiento_cartera = -res.fun
print(f"Rendimiento esperado de la cartera: {rendimiento_cartera:.2%}")

```

## Refs

