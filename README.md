# Métodos DLL (proyecto):
Lincenciatura en matemáticas. Joshua Estuardo 1018-26-13635

from traceback import print_tb

class Nodo:
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None
        self.anterior = None

class ListaEnlazadaDoble:
    def __init__(self):
        self.primero = None
        self.ultimo = None

    def insertar_final(self, dato):
        nuevo_nodo = Nodo(dato)
        if self.primero is None:
            self.primero = self.ultimo = nuevo_nodo
        else:
            aux = self.ultimo
            self.ultimo = aux.siguiente = nuevo_nodo
            self.ultimo.anterior = aux

    def insertar_inicio(self, dato):
        nuevo_nodo = Nodo(dato)

        if self.primero is None:
            self.primero = self.ultimo = nuevo_nodo
        else:
            nuevo_nodo.siguiente = self.primero
            self.primero.anterior = nuevo_nodo
            self.primero = nuevo_nodo

    def insertar_en_una_posicion(self, dato, pos):
        nuevo_nodo = Nodo(dato)

        if pos == 0:
            self.insertar_inicio(dato)
            return

        aux = self.primero
        con = 0

        while aux is not None and con < pos - 1:
            aux = aux.siguiente
            con += 1

        if aux is None:
            print("Posición fuera de rango")
            return

        if aux.siguiente is None:
            aux.siguiente = nuevo_nodo
            nuevo_nodo.anterior = aux
            self.ultimo = nuevo_nodo
        else:
            nuevo_nodo.siguiente = aux.siguiente
            nuevo_nodo.anterior = aux
            aux.siguiente.anterior = nuevo_nodo
            aux.siguiente = nuevo_nodo

    def insertar_despues_elemento(self, dato, valor):
        nuevo_nodo = Nodo(dato)

        aux = self.primero

        while aux is not None and aux.dato != valor:
            aux = aux.siguiente

        if aux is None:
            print("Elemento no encontrado")
            return

        if aux.siguiente is None:
            aux.siguiente = nuevo_nodo
            nuevo_nodo.anterior = aux
            self.ultimo = nuevo_nodo
        else:
            nuevo_nodo.siguiente = aux.siguiente
            nuevo_nodo.anterior = aux
            aux.siguiente.anterior = nuevo_nodo
            aux.siguiente = nuevo_nodo

    def mostrar_inverso(self):
        if self.ultimo is None:
            print("Lista vacia")
            return
        aux = self.ultimo
        text = ""
        while aux is not None:
            text += " " + str(aux.dato) + " <-->"
            aux = aux.anterior
        print(text + " nullo")

    def eliminar_inicio(self):
        if self.primero is None:
            print("No hay elementos en la lista")
        elif self.primero.siguiente is None:
            self.primero = self.ultimo = None
        else:
            self.primero = self.primero.siguiente
            self.primero.anterior = None

    def eliminar_final(self):
        if self.ultimo is None:
            print("No hay elementos en la lista")
        elif self.primero.siguiente is None:
            self.ultimo = self.primero = None
        else:
            self.ultimo = self.ultimo.anterior
            self.ultimo.siguiente = None

    def eliminar_nodo(self, dato):
        if self.primero is None:
            print("No hay elementos en la lista")
            return

        aux = self.primero

        while aux is not None and aux.dato != dato:
            aux = aux.siguiente

        if aux is None:
            print("Elemento no encontrado")
            return

        if aux == self.primero:
            self.eliminar_inicio()
        elif aux == self.ultimo:
            self.eliminar_final()
        else:
            aux.anterior.siguiente = aux.siguiente
            aux.siguiente.anterior = aux.anterior

    def modificar(self, dato, valor):
        if self.primero is None:
            print("No hay elementos en la lista")
            return

        aux = self.primero

        while aux is not None and aux.dato != dato:
            aux = aux.siguiente

        if aux is None:
            print("Elemento no encontrado")
            return

        aux.dato = valor

    def mayor_menor(self):
        aux = self.primero
        valores = []
        while aux is not None:
            valores.append(aux.dato)
            aux = aux.siguiente
        valores.sort(reverse = True)
        print(valores)

    def menor_mayor(self):
        aux = self.primero
        valores = []
        while aux is not None:
            valores.append(aux.dato)
            aux = aux.siguiente
        valores.sort()
        print(valores)

    def suma_todos_elemento(self):
        if self.primero is None:
            print("No hay ningún elemento en la lista")
            return

        text = ""
        apuntador = self.primero
        while apuntador is not None:
            text += " " + str(apuntador.dato) + " +"
            apuntador = apuntador.siguiente
        a= text + " nullo"

        aux = self.primero
        valores = []
        while aux is not None:
            valores.append(aux.dato)
            aux = aux.siguiente
        print(a)
        print(sum(valores))

    def __str__(self):
        if self.primero is None:
            print("No hay ningún elemento en la lista")
            return

        text = ""
        apuntador = self.primero
        while apuntador is not None:
            text += " " + str(apuntador.dato) + " <-->"
            apuntador = apuntador.siguiente
        return text + " Nullo"

lista = ListaEnlazadaDoble()

print("Insertar al final: ")
lista.insertar_final(1)
lista.insertar_final(2)
lista.insertar_final(3)
lista.insertar_final(4)
print(lista)

print("\n Eliminar al incio")
lista.eliminar_inicio()
lista.eliminar_inicio()
print(lista)

print("\n Insertar al inicio:")
lista.insertar_inicio(5)
lista.insertar_inicio(6)
print(lista)

print("\n Eliminar al final:")
lista.eliminar_final()
lista.eliminar_final()
print(lista)

print("\nInsertar en una posición: ")
lista.insertar_en_una_posicion(7, 2)
lista.insertar_en_una_posicion(8, 1)
lista.insertar_en_una_posicion(9, 4)
print(lista)

print("\n Eliminar un nodo específico:")
lista.eliminar_nodo(8)
lista.eliminar_nodo(9)
print(lista)

print("\n Mostrar lista invertida:")
lista.mostrar_inverso()

print("\n Insertar después de un elemento buscado:")
lista.insertar_despues_elemento(10, 7)
lista.insertar_despues_elemento(11, 6)
print(lista)

print("\n Modificar nodo:")
lista.modificar(11, 2)
lista.modificar(5, 2)
print(lista)

print("\n Mayor a menor elemento:")
lista.mayor_menor()

print("\n Menor a mayor elemento:")
lista.menor_mayor()

print("\n Suma de todos los elementos:")
lista.suma_todos_elemento()
