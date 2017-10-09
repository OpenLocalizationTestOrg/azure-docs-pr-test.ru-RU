#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop и начала облачному устройству

1. toostop устройством облака перейдите toohello виртуальной Машины для вашего устройства облака.
    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. На панели команд hello, нажмите кнопку **остановить**.

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. При появлении запроса на подтверждение нажмите кнопку **Да**.

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. При остановке виртуальная машина освобождается. Во время остановки hello облачному устройству, она находится в состоянии **Deallocating**. После остановки hello облачному устройству, она находится в состоянии **остановлена (освобождена)**.

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Когда виртуальная машина остановлена, щелкните **запустить** (становится доступной кнопка) toostart hello виртуальной Машины. После запуска hello облачному устройству она находится в состоянии **Started**.

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Используйте следующие командлеты toostop hello и запустите облачному устройству.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart облачному устройству

toorestart устройством облака перейдите toohello виртуальной Машины для вашего устройства облака. На панели команд hello, нажмите кнопку **перезапустите**. При появлении запроса подтвердите hello перезапуска. При готовности для вас toouse облачному устройству hello она находится в состоянии **под управлением**.

![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Используйте следующий командлет toorestart облачному устройству hello.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

