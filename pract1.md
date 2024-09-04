<h2>Задание 1</h2>
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).
<hr>
<strong>Решение:</strong>
<span>cut -d: -f1 /etc/passwd | sort</span>
<br>
<img src="https://github.com/user-attachments/assets/c8417021-8448-48f7-adbf-7edbbc22e4cf">

