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
<!-- La práctica consiste en desarrollar un prototipo de IA para Videojuegos, dentro de un entorno virtual que representa una prisión espacial con varios prisioneros (todos enemigos mortales entre sí) más un grupo de vigilantes robóticos que tratan de poner orden. En este entorno nosotros tenemos que programar a un agente inteligente capaz de percibir, moverse, navegar y decidir, como uno más de los prisioneros, de modo que logre maximizar el número de enemigos abatidos y minimizar el número de ocasiones en que él mismo es eliminado. -->

## Instalación y uso
<!-- Todo el contenido del proyecto está disponible en este repositorio, con **Unity 6000.0.66f2** siendo capaces de bajar todos los paquetes necesarios y editar el proyecto. -->

## Introducción
<!-- Este proyecto es una práctica de la asignatura de Inteligencia Artificial para Videojuegos del Grado en Desarrollo de Videojuegos de la UCM, cuyo enunciado original es este: [Disturbios Orbitales](https://narratech.com/es/inteligencia-artificial-para-videojuegos/navegacion/el-secreto-del-laberinto/).

Las prisiones espaciales funcionan como potentes metáforas sobre vigilancia extrema y deshumanización de los reclusos. En estos casos los disturbios pueden originarse por auténticas crisis de supervivencia que se dan en las órbitas de planetas perdidos y otros rincones olvidados del universo.

Entorno a este tema vamos a desarrollar un prototipo centrado en modelar la toma de decisiones de distintos «prisioneros», que intervienen en disturbios armados que se producen en una prisión imaginaria ubicada en una de las lunas que orbitan en torno a Saturno.

Este prototipo sirve para poner en práctica una de las herramientas de toma de decisiones más populares de la industria: la máquina de estados, concretamente la máquina de estados jerárquica. Además se aprovechará la búsqueda de caminos mediante mallas de navegación y el movimiento mediante comportamientos de dirección y hasta algo de gestión sensorial, pero esta vez aprovechando todo lo posible las herramientas que Unity trae integradas. -->

## Punto de partida
<!-- Hemos partido de un proyecto base proporcionado por el profesor y disponible en este repositorio: [fps](https://github.com/narratech/fps).

La base consiste en un menú inicial desde el que se puede iniciar la simulación y consultar los controles del juego.

La implementación de la práctica se centra en el desarrollo de la inteligencia artificial que controlará a *Player* en la escena. 

Al clicar al botón *Play* en la escena *IntroMenu*, con el que iniciará el juego, se va a la escena *MainScene*, el nivel de la cárcel espacial, un entorno 3D explorable donde irán apareciendo:
- Prisioneros. Aparecen en alguno de los puntos de regeneración. Pueden moverse, disparar, apuntar, cambiar de arma y correr. Sus movimientos podrán ser implementados mediante mecánicas de IA.

- Recogibles. Sólo los prisioneros pueden cogerlos o utilizarlos:
1. Blaster, pistola por defecto.
2. Escopeta (shotgun), causa daño en un radio más ancho.
3. Launcher, lanza discos de cadencia lenta.
4. Botiquines, para recuperar salud.

- Vigilantes robóticos. Hay de dos tipos, las torretas (Turrets) y los robots flotantes (HoverBots). Las primeras son más poderosas pero permanecen ancladas en sus ubicaciones originales, mientras que los segundos son más débiles pero tienen movilidad. Todos los vigilantes robóticos disparan a los prisioneros y pueden matarlos.  -->

#### Jerarquía de recursos
<!-- ```text
Assets
├── FPS
│   ├── Animation
│   ├── Art
│   ├── Audio
│   ├── Prefabs
│   ├── Scenes
│   ├── Scripts
│   │   ├── AI
│   │   ├── Game
│   │   ├── Gameplay 
│   │   ├── **StateMachine**
│   │   └── UI
│   └── Tutorials
├── ModAssets
├── NavMeshComponents
├── Rendering
└── TextMesh Pro
```

El grueso de la implementación que concierne a esta práctica está situado en la carpeta **StateMachine**. -->

### Estructura del proyecto
<!-- Dentro de FPS los recursos que conforman el proyecto están organizados de esta forma:
* **Animation**. Animaciones, character controllers, máscaras y rigs de todos los personajes que conforman el juego.
* **Art**. Fuentes, materiales, modelos, shaders y texturas.
* **Audio**. Efectos de sonido y música usada durante el juego.
* **Prefabs**. Los prefabricados que se usan en el juego, del avatar, los enemigos, la interfaz y las distintas partes del escenario. 
* **Scenes**. La escena inicial del menú, la escena de la cárcel, las escenas de victoria y derrota, etc. Así como los NavMesh .asset de los distintos escenarios.
* **Scripts**. Todas las clases con el código del proyecto base organizadas en una jerarquía de carpetas.
* **StateMachine**. Todas las clases con el código de la implementación de la práctica 3 "Disturbios orbitales" para la asignatura de Inteligencia Artificial para Videojuegos, usadas para la gestión de la máquina de estados de los agentes y de sus acciones.
* **Tutorials**. Recursos utilizados para la gestión del tutorial del proyecto base. -->

### Estructura de las escenas
<!-- Para la implementación del proyecto son relevantes dos escenas:
* IntroMenu: Se muestra un botón para jugar y un botón para visualizar los controles.
* MainScene: El mundo virtual con obstáculos, enemigos y puntos de regeneración de personajes y objetos, con su respectiva NavMesh para su correcta navegación. -->

## Planteamiento del problema
**Las características principales del prototipo son:**

* **A.** 

* **B.** 

* **C.** 

* **D.** 

* **E.** 

## Diseño de la solución



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

Implementación: Se adjuntan los scripts con el código fuente que implementan las principales características. Los scripts están documentados para mayor claridad y detalle sobre su implementación.

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

### Clases


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
En un PC de estas características:
- **CPU:** Intel Core i5-12600KF a 3.70 GHz
- **GPU:** NVIDIA GeForce RTX 5070 Ti con 16 GB
- **RAM:** 32 GB (16x2) de 4800 MT/s
- **SO:** Windows 11
- **Versión de Godot:** 4.6

<!-- Se han tomado las siguientes métricas: -->


<!-- ### Vídeo
- [Vídeo demostración](https://www.youtube.com/watch?v=wYVlIFyWK8Y) -->

<!-- ## Ampliaciones
Se han pensado las siguientes posibles ampliaciones: 
-->

## Conclusiones

## Licencia
<!-- Nieves Alonso Gilsanz y Cynthia Tristán Álvarez, con el permiso de Federico Peinado, autores de la documentación, código y recursos de este trabajo, concedemos permiso permanente para utilizar este material, con sus comentarios y evaluaciones, con fines educativos o de investigación; ya sea para obtener datos agregados de forma anónima como para utilizarlo total o parcialmente reconociendo expresamente nuestra autoría.  -->

## Referencias
<!-- A continuación se detallan todas las referencias bibliográficas, lúdicas o de otro tipo utilizdas para realizar este prototipo. Los recursos de terceros que se han utilizados son de uso público.

[^1]: -->