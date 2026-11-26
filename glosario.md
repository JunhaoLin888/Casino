# Casino

## Glosario

- **Cliente:** Sujeto que participa en una partida, utiliza una máquina o consume opcionalmente los servicios del bar del casino.
  - **DNI:** Número de identificación único del cliente.
  - **Nombre:** Nombre del cliente (se pueden repetir).
  - **Apellidos:** Apellidos del cliente (se pueden repetir).
  - **FechaNacimiento:** Día, mes y año de nacimiento del cliente.
  - **Fichas:** Crédito válido para jugar partidas en cualquier juego del casino. Las fichas se obtienen pagando dinero real con la tarjeta de crédito/débito de cada cliente.
  - **Vetado:** Indica si un cliente ha sido expulsado del casino o no.
  - **DineroTarjeta:** Dinero disponible en la tarjeta de crédito/débito del cliente. Si el saldo es insuficiente, el cliente no podrá comprar fichas.
  - **Registrado:** Estado de un cliente dado de alta en el sistema del casino, lo que le permite acceder a sus servicios y participar en partidas mientras no esté vetado. Al darse de baja, sus datos personales se eliminan del sistema (salvo que figure como vetado).

- **Empleado:** Sujeto que trabaja en el casino y realiza la actividad definida por su rol.
  - **DNI:** Número de identificación único del empleado.
  - **Nombre:** Nombre del empleado (se pueden repetir).
  - **Apellidos:** Apellidos del empleado (se pueden repetir).
  - **FechaNacimiento:** Día, mes y año de nacimiento del empleado.
  - **ROL:** Papel que desempeña cada empleado:
    - **Limpieza:** Rol que desempeña un empleado cuyo objetivo es eliminar la suciedad, el polvo, las manchas, los residuos y los malos olores del casino.
    - **Seguridad:** Rol que desempeña un empleado cuyo objetivo es proteger a las personas, los bienes y los inmuebles frente a riesgos o delitos.
    - **Crupier:** Rol que desempeña un empleado cuyo objetivo es dirigir y moderar los juegos de mesa del casino.
    - **Admin:** Rol que desempeña un empleado cuyo objetivo es administrar, supervisar y gestionar el funcionamiento general del casino, sus salas y los datos del sistema.
  - **Salario:** Paga mensual que recibe un empleado por su trabajo.

- **Partida:** Periodo en el que se desarrolla un juego con uno o más clientes.
  - **idPartida:** Número de identificación único de cada partida.
  - **hora_inicio:** Hora en la que empieza la partida.
  - **hora_salida:** Hora en la que finaliza la partida.

- **Sala:** Lugar en el que se desarrollan una o más partidas de un solo juego. Puede contener cero o varios elementos de mobiliario.
  - **IdSala:** Número de identificación único de cada sala.
  - **Privada:** Indica si una sala es exclusiva del casino y se reserva para el uso de personas determinadas.
  - **Abierta:** Indica si la sala está abierta o no.

- **Factura:** Documento que genera el cliente para reservar una partida.
  - **NumeroFactura:** Número de identificación único de cada factura.
  - **Importe:** Monto total de dinero gastado en la factura.

- **Bar:** Zona única del casino donde se sirven y gestionan bebidas y el dinero disponible en caja.
  - **abierto:** Indica si el bar está abierto o no.
  - **DineroDisponible:** Cantidad de dinero disponible en la caja del bar.

- **Bebida:** Producto consumible disponible y gestionado en el bar del casino.

- **Mobiliario:** Muebles y equipamiento físico pertenecientes a una única sala del casino.
  - **Modelo:** Tipo o modelo de mueble.
  - **cantidad:** Número de muebles de cada modelo.

- **Juego:** Tipo de actividad que se realiza en una partida, ya sea en una mesa o en una máquina.
  - **NumeroJuego:** Número de identificación único de cada juego.
  - **NombreJuego:** Identifica uno de los siguientes juegos:
    - **Ruleta:** Juego que consiste en predecir en qué casilla numerada caerá una bola tras girar dentro de una rueda horizontal.
    - **Poker:** Juego de cartas y estrategia cuyo objetivo principal es ganar el bote formando la mejor combinación de cinco cartas o logrando que los demás clientes se retiren.
    - **Dados:** Juego que consiste en apostar al resultado de lanzar dos dados en una mesa especial.
    - **BlackJack:** Juego que consiste en competir directamente contra el crupier para sumar 21 puntos o acercarse lo máximo posible sin pasarse.

- **Mesa:** Especialización de juego correspondiente a los juegos de mesa dirigidos por un crupier dentro del casino.

- **Máquina:** Especialización de juego correspondiente a las máquinas en las que un cliente introduce una cantidad de dinero y recibe un premio al obtener una combinación ganadora.
