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
