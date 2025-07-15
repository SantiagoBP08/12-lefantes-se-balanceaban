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

    {
	    "jadiazcoronado":{
		    "nombres": "Juan Antonio",
		    "apellidos": "Diaz Coronado",
		    "edad":19,
		    "colombiano":true,
		    "deportes":["Futbol","Ajedrez","Gimnasia"]
	    },
	    "dmlunasol":{
		    "nombres": "Dorotea Maritza",
		    "apellidos": "Luna Sol",
		    "edad":25,
		    "colombiano":false,
		    "deportes":["Baloncesto","Ajedrez","Gimnasia"]
	    }
    }

Codigo: 

    import json

    # Función para cargar un archivo JSON
    def cargar_json(ruta_archivo):
        try:
            with open(ruta_archivo, "r", encoding="utf-8") as archivo:
                return json.load(archivo)
        except FileNotFoundError:
            print("El archivo no fue encontrado. Asegúrate de que exista y esté en la misma carpeta.")
            return {}
        except json.JSONDecodeError:
            print("El archivo no tiene un formato JSON válido.")
            return {}


    # Función para buscar por deporte
    def buscar_por_deporte(datos, deporte):
        print(f"\nPersonas que practican '{deporte}':")
        deporte = deporte.lower()
        for persona in datos.values():
            deportes_normalizados = [d.lower() for d in persona.get("deportes", [])]
            if deporte in deportes_normalizados:
                nombre_completo = persona["nombres"] + " " + persona["apellidos"]
                print("-", nombre_completo)


    # Función para buscar por rango de edades
    def buscar_por_rango_edad(datos, edad_min, edad_max):
        print(f"\nPersonas entre {edad_min} y {edad_max} años:")
        for persona in datos.values():
            edad = persona.get("edad", 0)
            if edad_min <= edad <= edad_max:
                nombre_completo = persona["nombres"] + " " + persona["apellidos"]
                print("-", nombre_completo)


    # ------------------- PROGRAMA PRINCIPAL ---------------------
    if __name__ == "__main__":
        datos = cargar_json("personas.json")

        if datos:
            deporte_usuario = input("Ingrese el deporte que desea buscar: ").strip()
            buscar_por_deporte(datos, deporte_usuario)

            print("\nAhora ingrese el rango de edad:")
            try:
                edad_min = int(input("Edad mínima: "))
                edad_max = int(input("Edad máxima: "))
                buscar_por_rango_edad(datos, edad_min, edad_max)
            except ValueError:
                print("Debes ingresar números válidos para las edades.")

Al correr el codigo desde el terminal con el archivo (consulta_personas.py) basandonos en el Json que teniamo nos da una salida como esta:

<img width="1101" height="406" alt="image" src="https://github.com/user-attachments/assets/63651aa1-44b9-422c-af98-4db4da83aa5f" />

## 4. A través de un programa conectese a al menos 3 API's , obtenga el JSON, imprimalo y extraiga los pares de llave: valor.

        import requests

        # ----------- API 1: PokeAPI -----------
        print("\n--- API 1: PokeAPI ---")
        url1 = "https://pokeapi.co/api/v2/pokemon/pikachu"
        response1 = requests.get(url1)
        data1 = response1.json()
        print(data1)

        print("\nLlave : Valor de PokeAPI")
        for key, value in data1.items():
            print(f"{key} : {value}")


        # ----------- API 2: Advice Slip API -----------
        print("\n--- API 2: Advice Slip ---")
        url2 = "https://api.adviceslip.com/advice"
        response2 = requests.get(url2)
        data2 = response2.json()
        print(data2)

        print("\nLlave : Valor de Advice Slip")
        for key, value in data2.items():
            print(f"{key} : {value}")


        # ----------- API 3: JSONPlaceholder -----------
        print("\n--- API 3: JSONPlaceholder Posts ---")
        url3 = "https://jsonplaceholder.typicode.com/posts/1"
        response3 = requests.get(url3)
        data3 = response3.json()
        print(data3)

        print("\nLlave : Valor de JSONPlaceholder")
        for key, value in data3.items():
            print(f"{key} : {value}")

Con esto terminarias el reto 12 (El ultimo punto (4) lo hice con ayuda de inteligencia artificial para la mejor comprension y desarrollo del codigo).
