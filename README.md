# IAV26-TristanAlvarez

> [!NOTE]
> Versión: 0

<!-- > [!NOTE]
> Changelog: 
- [Instalación y uso](#instalación-y-uso), [Punto de partida](#punto-de-partida), [Planteamiento del problema](#planteamiento-del-problema)
  - Actualizados según el cambio del enunciado y plantilla.
- [Diseño de la solución](#diseño-de-la-solución)
  - Ampliada y clarificada la explicación sobre el diseño de la solución.
  - Rellenadas las transiciones entre estados en el diagrama de estados
  - Redactadas las explicaciones de los comportamientos del agente en cada estado.
- [Implementación](#implementación)
  - Rellenada tabla de tareas.
- [Pruebas y métricas](#pruebas-y-métricas)
  - Rellenada sección de métricas y vídeo. -->

## Índice
1. [Autores](#autores)
2. [Resumen](#resumen)
3. [Instalación y uso](#instalación-y-uso)
4. [Introducción](#introducción)
5. [Punto de partida](#punto-de-partida)
6. [Planteamiento del problema](#planteamiento-del-problema)
7. [Diseño de la solución](#diseño-de-la-solución)
8. [Implementación](#implementación)
9. [Pruebas y métricas](#pruebas-y-métricas)
10. [Ampliaciones](#ampliaciones)
11. [Conclusiones](#conclusiones)
12. [Licencia](#licencia)
13. [Referencias](#referencias)

## Autores
- Cynthia Tristán Álvarez [@cyntrist](https://github.com/cyntrist)

## Resumen
Prototipo de combate táctico por turnos en Godot, basado en la serie *Tactics RPG* de The Liquid Fire y a su vez en su adaptación a Godot por *7thSage*. El estado actual incluye tablero con alturas, selección de unidades, movimiento por casillas, control de cámara y una máquina de estados para el flujo principal del combate, pero está previsto continuar el desarrollo hasta el estado más reciente de la serie con habilidades, estadísticas y turnos.

El objetivo académico es extender esta base con inteligencia artificial para enemigos, implementando dos tipos de sistemas: sistemas basados en reglas y sistemas de utilidad, permitiendo evaluar decisiones tácticas en un entorno controlado. El objetivo práctico es comparar los dos enfoques de IA enfrentándolos entre sí en batallas automáticas y analizando métricas de rendimiento y eficacia.

## Instalación y uso
Todo el contenido del proyecto está disponible en este repositorio, con **Godot 4.6** siendo la versión con la que ejecutar el proyecto.

## Introducción
El proyecto se enmarca en la asignatura de Inteligencia Artificial para Videojuegos del Grado en Desarrollo de Videojuegos (UCM). La propuesta parte de un prototipo táctico por turnos para estudiar, implementar y evaluar técnicas de toma de decisiones en agentes no jugadores. 

La referencia principal es la serie *Tactics RPG* de The Liquid Fire y, en particular, la serie *Godot Tactics RPG*. Esta elección permite trabajar sobre una base técnica conocida (tablero, unidades, movimiento, habilidades y estados de batalla) y centrar el esfuerzo en la capa de IA, campo que la serie de tutoriales aún no cubre, a diferencia de la versión original en Unity.

Este prototipo sirve para poner en práctica una de las formas de IA más fundamentales y entendibles de la historia de la inteligencia artificial, sistemas basados en reglas, junto a sistemas basados en utilidad como enfoque avanzado con mejor adaptación situacional. El resultado esperado es un sistema capaz de ejecutar combates tácticos con agentes autónomos, con comportamientos comparables y medibles dentro de un mismo entorno de juego.

## Punto de partida
Se ha implementado desde cero, siguiendo la serie de tutoriales en la que está basado el proyecto, la base sobre la trabajar, que consiste en un entorno isométrico 3D de combate entre dos bandos con unidades capaces de moverse y atacar cuerpo a cuerpo o con habilidades en un cierto rango a lo largo de un entorno en cuadrícula con distintas alturas. 

La implementación de la práctica se centra en el desarrollo de la inteligencia artificial que controlará cada unidad de las tropas de dos ejércitos en la escena. Las tropas de cada bando se diferencian por su color principal.

Al iniciar el prototipo, en el menú principal habrá botones para salir y jugar. Al clicar el de jugar, se iniciará la escena principal de combate y a su vez la simulación, que contará con dos bandos enfrentados y cada uno con distintos tipos de unidades.

Según el tipo que son, una unidad puede ser:

- Terrestre: en su movimiento puede saltar diferencias de altura +/- 1.
- Volador: en su movimiento ignora las alturas, pero necesita que haya suelo en todo su camino.
- Teleportante: en su movimiento ignora tanto las alturas como la necesidad de suelo entre su inicio y su final de trayecto.

<!-- Al clicar al botón *Play* en la escena *IntroMenu*, con el que iniciará el juego, se va a la escena *MainScene*, el nivel de la cárcel espacial, el entorno 3D donde irán apareciendo:
- Prisioneros. Aparecen en alguno de los puntos de regeneración. Pueden moverse, disparar, apuntar, cambiar de arma y correr. Sus movimientos podrán ser implementados mediante mecánicas de IA.

- Recogibles. Sólo los prisioneros pueden cogerlos o utilizarlos:
1. Blaster, pistola por defecto.
2. Escopeta (shotgun), causa daño en un radio más ancho.
3. Launcher, lanza discos de cadencia lenta.
4. Botiquines, para recuperar salud.

- Vigilantes robóticos. Hay de dos tipos, las torretas (Turrets) y los robots flotantes (HoverBots). Las primeras son más poderosas pero permanecen ancladas en sus ubicaciones originales, mientras que los segundos son más débiles pero tienen movilidad. Todos los vigilantes robóticos disparan a los prisioneros y pueden matarlos.  -->


#### Jerarquía de recursos
```text
GodotProject
|-- addons
|   `-- BoardCreatorInspector
|-- Data
|   `-- Levels
|-- Materials
|-- Prefabs
|-- Scenes
|-- Scripts
|   |-- Common
|   |   |-- Input
|   |   |-- State Machine
|   |   `-- UI
|   |-- Controller
|   |   `-- Battle States
|   |-- Enum Extensions
|   |-- PreProduction
|   |-- Test
|   `-- View Model Component
|       `-- Movement
|-- Settings
`-- Textures
    `-- UI
```

<!-- ### Estructura del proyecto -->
<!-- Dentro de FPS los recursos que conforman el proyecto están organizados de esta forma:
* **Animation**. Animaciones, character controllers, máscaras y rigs de todos los personajes que conforman el juego.
* **Art**. Fuentes, materiales, modelos, shaders y texturas.
* **Audio**. Efectos de sonido y música usada durante el juego.
* **Prefabs**. Los prefabricados que se usan en el juego, del avatar, los enemigos, la interfaz y las distintas partes del escenario. 
* **Scenes**. La escena inicial del menú, la escena de la cárcel, las escenas de victoria y derrota, etc. Así como los NavMesh .asset de los distintos escenarios.
* **Scripts**. Todas las clases con el código del proyecto base organizadas en una jerarquía de carpetas.
* **StateMachine**. Todas las clases con el código de la implementación de la práctica 3 "Disturbios orbitales" para la asignatura de Inteligencia Artificial para Videojuegos, usadas para la gestión de la máquina de estados de los agentes y de sus acciones.
* **Tutorials**. Recursos utilizados para la gestión del tutorial del proyecto base. -->

<!-- ### Estructura de las escenas -->
<!-- Para la implementación del proyecto son relevantes dos escenas:
* IntroMenu: Se muestra un botón para jugar y un botón para visualizar los controles.
* MainScene: El mundo virtual con obstáculos, enemigos y puntos de regeneración de personajes y objetos, con su respectiva NavMesh para su correcta navegación. -->

## Planteamiento del problema
**Las características principales del prototipo son:**

* **A.** Hay un **mundo virtual** representado por una cuadrícula 3D de distintas alturas que representa el terreno del combate entre dos bandos con el mismo número de tropas cada uno, diferenciados por su color principal. El escenario sobre el que se combatirá será generado proceduralmente en cada simulación. Hay una cámara principal que el jugador controla en su la rotación y que se centrará en la unidad que esté realizando su turno, y también se contará con una cámara secundaria con una visión general de toda la rejilla.

* **B.** El **flujo del combate** está modelado con estados explícitos a través de una máquina de estados finita para mantener trazabilidad y facilitar la integración de decisiones automáticas. La máquina de estados diferencia entre las distintas fases de los turnos de cada unidad. El órden de ejecución de dichos turnos viene dado por las estadísticas de la unidad al principio de la simulación y tras acabar su turno se recalcula su próxima posición.

* **C.**  El movimiento de las **tropas** y sus habilidades están limitados por alcance, calculado por BFS, según el tipo de unidad y la ejecución de sus acciones es secuencial. En su turno, una unidad podrá moverse y atacar o esperar, y la toma de decisiones será llevada a cabo por inteligencia artificial sin intervención del jugador. 

* **D.** Uno de los bandos luchará a través de un **sistema de decisión basado en reglas**, compuesto por reglas tácticas explícitas y ordenadas por prioridad. Este controlador resolverá cada turno evaluando condiciones del estado del combate (vida propia y enemiga, alcance de movimiento, objetivos disponibles, riesgo de fuego amigo y exposición) para elegir acciones concretas. La interfaz mostrará las métricas principales: FPS y bajas de cada equipo. Cada sistema de IA intentará minimizar sus propias bajas y maximizar los FPS, por lo tanto minimizando su tiempo de ejecución.

* **E.** El otro bando usará un **sistema basado en utilidad** en el que cada acción candidata (moverse a una casilla, usar una habilidad, elegir objetivo y orientación) recibirá una puntuación numérica. Esa puntuación combinará factores como daño esperado, probabilidad de impacto, riesgo recibido, ventaja posicional y valor estratégico del objetivo. 

## Diseño de la solución

<!-- Su principal ventaja es la interpretabilidad: cada decisión puede trazarse a una regla concreta, facilitando depuración y análisis. -->
<!-- La IA seleccionará la alternativa con mayor utilidad total, permitiendo decisiones más adaptativas y un comportamiento menos rígido que el enfoque por reglas. -->

## Implementación
**Tareas:**
<!-- | Estado  |  Tarea  |  Fecha  |  
|:-:|:--|:-:|
| ✔ | Organización del proyecto | 15-4-2026 |
| ✔ | Máquina de estados base | 18-4-2026 |
| ✔ | Manager de transiciones de estados | 18-4-2026 |
| ✔ | Máquina de estados enlazada con HFSM | 18-4-2026 |
| ✔ | HFSM enlazada con BotGameplayActions | 19-4-2026 |
| ✔ | Cámara top down | 19-4-2026 |
| ✔ | Organización del proyecto | 15-4-2026 |
| ✔ | README | 23-4-2026 |
| ✔ | Estados scriptable objects | 27-4-2026 |
| ✔ | Cambio a la nueva plantilla | 30-4-2026 |
| ✔ | HUD métricas | 3-5-2026 |
| ✔ | Implementación de las acciones | 5-5-2026 |
| ✔ | Implementación de los estados | 5-5-2026 |
| ✔ | Transiciones entre estados | 6-4-2026 |
| ✔ | Vídeo | 6-4-2026 |
| ✔ | README | 7-4-2026 | -->

**Diagrama de clases:**
<!-- Las clases principales que se han desarrollados son las siguientes:
```mermaid
classDiagram
      MetricsManager <|-- MonoBehaviour

      CameraCycler <|-- MonoBehaviour

      BotGameplayActions <|-- MonoBehaviour
        class BotGameplayActions {
            +m_NavMeshAgent : NavMeshAgent
            +m_Weapons : PlayerWeaponsManager
            +m_Health : Health
            +m_PlayerCc : PlayerCharacterController
            +m_LastWorldPosForAnim : Vector3
            +m_HasLastWorldPosForAnim : bool
        }

    HFSM <|-- MonoBehaviour
    class HFSM {
        +root : State
        +machine : StateMachine
        +Actions : BotGameplayActions
    }

State <|-- ScriptableObject
      class State {
        +Machine : StateMachine Machine
        +Parent : State
        +ActiveChild : State
        +stateName : string
        +_initialState : State
        +Trasitions : List<State>
    }

AliveState <|-- State
AttackState <|-- State
BotRoot <|-- State
DeadState <|-- State
EngageState <|-- State
HealState <|-- State
PatrolState <|-- State
PursueState <|-- State
RecoverState <|-- State
RunAwayState <|-- State

      class StateMachine {
        +Root : State Root
        +Transitions : TransitionManager
        +Owner : HFSM
        +started : bool started
    }

      class StateMachineBuilder {
        +root : State
    }

      class TransitionManager {
        + Machine : StateMachine
    }
``` -->

<!-- Implementación: Se adjuntan los scripts con el código fuente que implementan las principales características. Los scripts están documentados para mayor claridad y detalle sobre su implementación. -->

<!-- | Característica del prototipo | Descripción de la característica | Script |
|:-:|:-:|:-:|
| A | Cámaras | [CameraCycler](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/Gameplay/CameraCycler.cs) |
| A, B | Acciones de input | [PlayerInputHandler](https://github.com/IAV26-G09/IAV26-G09-P3/blob/main/Assets/FPS/Scripts/Gameplay/Managers/PlayerInputHandler.cs) |
| B, C | Acciones del agente | [BotGameplayActions](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/BotGameplayActions.cs) |
| C, D | Definición de los estados | [Carpeta con todos los estados](https://github.com/IAV26-G09/IAV26-G09-P3/tree/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/States) |
| D | Máquina de estados finita jerárquica | [HFSM](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/HFSM.cs) |
| D | Máquina de estados finita jerárquica | [State](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/State.cs) |
| D | Máquina de estados finita jerárquica | [StateMachine](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/StateMachine.cs) |
| D | Máquina de estados finita jerárquica | [TransitionManager](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/TransitionManager.cs) |
| E | Toma de métricas | [MetricsManager](https://github.com/IAV26-G09/IAV26-G09-P3/blob/1987505ce5d31421eb2d23ec03879448808f8ba5/Assets/FPS/Scripts/StateMachine/MetricsManager.cs) | -->

<!-- | Nuevas respecto a la plantilla | De la plantilla modificadas |  
|:-:|:-:|
| 🟣​​ | 🟡​ | -->

<!-- ### Clases -->


## Pruebas y métricas
### Plan de pruebas

Serie corta y rápida posible de pruebas que pueden realizarse para verificar que se cumplen las características requeridas:
<!-- 
* **1 (A).** Iniciar el juego, seleccionar la opción de *Play*.
* **2 (A).** Observar a través de tanto la vista del agente como alternando con el botón N a la visión de planta del nivel el mundo virtual las diferentes cámaras y el mundo virtual descrito.
* **3 (B).** Observar a través del comportamiento del agente las acciones que puede realizar, dónde ha sido generado y dónde se genera tras morir.
* **4 (C).** Observar el movimiento del agente a lo largo del nivel y su reacción ante enemigos.
* **5 (D).** Observar los cambios de estado del agente ante sus distintas circunstancias, como al percibir a un enemigo, eliminarlo y volver a la patrulla.
* **6 (E).** Observar en la interfaz de usuario las distintas métricas tomadas en tiempo real sobre las estadísticas del agente.
* **7 (A, B, C, D, E).** Pulsar tecla Escape y volver a inicar la observación desde el paso 1. 
-->

### Métricas tomadas
Se tomarán métricas en un PC de estas características:
- **CPU:** Intel Core i5-12600KF a 3.70 GHz
- **GPU:** NVIDIA GeForce RTX 5070 Ti con 16 GB
- **RAM:** 32 GB (16x2) de 4800 MT/s
- **SO:** Windows 11
- **Versión de Godot:** 4.6

<!-- Se han tomado las siguientes métricas: -->


### Vídeo
- Próximamente
<!-- - [Vídeo demostración](https://www.youtube.com/watch?v=wYVlIFyWK8Y) -->

<!-- ## Ampliaciones
Se han pensado las siguientes posibles ampliaciones: 
-->

## Conclusiones
Próximamente.

## Licencias
Licencia MIT [del punto de partida](https://theliquidfire.com/license/).
Licencia MIT [de la adaptación de este repositorio](https://github.com/cyntrist/IAV26-TristanAlvarez/blob/main/LICENSE).

## Referencias
A continuación se detallan todas las referencias bibliográficas, lúdicas o de otro tipo utilizdas para realizar este prototipo. Los recursos de terceros que se han utilizados son de uso público.

Referencias acerca del punto de partida:

[^1]: https://theliquidfire.com/projects/

[^2]: https://theliquidfire.com/2015/11/30/tactics-rpg-intro-to-a-i/

[^3]: https://theliquidfire.com/2015/12/07/tactics-rpg-a-i-part-1/

[^4]: https://theliquidfire.com/projects/

Referencias sobre Rule-based systems:

[^5]: https://narratech.com/es/inteligencia-artificial-para-videojuegos/decision/reglas-y-planificacion/

[^6]: https://en.wikipedia.org/wiki/Rule-based_system

[^7]: https://www.geeksforgeeks.org/artificial-intelligence/rule-based-system-in-ai/

Referencias sobre Utility AI:

[^8]: https://narratech.com/es/inteligencia-artificial-para-videojuegos/decision/probabilidad-y-utilidad/

[^9]: https://en.wikipedia.org/wiki/Utility_system

[^10]: https://www.geeksforgeeks.org/artificial-intelligence/utility-based-agents-in-ai/

[^11]: https://psichix.github.io/emergent/decision_makers/utility_ai/introduction.html

[^12]: https://shaggydev.com/2023/04/19/utility-ai/
