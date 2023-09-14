# Código Limpio | Clean Code

El libro "Clean Code" promueve la escritura de código que sea fácil de leer, mantener y extender. Aquí te presentamos los conceptos clave y recomendaciones del libro con ejemplos prácticos:

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

- **Evitar variables globales y clases Singleton**:

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

- **Test unitarios**:

```java
@Test
public void testSum() {
    assertEquals(5, sum(2, 3));
}
```

---

Un código limpio facilita el entendimiento y el mantenimiento de tu aplicación. 
