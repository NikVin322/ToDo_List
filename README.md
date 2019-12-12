# ToDo_List
## Задание №1 (PHP+XML)

#### Задание
Создать XML файл с определенными полями и заполнить его подходящими данными (XML файл должен быть из 2 или 3 логических уровней), создать функцию которая будет выводить объекты в таблицу, сделать 3 свои функции, добавить функцию которая ищет предметы по имени. Вывести данные в HTML таблицу из XML.
XML файл должен содержать следующие поля : 
- Id
- Ülesanne
- Info
- Kuupaev


#### XML файл
```
<?xml version="1.0" encoding="utf-8" ?>
<TODO>
  <Task>
    <id>1</id>
    <Ulesanne>Do home work(Math)</Ulesanne>
    <Info>Tasks N11, N12, N13</Info>
    <CreateDate>10.11.18</CreateDate>
    <Deadline>11.11.19</Deadline>
    <BoolStatus>true</BoolStatus>
  </Task>
  <Task>
    <id>2</id>
    <Ulesanne>Buy new pencil</Ulesanne>
    <Info>I need new plastic ruler</Info>
    <CreateDate>10.12.19</CreateDate>
    <Deadline>30.12.19</Deadline>
    <BoolStatus>true</BoolStatus>
  </Task>
  <Task>
    <id>3</id>
    <Ulesanne>Buy notebook</Ulesanne>
    <Info>Buy notebook for Engl.</Info>
    <CreateDate>10.10.18</CreateDate>
    <Deadline>12.10.18</Deadline>
    <BoolStatus>false</BoolStatus>
  </Task>
  <Task>
    <id>4</id>
    <Ulesanne>Learn new verse</Ulesanne>
    <Info>Learn verse by random man from textbook</Info>
    <CreateDate>10.12.19</CreateDate>
    <Deadline>21.12.19</Deadline>
    <BoolStatus>true</BoolStatus>
  </Task>
  <Task>
    <id>5</id>
    <Ulesanne>Talk with history teacher</Ulesanne>
    <Info>I don't know some events in WWII</Info>
    <CreateDate>10.01.19</CreateDate>
    <Deadline>12.03.19</Deadline>
    <BoolStatus>false</BoolStatus>
  </Task>
</TODO>
```

#### Чтение XML файла
```
$tasks = simplexml_load_file("todo.xml") -> Task;
```

#### Вывод всех заданий в таблицу
```
<table border="1">
            <tr>
               <th>Id</th>
               <th>Task name</th>
               <th>Description</th>
               <th>CreateDate</th>
               <th>Deadline</th>
               <th>Status</th>
            </tr>
            <?php
            $result = xmlToArray();
            foreach($result as $task) {//выводим данные из XML файла в таблицу
                echo '<tr>';
                    echo '<td>'.($task -> id).'</td>';
                    echo '<td>'.($task -> Ulesanne).'</td>';
                    echo '<td>'.($task -> Info).'</td>';
                    echo '<td>'.($task -> CreateDate).'</td>';
                    echo '<td>'.($task -> Deadline).'</td>';
                    echo '<td>'.($task -> BoolStatus).'</td>';
                echo '</tr>';
            }
            ?>
        </table>
```

#### Функция поиска по названию
```
function searchItemByTask($query){//функция поиска по Task'у и вывода данных в таблицу
    global $tasks;
    $result = array();
    foreach ($tasks as $task){
        if(substr(strtolower($task -> Ulesanne), 0, strlen($query)) == strtolower($query))
            array_push($result, $task);
    }
    return $result;
}
```

#### Берем из первого Task'a название (Ulesanne)
```
<?php
    echo $tasks[0] -> Ulesanne;
?>
```

#### Считаем знаки с помощью функции strlen()
```
<?php
    $var_Ps=$tasks->xpath('/TODO/Task[last()-1]/Info')[0];
    echo strlen($var_Ps);
?>
```

#### Создаем таблицу для данных которые мы будем искать по имени
```
<table border="1">
    <tr>
        <th>Id</th>
        <th>Task name</th>
        <th>Description</th>
        <th>Date of create</th>
        <th>Deadline</th>
        <th>Status</th>
    </tr>
    <?php
        if(!empty($_POST['searchName'])){$result = searchItemByTask($_POST['searchName']);
            foreach($result as $task) {
                echo '<tr>';
                echo '<td>'.($task -> id).'</td>';
                echo '<td>'.($task -> Ulesanne).'</td>';
                echo '<td>'.($task -> Info).'</td>';
                echo '<td>'.($task -> CreateDate).'</td>';
                echo '<td>'.($task -> Deadline).'</td>';
                echo '<td>'.($task -> BoolStatus).'</td>';
                echo '</tr>';
            }
        }
    ?>
</table>
```

#### Строка подключения Bootstrap
```
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
```

#### Строка подключения своего CSS
```
<link rel="stylesheet" href="https://vinogradov17.thkit.ee/ToDo/style.css">
```

## Задание №2 (ASP.NET)

#### Задание
Создать сайт на ASP.NET MVC, где можно будет добавлять задачи к разным датам и разным месяцам. Добавить возможность регистрации и авторизации. Редактирование уже добавленных событий, тасков, дат, а также возможность отметить сделанный таск. Удаление уже ранее добавленных событий и тасков, а также их редактирование и обновление.

#### Сценарий
При заходе на сайт пользователь видит главную старницу, а при попытке перейти на другую страницу пользователя переносит на страницу Log in, а если у него ещё нет своего аккаунта, то ему необходимо перейти на страницу регистрации и зарегистрироваться
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/1.PNG)
Log in пользователя
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/3.PNG)
Регистрация пользователя
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/2.PNG)
После входа в учетную запись пользователь может создавать свои таски, редактировать их, удалять и ставить галочку если пользователь их выполнил
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/4.PNG)
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/5.PNG)
Создание таска
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/7.PNG)
Редактирование таска
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/8.PNG)
Удаление таска
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/9.PNG)
Также пользователь может зайти во вкладку календаря и более удобным способом выбрать дату таска
![ToDo](https://github.com/NikVin322/ToDo_List/blob/master/Screens/6.PNG)
