Claro, aquí está el contenido del archivo `sql-tscript.doc` convertido y estructurado en formato Markdown.

---

# Código Transact-SQL

Transact-SQL (o T-SQL) es una extensión del lenguaje SQL (Structured Query Language) desarrollada por Microsoft y Sybase. Es el lenguaje principal utilizado para interactuar con Microsoft SQL Server.

### ¿Para qué se usa Transact-SQL?

Se utiliza para:
*   Consultar datos (como con SELECT)
*   Insertar, actualizar y eliminar datos (INSERT, UPDATE, DELETE)
*   Crear y modificar estructuras de bases de datos (tablas, vistas, procedimientos, etc.)
*   Programar lógica dentro del servidor (procedimientos almacenados, funciones, triggers)

### ¿Qué lo diferencia de SQL estándar?

Transact-SQL agrega características que no existen en el SQL estándar, como:
*   Variables locales (DECLARE, SET)
*   Control de flujo (IF...ELSE, WHILE)
*   Procedimientos almacenados (CREATE PROCEDURE)
*   Manejo avanzado de errores (TRY...CATCH)
*   Cursores para recorrer resultados fila por fila
*   Funciones propias del sistema (GETDATE(), ROW_NUMBER(), etc.)

## 1. Configuración Inicial y Uso de Base de Datos

```sql
Use Lesson9
go

Set Dateformat DMY
go
```

*   `Use Lesson9`: Esta línea especifica que las operaciones SQL subsiguientes se ejecutarán dentro del contexto de la base de datos `Lesson9`. Es fundamental para asegurar que las operaciones se realicen sobre las tablas y objetos correctos en esa base de datos.
*   `go`: Es un comando de terminación de lote en SQL Server. Indica el final de un lote de comandos T-SQL y envía los comandos al servidor para su ejecución.
*   `Set Dateformat DMY`: Esta configuración establece el formato de fecha predeterminado para el servidor a Día/Mes/Año. Esto es importante para la correcta interpretación de las cadenas de fecha, como '10/10/2007', evitando posibles errores de conversión.

## 2. Variables Globales

```sql
--Variables Globales
Select        @@language                [Lenguaje del servidor],
              @@servicename             [Nombre del servicio],
              @@version                 [Versión del motor de base de datos SQL Serve],
              @@max_connections         [Nro Máximo de conecciones soportados por SQL Server]
go
```

*   `@@language`: Devuelve el nombre del idioma configurado para el servidor SQL Server.
*   `@@servicename`: Devuelve el nombre del servicio de SQL Server bajo el cual se está ejecutando la instancia actual.
*   `@@version`: Muestra información sobre la versión, el procesador, la edición y el sistema operativo de la instancia de SQL Server actual.
*   `@@max_connections`: Indica el número máximo de conexiones de usuario simultáneas que SQL Server puede soportar.
Estas son variables de sistema predefinidas por SQL Server que proporcionan información sobre el entorno del servidor.

## 3. Variables Locales (Definidas por el Usuario)

### Bloque Anónimo Básico

```sql
--Varibles Locales (definidas por el usuario)
--Bloque anónimo
Begin
        Declare @v_nom varchar(50)
        Declare @v_fechaNac date, @v_sueldo smallmoney
        ------
        Set @v_nom='Javier'
        Select @v_fechaNac='10/10/2007', @v_sueldo=3600
        ------
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Nombre :'+@v_nom
        Print 'Fecha de Nacimiento: '+@v_fechaNac
        Print 'Sueldo: '+@v_Sueldo
End
go
```

*   `Begin ... End`: Define un bloque de código.
*   `Declare @v_nom varchar(50)`: Declara una variable local llamada `@v_nom` de tipo `varchar` con una longitud máxima de 50 caracteres.
*   `Declare @v_fechaNac date, @v_sueldo smallmoney`: Declara dos variables: `@v_fechaNac` de tipo `date` y `@v_sueldo` de tipo `smallmoney`.
*   `Set @v_nom='Javier'`: Asigna el valor 'Javier' a la variable `@v_nom`.
*   `Select @v_fechaNac='10/10/2007', @v_sueldo=3600`: Asigna valores a `@v_fechaNac` y `@v_sueldo` utilizando la sentencia `SELECT`. Ambas `SET` y `SELECT` pueden ser usadas para asignar valores a variables.
*   `Print Replicate ('=',50)`: Imprime una cadena de 50 caracteres '='. `REPLICATE` repite una cadena un número especificado de veces.
*   `Print space(20)+'Reporte de Datos'`: Imprime 20 espacios en blanco seguidos de la cadena 'Reporte de Datos'. `SPACE` genera una cadena de espacios.
*   `Print 'Nombre :'+@v_nom`: Imprime la cadena 'Nombre :' concatenada con el valor de la variable `@v_nom`.
*   `Print 'Fecha de Nacimiento: '+@v_fechaNac`: Intenta imprimir la fecha de nacimiento.
*   `Print 'Sueldo: '+@v_Sueldo`: Intenta imprimir el sueldo.

### Bloque con Error de Tipo de Datos

```sql
------Bloque con error de tipo de datos ------------------------------
Begin
        Declare @v_nom varchar(50)
        Declare @v_fechaNac date, @v_sueldo smallmoney
        ------
        Set @v_nom='Javier'
        Select @v_fechaNac='10/10/2007', @v_sueldo=3600
        ------
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Nombre :'+@v_nom
        Print 'Fecha de Nacimiento: '+@v_fechaNac        --Error Tipo de Dato
        Print 'Sueldo: '+@v_Sueldo                                        --Error Tipo de Dato
End
go
```

Este bloque es idéntico al anterior, pero se señala que las líneas que intentan concatenar directamente `date` y `smallmoney` con una cadena ('Fecha de Nacimiento: ' y 'Sueldo: ') causarán un error de tipo de dato. SQL Server no puede convertir implícitamente estos tipos a `varchar` para la concatenación en la sentencia `PRINT`.

### Solución: Aplicar Función de Conversión (CAST/CONVERT)

```sql
------------Solución: Aplicar función de Conversión o formato-------------
Begin
        Declare @v_nom varchar(50)
        Declare @v_fechaNac date, @v_sueldo smallmoney
        ------
        Set @v_nom='Javier'
        Select @v_fechaNac='10/10/2007', @v_sueldo=3600
        ------
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Nombre :'+@v_nom
        Print 'Fecha de Nacimiento: '+ Cast (@v_fechaNac as varchar(18))
        Print 'Sueldo: '+ Convert (Varchar(18), @v_Sueldo,4)
End
go
```

*   `Cast (@v_fechaNac as varchar(18))`: Convierte explícitamente la variable `@v_fechaNac` (tipo `date`) a `varchar(18)`. `CAST` es una función ANSI SQL estándar para conversión de tipos.
*   `Convert (Varchar(18), @v_Sueldo,4)`: Convierte explícitamente la variable `@v_Sueldo` (tipo `smallmoney`) a `varchar(18)`. `CONVERT` es una función específica de SQL Server que permite un tercer parámetro para especificar un estilo de formato.

### Bloque Aplicando Formato (FORMAT)

```sql
--Bloque Aplicando Formato
Begin
        Declare @v_nom varchar(50)
        Declare @v_fechaNac date, @v_sueldo smallmoney
        ------
        Set @v_nom='Javier'
        Select @v_fechaNac='10/10/2007', @v_sueldo=3600
        ------
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Nombre :'+@v_nom
        Print 'Fecha de Nacimiento: '+Format(@v_fechaNac,'D','es-pe')
        Print 'Sueldo: '+Format(@v_Sueldo,'C','es-pe')
End
go
```

*   `Format(@v_fechaNac,'D','es-pe')`: Formatea la fecha `@v_fechaNac` a un formato de fecha larga ('D') utilizando la cultura `es-pe` (español - Perú). Esto produce una salida legible como "lunes, 10 de octubre de 2007".
*   `Format(@v_Sueldo,'C','es-pe')`: Formatea el sueldo `@v_Sueldo` a un formato de moneda ('C') utilizando la cultura `es-pe`. Esto añade el símbolo de moneda y separadores de miles/decimales apropiados.
La función `FORMAT` es una forma más moderna y flexible de dar formato a la salida, especialmente útil para internacionalización.

### Variable Conteniendo el Resultado de una Consulta

```sql
---Una Variable puede contener resultado de una consulta, si este devuelve solo un dato
Begin
        Declare @V_IdVendedor int =1
        Declare @v_nomVendedor varchar(max), @v_cantPedidos smallint
        Select @v_nomVendedor=nomVendedor from Vendedor where IdVendedor=@V_IdVendedor
        Select @v_cantPedidos=count(*) from Pedido where IdVendedor=@V_IdVendedor
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Vendedor :' +@v_nomVendedor
        Print 'Cantidad de Pedidos :' +cast(@v_cantPedidos as varchar(25))
End
go
```

*   `Declare @V_IdVendedor int = 1`: Declara e inicializa la variable `@V_IdVendedor` con el valor 1.
*   `Select @v_nomVendedor=nomVendedor from Vendedor ...`: Asigna el nombre del vendedor de la tabla `Vendedor` a la variable `@v_nomVendedor`. Esta consulta debe devolver exactamente una fila y una columna.
*   `Select @v_cantPedidos=count(*) from Pedido ...`: Asigna el conteo de pedidos para el vendedor especificado a la variable `@v_cantPedidos`.
*   `Print 'Cantidad de Pedidos :' +cast(@v_cantPedidos as varchar(25))`: Se utiliza `CAST` para convertir el `smallint` `@v_cantPedidos` a `varchar` para poder concatenarlo con la cadena.

## 4. Estructuras de Control de Flujo

### Estructura de Control IF

```sql
--Estructura de constrol IF --------------------------------------------------------------
--Ejemplo para determinar el tipo de vendedor
Begin
        Declare @V_IdVendedor int =9
        Declare @v_nomVendedor varchar(max), @v_cantPedidos smallint, @v_tipoV varchar(max)
        Select @v_nomVendedor=nomVendedor from Vendedor where IdVendedor=@V_IdVendedor
        Select @v_cantPedidos=count(*) from Pedido where IdVendedor=@V_IdVendedor
        if @v_cantPedidos>100
                Set @v_tipoV='Vendedor Excelente'
        else if @v_cantPedidos<50
                Set @v_tipoV='Vendedor Regular'
        else
                Set @v_tipoV='Vendedor Normal'
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Vendedor :' +@v_nomVendedor
        Print 'Cantidad de Pedidos :' +cast(@v_cantPedidos as varchar(25))
        Print 'Tipo Vendedor :'+@v_tipoV
End
go
```

*   `if @v_cantPedidos>100 ... else if @v_cantPedidos<50 ... else ...`: Esta es una estructura condicional que evalúa la cantidad de pedidos (`@v_cantPedidos`) y asigna un tipo de vendedor (`@v_tipoV`) basado en el rango.

### Estructura de Control CASE

```sql
--Estructura de constrol CASE --------------------------------------------------------------
--Ejemplo para determinar el tipo de vendedor
Begin
        Declare @V_IdVendedor int =9
        Declare @v_nomVendedor varchar(max), @v_cantPedidos smallint, @v_tipoV varchar(max)
        Select @v_nomVendedor=nomVendedor from Vendedor where IdVendedor=@V_IdVendedor
        Select @v_cantPedidos=count(*) from Pedido where IdVendedor=@V_IdVendedor
        Set @v_tipoV=        Case
                                when @v_cantPedidos>100 then 'Vendedor Excelente'
                                when @v_cantPedidos<50 then 'Vendedor Regular'
                                else 'Vendedor Normal'
                             End
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        Print 'Vendedor :' +@v_nomVendedor
        Print 'Cantidad de Pedidos :' +cast(@v_cantPedidos as varchar(25))
        Print 'Tipo Vendedor :'+@v_tipoV
End
go
```

*   `Set @v_tipoV = Case ... End`: La expresión `CASE` es una alternativa al `IF/ELSE IF` para asignar un valor a una variable basado en múltiples condiciones. Es más concisa y a menudo preferida para este tipo de lógica.

### Estructura de Control WHILE

```sql
--Estructura de constrol WHILE --------------------------------------------------------------
--Ejemplo para determinar el tipo de vendedor
Begin

        Declare @V_IdVendedor int
        Set @V_IdVendedor=1
        Print Replicate ('=',50)
        Print space(20)+'Reporte de Datos'
        Print Replicate ('=',50)
        While @V_IdVendedor<=9
        Begin
                Declare @v_nomVendedor varchar(max), @v_cantPedidos smallint, @v_tipoV varchar(max)
                Select @v_nomVendedor=nomVendedor from Vendedor where IdVendedor=@V_IdVendedor
                Select @v_cantPedidos=count(*) from Pedido where IdVendedor=@V_IdVendedor
                if @v_cantPedidos>100
                        Set @v_tipoV='Vendedor Excelente'
                else if @v_cantPedidos<50
                        Set @v_tipoV='Vendedor Regular'
                else
                        Set @v_tipoV='Vendedor Normal'
                Print 'Vendedor :' +@v_nomVendedor
                Print 'Cantidad de Pedidos :' +cast(@v_cantPedidos as varchar(25))
                Print 'Tipo Vendedor :'+@v_tipoV
                Set @V_IdVendedor=@v_IDVendedor + 1
                Print Replicate ('=',50)
        End
End
go
```

*   `While @V_IdVendedor<=9 Begin ... End`: Este bucle `WHILE` itera desde `IdVendedor = 1` hasta `IdVendedor = 9`.
*   Dentro del bucle, para cada `IdVendedor`, se recuperan y procesan los datos.
*   `Set @V_IdVendedor=@v_IDVendedor + 1`: Esta línea incrementa el contador, lo que es crucial para que el bucle eventualmente termine.

## 5. Manejo de Errores

### Generación de Errores: RAISERROR

```sql
/**Generación de Errores: RaisError**/
Begin
        Declare @v_cantidadPedida smallint=110
        If @v_cantidadPedida>100
                Raiserror('Cantidad Excede lo permitido..',10,1) --Error leve
        else
                Print 'Cantidad Correcta'
End
go
-------------------------------
Begin
        Declare @v_cantidadPedida smallint=110
        If @v_cantidadPedida>100
                Raiserror('Cantidad Excede lo permitido..',16,1) --Error Grave
        else
                Print 'Cantidad Correcta'
End
go
```

*   `Raiserror('Mensaje', Severidad, Estado)`: Genera un mensaje de error definido por el usuario.
    *   **Mensaje**: La cadena de texto del error.
    *   **Severidad**: Un número del 0 al 25 que indica la gravedad.
        *   `10`: Errores informativos, no detienen la ejecución.
        *   `16`: Errores graves que pueden detener la ejecución del lote si no se manejan con `TRY/CATCH`.
    *   **Estado**: Un número entero (1-127) para distinguir diferentes ocurrencias del mismo error.

### Excepcionar Errores: TRY/CATCH

```sql
/**Excepcionar Errores: TRY/CATCH**/
Begin
        Declare @v_cantidadPedida smallint=110
        Begin Try
                If @v_cantidadPedida>100
                        Raiserror('Cantidad Excede lo permitido..',16,1) --Error Grave
                else
                        Print 'Cantidad Correcta'
        End Try
        Begin Catch
                Print Error_message()
        End Catch
End
go
```

*   `Begin Try ... End Try`: Contiene el código que se desea monitorear en busca de errores.
*   `Begin Catch ... End Catch`: Contiene el código que se ejecuta si ocurre un error dentro del bloque `TRY`.
*   `Error_message()`: Una función de sistema que devuelve el texto del mensaje de error que causó la ejecución del bloque `CATCH`.

## 6. Transacciones

Las transacciones son secuencias de operaciones que se realizan como una única unidad lógica de trabajo. Todas las operaciones en una transacción deben completarse con éxito (commit) o ninguna de ellas debe aplicarse (rollback).

### Creación de Tabla para Demostración

```sql
Create Table OperadoresLogisto
(
idOpe        int,
nomOpe        varchar(50),
distOpe        varchar(50),
busesOpe smallint
)
go
```

### Transacción Implícita

```sql
--Transacción: Implícita - Explícita
--Transacción implícita
Begin
        Declare @vidOpe                int                        ='101',
                        @vnomOpe        varchar(50)        ='Ransa S.A',
                        @vdistOpe        varchar(50)        ='Callao',
                        @vbusesOpe        smallint        = '120'
        Insert OperadoresLogisto
        values (@vidOpe, @vnomOpe, @vdistOpe, @vbusesOpe)
End

Select * From OperadoresLogisto
go
```
En un entorno de SQL Server por defecto, cada sentencia DML (como `INSERT`) se ejecuta como una transacción atómica implícita. Si la sentencia se completa sin errores, los cambios se confirman automáticamente.

### Transacción Explícita

```sql
--Transacción Explícita
Begin
        Begin Transaction T1
                Declare @vidOpe                int                        ='102',
                                @vnomOpe        varchar(50)        ='REFASA',
                                @vdistOpe        varchar(50)        ='RIMAC',
                                @vbusesOpe        smallint        = '15'
                Insert OperadoresLogisto
                values (@vidOpe, @vnomOpe, @vdistOpe, @vbusesOpe)
                If @vdistOpe Not In ('Rimac','Callao','Cercado')
                        Commit Tran T1
                Else
                        RollBack Tran T1
End
go

Select * From OperadoresLogisto
go
```

*   `Begin Transaction T1`: Inicia una transacción explícita con el nombre T1.
*   `Commit Tran T1`: Si la condición es verdadera, la transacción se confirma, haciendo permanentes los cambios.
*   `RollBack Tran T1`: Si la condición es falsa, la transacción se revierte, deshaciendo todos los cambios realizados dentro de ella.
En este ejemplo, dado que `@vdistOpe` es 'RIMAC', la transacción se revertirá (`RollBack`) y la inserción no se hará efectiva.

### Transacción Explícita con RAISERROR y TRY/CATCH

```sql
----Transacción Explícita con RaisError y Try Catch
Begin
        Begin Try
        Begin Transaction T1
                Declare @vidOpe                int                        ='102',
                                @vnomOpe        varchar(50)        ='REFASA',
                                @vdistOpe        varchar(50)        ='RIMAC',
                                @vbusesOpe        smallint        = '15'
                Insert OperadoresLogisto
                values (@vidOpe, @vnomOpe, @vdistOpe, @vbusesOpe)
                If @vdistOpe Not In ('Rimac','Callao','Cercado')
                        Commit Tran T1
                Else
                        RaisError('Distrito no permitido...!!',16,1)
        End Try
        Begin Catch
                        Print error_message()
                        RollBack Tran T1
        End Catch
End
go

-----
Select * From OperadoresLogisto
go
```

Este es el escenario más robusto para el manejo de transacciones y errores:
*   La transacción se inicia dentro de un bloque `TRY`.
*   Si la lógica de negocio falla (distrito no permitido), se lanza un `RAISERROR` con severidad 16.
*   El control pasa al bloque `CATCH`.
*   Dentro del bloque `CATCH`, se imprime el mensaje de error y, de forma crucial, se ejecuta `RollBack Tran T1` para asegurar que la transacción se deshaga completamente, manteniendo la integridad de los datos.
