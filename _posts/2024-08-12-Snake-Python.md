---
layout: single
title:  Clásico juego de snake en python  
excerpt: "Revive la nostalgia con Snake, el clásico juego de la serpiente, ahora hecho en Python! 🐍📜 Disfruta de un código simple y adictivo que crece a medida que recoges alimentos. Ideal para aprender y jugar. 🚀🎮"
date: 2024-08-12
classes: wide
header:
  teaser: assets/images/Snake/snake.png
  teaser_home_page: true
categories:
  - python
tags:
  - juegos 
---
# Historia
El juego de la serpiente es uno de los videojuegos más icónicos y conocidos, originalmente popularizado en teléfonos móviles Nokia a finales de los años 90. El objetivo es simple: controlar una serpiente que se mueve por la pantalla, consumiendo comida para crecer, mientras se evita chocar contra las paredes o contra sí misma. Este juego, a pesar de su simplicidad, sigue siendo muy popular y ha sido recreado en innumerables plataformas y lenguajes de programación.

# Funcionalidad
Este proyecto recrea el clásico juego de la serpiente usando Python y la biblioteca gráfica Tkinter. La serpiente se mueve dentro de un área de juego definida (un Canvas) y puede cambiar de dirección en respuesta a las teclas de flecha del teclado. Un cuadrado rojo representa la "comida" y aparece en posiciones aleatorias dentro del área de juego. Cuando la serpiente come la comida, su longitud aumenta y la puntuación del jugador se incrementa. El juego termina si la serpiente choca contra sí misma.

# Explicación del Código
Inicialización de la Ventana y Componentes
```py
class SnakeApp():
    def __init__(self, root):
        self.root = root
        self.root.title("Snake")
        self.root.geometry("450x480")
        self.root.configure(bg='#654321')
        self.root.resizable(width=False, height=False)
```
Aquí se inicializa la ventana principal del juego. Se establece el tamaño de la ventana, el color de fondo, y se impide que la ventana sea redimensionada.

### Lienzo y Etiquetas
```py
self.canvas = Canvas(root, width=400, height=400, bg='black', highlightthickness=0)
self.canvas.place(relx=0.5, rely=0.5, anchor=CENTER)

self.score_label = Label(root, text="Puntuación: 0", font=("Arial", 14), bg='#654321', fg='white')
self.score_label.place(relx=0.5, rely=0.05, anchor=CENTER)
```
Se crea un Canvas donde se dibujará la serpiente y la comida. Además, se añade una etiqueta para mostrar la puntuación actual del jugador.

### Configuración Inicial de la Serpiente
```py
self.snake = []
self.snake_x = 100
self.snake_y = 100
self.direction = {'x': 1, 'y': 0}
self.initial_length = 3
self.create_snake()
```
Se define la posición inicial de la serpiente y su dirección de movimiento. La serpiente comienza con una longitud de 3 segmentos.

### Movimiento de la Serpiente
```py
def move(self):
    if not self.game_over:
        self.snake_x += self.direction['x'] * self.square_size 
        self.snake_y += self.direction['y'] * self.square_size
        self.snake_x %= 400
        self.snake_y %= 400
        if self.check_collision():
            self.end_game()
        for i in range(len(self.snake)-1, 0, -1):
            x1, y1, x2, y2 = self.canvas.coords(self.snake[i-1])
            self.canvas.coords(self.snake[i], x1, y1, x2, y2)
        x1 = self.snake_x
        y1 = self.snake_y
        x2 = x1 + self.square_size
        y2 = y1 + self.square_size
        self.canvas.coords(self.snake[0], x1, y1, x2, y2)
        head_coords = self.canvas.coords(self.snake[0])
        x1_r, y1_r, x2_r, y2_r = self.canvas.coords(self.rect_2)
        if (head_coords[0] < x2_r and head_coords[2] > x1_r) and (head_coords[1] < y2_r and head_coords[3] > y1_r):
            self.randomize_red_square_position()
            self.extend_snake()
            self.score += 1
            self.score_label.config(text=f"Puntuación: {self.score}")
    self.root.after(100, self.move)
```
Este método se ejecuta repetidamente para mover la serpiente en la dirección actual. También verifica si la serpiente ha chocado contra sí misma o si ha comido la comida roja. En caso de que coma, se actualiza la puntuación y se incrementa la longitud de la serpiente.

### Finalización del Juego
```py
def end_game(self):
    if not self.game_over:
        self.game_over = True
        messagebox.showinfo("Game Over", "¡Has perdido!\nPresiona aceptar")
        self.game_over = False
        self.reset_game()
```

Este método muestra un mensaje de "Game Over" y reinicia el juego si la serpiente choca contra sí misma.

### Posibles Mejoras
- **Incremento de Velocidad**: A medida que la puntuación aumenta, se podría incrementar la velocidad de la serpiente para hacer el juego más desafiante.

- **Obstáculos**: Agregar obstáculos aleatorios en el área de juego para aumentar la dificultad.

- **Sonidos**: Incluir efectos de sonido para las acciones como comer la comida o chocar contra sí misma.
Mejorar la Aleatorización del Cuadrado Rojo: Actualmente, el cuadrado rojo aparece en posiciones simétricas. Sería mejor permitir que aparezca en cualquier parte del lienzo.

### Recomendación
Este proyecto es un excelente punto de partida para aprender sobre la programación de interfaces gráficas y la lógica de juegos en Python. Se recomienda experimentar con diferentes mejoras para aprender cómo afectan la jugabilidad y la interacción del usuario.


