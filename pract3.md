# Практическое занятие №3. Конфигурационные языки

## Задача 1
Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

```
local get_group_name(num) = 'ИКБО-%s-20' % num;


local get_student(age, group, name) ={
  age: age,
  group: group,
  name: name,
} ;

{
  groups: [get_group_name(i) for i in std.range(1, 24)],
  students:[
    get_student(19, get_group_name(4), 'Иванов И.И'),
    get_student(18, get_group_name(5), 'Петров П.П.'),
    get_student(18, get_group_name(5), 'Сидоров С.С.'),
    get_student(19, 'ИКБО-10-23', 'Татаркин Е.Ю.'),
  ],
  "subject": "Конфигурационное управление",
}
```

Результат:

```
{
   "groups": [
      "ИКБО-1-20",
      "ИКБО-2-20",
      "ИКБО-3-20",
      "ИКБО-4-20",
      "ИКБО-5-20",
      "ИКБО-6-20",
      "ИКБО-7-20",
      "ИКБО-8-20",
      "ИКБО-9-20",
      "ИКБО-10-20",
      "ИКБО-11-20",
      "ИКБО-12-20",
      "ИКБО-13-20",
      "ИКБО-14-20",
      "ИКБО-15-20",
      "ИКБО-16-20",
      "ИКБО-17-20",
      "ИКБО-18-20",
      "ИКБО-19-20",
      "ИКБО-20-20",
      "ИКБО-21-20",
      "ИКБО-22-20",
      "ИКБО-23-20",
      "ИКБО-24-20"
   ],
   "students": [
      {
         "age": 19,
         "group": "ИКБО-4-20",
         "name": "Иванов И.И"
      },
      {
         "age": 18,
         "group": "ИКБО-5-20",
         "name": "Петров П.П."
      },
      {
         "age": 18,
         "group": "ИКБО-5-20",
         "name": "Сидоров С.С."
      },
      {
         "age": 19,
         "group": "ИКБО-10-23",
         "name": "Татаркин Е.Ю."
      }
   ],
   "subject": "Конфигурационное управление"
}

```

## Задача 2
Реализовать на Dhall приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

```
let group_count = 24

let get_group = \(i : Natural) -> "ИКБО-${Natural/show (i + 1)}-20"

let range = https://prelude.dhall-lang.org/List/generate

let groups : List Text = range group_count Text get_group

let get_student = 
  \(name : Text) -> 
  \(age : Natural) -> 
  \(group_num : Natural) ->
{ 
  name = name, 
  group = get_group group_num, 
  age = age 
}

let students = [
      get_student "Иванов И.И." 19 3,
      get_student "Иванов И.И." 18 4,
      get_student "Иванов И.И." 18 4,
      get_student "Татаркин Е.Ю" 19 9,
]


let subject = "Конфигурационное управление"

let json =
    { groups = groups
    , students = students
    , subject = subject
    }

in json
```
Результат:
```
{
  "groups": [
    "ИКБО-1-20",
    "ИКБО-2-20",
    "ИКБО-3-20",
    "ИКБО-4-20",
    "ИКБО-5-20",
    "ИКБО-6-20",
    "ИКБО-7-20",
    "ИКБО-8-20",
    "ИКБО-9-20",
    "ИКБО-10-20",
    "ИКБО-11-20",
    "ИКБО-12-20",
    "ИКБО-13-20",
    "ИКБО-14-20",
    "ИКБО-15-20",
    "ИКБО-16-20",
    "ИКБО-17-20",
    "ИКБО-18-20",
    "ИКБО-19-20",
    "ИКБО-20-20",
    "ИКБО-21-20",
    "ИКБО-22-20",
    "ИКБО-23-20",
    "ИКБО-24-20"
  ],
  "students": [
    {
      "age": 19,
      "group": "ИКБО-4-20",
      "name": "Иванов И.И."
    },
    {
      "age": 18,
      "group": "ИКБО-5-20",
      "name": "Иванов И.И."
    },
    {
      "age": 18,
      "group": "ИКБО-5-20",
      "name": "Иванов И.И."
    },
    {
      "age": 19,
      "group": "ИКБО-10-20",
      "name": "Татаркин Е.Ю"
    }
  ],
  "subject": "Конфигурационное управление"
}
```

## Задача 3
Язык нулей и единиц.

```
E = 1 | 0 | E E
```

![image](https://github.com/user-attachments/assets/c3e9b3e0-0c02-4c98-a243-d5621cd351d5)


## Задача 4
Язык правильно расставленных скобок двух видов.

```
E = ( E ) | { E } | E E | 
```

![image](https://github.com/user-attachments/assets/9bbe7d66-d925-4b64-9cb7-e0273d319a33)


## Задача 5
Язык выражений алгебры логики.

```
E = ( E ) | E & E | ~ E | x | y | E
```
![image](https://github.com/user-attachments/assets/cf03353d-76ef-47a1-afdb-b23796b9b5ed)



