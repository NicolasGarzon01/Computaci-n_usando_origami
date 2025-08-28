# 🧮 Taller: Computación usando origami
Este proyecto implementa un simulador de circuitos lógicos, modelando de manera abstracta la computación como una "red de pliegues" y "gadgets" inspirada en el origami. Los pliegues (pleats) actúan como portadores de señales booleanas (True, False o None para un valor indefinido), mientras que los gadgets son los bloques lógicos que procesan estas señales. El sistema permite construir circuitos y propagar las señales desde las entradas hasta obtener las salidas finales.

---

## Modelo de Datos 📂
El núcleo del simulador se basa en tres componentes principales:

Pleat: Representa un conducto para una señal booleana. Cada Pleat tiene un nombre único y puede almacenar uno de tres valores: True, False o None.

Gadget: La clase base para los bloques lógicos (compuertas). Define la interfaz común evaluate(), que calcula las salidas a partir de las entradas. Las subclases específicas como ANDGadget, ORGadget, etc., implementan la lógica de sus respectivas compuertas.

Network: Es el contenedor principal que gestiona la interconexión de Pleats y Gadgets. Se encarga de la construcción del circuito, la configuración de las entradas y, crucialmente, de la propagación de las señales.

---

## Pruebas Unitarias de Compuertas Lógicas 🧪
Esta sección valida el comportamiento de cada gadget por separado. Para cada compuerta (NOT, AND, OR, NAND), se verifica su tabla de verdad. Los casos de prueba incluyen combinaciones con valores booleanos (True/False) y también con el valor None (indefinido).

NOT: Invierte el valor de la entrada. Si la entrada es True, la salida es False, y viceversa. Si la entrada es None, la salida es None.

AND: La salida solo es True si ambas entradas son True. Si alguna entrada es False, la salida es False. Si una entrada es True y la otra None, la salida es None.

OR: La salida es True si al menos una entrada es True. La salida solo es False si ambas entradas son False. Si una entrada es False y la otra None, la salida es None.

NAND: Es la negación de la compuerta AND. La salida es False solo si ambas entradas son True. En cualquier otro caso, la salida es True. Si una entrada es None, la salida es None.

Todos los resultados de estas pruebas muestran un (Éxito), lo que confirma que la lógica de cada gadget es correcta y maneja adecuadamente los valores indefinidos.

<img width="482" height="516" alt="image" src="https://github.com/user-attachments/assets/0ada10ec-9cba-4b31-ba19-d523ba460352" />



## Prueba de Integración del Medio Sumador ➕
Esta prueba demuestra cómo los gadgets se interconectan para formar un circuito funcional más complejo: un medio sumador (half-adder). Un medio sumador es un circuito que suma dos bits de entrada (a y b) y produce una suma (sum) y un acarreo (carry).

El output muestra la ejecución del circuito para las cuatro posibles combinaciones de entrada (00, 01, 10, 11). Para cada caso, se muestra:

El orden de evaluación (['or1', 'nand1', 'and_carry', 'and_sum']), que corresponde al orden topológico que el simulador ha calculado para propagar las señales.

El registro de evaluación (Evaluando '...'), que detalla cómo cada gadget calcula su salida basándose en sus entradas, mostrando el flujo de las señales a través de la red.

El resultado final (Resultado: {'sum': ..., 'carry': ...}) que coincide con los valores esperados de la suma binaria, lo que verifica que el circuito funciona como se diseñó.

<img width="667" height="653" alt="image" src="https://github.com/user-attachments/assets/c0ad82f2-96b4-4c11-99bc-6c6c28db4959" />
<img width="624" height="206" alt="image" src="https://github.com/user-attachments/assets/b3b69058-2f3f-48d8-a9e6-1a24d552f423" />


## Carga y Ejecución desde JSON 📄
La última parte del output muestra un ejemplo de la carga y simulación de un circuito desde un archivo JSON. En este caso, el archivo half_adder.json define la misma topología de circuito que se probó anteriormente. El resultado muestra que, al cargar el archivo con las entradas {'a': True, 'b': False}, el simulador produce las salidas correctas de {'sum': True, 'carry': False}. Esto demuestra que el simulador puede construir y ejecutar circuitos a partir de una configuración externa, lo que lo hace flexible y modular

<img width="662" height="177" alt="image" src="https://github.com/user-attachments/assets/02069bf1-299f-4cfc-bbb1-c368fd383007" />
