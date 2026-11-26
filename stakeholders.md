# Casino

## Stakeholders

Un *stakeholder* es cualquier persona, rol o entidad con influencia directa o indirecta sobre los requisitos del sistema, independientemente de si interactúa con él o no.

| Stakeholder | Quién es | Qué necesita del sistema | Interacción con el sistema | Influencia sobre los requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **Cliente** | Persona que participa en partidas (en mesas o máquinas) y que opcionalmente consume bebidas en el bar del casino. | Que sus datos personales, saldo de fichas y facturas (`NumeroFactura`, `Importe`) sean correctos, y que no se le impida jugar por error. | Aparece registrado en los datos gestionados por el personal. Interactúa directamente solo si el sistema incluye la compra de fichas online/autoservicio. | **Alta:** condiciona los requisitos de precisión en facturación, saldo de fichas y control de vetos. |
| **Crupier** | Empleado que dirige y modera los juegos de mesa (Ruleta, Poker, Dados, BlackJack). | Saber en qué sala y partida trabaja, y poder iniciar, finalizar y consultar las partidas y sus participantes de forma ágil. | Consulta salas, mesas y participantes; registra y actualiza el estado y horarios de las partidas (`hora_inicio`, `hora_salida`). | **Media:** influye en la usabilidad y rapidez de los flujos de gestión de partidas. |
| **Equipo de seguridad** | Empleados encargados de vigilar el casino y proteger personas y bienes. | Saber rápidamente qué clientes están vetados (`Vetado`) y controlar el acceso a las salas privadas. | Consulta datos de clientes y estado de salas; notifica o solicita la aplicación/retirada de vetos. | **Alta:** define requisitos críticos de control de acceso y gestión de clientes vetados. |
| **Equipo de limpieza** | Empleados encargados de la limpieza y el mantenimiento de las instalaciones. | Saber qué salas están abiertas o cerradas y qué mobiliario pertenece a cada sala para su mantenimiento. | Consulta el listado y estado de salas y mobiliario (solo lectura). | **Baja:** solo requiere acceso de consulta al estado de salas y mobiliario. |
| **Administrador (`admin`)** | Empleado encargado de la gestión operativa diaria del sistema. | Gestionar altas, bajas y vetos de clientes; gestionar empleados, salas, mobiliario, juegos (mesas y máquinas), bar (estado, bebidas y `DineroDisponible`), reservas y facturas. | Uso directo e intensivo: realiza la mayoría de las operaciones CRUD, reservas de plaza, facturación, control del bar y apertura/cierre de salas. | **Muy alta:** cubre la mayor parte de los requisitos funcionales del día a día del casino. |
| **Dirección del casino** | Responsables de administrar y supervisar el negocio. | Tener una visión global y ordenada de la actividad diaria (empleados, salarios, salas, mobiliario, ingresos, bebidas y dinero disponible del bar). | Consulta reportes generales y supervisa la gestión de empleados (`Salario`, `ROL`), salas y recursos del casino. | **Muy alta:** decide el alcance del sistema, las prioridades y el nivel de control requerido. |
| **Organismos reguladores** | Autoridades del juego y normativa legal aplicable a un casino real. | Garantizar el cumplimiento legal: verificación de mayoría de edad (`FechaNacimiento`), respeto estricto de vetos y conservación de datos y facturas. | No interactúa con el sistema (es *stakeholder*, pero **no actor**). | **Muy alta:** impone restricciones legales obligatorias que derivan en reglas de negocio y requisitos no funcionales. |
| **Pasarela de pago / Banco** *(si entra compra de fichas)* | Entidad o sistema externo que procesa los pagos con tarjeta de crédito/débito. | Validar que el cliente dispone de saldo suficiente (`DineroTarjeta`) y autorizar el cobro al comprar fichas. | Sistema externo conectado al casino para validar y confirmar transacciones de compra de fichas. | **Media:** condiciona la interfaz externa de pagos y la integridad del saldo de fichas. |

---

### Conflictos detectados entre stakeholders

- **Dirección del casino vs. Crupier:** La dirección necesita que cada detalle de las partidas quede registrado para tener trazabilidad completa, mientras que el crupier necesita un registro rápido para no entorpecer el ritmo de las mesas.
- **Organismos reguladores / Seguridad vs. Cliente:** Los controles estrictos de identidad (`DNI`, `FechaNacimiento`) y el bloqueo inmediato por veto garantizan la legalidad y seguridad, pero pueden chocar con la expectativa del cliente de acceder y jugar de forma rápida y sin fricciones.
- **Dirección del casino vs. Equipo de limpieza:** La dirección prioriza mantener las salas abiertas el mayor tiempo posible para maximizar partidas, mientras que limpieza necesita ventanas en las que las salas figuren como cerradas para realizar su trabajo.

---

### Decisiones sobre roles y actores

- **Gestión centralizada en `admin`:** El rol **Administrador (`admin`)** asume las tareas de gestión de clientes, reservas/facturación, empleados, salas, mobiliario, juegos (mesas y máquinas) y control del bar (abrir, cerrar, gestionar bebidas, dinero disponible y asignar empleados), evitando crear roles adicionales innecesarios.
- **Stakeholders que no son actores:** Los **Organismos reguladores** condicionan los requisitos del sistema, pero no aparecerán como actores en los diagramas de casos de uso.
- **Participación del Cliente y Pasarela de pago:** Queda supeditado al alcance final del equipo confirmar si la compra de fichas con tarjeta entra en el sistema; en caso negativo, se eliminará la fila de la pasarela de pago y el cliente pasará a no ser actor directo.
