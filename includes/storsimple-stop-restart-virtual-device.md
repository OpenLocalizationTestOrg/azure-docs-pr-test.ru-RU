#### <a name="toostop-and-start-a-virtual-device"></a>toostop и запуск виртуального устройства
toostop виртуального устройства, щелкните ее имя и нажмите кнопку **завершение работы**. Пока виртуальное устройство hello завершает работу, она находится в состоянии **остановка**. После остановки hello виртуального устройства, его состояние — **остановлена**.

Используйте следующие командлеты toostop hello и запуск виртуального устройства.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart виртуального устройства
Запуск виртуального устройства, если необходимо toorestart его, щелкните ее имя и нажмите кнопку **перезапустите**. Во время перезапуска виртуального устройства hello, она находится в состоянии **перезапуск**. Когда hello виртуального устройства готов для вас toouse, она находится в состоянии **под управлением**.

Используйте следующий командлет toorestart виртуальное устройство hello.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

