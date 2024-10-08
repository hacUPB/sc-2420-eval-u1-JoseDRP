[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/WfEJSxe8)
# Bitácora de la Unidad 1

### Estudiante:  José David Ruiz Pérez
### ID:  000448081


### Solución actividad - Unidad 1

**1.**	Los principales componentes de un PC son: 

**Hardware:**

**Placa base (Motherboard)** - La placa principal que conecta todos los componentes del hardware.
**Procesador (CPU)** - Unidad central de procesamiento que ejecuta instrucciones y procesa datos.
**Memoria RAM** - Memoria de acceso aleatorio utilizada para almacenar datos temporales mientras se ejecutan programas.
**Disco duro o SSD** - Almacena datos permanentemente en el sistema.
**Tarjeta gráfica (GPU)** - Procesa datos relacionados con gráficos y video.
**Fuente de alimentación (PSU)** - Suministra energía a todos los componentes del sistema.

**Software:**

**Sistema operativo** - (por ejemplo, Windows, macOS, Linux)
**Controladores de dispositivo** - Software que permite a la PC comunicarse con hardware específico.
**Software de aplicaciones** - Programas que realizan tareas específicas, como navegadores web, procesadores de texto, software de edición de imágenes, etc.
**Antivirus y software de seguridad** - Protege contra virus y amenazas de seguridad.
**Herramientas de productividad** - Suites de oficina, gestores de correo electrónico, etc.

**2.** La arquitectura de un computador es el diseño estructural que define cómo los componentes de hardware están organizados y cómo interactúan entre sí para ejecutar programas y procesar datos.

Existen diferentes variantes de arquitecturas, como por ejemplo:

- Arquitectura Von Neumann
- Arquitectura Harvard
- Arquitectura RISC
- Arquitectura CISC

**3-4.** [Link Mapa conceptual](https://www.goconqr.com/es-ES/mindmap/39709115/arquitectura-de-un-computador)


### Solución actividad 2 - Unidad 1

#### Ejercicio 1. 

- Lo primero que hice para darle solución al problema es resolverlo en un lenguaje de alto nivel como c#. Esto debido a que aún tengo ciertas dudas con el lenguaje ensamblador por lo que prefiero hacerlo de esta manera para tener claro el problema y buscar alternativas. El código en c# me funcionó bien, es el siguiente: 

```assembler
using System;

class Program
{
    static void Main()
    {
        Console.Write("Valor de N: ");
        int N = int.Parse(Console.ReadLine());

        int suma = 0;
        for (int i = 1; i <= N; i++)
        {
            suma += i;
        }

        // Resultado
        Console.WriteLine($"La suma de los primeros {N} números naturales es: {suma}");
    }
}
```

- Este código me funcionó bastante bien en la prueba que realicé, corrió justo como debería. El profesor me dió unos consejos para comenzar con el código en ensamblador. Así que intenté comenzar con el código en ensamblador.

- Tuve ciertos retrasos por gitbash ya que no me estaba funcionando como debería

- Luego de esto, usé chat gpt para ver de qué manera hacía el código y poder entenderlo y tomar una referencia:

```
// Inicialización
@0

D=M  
@i
M=D

@1
M=0

// Inicializar el índice i
@2
M=1

// Comenzar el bucle
(LOOP)
    @i
    D=M
    @2
    D=D-M
    @END
    D;JEQ
    
    @2
    D=M
    @1
    M=M+D
    
    @2
    M=M+1
    
    @LOOP
    0;JMP
    
(END)
```

- puse este código en la consola del ensamblador pero me saltaban ciertos errores que no supe solucionar.

- finalmente y luego de diversos intentos con ayuda de chat gpt y modificandolo con conocimientos vistos en clase, pude hacer un código que me funcionaba medianamente bien:

```
@0
D=A
@1
M=D

@15
D=A
@16
M=D

@0
D=M

@1
D=A
@2
M=D

(LOOP)
@0
D=M
@2
D=D-M
@END_LOOP
D;JLE
END_LOOP

@1
D=M
@2
D=D+A
@1
M=D

@2
D=M
@3
D=D+1
@2
M=D

@LOOP
0;JMP

(END_LOOP)


@1
D=M
@15
M=D

@0
0;JMP
```

#### Ejercicio 2.

- Tal y cómo hice en el ejercicio 1, comencé realizando el código en c# para tener el problema más claro y facilitar el posterior código en assembler; este apartado es fácil porque tengo buenos conocimientos en el lenguaje c#.

Este es el código que diseñé rápidamente:

```assembler
using System;

class Program
{
    static void Main()
    {
        // Leer el número del usuario
        Console.Write("Ingrese un número entero positivo: ");
        int number = int.Parse(Console.ReadLine());

        // Validar si el número es positivo
        if (number < 0)
        {
            Console.WriteLine("El número debe ser entero positivo.");
            return;
        }

        // Calcular el factorial
        long factorial = CalculateFactorial(number);

        // Mostrar el resultado
        Console.WriteLine($"El factorial de {number} es {factorial}");
    }

    static long CalculateFactorial(int n)
    {
        // Caso base: factorial de 0 es 1
        if (n == 0)
            return 1;

        // Calcular el factorial usando un bucle
        long result = 1;
        for (int i = 1; i <= n; i++)
        {
            result *= i;
        }

        return result;
    }
}
```
- luego de esto, y con los conocimientos que logré asentar luego del ejercicio 1, pude hacer este código en assembler:

```assembler
@2
D=M
@3
M=1

(LOOP)
    @2
    D=M
    @END
    D;JEQ

    @3
    D=M
    @2
    M=D*M
    @2
    D=M
    D=D-1
    @2
    M=D

    @LOOP
    0;JMP

(END)
    @END
    0;JMP
```

- sin embargo, por alguna razón que desconozco, el archivo no era reconocido por la consola entonces no pude hacer el testeo para que funcionara a pesar de hacer varios intentos modificando el código para comprobar si esa era la fuente del problema.

  
### Solución actividad 3: Pantalla y teclado.

#### Ejercicio 1:

- Lo primero fue plantearme el primer objetivo, el cuál fue pintar la mitad de la pantalla de negro y dejar el resto de blanco al presionar un botón específico.

- Para comenzar con esto, lo primero que hice fue replicar uno de los ejercicios planteados en el curso de nand2tetris, este tenía una buena parte del código para pintar un pequeño rectángulo en la parte superior derecha pero estaba incompleto, luego de algunos intentos para completarlo, el código me quedó de esta manera:


```assembler
@R0
D=M
@n
M=D
@i
M=0

@SCREEN
D=A
@adress
M=D

(LOOP)
@i
D=M
@n
D=D-M
@END
D;JGE

@adress
D=M
@i
D=D+M
@SCREEN
D=D-A
A=D
@R0
D=M
M=D

@i
D=M
@1
D=D+A
@i
M=D

@LOOP
0;JMP

(END)
@END
0;JMP
```

- Esta primera versión de código no me funcionó ya que; a pesar de que en la posición 17 de la memoria RAM hacía el loop correspodiente hasta 50 como se indicó en la posición 0 de la memoria, seguía sin pintar los píxeles indicados.

- Para solucionar este último código agregué un M=-1 que me faltaba en @adress, ahora pintaba la primera línea pero al hacer el loop, se pintaba en la misma haciendo que no se genere la figura. Por lo que tuve que solucionar esto.

```assembler

@R0
D=M
@n
M=D
@i
M=0

@SCREEN
D=A
@adress
M=D

(LOOP)
@i
D=M
@n
D=D-M
@END
D;JGE

@adress
A=M
M=-1
@i
D=D+M
@SCREEN
D=D-A
A=D
@R0
D=M
M=D

@i
D=M
@1
D=D+A
@i
M=D

@LOOP
0;JMP

(END)
@END
0;JMP
```

- Con este código logré que pintara la primera línea sin problemas, ahora me disponía a agregar punteros R0, R1 y R2 de algún modo para que estos apuntaran hacia las filas y columnas. 
