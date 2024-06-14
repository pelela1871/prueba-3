# prueba-3
me llamo jose palacios de la seccion FPY1101-005D.
import random

# Función para mostrar el tablero
def mostrar_tablero(tablero):
    print("   |   |")
    print(" " + tablero[0] + " | " + tablero[1] + " | " + tablero[2])
    print("   |   |")
    print("-----------")
    print("   |   |")
    print(" " + tablero[3] + " | " + tablero[4] + " | " + tablero[5])
    print("   |   |")
    print("-----------")
    print("   |   |")
    print(" " + tablero[6] + " | " + tablero[7] + " | " + tablero[8])
    print("   |   |")

# Función para comprobar victoria
def comprobar_victoria(tablero, jugador):
    # Combinaciones ganadoras
    combinaciones = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # Horizontales
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # Verticales
        [0, 4, 8], [2, 4, 6]               # Diagonales
    ]
    for combo in combinaciones:
        if all(tablero[i] == jugador for i in combo):
            return True
    return False

# Función para jugar contra la computadora
def nueva_partida():
    tablero = [" "] * 9
    jugador = "X"
    movimientos = {'X': [], 'O': []}  # Diccionario para almacenar los movimientos de los jugadores
    while " " in tablero:
        mostrar_tablero(tablero)
        if jugador == "X":
            movimientos_disponibles = [i for i in range(9) if tablero[i] == " "]
            movimiento = random.choice(movimientos_disponibles)
            tablero[movimiento] = jugador
            movimientos[jugador].append(movimiento)  # Almacenar movimiento del jugador en el diccionario
            if comprobar_victoria(tablero, jugador):
                mostrar_tablero(tablero)
                print("¡Has ganado!")
                return
            jugador = "O"
        else:
            while True:
                movimiento = int(input("Ingrese su movimiento (1-9): ")) - 1
                if movimiento >= 0 and movimiento <= 8 and tablero[movimiento] == " ":
                    tablero[movimiento] = jugador
                    movimientos[jugador].append(movimiento)  # Almacenar movimiento del jugador en el diccionario
                    break
                else:
                    print("Movimiento inválido. Inténtalo de nuevo.")
            if comprobar_victoria(tablero, jugador):
                mostrar_tablero(tablero)
                print("¡La computadora ha ganado!")
                return
            jugador = "X"
    mostrar_tablero(tablero)
    print("¡Empate!")

# Función para jugar contra otro jugador
def versus():
    tablero = [" "] * 9
    jugador = "X"
    movimientos = {'X': [], 'O': []}  # Diccionario para almacenar los movimientos de los jugadores
    while " " in tablero:
        mostrar_tablero(tablero)
        while True:
            movimiento = int(input("Jugador " + jugador + ", ingrese su movimiento (1-9): ")) - 1
            if movimiento >= 0 and movimiento <= 8 and tablero[movimiento] == " ":
                tablero[movimiento] = jugador
                movimientos[jugador].append(movimiento)  # Almacenar movimiento del jugador en el diccionario
                break
            else:
                print("Movimiento inválido. Inténtalo de nuevo.")
        if comprobar_victoria(tablero, jugador):
            mostrar_tablero(tablero)
            print("¡El Jugador " + jugador + " ha ganado!")
            return
        jugador = "O" if jugador == "X" else "X"
    mostrar_tablero(tablero)
    print("¡Empate!")

# Función principal para mostrar el menú
def menu():
    print("¡Bienvenido al juego de El Gato!")
    while True:
        print("\nMenú:")
        print("1. Nueva Partida (Jugador VS Computadora)")
        print("2. Versus (Jugador 1 VS Jugador 2)")
        print("3. Salir")
        opcion = input("Seleccione una opción: ")
        if opcion == "1":
            nueva_partida()
        elif opcion == "2":
            versus()
        elif opcion == "3":
            print("¡Gracias por jugar!")
            break
        else:
            print("Opción inválida. Por favor, seleccione una opción válida.")

# Llamar a la función principal para iniciar el juego
menu()
