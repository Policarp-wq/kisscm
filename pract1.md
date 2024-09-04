<h2>Задача 1</h2>
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).
<hr>
<strong>Решение:</strong>
<br>
<span>cut -d: -f1 /etc/passwd | sort</span>
<br>
<img src="https://github.com/user-attachments/assets/c8417021-8448-48f7-adbf-7edbbc22e4cf">
<h2>Задача 2</h2>
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов
<hr>
<strong>Решение:</strong>
<br>
<span>cut -d: -f1 /etc/passwd | sort</span>
<br>
<img src="https://github.com/user-attachments/assets/c8417021-8448-48f7-adbf-7edbbc22e4cf">
