# Установка ROS Noetic на Ubuntu 20.04

Сейчас актуальным дистрибутивом ROS (ROS1) является **ROS Noetic Ninjemys** [http://wiki.ros.org/noetic](http://wiki.ros.org/noetic) этот дистрибутив мы и установим.

Оригинальная инструкция по установке ROS находится на сайте ROS [https://www.ros.org/install/](https://www.ros.org/install/). За основу дальнейшей инструкции будет взята страница [https://wiki.ros.org/noetic/Installation/Ubuntu](https://wiki.ros.org/noetic/Installation/Ubuntu)

Для установки ROS на Ubuntu существуют готовые пакеты, нам достаточно добавить репозиторий, содержащий пакеты ROS и установить их обычным для Linux способом.

## Установка пакетов

### Добавление репозитория пакетов ROS

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

### Добавление ключей

(curl может быть уже установлен, тогда при выполнении команды ниже терминал сообщит вам об  этом)

```bash
sudo apt install curl
```

Добавляем ключи:

```bash
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

### Обновление списка пакетов

Когда мы добавили и настроили репозиторий с пакетами ROS, мы должны обновить список пакетов доступных системе для установки. Также рекомендуется обновить все установленные пакеты Ubuntu до установки ROS.

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Установка пакетов ROS

На этапе знакомства с ROS, проще всего установить самую полную версию системы. Данный пакет автоматический установит все основные пакеты ROS, rqt, rviz, библиотеки 2D/3D симуляции, навигации и тп.

```bash
sudo apt install ros-noetic-desktop-full
```

<details>

<summary>Установка дополнительных пакетов</summary>

Если необходимо установить дополнительный пакет, то это можно сделать обычной утилитой установщиком `apt-get`. Например добавить пакет slam-gmapping можно командой.

```bash
sudo apt install ros-noetic-slam-gmapping
```

Поиск пакетов выполняется командой

```bash
apt search ros-noetic
```



</details>

Прежде чем переходить дальше, убедитесь, что в процессе установки не появились сообщения об ошибках.

### Настройка после установки <a href="#nastroika-posle-ustanovki" id="nastroika-posle-ustanovki"></a>

**Установка rosdep**

Прежде чем использовать ROS, вам необходимо инициализировать `rosdep`. `rosdep` позволяет устанавливать системные зависимости для исходных кодов, который вы хотите скомпилировать и требуется для запуска некоторых основных компонентов в ROS.

```bash
sudo rosdep init
```

Затем

```
rosdep update
```

<details>

<summary>Если вылезла ошибка rosdep command not found</summary>

Если при выполнении команды sudo rosdep init возникла ошибка rosdep command not found, нужно выполнить его установку отдельно:

```bash
sudo apt-get install python3-pip
```

```bash
sudo pip install -U rosdep
```

Затем уже инициализировать:

```bash
sudo rosdep init
```

```bash
rosdep update
```

</details>

#### Настройка рабочего окружения <a href="#nastroika-rabochego-okruzheniya" id="nastroika-rabochego-okruzheniya"></a>

Настройка рабочих параметров ROS, происходит через установку переменных окружения (например пути библиотек, адреса серверов и тд). Эту операцию можно делать руками, но проще настроить их автоматический экспорт при запуске интерактивной оболочки bash.

Добавим переменные окружения ROS, для их автоматической установки при запуске bash:

```bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
```

```bash
source ~/.bashrc
```

Если вы просто хотите загрузить переменные ROS **только в текущем сеансе**, то вы можете ввести:

```bash
source /opt/ros/melodic/setup.bash
```

### Установка дополнительных пакетов для разработчиков <a href="#ustanovka-dopolnitelnykh-paketov-dlya-razrabotchikov" id="ustanovka-dopolnitelnykh-paketov-dlya-razrabotchikov"></a>

Если вы собираетесь самостоятельно разрабатывать или вносить изменения в пакеты (вы собираетесь), вам необходимо установить дополнительные пакеты.

```bash
sudo apt-get install python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

**Создание рабочего пространства**

ROS использует специальную систему сборки под названием `catkin`. Чтобы использовать ее, вам необходимо создать и инициализировать папку рабочего пространства.

```bash
 mkdir -p ~/catkin_ws/src
```

```bash
cd ~/catkin_ws/src
```

```bash
catkin_init_workspace
```

### Первый запуск <a href="#pervyi-zapusk" id="pervyi-zapusk"></a>

Установка для ROS завершена, следующая команда запустит сервер (главную ноду) ROS. Закройте все окна терминала и откройте новое окно терминала.

```bash
roscore
```

Если ROS установлена верно, то мы увидим приблизительно такое сообщение при запуске:

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Для остановки `roscore` необходимо нажать Ctrl+C

Если вы хотите чтобы `roscore` запустился в фоновом режиме, то запустите его командой

```bash
roscore &
```
