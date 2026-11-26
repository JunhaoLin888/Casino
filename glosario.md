"# Casino"

—- Glosario —-

-Cliente: Sujeto que participa en una partida, máquina o consume los servicios del casino.
  DNI: Número de identificación único del cliente
  Nombre: Nombre del cliente (se pueden repetir)
  Apellidos: Apellidos del cliente (se pueden repetir)
  FechaNacimiento: Día, mes y año de nacimiento del cliente
  Fichas: Crédito válido para jugar partidas en cualquier juego del casino. Las fichas se sacan pagando dinero real de la tarjeta de crédito/débito de cada cliente
  Vetado: Describe si un cliente ha sido o no expulsado
  DineroTarjeta: Dinero que tiene un cliente en su tarjeta de crédito/débito. Si el dinero es insuficiente, el cliente no podrá comprar fichas

-Empleado: Sujeto que trabaja en el casino y realiza la actividad que le venga definida por su rol.
  DNI: Número de identificación único del empleado
  Nombre: Nombre del empleado (se pueden repetir)
  Apellidos: Apellidos del empleado (se pueden repetir)
  FechaNacimiento: Día, mes y año de nacimiento del empleado
  ROL: Papel que desempeña cada empleado: 
  Limpieza: Rol que desempeña un empleado en la cual su objetivo es eliminar la suciedad, el polvo, las manchas, los residuos y los malos olores del casino.
  Seguridad: Rol que desempeña un empleado en la cual su objetivo es proteger a las personas, los bienes y los inmuebles frente a riesgos o delitos.
  Crupier: Rol que desempeña un empleado en la cual su objetivo es dirigir y moderar los juegos de mesa del casino.
  Salario: Paga que recibe mensualmente por su trabajo un empleado

-Partida: Periodo en el que se desarrolla un juego con uno o más clientes 
  idPartida: Número de identificación único de cada partida
  hora_inicio: Hora en la que empieza la partida
  hora_final: Hora en la que finaliza la partida

-Sala: Lugar en el que se desarrollan una o más partidas de un solo juego.
  IdSala: Número de identificación único de cada sala
  Privada: Sala exclusiva del casino que se reserva para el uso de personas determinadas. Indica si una sala es privada o no 
  Abierta: Indica si la sala está abierta o no

-Factura: Documento que hace el cliente para reservar una partida.
  idFactura: Número de identificación único de cada factura
  costo: Monto de dinero total gastado en la factura

-Bar: Zona del bar donde se consumen bebidas alcohólicas. 
  Abierta: Indica si el bar está abierto o no.

-Mobiliario: Muebles del casino.
  Modelo: Tipo de mueble.
  Máquina: Mobiliario en el que un usuario juega metiendo una cantidad de dinero y al salir una combinación ganadora devuelve dinero.

-Juego: Tipo de actividades que se realizan en una partida.
  *NombreJuego:  Identifica uno de los siguientes juegos:
    Ruleta: Tipo de juego en el que consiste en predecir en qué casilla numerada caerá una bola tras girar dentro de una rueda horizontal.
    Poker: Tipo de juego en el que consiste en juego de cartas y estrategia donde el objetivo principal es ganar el bote de apuestas formando la mejor combinación de cinco cartas o logrando     que los demás se retiren.
    Dados: Tipo de juego en el que consiste en apostar al resultado de lanzar dos dados en una mesa especial.
    BlackJack: Tipo de juego en el que consiste en competir directamente contra el croupier para sumar 21 puntos o acercarse lo máximo posible sin pasarte.

