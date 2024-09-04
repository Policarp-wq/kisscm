<h2>Задание 1</h2>
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).
<s>Решение:</s>
cut -d: -f1 /etc/passwd | sort
<img src="https://github.com/user-attachments/assets/c8417021-8448-48f7-adbf-7edbbc22e4cf">

