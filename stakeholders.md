# Casino

## Stakeholders

Un *stakeholder* es cualquier persona, rol o entidad con influencia directa o indirecta sobre los requisitos del sistema, independientemente de si interactúa con él o no.

| Stakeholder | Quién es | Qué necesita del sistema | Interacción con el sistema | Influencia sobre los requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **Cliente** | Persona que participa en partidas/máquinas o consume opcionalmente en el bar. | Que sus datos personales, saldo de fichas y facturas (`NumeroFactura`, `Importe`) sean correctos, y que no se le impida jugar por error. | No usa el sistema directamente; aparece registrado en los datos gestionados por el personal. | **Alta:** condiciona los requisitos de precisión en facturación, saldo de fichas y control de vetos. |
| **Crupier** | Empleado que dirige y modera los juegos de mesa (Ruleta, Poker, Dados, BlackJack). | Saber en qué sala y partida trabaja, y poder registrar los datos de cada partida de forma ágil. | Consulta salas y juegos; registra y actualiza datos de las partidas (`hora_inicio`, `hora_final`, participantes). | **Media:** influye en la usabilidad y rapidez de los flujos de registro de partidas. |
| **Equipo de seguridad** | Empleados encargados de vigilar el casino y proteger personas y bienes. | Saber rápidamente qué clientes están vetados (`Vetado`) y controlar el acceso a salas privadas. | Consulta datos de clientes y estado de salas; solicita o registra cambios en el estado de veto. | **Alta:** define requisitos críticos de control de acceso y gestión de clientes vetados. |
| **Equipo de limpieza** | Empleados encargados de la limpieza y el mantenimiento de las instalaciones. | Saber qué salas están abiertas o cerradas y qué mobiliario requiere mantenimiento. | Consulta el listado y estado de salas y mobiliario (solo lectura). | **Baja:** solo requiere acceso de consulta al estado de salas y mobiliario. |
| **Administrador (`admin`)** | Empleado encargado de la gestión operativa diaria del sistema (alta de clientes, caja y facturación). | Dar de alta y actualizar clientes, gestionar la compra de fichas (`DineroTarjeta`), emitir facturas y mantener actualizados los juegos y salas. | Uso directo e intensivo: altas, bajas, modificaciones y emisión de facturas. | **Muy alta:** cubre gran parte de los requisitos funcionales del día a día del casino. |
| **Dirección del casino** | Responsables de administrar y supervisar el negocio. | Tener una visión global y ordenada de la actividad diaria (empleados, salarios, salas, mobiliario, bar e ingresos). | Consulta reportes generales y gestiona empleados (`Salario`, `ROL`), salas y mobiliario. | **Muy alta:** decide el alcance del sistema, las prioridades y el nivel de control requerido. |
| **Encargado del bar** | Responsable de la zona del bar del casino. | Gestionar y reflejar en tiempo real si el bar está abierto o cerrado (`Abierta`). | Consulta y modifica el estado del bar en el sistema. | **Baja:** su influencia se limita al control del estado del bar. |
| **Organismos reguladores** | Autoridades del juego y normativa legal aplicable a un casino real. | Garantizar el cumplimiento legal: verificación de mayoría de edad (`FechaNacimiento`), respeto estricto de vetos y conservación de datos y facturas. | No interactúa con el sistema (es *stakeholder*, pero **no actor**). | **Muy alta:** impone restricciones legales obligatorias que derivan en reglas de negocio y requisitos no funcionales. |

---

### Conflictos detectados entre stakeholders

- **Dirección del casino vs. Crupier:** La dirección necesita que cada detalle de las partidas quede registrado para tener trazabilidad completa, mientras que el crupier necesita un registro rápido para no entorpecer el ritmo de las mesas.
- **Organismos reguladores / Seguridad vs. Cliente:** Los controles estrictos de identidad (`DNI`, `FechaNacimiento`) y el bloqueo inmediato por veto garantizan la legalidad y seguridad, pero pueden chocar con la expectativa del cliente de acceder y jugar de forma rápida y sin fricciones.
- **Dirección del casino vs. Equipo de limpieza:** La dirección prioriza mantener las salas abiertas el mayor tiempo posible para maximizar partidas, mientras que limpieza necesita ventanas en las que las salas figuren como cerradas para realizar su trabajo.

---

### Decisiones sobre roles y actores

- **Cobertura del hueco de roles:** El rol **`admin`** asume las tareas de dar de alta clientes, gestionar la compra de fichas, emitir facturas y administrar el sistema, por lo que aparecerá como actor principal en los casos de uso de gestión.
- **Stakeholders que no son actores:** Los **Organismos reguladores** (y el **Cliente**, si no opera ninguna interfaz propia) condicionan los requisitos del sistema, pero no aparecerán como actores directos en los diagramas de casos de uso.
