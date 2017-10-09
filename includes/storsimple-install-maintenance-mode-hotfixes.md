<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall исправлений в режиме обслуживания через Windows PowerShell для StorSimple
> [!IMPORTANT]
> В режиме обслуживания сначала требуется tooapply hello исправления на одном контроллере и затем на hello другой контроллер.
> 
> 

1. Поместите hello устройства в режим обслуживания. В разделе [шаг 2: режим обслуживания, введите](../articles/storsimple/storsimple-update-device.md#step2) инструкции tooenter режима обслуживания.
2. исправление tooapply hello, тип:
   
     `Start-HcsHotfix` 
3. При появлении запроса укажите hello путь toohello общей сетевой папке, содержащей файлы исправлений hello.
4. После этого введите подтверждение для применения этих исправлений. Тип **Y** tooproceed с установкой исправления hello.
5. После применения исправления hello на одном контроллере, вход в систему toohello другой контроллер. Примените исправление hello, как и для предыдущего контроллера hello.
6. После применения исправления hello, выйдите из режима обслуживания. Инструкции см. в разделе [Шаг 4. Выход из режима обслуживания](../articles/storsimple/storsimple-update-device.md#step4).

