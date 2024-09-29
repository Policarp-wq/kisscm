# Практическое занятие №2. Менеджеры пакетов

## Задача 1

Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?

```
sudo apt show python3-matplotlib
```

![image](https://github.com/user-attachments/assets/6edfd5c4-1737-4732-b4ac-3de1ec6b50a3)

Содержит информацию о названии пакета, версии, размере, а также зависимостях.

Чтобы установить пакет без менеджера, необходимо скачать его с помощью wget, установить его и зависимости с помощью dpkg.

## Задача 2

Вывести служебную информацию о пакете express (JavaScript). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?

```
npm view express
```
![image](https://github.com/user-attachments/assets/1c166279-82b1-4e9d-94e1-621e28a8b76c)

Содержит зависимости, разработчиков, ключевые слова и время последнего обновления
Установить можно с помощью sudo apt install -y nodejs, скачав при этом репозиторий
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -


## Задача 3

Сформировать graphviz-код и получить изображения зависимостей matplotlib и express.

```
digraph dependencies {
    node [shape=box];

    subgraph cluster_matplotlib {
        label="matplotlib";
        color=blue;
        "matplotlib" -> "jquery";
        "matplotlib" -> "dateutil";
        "matplotlib" -> "packaging";
        "matplotlib" -> "numpy";
        "matplotlib" -> "pyparsing";
        "matplotlib" -> "python-dateutil";
        "matplotlib" -> "cycler";
        "matplotlib" -> "kiwisolver";
        "matplotlib" -> "pillow";
    }

    subgraph cluster_express {
        label="express";
        color=red;
        "express" -> "body-parser";
        "express" -> "cookie";
        "express" -> "accepts";
        "express" -> "array-flatten";
        "express" -> "content-disposition";
        "express" -> "content-type";
        "express" -> "depd";
        "express" -> "etag";
        "express" -> "fresh";
        "express" -> "http-errors";
        "express" -> "encodeurl";
        "express" -> "path-to-regexp";
        "express" -> "qs";
        "express" -> "debug";
    }
}!


```

[image](https://github.com/user-attachments/assets/d2151f63-c518-4f78-90fc-0979cd84b97d)

## Задача 4

**Следующие задачи можно решать с помощью инструментов на выбор:**

* Решатель задачи удовлетворения ограничениям (MiniZinc).
* SAT-решатель (MiniSAT).
* SMT-решатель (Z3).

Изучить основы программирования в ограничениях. Установить MiniZinc, разобраться с основами его синтаксиса и работы в IDE.

Решить на MiniZinc задачу о счастливых билетах. Добавить ограничение на то, что все цифры билета должны быть различными (подсказка: используйте all_different). Найти минимальное решение для суммы 3 цифр.


```
include "alldifferent.mzn";

var 1..9: a;
var 1..9: b;
var 1..9: c;
var 1..9: d;
var 1..9: e;
var 1..9: f;

constraint alldifferent([a, b, c, d, e, f]);

constraint a + b + c = d + e + f;

solve minimize a + b + c;

output [show(a)," ", show(b)," ", show(c)," ", show(d)," ", show(e)," ", show(f)];
```

![image](https://github.com/user-attachments/assets/1b6c4fae-5c4c-419f-bde2-cb3b5f374b42)


## Задача 5

Решить на MiniZinc задачу о зависимостях пакетов для рисунка


```
enum Menu = { v1_5_0, v1_4_0, v1_3_0, v1_2_0, v1_1_0, v1_0_0 };
enum Dropdown = { v2_3_0, v2_2_0, v2_1_0, v2_0_0, v1_8_0 };
enum Icons = {v_2_0_0, v_1_0_0};

array[Menu, Dropdown] of bool: MenuDropdown_compatibility = 
[| true,  true,  true,  true,  false   
 |  true,  true,  true,  true,  false 
 |  true,  true,  true,  true,  false   
 |  true,  true,  true,  true,  false 
 |  true,  true,  true,  true,  false   
 |  false, false, false, false,  true |];

array[Icons, Dropdown] of bool: DropdownIcons_compatibility = 
[| true,  true,  true,  true,  false     
 | false, false, false, false,  true |];
 
var Menu: selectedMenu;
var Dropdown: selectedDropdown;
var Icons: selectedIcon;

constraint MenuDropdown_compatibility[selectedMenu, selectedDropdown] = true;

constraint DropdownIcons_compatibility[selectedIcon, selectedDropdown] = true;

constraint selectedIcon = v_1_0_0;

solve satisfy;

output ["Selected Menu: " ++ show(selectedMenu) ++ "\n" ++
        "Selected Dropdown: " ++ show(selectedDropdown) ++ "\n" ++
        "Selected Icon: " ++ show(selectedIcon)];
```

![image](https://github.com/user-attachments/assets/1a2aa8c2-593b-42ea-8639-1c04d870b3da)


## Задача 6

Решить на MiniZinc задачу о зависимостях пакетов для следующих данных:

```
root 1.0.0 зависит от foo ^1.0.0 и target ^2.0.0.
foo 1.1.0 зависит от left ^1.0.0 и right ^1.0.0.
foo 1.0.0 не имеет зависимостей.
left 1.0.0 зависит от shared >=1.0.0.
right 1.0.0 зависит от shared <2.0.0.
shared 2.0.0 не имеет зависимостей.
shared 1.0.0 зависит от target ^1.0.0.
target 2.0.0 и 1.0.0 не имеют зависимостей.
```

```
enum packages = {
      root, 
      foo_1_0_0, foo_1_1_0, 
      left_1_0_0, right_1_0_0, 
      shared_1_0_0, shared_2_0_0, 
      target_1_0_0, target_2_0_0
  };
  
  array[packages] of var bool: installed;
  
  constraint installed[root];

  constraint
      (installed[root]) -> (installed[foo_1_1_0] /\ installed[target_2_0_0]) /\
      (installed[foo_1_1_0]) -> (installed[left_1_0_0] /\ installed[right_1_0_0]) /\
      (installed[left_1_0_0]) -> (installed[shared_1_0_0]) /\
      (installed[right_1_0_0]) -> (installed[shared_2_0_0]) /\ (not installed[shared_1_0_0]) /\
      (installed[shared_1_0_0]) -> (installed[target_1_0_0]);
  
  output [
      "root " ++ show(installed[root]) ++ "\n" ++ 
      "foo_1_0_0 " ++ show(installed[foo_1_0_0]) ++ "\n" ++ 
      "foo_1_1_0 " ++ show(installed[foo_1_1_0]) ++ "\n" ++ 
      "left_1_0_0 " ++ show(installed[left_1_0_0]) ++ "\n" ++ 
      "right_1_0_0 " ++ show(installed[right_1_0_0]) ++ "\n" ++ 
      "shared_1_0_0 " ++ show(installed[shared_1_0_0]) ++ "\n" ++ 
      "shared_2_0_0 " ++ show(installed[shared_2_0_0]) ++ "\n" ++ 
      "target_1_0_0 " ++ show(installed[target_1_0_0]) ++ "\n" ++
      "target_2_0_0 " ++ show(installed[target_2_0_0]) ++ "\n" 
       ];
```

![image](https://github.com/user-attachments/assets/99ca5178-da09-42d6-86ba-e5c0a09f8a2f)


## Задача 7

Представить задачу о зависимостях пакетов в общей форме. Здесь необходимо действовать аналогично реальному менеджеру пакетов. То есть получить описание пакета, а также его зависимости в виде структуры данных. Например, в виде словаря. В предыдущих задачах зависимости были явно заданы в системе ограничений. Теперь же систему ограничений надо построить автоматически, по метаданным.
