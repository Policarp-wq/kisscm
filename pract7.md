# Практическое занятие №7. Генераторы документации

П.Н. Советов, РТУ МИРЭА

## Задача 1

Реализовать с помощью математического языка LaTeX нижеприведенную формулу:
![image](https://github.com/user-attachments/assets/353aa3cb-e3c6-44e7-a434-b640ee8c6ab5)

Прислать код на LaTeX и картинку-результат, где, помимо формулы, будет указано ФИО студента.

Решение:
![image](https://github.com/user-attachments/assets/d5bbaaac-2b76-474e-9969-da099d95e3bb)

<hr>

```Latex
\documentclass[12pt]{article}
\usepackage{amsmath}
\usepackage{amsfonts}

\begin{document}
Tatarkin Evgeniy 

\[
\int_{x}^{\infty} \frac{dt}{t(t^2-1)\log t} = \int_{x}^{\infty} \frac{1}{t \log t} \left( \sum_{m} t^{-2m} \right) dt 
= \sum_{m} \int_{x}^{\infty} \frac{t^{-2m}}{t \log t} dt^{(u = t^{-2m})} = -\sum_{m} \text{li}(x^{-2m})
\]
\end{document}

```

## Задача 2
На языке PlantUML реализовать диаграмму на рисунке ниже. Прислать текст на PlantUML и картинку-результат, в которой ФИО студента заменены Вашими собственными. Обратите внимание на оформление, желательно придерживаться именно его, то есть без стандартного желтого цвета и проч. Чтобы много не писать используйте псевдонимы с помощью ключевого слова "as".

![image](https://github.com/user-attachments/assets/8e3819c6-9cdb-4e71-85b6-5bb9596eacdd)
<hr>
Решение:
```plantuml
@startuml
skinparam monochrome true
actor "Татаркин Евгений Юрьевич" as S
database Piazza as P
actor Преподаватель as T

T -> P : Публикация задачи
activate P
P -> T : Задача опубликована
deactivate P

S -> P : Поиск задач
activate P
P -> S : Получение задачи
deactivate P

S -> P : Публикация решения
activate P
P -> S : Решение опубликовано
deactivate P

T -> P : Поиск решений
activate P
P -> T : Решение найдено
T -> P : Публикация оценки
P -> T : Оценка опубликована
deactivate P

S -> P : Проверка оценки
P -> S : Оценка получена
@enduml
```

![image](https://github.com/user-attachments/assets/6ed7aefc-76f3-49ae-97a1-942cc4d6db90)


