import random
import turtle

# 1. Настройка экрана
screen = turtle.Screen()
screen.title("Черепашьи гонки")
screen.setup(width=500, height=400)

# Рисуем линию финиша (на отметке x = 200)
finish_line = turtle.Turtle()
finish_line.penup()
finish_line.goto(200, 150)
finish_line.pendown()
finish_line.goto(200, -150)
finish_line.hideturtle()

# 2. Создаем 4 черепашек
colors = ["red", "blue", "green", "purple"]
y_positions = [90, 30, -30, -90]  # Чтобы они стояв в ряд и не толкались
all_turtles = []

for i in range(4):
    new_turtle = turtle.Turtle(shape="turtle")
    new_turtle.color(colors[i])
    new_turtle.penup()
    # Стартуем с x = -200, чтобы до финиша (x = 200) было ровно 400 пикселей.
    # Если тебе нужно, чтобы весь путь был ровно 200, поставь стартовый x = 0.
    new_turtle.goto(x=-200, y=y_positions[i])
    all_turtles.append(new_turtle)

# 3. Сама гонка
is_race_on = True

while is_race_on:
    for racer in all_turtles:
        # Случайный шаг от 1 до 5
        random_distance = random.randint(1, 5)
        racer.forward(random_distance)

        # Проверяем, пересек ли кто-то финиш (x >= 200)
        if racer.xcor() >= 200:
            is_race_on = False
            winning_color = racer.pencolor()
            print(f"Победила {winning_color} черепашка!")
            break

# Чтобы окно не закрывалось сразу
screen.exitonclick()
