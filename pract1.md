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

## Задача 5

Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin

### Решение

```
#!/bin/sh
chmod a=rwx $1
sudo cp $1 /usr/local/bin
```

<img src="https://github.com/user-attachments/assets/ba2b3ff8-af76-442b-a570-dac77fda5c9d">
<hr>

## Задача 6

Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

### Решение

```
#!/bin/bash

filename="$1"
file_extension="${filename##*.}"

if [[ "$file_extension" == "js" || "$file_extension" == "py" || "$file_extension" == "c" ]]; then
    first=$(head -n 1 $filename) 
	if [[ $first =~ "#" || $first =~ "//" ]]
		then echo "First line contains comment"
		else echo "No comment"
	fi
else 
	echo "Wrong extension"
fi
	
```

<img src="https://github.com/user-attachments/assets/9d0dee0a-03c8-4ce2-97ed-57e737f52315">
<hr>

## Задача 7

Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

### Решение

```
#!/bin/bash
#Решение построено на идеии сравнивания хэшей
# Переменная для директории
directory="$1"
# Поиск всех файлов, вычисление их хеша и сохранение в файл временного списка
# -exec md5sum {} + позволяет выполнить команду для каждого файла а не по отдельности
find "$directory" -type f -exec md5sum {} + | sort > /tmp/file_hashes.txt
# Вывод файлов-дубликатов
echo "Найденные дубликаты:"
awk '{print $1}' /tmp/file_hashes.txt | uniq -d | while read hash; do
  grep "^$hash" /tmp/file_hashes.txt | awk '{print $2}'
done

```

<img src="https://github.com/user-attachments/assets/de4604c8-0e84-43a4-8ea4-54a75cf82519">
<hr>

## Задача 8

Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.

### Решение

```
#!/bin/sh
extension=$1
find . -name "*.$extension" -print0 | tar -czvf archive.tar.gz --null -T -
```

<img src="https://github.com/user-attachments/assets/1110930f-6520-4b11-8ad5-ad7dcad5c086">
<img src="https://github.com/user-attachments/assets/d8c2259e-4d08-4cfe-ae2d-49892e436863">
<hr>

## Задача 9

Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.

### Решение

```
#!/bin/bash
input=$1
output=$2
cp $input $output
sed -i 's/    /\t/g' $output
```

<img src="https://github.com/user-attachments/assets/3a1953e0-ae9e-4281-ae67-5c4108834005">

<img src="https://github.com/user-attachments/assets/39ebbb07-1c8b-4731-a794-72372730c003">
<hr>

## Задача 10

Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром.

### Решение

```
#!/bin/bash
dir=$1
for file in "$dir"/*.txt; do
	if [ -f "$file" ]&&[ ! -s "$file" ]; then
		echo "$file"
	fi 
done
```

<img src="https://github.com/user-attachments/assets/7905b39e-826e-4c32-8090-1655f9bb209b">
<hr>
