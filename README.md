print("Gestor de entradas Conejo simpatico")
# datos principales
lista_nombres = []              # lista para mostrar orden
compradores   = {}              # nombre : {"tipo": ..., "codigo": ...}

# validación de código
def codigo_valido(c):
    if len(c) < 6 or " " in c:
        return False
    hay_mayus = hay_num = False
    for ch in c:
        if 'A' <= ch <= 'Z':
            hay_mayus = True
        if '0' <= ch <= '9':
            hay_num = True
    return hay_mayus and hay_num

# funciones del menú
def comprar_entrada():
    while True:
        nombre = input("Ingrese nombre de comprador: ").strip()
        if nombre and nombre not in compradores:
            break
        print("Nombre repetido o vacío. Intente otra vez.")
    while True:
        tipo = input("Ingrese tipo de entrada (G/V): ").strip()
        if tipo == "g":
            tipo = "G"
        elif tipo == "v":
            tipo = "V"
        if tipo in ("G", "V"):
            break
        print("Solo G o V.")
    while True:
        codigo = input("Ingrese código de confirmación: ").strip()
        if codigo_valido(codigo):
            print("Código validado. ¡Entrada registrada con éxito!")
            break
        print("Código no válido. Intente otra vez.")

    if tipo == "V":
        lista_nombres.insert(0, nombre)  # VIP miembros
    else:
        lista_nombres.append(nombre)     # Publico general
    compradores[nombre] = {"tipo": tipo, "codigo": codigo}

# Guardar datos del comprador
def consultar_comprador():
    nombre = input("Ingrese nombre de comprador a buscar: ").strip()
    datos = compradores.get(nombre)
    if datos:
        print(f"Tipo de entrada: {datos['tipo']}, Código: {datos['codigo']}")
    else:
        print("El comprador no se encuentra.")

def cancelar_compra():
    nombre = input("Ingrese nombre de comprador a cancelar: ").strip()
    if nombre in compradores:
        compradores.pop(nombre)       
        if nombre in lista_nombres:
            lista_nombres.remove(nombre) 
        print("¡Compra cancelada!")
    else:
        print("No se pudo cancelar la compra.")

# ciclo principal
while True:
    try:
        print("\nMENU PRINCIPAL")
        print("1.- Comprar entrada.")
        print("2.- Consultar comprador.")
        print("3.- Cancelar compra.")
        print("4.- Salir.")
        opcion = int(input("Ingrese opción: "))
    except ValueError:
        print("Debe ingresar un número.")
        continue

    if   opcion == 1: comprar_entrada()
    elif opcion == 2: consultar_comprador()
    elif opcion == 3: cancelar_compra()
    elif opcion == 4:
        print("Programa terminado...")
        break
    else:
        print("Debe ingresar una opción válida!!")
else:
    print("Gracias por usar el sistema.")
