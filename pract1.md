## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

### Решение

```
cut -d: -f1 /etc/passwd | sort
```

<img src="https://github.com/user-attachments/assets/c8417021-8448-48f7-adbf-7edbbc22e4cf">
<hr>

## Задача 2

Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов

### Решение

```
cat /etc/protocols | tail -n5 | sort -n -r -k2 | awk '{print($2, $1)}'
```

<img src="https://github.com/user-attachments/assets/23f82735-5872-4e81-8dd3-82548057f686">
<hr>

## Задача 3

Написать программу banner средствами bash для вывода текстов

### Решение

```
string=$1
size=${#string}
echo -n "+"
for ((i=-2;i<size;i++))
do
echo -n "-"
done
echo "+"
echo "| $string |"
echo -n "+"
for ((i=-2;i<size;i++))
do
echo -n "-"
done
echo "+"
```

<img src="https://github.com/user-attachments/assets/23f82735-5872-4e81-8dd3-82548057f686">
<hr>
