# мастер-класс проверка

1. Зайти в vs code, слева нажать на иконку расширения ssh, в столбце справа навести мышь на конфиг turtlebroXX, выбрать вторую иконку (открыть новый терминал по ssh)
2. внизу откроется терминал "внутри робота"
3. в терминале ввести:

```bash
roslaunch turtlebro_navigation turtlebro_slam_navigation.launch
```

4. в терминале ноута ввести `rviz`
5.  Теперь нужно настроить отображение элементов в Rviz:



* Нажмите Add, выберите вкладку By topic, выберите источник данных /scan/LaserScan
* Измените Fixed Frame на вкладке Global Option указав точку отсчета - базу робота base\_footprint
* Добавьте отображение карты Add->By Topic->/map->Map
* добавьте отображение модели робота Add -> by display type -> robot model

6. зайти в веб-интерфейс робота, убедиться, что он ездит и все работает в rviz
