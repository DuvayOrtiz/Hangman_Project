# :musical_note: **Hangman_Project** :notes:
Proyecto del curso de programación Universidad Nacional de Colombia, Brayan Ortiz y Laura de la rosa.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/2b5065ce-a8b4-46b0-a619-21b904e05cbf)

# :snowflake: **Proceso de codificación y explicación del codigo** :snowman:
## :zap: **Problemas** :zap:
- El objetivo era hacer un codigo del ahorcado en python y se logró con varias partes
### :maple_leaf: Codigo principal :maple_leaf:
- El codigo principal es el hangman en el que se piden letras para adivinar la palabra dada
```ruby
def ahorcado(prandom, user):
    letrasusadas = []
    n = 6
    x = "_" * (len(prandom)) # lista para mostrar las letras adivinadas

    while n > 0:
        letra = input(user + ", ingresa una letra: ").lower()
        if letra in letrasusadas:
            print(user + ", esa letra ya se usó.")
        else:
            letrasusadas.append(letra)

            if letra in prandom:
                for i in range(len(prandom)):
                    if prandom[i] == letra:
                        x[i] = letra
                print(user + ", Adivinaste una letra")
                print(user + ", La palabra de momento es: " + " ".join(x))
                if "_" not in x:
                    print("Has adivinado la palabra, " + user + " y tu puntaje del 1.0-10.0 es " + str(score))
                    return
            else:
                n -= 1
                print("Faltan", n, "Vidas")

    print("Perdiste, " + user + ". La palabra era: " + prandom)

user = input("ingresar tu nombre: ")
prandom = "palabra" 

ahorcado(prandom)

```
### :cactus: **Evolución del codigo** :cactus:
- Base de datos de al menos 1000 palabras
El archivo se encuentra al inicio y se menciona en las cosas necesarias para poder usar el codigo, es un archivo .txt en el cual hay poco mas de 1000 palabras en español con su definición, y se ingresa al mismo para ser usado en el codigo como diccionario

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/bf7170c7-bf8f-414f-adb6-b54076f214e1)


```ruby
ruta = r"C:\Users\PC\OneDrive\Documents\palesp.txt" # Se abre el archivo y se vuelve un diccionario el contenido
definiciones = {}
with open(ruta, "r", encoding="utf-8") as archivo:
    for linea in archivo:
        partes = linea.strip().split(":")
        if len(partes) == 2:
            palabra = partes[0]
            definicion = partes[1]
            definiciones[palabra] = definicion
```


- Las dos librerias


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/64474844-2024-4b57-817e-d93b93902a48)

- Dibujo de hangman en integraz gráfica
El dibujo se mostrará con una libreria que tenga imagenes predeterminadas y se muestren: 
Algo como asi:
```ruby
import tkinter as tk # Se importan dos librerias, una para elegir palabras random y la otra para mostrar imagenes 
from PIL import ImageTk, Image
root = tk.Tk()
imagen = ImageTk.PhotoImage(Image.open(r"C:\Users\PC\downloads\ss1.ico"))
boton = tk.Button(image=imagen, command=root.quit)
boton.pack()
root.mainloop()
```


- Nivel de dificultad: Asociado a la cantidad de intentos para dibujar el ahorcado, cantidad de caracteres de la palabra.
Lo que se hace es elegir la cantidad de vidas y la cantidad de letras 

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/648c9d49-c83b-44d8-bf01-0d70956e7b2d)

```ruby
difi=input("Ingrese la dificultad, facil(1), normal(2), dificil(3), imposible(4); ") # pedimos al usuario la dificultad de acuerdo con el numero ingresado
    if difi == "1": # Depende del caso se elige el número de vidas y la cantidad de las letras de "prandom"
        prandom = random.choice(palkeysEz)
        n=8
    elif difi == "2":
        prandom = random.choice(palkeysMed)
        n=6
    elif difi == "3":
        prandom = random.choice(palkeysHard)
        n=4
    else:
        prandom = random.choice(palkeysHard)
        n=1
```
##  :herb: **Eventualmente agregamos varias ayudas que son usuales en un juego del ahorcado en la vida real** :herb:
- Poner la palabra entera y que se adivine

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/83c5efc7-7044-4d0d-9dae-5803fd6be15f)




```ruby
palabradefe = input(user + ", ingresa una palabra: ").lower() # Se pide una palabra para ver si se adivina directamente
if palabradefe.lower() == prandom.lower():
    x = palabradefe # Si la palabra es igual se acaba el programa
    print(str(x))
    print("Has adivinado la palabra, " + user + "y tu puntaje del 1.0-10.0 es " + str(score) )
    return
else:
    score -= 0.3 # En caso de no adivinar se hace una reducción de vidas y score
    n -= 1
```
- Saber si hay tildes


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/460bc0b1-5a74-44dc-9649-3d89b4e11589)



```ruby
for i in prandom: # Se busca en la palabra a ver si tiene vocales con tilde
      if i in "áéíóú":
          sitildes = True # Se hace un bandera si existen tildes
      else:
          sitildes = False
  if sitildes:
      print("La palabra contiene tildes") # si es verdadera se imprime que si hay tildes
  else:
      print("La palabra no contiene tildes") # Lo contrario en caso de que no
```
- Poner la primera letra


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/4f4b1742-8cc4-4593-a05f-8d1c186cd7b2)


```ruby
x[0] = prandom[0] # Reemplaza la incognita con la letra en la posicion 0
print(user + ", La palabra de momento es: " + " ".join(x))
proh5 = True # se cambia la bandera a True parano volver a usar la opción

```
- Poner la ultima letra


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/0c6a2e9d-e585-4459-867f-f66a716c9773)


```ruby
x[-1] = prandom[-1]  # Reemplaza la incognita con la letra en la posicion -1
print(user + ", La palabra de momento es: " + " ".join(x))
```
- Poner las vocales



![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/1072b69a-b487-4eda-a212-245136cf4008)


```ruby
vocales = "aeiouáéíóú"
for i in range(len(prandom)):
    if prandom[i] in vocales: # Se revisa si la palabras secreta tiene vocales
        x[i] = prandom[i] # Se ponen las vocales en la incognita
        print(user + ", La palabra de momento es: " + " ".join(x)) # Se muestar la palabra
```
- Dar una definición de la palabra


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/0ea1a90d-33d1-4d4d-8725-f2bde0b86924)


```ruby
if prandom in definiciones:
    print(definiciones[prandom]) # Se imprime el key y la definición de la misma
    proh8 = True # se cambia la bandera a True parano volver a usar la opción
else:
    print("No se encontró la definición de la palabra")
```
- Hacer un menú para interactuar


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/f801cfc7-e833-494a-a0f7-bf35c1afafd2)


```ruby 
while n > 0: # Hacemos un menú que se muestra en bucle hasta que se acaben las vida "n" o cuando se adivine la palabra
        print("_-_-_-_ MENÚ _-_-_-_")
        print("1: Adivinar una letra")
        print("2: Adivinar la palabra directamente")
        print("3: ¿Hay tildes?")
        print("4: Poner vocales")
        print("5: Poner primera letra")
        print("6: Poner última letra")
        print("7: Poner letra aleatoria")
        print("8: ¿Cuál es la definición de la palabra?")
        print("9: Salir")
        opcion = input("Elige una opción: ") # Pedimos un valor para poder usar las opciones
```
# :moyai: **Codigos** :rocket:
##  :four_leaf_clover: **Codigo para jugar solo con la base de datos proporcionada** :four_leaf_clover:

```ruby
Está al inicio como "Hangman_ProjectS"
```


## :hotsprings: **Codigo para jugar y que otra persona elija la palabra** :izakaya_lantern:

```ruby
Está al inicio como "Hangman_ProjectMJ"

```
## :crossed_flags: **Codigo respuesta al problema planteado** :checkered_flag:
```ruby
Está al inicio como "Hangman_Project"
```

# :gem: **Requisitos para uso del codigo** :gem:
- El codigo requiere importar dos librerias:
Importamos ambas librerias.
Ramdom y Tkinder
```ruby
import random
import tkinter
```
# :trophy: Se necesita descargar: :trophy:
HAY QUE TENER EN CUENTA QUE SE DEBE PONER CORRECTAMENTE LA RUTA EN EL CODIGO PARA QUE FUNCIONE BIEN, 
a continuación se ponen los ejemplos usados en mi codigo.
- Las imagenes del inicio que estan como archivos .ico
```ruby
imagen = ImageTk.PhotoImage(Image.open(r"C:\Users\PC\downloads\ss1.ico"))
```
- la base de datos con las palabras y definiciones
```ruby
ruta = r"C:\Users\PC\OneDrive\Documents\palesp.txt" 
with open(ruta, "r", encoding="utf-8") as archivo:
```

## :globe_with_meridians: Instrucciones en el juego :crystal_ball:


- **Nombre**

Pide al usuario una nombre para posteriormente usarlo para referirse al user.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/c8a4b7ae-f16d-49d3-bbb7-f203394ef4a7)



- **Opciones de juego**

Pide al usuario la manera en la que se quiere jugar, hay dos opciones, dos jugadores y solo.


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/3f767d69-5979-497f-9482-99be17637ba6)


- **Dos jugadores**

Si se selecciona esta opción(de hecho tiene su codigo individual), un jugador le pone las condiciones al otro para jugar, le pide de hecho:

La palabra

la definición

La cantidad de intentos


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/376d8e4d-c835-4f0f-a4a6-c00011bad6ac)



- **Solo**

Con esta opción lo que se hace es que la palabra se da de la base de datos, y se pide la dificultad, sabiendo que:

Facil: 8 intentos, palabras con hasta 5 letras;
Medio: 6 intentos, palabras con 5 o 6 letras;
Dificil: 4 intentos, palabras 6 letras en adelante;
Imposible: 1 intento, palabras 6 letras en adelante.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/85fff61c-4fbb-471a-8c61-d23fb14e6915)


- **Menú**

Se muestra el panel con todas las opciones y comodines que se pueden usar.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/21662824-32b4-44ad-932e-ede1441a4f7c)



- **Tildes**

Opción optenida luego de elegir el número 3, se dice si exiten o no exiten tildes en la palabra.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/cf0a8779-b9ac-4a00-ac23-c1b4b12c93db)



- **Adivinar letra**

Opción optenida luego de elegir el número 1, permite poner una letra y ver si se adivina en la palabra.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/98484529-7a30-44df-a404-2fc25d53e8dd)



- **Poner palabra toda falla**

Opción optenida luego de elegir el número 2, se puede adivinar toda la palabra en un solo intento.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/68c94220-0872-4e18-872a-897160a86d50)



- **Letra dada por alguno de los comodines**

Opción optenida luego de elegir los números del 4 al 7, son comodines para elegir una de las letras de la palabra.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/25278205-c6c7-4327-a08a-a3cc77a4e595)



- **Definición**

Opción optenida luego de elegir el número 8, nos da una definición de la palabra que estamos adivinando.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/53ff501e-3fb9-4351-8e51-9d7f591a05b1)


- **Salir del juego**

Opción optenida luego de elegir el número 9, se sale del paenl.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/5d44ec1f-a39c-41ae-a455-7aa6a78da5fb)


- **En caso de fallar** 

En caso de perder intentos se iran poniendo imagenes hasta llegar a la del hangman, la que se ve acontinuación.


![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/33930c12-05e0-4574-833c-dfb8bb760b20)



- **Palabra adivinada**

Mensaje mostrado al adivinar la palabra, muestra a parte un score que depende de los comodines usados.

![image](https://github.com/DuvayOrtiz/Hangman_Project/assets/124726079/7fc8b1fe-cc3b-49d3-8b14-00a57109eacc)



#### **Sin ser más eso es toda la información sobre nuestro codigo** :green_heart:
#### *Creditos Duvay Ortiz :tulip: y Laura De La Rosa 🌹* :smiley:
