> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

В этой статье предоставляет Подробное пошаговое руководство по hello [образец кода Hello World] [ lnk-helloworld-sample] tooillustrate hello базовые компоненты hello [Azure IoT Edge] [ lnk-iot-edge] архитектуры. Hello образец использует hello Azure IoT Edge toobuild простой шлюза, который входит файл tooa сообщение «hello world» каждые пять секунд.

В этом руководстве рассматриваются следующие темы.

* **Hello World пример архитектуры**: описывает как [принципы Azure IoT Edge] [ lnk-edge-concepts] применить Образец Hello World toohello и как взаимодействуют компоненты hello.
* **Как toobuild hello образец**: hello образец hello toobuild необходимые действия.
* **Как toorun hello образец**: hello образец hello toorun необходимые действия. 
* **Обычно результат выполнения**: пример hello вывода tooexpect при запуске образца hello.
* **Фрагменты кода**: коллекцию tooshow фрагменты кода, как Образец Hello World hello реализует ключевые компоненты IoT пограничного шлюза.


## <a name="hello-world-sample-architecture"></a>Архитектура примера hello World
Образец Hello World Hello иллюстрирует hello основные понятия, описанные в предыдущем разделе hello. Образец Hello World Hello реализует IoT шлюзом, имеет конвейер состоит из двух модулей IoT Edge.

* Hello *Здравствуй, мир!* модуль создает сообщение каждые пять секунд и передает его toohello модуль ведения журнала.
* Hello *средства ведения журнала* сообщений hello модуля записи, он получает файл tooa.

![Архитектура примера приложения Hello World, созданного с помощью Edge Интернета вещей Azure][4]

Как описано в предыдущем разделе hello hello World Hello, модуль не проходит сообщений напрямую toohello средства ведения журнала модуля каждые пять секунд. Вместо этого он публикует посредник toohello сообщений каждые пять секунд.

модуль ведения журнала Hello получает сообщение hello из hello broker и обрабатывают, запись содержимого hello файла tooa сообщения hello.

модуль ведения журнала Hello потребляет только сообщения от hello брокера, он никогда не публикует новый брокер toohello сообщений.

![Как hello компонент Service broker перенаправляет сообщения между модулями в Azure IoT Edge][5]

Hello выше рисунке показана hello архитектура Образец Hello World hello и относительные пути hello toohello исходные файлы, которые реализуют различные части образца hello hello [репозитория][lnk-iot-edge]. Изучение кода hello самостоятельно или использовать фрагменты кода hello ниже в качестве руководства.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md