# Código Limpio | Clean Code

 Código limpio o "Clean Code" promueve la escritura de código que sea fácil de leer, mantener y extender. 

# ¿Por qué escribir código limpio?

1. **Legibilidad**: El software es escrito por humanos y para humanos. Una buena parte del tiempo de desarrollo se dedica a leer código. Si el código es limpio y fácil de entender, los desarrolladores pueden discernir rápidamente qué hace y cómo lo hace.

2. **Mantenibilidad**: Las necesidades del negocio cambian y el software necesita evolucionar. Un código limpio es más fácil de modificar y extender, lo que reduce el tiempo y el coste del mantenimiento.

3. **Reducción de errores**: Un código limpio y bien estructurado es menos propenso a errores. Es más fácil identificar problemas potenciales en un código ordenado y coherente que en uno desordenado.

4. **Colaboración**: En equipos grandes o con proyectos que tienen una vida útil larga, muchos desarrolladores pueden trabajar en el mismo código. Un código limpio garantiza que todos puedan entender y colaborar eficientemente en el proyecto.

5. **Eficiencia en el desarrollo**: Con un código más limpio y estructurado, es más fácil añadir nuevas características sin romper funcionalidades existentes. También se facilita la identificación y corrección de errores.

6. **Sostenibilidad**: Proyectos con código limpio pueden sobrevivir y adaptarse a lo largo del tiempo. Un código mal escrito puede llevar a un software obsoleto que necesita ser reescrito desde cero.

7. **Testabilidad**: El código limpio suele seguir principios que lo hacen modular y desacoplado, lo que facilita la creación de pruebas unitarias y la verificación de que todo funciona como se espera.

8. **Eficiencia en costos**: Aunque puede parecer que escribir código limpio lleva más tiempo inicialmente, a largo plazo ahorra dinero. Los errores son más costosos de solucionar en las etapas posteriores del desarrollo, y el tiempo invertido en solucionar problemas en un código mal escrito puede superar con creces el tiempo que se habría invertido en hacerlo bien desde el principio.

9. **Profesionalismo**: Escribir código limpio es una cuestión de profesionalidad. Los desarrolladores que se preocupan por su oficio y la calidad de su trabajo tienden a escribir código limpio.

10. **Satisfacción personal**: Muchos desarrolladores encuentran una sensación de logro y satisfacción al escribir código limpio y elegante. Es gratificante ver un sistema bien diseñado que funciona sin problemas.

En resumen, el código limpio beneficia tanto a los desarrolladores como a las empresas. Aumenta la eficiencia, reduce los costos y garantiza que el software sea sostenible, mantenible y de alta calidad. Es una inversión en el presente que paga dividendos en el futuro.
 
Aquí te presentamos los conceptos clave y recomendaciones con ejemplos prácticos:

## 1. **Código Limpio**

Es aquel que ha sido escrito por alguien que se preocupa. Es fácil de leer y entender por otros.

**Malo**:
```java
public double calc(int a, int b) {
    return a + b*0.5;
}
```

**Bueno**:
```java
public double calculateAverage(int sum, int numberOfItems) {
    return sum + numberOfItems * 0.5;
}
```

## 2. **Boy Scout Rule**

Deja el código más limpio de lo que lo encontraste.

## 3. **Significado de los nombres**

Los nombres deben ser descriptivos y evitar la desinformación.

**Malo**:
```java
int d;  // Tiempo transcurrido en días
```

**Bueno**:
```java
int elapsedDays;
```

## 4. **Funciones**

Deben hacer una sola cosa, hacerla bien y solo hacer esa cosa.

**Malo** (hace más de una cosa):
```java
public void emailAndLogUserInfo(User user) {
    sendEmail(user);
    logUserDetails(user);
}
```

**Bueno** (separar responsabilidades):
```java
public void emailUser(User user) {
    sendEmail(user);
}

public void logUserInfo(User user) {
    logUserDetails(user);
}
```

## 5. **Comentarios**

Es mejor tener código que se autoexplique que tener muchos comentarios.

**Malo** (comentario innecesario):
```java
// Suma a y b
public int sum(int a, int b) {
    return a + b;
}
```

**Bueno** (el código se explica por sí solo):
```java
public int sum(int a, int b) {
    return a + b;
}
```

## 6. **Formato**

La organización y formato del código es crucial. Mantener una estructura coherente y estandarizada.

**Malo**:
```java
public class MyClass{int x;public void myFunction(){if(x>0) {System.out.println("X is positive");}}}
```

**Bueno**:
```java
public class MyClass {
    int x;

    public void myFunction() {
        if (x > 0) {
            System.out.println("X is positive");
        }
    }
}
```

## Recomendaciones clave:

- **Nombres**:

**Malo**:
```java
public void pR() {...}
```

**Bueno**:
```java
public void printReport() {...}
```

- **Funciones**:

**Malo** (función larga y compleja):
```java
public void process() {
    // Lógica A
    ...
    // Lógica B
    ...
}
```

**Bueno** (dividir en subfunciones):
```java
public void process() {
    processLogicA();
    processLogicB();
}
```

- **Argumentos**:

**Malo**:
```java
public String format(String value, int type, boolean isBold, boolean isItalic, Color color) {...}
```

**Bueno** (usar objetos para agrupar):
```java
public String format(TextAttributes attributes) {...}
```

- **Evitar variables globales y clases Singleton, usar la iyección de dependia en la medida de lo posible**:

**Malo** (Singleton):
```java
public class Logger {
    private static final Logger instance = new Logger();

    private Logger() {}

    public static Logger getInstance() {
        return instance;
    }
}
```

**Bueno** (inyección de dependencias):
```java
public class Logger {
    public Logger() {}

    // Lógica del logger
}
```

- **No usar banderas en funciones**:

**Malo**:
```java
public void process(boolean isAdvanced) {
    if (isAdvanced) {
        advancedProcessing();
    } else {
        basicProcessing();
    }
}
```

**Bueno**:
```java
public void basicProcessing() {...}
public void advancedProcessing() {...}
```

- **Evitar efectos secundarios**:

**Malo** (efecto secundario en una función que calcula):
```java
public int calculateTotal(Order order) {
    order.setProcessedDate(new Date());
    return order.getItems().stream().mapToInt(Item::getPrice).sum();
}
```

**Bueno**:
```java
public int calculateTotal(Order order) {
    return order.getItems().stream().mapToInt(Item::getPrice).sum();
}

public void markOrderAsProcessed(Order order) {
    order.setProcessedDate(new Date());
}
```

- **Uso de test unitarios**:

```java
@Test
public void testSum() {
    assertEquals(5, sum(2, 3));
}
```
---

## Manejo de Errores

1. **Usar excepciones en lugar de códigos de retorno**:
   - En lugar de devolver códigos de error, es más legible lanzar y capturar excepciones.

**Malo**:
```java
public int divide(int a, int b) {
    if (b == 0) return -1;  // Código de error
    return a / b;
}
```

**Bueno**:
```java
public int divide(int a, int b) {
    if (b == 0) throw new ArithmeticException("División por cero.");
    return a / b;
}
```

2. **Evitar comprobar null**:
   - Si es posible, evita devolver null en tus funciones. Puede llevar a errores de Null Pointer.

**Malo**:
```java
public User findUser(String username) {
    // Si no se encuentra, devuelve null
}
```

**Bueno**:
```java
public Optional<User> findUser(String username) {
    // Devuelve un Optional que puede o no contener un User
}
```

3. **No captures excepciones sin motivo**:
   - Evita atrapar excepciones genéricas o atrapar y luego ignorarlas. Maneja solo las que puedes gestionar adecuadamente.

**Malo**:
```java
try {
    // Código
} catch (Exception e) {
    // Ignora el error
}
```

**Bueno**:
```java
try {
    // Código
} catch (SpecificException e) {
    // Maneja el error específico
}
```

4. **Proporciona contexto en las excepciones**:
   - Cuando lances una excepción, proporciona toda la información relevante para entender el origen y causa del problema.

```java
throw new UserNotFoundException("Usuario con ID " + userId + " no fue encontrado.");
```

5. **Mantén limpias las estructuras try/catch/finally**:
   - Extrae los bloques `try`, `catch`, o `finally` en funciones para que la estructura y la intención del código sean claras.

**Malo**:
```java
public void loadData() {
    try {
        // lógica de carga de datos
    } catch (DataException e) {
        // manejo de errores
    }
}
```

**Bueno**:
```java
public void loadData() {
    try {
        executeDataLoading();
    } catch (DataException e) {
        handleDataError(e);
    }
}

private void executeDataLoading() {
    // lógica de carga de datos
}

private void handleDataError(DataException e) {
    // manejo de errores
}
```

---
## Arquitectura Limpia

El objetivo principal de la Arquitectura Limpia es crear un sistema desacoplado, donde los componentes más internos no tienen dependencias sobre los componentes externos, permitiendo así una mayor flexibilidad y facilidad de prueba.

### Estructura Principal:

1. **Entidades**: Están en el centro de la arquitectura. Representan las reglas de negocio de alto nivel y son independientes de cualquier detalle específico de la aplicación.
   
2. **Casos de Uso**: Encapsulan y representan todas las acciones que pueden ser invocadas en la aplicación. Dependen de las entidades.

3. **Interfaces Adaptables**: Actúan como puentes entre los casos de uso y los agentes externos como bases de datos, frameworks web o bibliotecas.

4. **Frameworks y Controladores**: Se sitúan en la capa más externa. Esta capa contiene detalles específicos de implementación y se comunica con la aplicación a través de las interfaces adaptadoras.

### Ejemplo:

Imaginemos una aplicación simple de gestión de usuarios:

- **Entidad**: `User`, con operaciones básicas como `create`, `update` o `delete`.
  
- **Caso de Uso**: `RegisterUser`, `UpdateUserDetails`, `DeleteUser`. Cada uno de estos se comunica con la entidad `User` para realizar la lógica de negocio necesaria.

- **Interfaces Adaptables**: Podríamos tener una `UserRepository` que define cómo se deben guardar y recuperar los usuarios.

- **Frameworks y Controladores**: Aquí es donde integraríamos una base de datos específica, como PostgreSQL o MySQL, implementando la `UserRepository` interfaz. También podríamos tener controladores para una API web que invoque nuestros casos de uso.

### Beneficios:

1. **Independencia del Framework**: La arquitectura no está atada a un framework específico, permitiendo cambiarlo o actualizarlo sin afectar al resto del código.
   
2. **Pruebas**: Los componentes están desacoplados y, por lo tanto, son más fáciles de probar. Las entidades y los casos de uso, en particular, pueden probarse sin depender de detalles externos.

3. **Independencia de UI**: Puedes cambiar la interfaz de usuario (web, móvil, escritorio) sin afectar la lógica de negocio.

4. **Independencia de la Base de Datos**: Puedes cambiar la base de datos o el ORM sin afectar la lógica de negocio.

5. **Flexibilidad**: Con una arquitectura desacoplada, es más fácil adaptar el sistema a cambios futuros.

---
# S.O.L.I.D
---

## 1. Principio de Responsabilidad Única (Single Responsibility Principle - SRP)

Este principio establece que una clase debe tener una única razón para cambiar. En otras palabras, una clase debe tener una sola responsabilidad.

**Ejemplo**:

**Malo** (una clase con múltiples responsabilidades):
```java
class Usuario {
    void crearUsuario() {...}
    void autenticarUsuario() {...}
    void generarReporte() {...}
}
```

**Bueno** (clases con una sola responsabilidad):
```java
class UsuarioCreator {
    void crearUsuario() {...}
}

class AutenticadorUsuario {
    void autenticarUsuario() {...}
}

class ReporteGenerator {
    void generarReporte() {...}
}
```

## 2. Principio de Abierto/Cerrado (Open/Closed Principle - OCP)

Este principio establece que las clases deben estar abiertas para su extensión pero cerradas para su modificación. Debe ser posible agregar nuevas funcionalidades sin modificar el código existente.

**Ejemplo**:

**Malo** (modificando una clase existente):
```java
class Rectangulo {
    double largo;
    double ancho;
}

class AreaCalculator {
    double calcularArea(Rectangulo rectangulo) {
        return rectangulo.largo * rectangulo.ancho;
    }
}
```

**Bueno** (extensión sin modificación):
```java
abstract class Figura {
    abstract double area();
}

class Rectangulo extends Figura {
    double largo;
    double ancho;

    double area() {
        return largo * ancho;
    }
}

class Circulo extends Figura {
    double radio;

    double area() {
        return Math.PI * radio * radio;
    }
}
```

## 3. Principio de Sustitución de Liskov (Liskov Substitution Principle - LSP)

Este principio establece que las clases derivadas deben poder reemplazar a sus clases base sin afectar el comportamiento del programa.

**Ejemplo**:

**Malo** (una subclase que no sigue el principio LSP):
```java
class Pajaro {
    void volar() {...}
}

class Pinguino extends Pajaro {
    // Los pingüinos no pueden volar
}
```

**Bueno** (evitar subclases que contradigan el comportamiento de la clase base):
```java
abstract class Ave {
    abstract void volar();
}

class Pajaro extends Ave {
    void volar() {...}
}

class Pinguino extends Ave {
    void volar() {
        // Los pingüinos no pueden volar, pero implementamos el método de todos modos
        throw new UnsupportedOperationException("Los pingüinos no vuelan");
    }
}
```

## 4. Principio de Segregación de Interfaces (Interface Segregation Principle - ISP)

Este principio establece que una clase no debe verse obligada a implementar interfaces que no utiliza. Debe ser específica en cuanto a las interfaces que implementa.

**Ejemplo**:

**Malo** (una clase que implementa una interfaz con métodos innecesarios):
```java
interface Trabajo {
    void trabajar();
    void descansar();
}

class Programador implements Trabajo {
    void trabajar() {...}
    void descansar() {...}
}
```

**Bueno** (interfaces más específicas):
```java
interface Trabajar {
    void trabajar();
}

interface Descansar {
    void descansar();
}

class Programador implements Trabajar {
    void trabajar() {...}
}
```

## 5. Principio de Inversión de Dependencia (Dependency Inversion Principle - DIP)

Este principio establece que las clases de alto nivel no deben depender de las clases de bajo nivel. Ambas deben depender de abstracciones. Además, las abstracciones no deben depender de los detalles, sino que los detalles deben depender de las abstracciones.

**Ejemplo**:

**Malo** (dependencia directa entre clases de alto y bajo nivel):
```java
class Switch {
    LightBulb bulb = new LightBulb();

    void turnOn() {
        bulb.turnOn();
    }

    void turnOff() {
        bulb.turnOff();
    }
}
```

**Bueno** (dependencia a través de una abstracción):
```java
interface Switchable {
    void turnOn();
    void turnOff();
}

class LightBulb implements Switchable {
    void turnOn() {...}
    void turnOff() {...}
}

class Switch {
    Switchable device;

    void connect(Switchable device) {
        this.device = device;
    }

    void turnOn() {
        device.turnOn();
    }

    void turnOff() {
        device.turnOff();
    }
}
```

Estos principios SOLID son fundamentales para crear software que sea modular, flexible y fácil de mantener a lo largo del tiempo. Al aplicar estos principios, se puede lograr un código limpio y de alta calidad.



