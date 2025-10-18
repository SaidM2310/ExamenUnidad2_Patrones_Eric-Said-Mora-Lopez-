### Autor
**Eric Said Mora López** 
**21210403**
---
# 🎮 Sala de Juegos en Línea


## Descripción del Proyecto

El proyecto consiste en una lobby con 6 salas de juego donde los jugadores pueden conectarse, moverse libremente y participar en partidas de Piedra, Papel o Tijera.

### Características principales:
- La lobby cuenta con:
  - **6 salas de juego**
  - **1 botón para conectar jugador**
  - **1 botón para desconectar jugador**
  - **Jugadores visibles en el escenario**

### Conexión de jugadores
- Se puede presionar el botón "Conectar jugador" hasta un máximo de 3 jugadores.  
- Cada jugador es tomado de un Object Pool y puede moverse libremente por la lobby.

### Controles de movimiento
- **Jugador 1:** `W`, `A`, `S`, `D`  
- **Jugador 2:** `I`, `J`, `K`, `L`  
- **Jugador 3:** `G`, `V`, `B`, `N`

### Salas de juego
- Al entrar a una sala, se abre otra pestaña:
  - Si es el primer jugador, aparecerá un mensaje:  
    > "Esperando 1 jugador más..."
  - El juego inicia automáticamente cuando entra el segundo jugador.

### Juego: Piedra, Papel o Tijera
- En la pestaña de la sala de juego aparecen 6 botones:
  - **3 botones inferiores:** jugador 1  
  - **3 botones superiores:** jugador 2  
- Cada jugador selecciona una sola opción.  
- El resultado puede ser:
  1. **Empate**
  2. **Victoria**
  3. **Derrota**

- Al finalizar, el juego se cierra y los jugadores regresan a la lobby principal.

### Desconexión
- Al presionar el botón "Desconectar jugador", el jugador 1 regresa al Object Pool.
