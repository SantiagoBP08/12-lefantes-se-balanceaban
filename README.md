# RETO #12
## 1. Desarrollar un algoritmo que imprime de manera ascendente los valores (todos del mismo tipo) de un diccionario.

    # Diccionario con TODAS las letras del abecedario y valores asignados
    letras_valores = {
        'a': 5,  'b': 12, 'c': 3,  'd': 15, 'e': 7,  'f': 1,  'g': 20,
        'h': 10, 'i': 4,  'j': 8,  'k': 18, 'l': 2,  'm': 9,  'n': 13,
        'o': 25, 'p': 6,  'q': 14, 'r': 11, 's': 19, 't': 17, 'u': 21,
        'v': 16, 'w': 22, 'x': 23, 'y': 24, 'z': 26
    }

    # Función para imprimir los valores en orden ascendente
    def imprimir_valores_ordenados(diccionario):
        valores = list(diccionario.values())  # Obtiene todos los valores numéricos
        valores.sort()  # Ordena de menor a mayor

        print("\nValores en orden ascendente:")
        for valor in valores:
            print(valor, end=" ")

    # Programa principal
    if __name__ == "__main__":
        print("Diccionario de todas las letras y sus valores:")
        for letra, valor in letras_valores.items():
            print(f"{letra} : {valor}")

        imprimir_valores_ordenados(letras_valores)

## 2. Desarrollar una función que reciba dos diccionarios como parámetros y los mezcle, es decir, que se construya un nuevo diccionario con las llaves de los dos diccionarios; si hay una clave repetida en ambos diccionarios, se debe asignar el valor que tenga la clave en el primer diccionario.

    # Importar pprint para imprimir bonito los diccionarios
    from pprint import pprint

    # Función que mezcla dos diccionarios
    def mezclar_diccionarios(dic1, dic2):
        """
        Mezcla dos diccionarios.
        Si hay claves repetidas, se conservan las del primer diccionario (dic1).
        """
        # Copia del primer diccionario para no modificarlo
        nuevo_dic = dic1.copy()

        # Agrega al nuevo diccionario los elementos del segundo diccionario,
        # solo si la clave no existe ya en el primero
        for clave, valor in dic2.items():
            if clave not in nuevo_dic:
                nuevo_dic[clave] = valor

        return nuevo_dic


    # Diccionario 1
    diccionario1 = {
        'a': 1,
        'b': 2,
        'c': 3,
        'z': 26,
        'h': 15,
        'p': 14
    }

    # Diccionario 2
    diccionario2 = {
        'd': 4,
        'e': 5,
        'f': 6,
        'g': 7,
        'r': 20
    }

    # Mostrar los diccionarios originales
    print("Primer diccionario:")
    pprint(diccionario1)

    print("\nSegundo diccionario:")
    pprint(diccionario2)

    # Mezclar los diccionarios
    mezclado = mezclar_diccionarios(diccionario1, diccionario2)

    # Mostrar el diccionario mezclado ordenado alfabéticamente
    print("\nDiccionario mezclado (ordenado alfabéticamente):")
    for clave in sorted(mezclado):
        print(f"{clave} : {mezclado[clave]}")

    # Mostrar el diccionario completo en una sola línea
    print("\nDiccionario mezclado (en una sola línea):")
    pprint(mezclado)

## 3. Dado el JSON:
