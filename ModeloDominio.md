# Casino

## Modelo del Dominio

---

### 1. Entidades y atributos

- **Cliente:** `String DNI`, `String Nombre`, `String Apellidos`, `Date FechaNacimiento`, `int Fichas`, `boolean Vetado`, `double DineroTarjeta`, `boolean Registrado`
- **Empleado:** `String DNI`, `String Nombre`, `String Apellidos`, `Date FechaNacimiento`, `String ROL` *(crupier, limpieza, seguridad, admin)*, `double Salario`
- **Partida:** `String idPartida`, `String hora_inicio`, `String hora_final`
- **Sala:** `String IdSala`, `boolean Privada`, `boolean Abierta`
- **Factura:** `String NumeroFactura`, `float Importe`
- **Bar:** `boolean Abierto`, `double DineroDisponible`
- **Producto:** `String IdProducto`, `String Nombre`, `double PrecioCompra`, `double PrecioVenta`, `int Stock`
- **Mobiliario:** `String Modelo`, `int Cantidad`
- **Juego:** `int NumeroJuego`, `String NombreJuego` *(Ruleta, Poker, Dados, BlackJack)*
- **Mesa:** *(subclase de Juego)* `int NumeroMesa`, `int numeroJugadores`, `double LimiteApuesta`
- **Maquina:** *(subclase de Juego)* `String NumeroMaquina`, `double ApuestaMinima`

> **Nota de modelado:** Ninguna clase incluye listas o arrays procedentes de otras clases como atributos, ya que las asociaciones se representan mediante relaciones y cardinalidades en el diagrama de Modelio.

---

## 2. Tabla de relaciones

| | Factura | Cliente | Partida | Juego | Sala | Empleado | Bar | Mobiliario | Producto |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Factura** | | 1 | 0..1 | | | | | | * |
| **Cliente** | * | | | | | | 0..1 | | |
| **Partida** | 1..* | | | 1 | | | | | |
| **Juego** | | | * | | 1..* | | | | |
| **Sala** | | | | 1 | | 1..* | | * | |
| **Empleado** | | | | | * | | 0..1 | | |
| **Bar** | | * | | | | 1..* | | | * |
| **Mobiliario** | | | | | 1 | | | | |
| **Producto** | * | | | | | | 1 | | |

---

## Diagrama de clases

```text
                     ┌──────────────┐
                     │   Cliente    │
                     └─┬──────────┬─┘
                     * │          │ 1
            ┌──────────┘          └──────────┐
       0..1 │                                │ *
     ┌──────┴───────┐                 ┌──────┴───────┐
     │     Bar      │                 │   Factura    │
     └─┬──────────┬─┘                 └─┬──────────┬─┘
  0..1 │        1 │                     │ *        │ 1..*
       │          │   ┌──────────────┐  │          │
       │          └───┤   Producto   ├──┘          │
       │            * └──────────────┘ *           │
  1..* │                                           │ 0..1
┌──────┴───────┐                            ┌──────┴───────┐
│   Empleado   │                            │   Partida    │
└──────┬───────┘                            └──────┬───────┘
  1..* │                                           │ *
       │                                           │
     * │                                         1 │
┌──────┴───────┐ 1..*                     1 ┌──────┴───────┐
│     Sala     ├────────────────────────────┤    Juego     │
└──────┬───────┘                            └──────────────┘
     1 │
       │
     * │
┌──────┴───────┐
│  Mobiliario  │
└──────────────┘
```

### 3. Restricciones de integridad

1. **Unicidad de DNI:** El atributo `DNI` es único e irrepetible tanto para cada `Cliente` como para cada `Empleado`.
2. **Unicidad de identificadores:** Los atributos `idPartida`, `IdSala`, `NumeroFactura`, `IdProducto`, `NumeroJuego`, `NumeroMesa` y `NumeroMaquina` son únicos dentro de sus respectivas entidades.
3. **Mayoría de edad:** Todo `Cliente` y `Empleado` debe ser mayor de edad según su `FechaNacimiento`.
4. **Control de vetos:** Un `Cliente` con `Vetado = true` no puede reservar plaza ni participar en ninguna `Partida` ni utilizar máquinas.
5. **Participación simultánea:** Un `Cliente` solo puede participar en una única `Partida` activa a la vez (controlado a través de sus facturas activas).
6. **Coherencia horaria:** En toda `Partida`, `hora_final` debe ser siempre posterior a `hora_inicio`.
7. **Saldo para fichas:** Un `Cliente` con `DineroTarjeta` insuficiente no puede comprar `Fichas`.
8. **Un juego por sala:** Cada `Sala` aloja partidas de un único `Juego`. (`Bar` es una entidad independiente y no cuenta como sala).
9. **Salas cerradas:** Una `Sala` con `Abierta = false` no puede tener ninguna `Partida` en curso.
10. **Acceso a salas privadas:** Solo los clientes autorizados expresamente por el `Admin` (y que no estén vetados) pueden reservar plaza en una `Sala` con `Privada = true`.
11. **Límites en mesas y máquinas:** En una `Mesa`, el número de clientes simultáneos no puede superar `numeroJugadores` (`> 0`), y tanto `LimiteApuesta` como `ApuestaMinima` en `Maquina` deben ser valores positivos (`> 0`).
12. **Stock y precios en el bar:** El `Stock` de cada `Producto` y el `DineroDisponible` del `Bar` no pueden ser negativos (`>= 0`).

---

### 4. Requisitos de retención de datos

- **Cliente:** Se conservan los datos del cliente mientras permanezca registrado (`Registrado = true`). Cuando se da de baja, se eliminan sus datos personales, salvo que figure como vetado (`Vetado = true`), en cuyo caso se conservan para impedir su reingreso.
- **Empleado:** Se conservan los datos del empleado mientras mantenga relación laboral activa con el casino.
- **Partida y Factura:** Tanto la `Partida` como las `Factura` asociadas se conservan durante todo el desarrollo de la partida (para controlar quién participa y cumplir la restricción de una partida simultánea por cliente) y se mantienen o archivan una vez finalizada la partida según normativa de facturación.
- **Sala, Juego (Mesa y Maquina) y Bar:** Se mantienen de forma permanente mientras estén dados de alta en el casino, actualizando dinámicamente su estado (`Abierta`, `Privada`, `Abierto`, `DineroDisponible`) o configuración (`numeroJugadores`, `LimiteApuesta`, `ApuestaMinima`).
- **Producto:** Se conserva en el inventario del `Bar` mientras forme parte del catálogo, actualizando su `Stock` con cada venta o reposición.
- **Mobiliario:** Se guarda el registro de cada `Modelo` junto con su `Cantidad` y la `Sala` a la que pertenece, actualizándose cuando se reubica o retira equipamiento.
