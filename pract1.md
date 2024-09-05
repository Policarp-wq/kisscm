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
#!/bin/sh
message=$1
size=${#message}
echo -n "+"
for ((i=0;i<size + 2; i++))
do
echo -n "-"
done
echo "+"
echo "| $message |"
echo -n "+"
for ((i=0;i<size + 2; i++))
do
echo -n "-"
done
echo "+"
```

<img src="https://github.com/user-attachments/assets/6ad7834d-76bf-4756-ab1f-fe6727d3b2e7">
<hr>

## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

### Решение

```
cat $file | grep -Eo "[a-zA-Z]*" | sort | uniq | xargs
```

<img src="https://github.com/user-attachments/assets/a4110b9c-9ff0-4b02-8a83-f680b2926c0d">
<hr>
