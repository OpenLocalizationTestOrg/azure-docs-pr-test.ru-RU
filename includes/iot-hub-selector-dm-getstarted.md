> [!div class="op_single_selector"]
> * [Устройство — служба Node.js — Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Устройство — служба Node.js — C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Устройство — служба Java — Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Серверной части приложения могут использовать центр IoT Azure примитивы, такие как [двойных устройства] [ lnk-devtwin] и [прямой методы][lnk-c2dmethod], tooremotely запуск и отслеживание Управление действиями устройства на устройствах. Этот учебник показывает, как серверная часть приложения и приложения для устройств совместно tooinitiate и отслеживать перезагрузка удаленного устройства, с помощью центра IoT.

Используйте прямой метод tooinitiate Управление действиями устройства (например, перезагрузки, восстановление заводских настроек и обновление встроенного по) из серверной части приложения в облаке hello. устройство Hello отвечает за:

* Обработка запроса метода hello, отправленных из центра IoT.
* Инициализация hello соответствующее действие конкретного устройства на устройстве hello.
* Предоставление обновления состояния с помощью *сообщил свойства* tooIoT концентратора.

Серверная часть приложения можно использовать в hello облака toorun устройства двойных запросы tooreport о ходе выполнения hello действий управления устройствами.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
