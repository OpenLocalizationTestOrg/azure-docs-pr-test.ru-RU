### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Подготовка к принудительной установке на компьютер Windows

1. Убедитесь, что сетевое подключение между компьютером Windows hello и сервера обработки hello.
2. Создайте учетную запись, что сервер обработки hello можно использовать tooaccess hello компьютера. Hello учетная запись должна иметь права администратора (локальные или доменные). (Использовать эту учетную запись только для принудительной установки hello и для обновлений агента).

   > [!NOTE]
   > Если вы не используете учетную запись домена, отключите управления удаленного доступа пользователя на локальном компьютере hello. toodisable управления удаленного доступа пользователя, ключом реестра HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System hello, добавьте новый параметр DWORD: **LocalAccountTokenFilterPolicy**. Задайте значение hello слишком**1**. toodo это в командной строке, запустите hello следующую команду:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. В брандмауэре Windows на компьютере hello требуется tooprotect, выберите **разрешить запуск программы или компонента через брандмауэр**. Активируйте **общий доступ к файлам и принтерам** и **инструментарий управления Windows (WMI)**. Для компьютеров, принадлежащих домену tooa можно настроить параметры брандмауэра hello с помощью объекта групповой политики (GPO).

   ![Параметры брандмауэра](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Добавьте учетную запись hello, созданную в CSPSConfigtool.
    1.  Войдите в сервер tooyour конфигурации.
    2.  Запустите файл **cspsconfigtool.exe**. (Она доступна как ярлык на рабочем столе hello и в папке %ProgramData%\home\svsystems\bin hello.)
    3.  На hello **управление учетными записями** выберите **Добавление учетной записи**.
    4.  Добавьте созданную учетную запись hello.
    5.  Введите учетные данные hello, используемой при включении репликации для компьютера.
