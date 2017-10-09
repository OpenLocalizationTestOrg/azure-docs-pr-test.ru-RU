
1. В hello **гибридных подключений** колонке hello гибридного подключения только что созданные выберите **установки прослушивателя**.
   
    ![Щелкните «Установка прослушивателя»](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Hello **свойства гибридного подключения** открывает колонку. В разделе **на локальный диспетчер гибридного подключения**, выберите **загрузить и настроить вручную**, сохранение пакета HybridConnectionManager.msi загружаются hello и скопируйте строку подключения для шлюза hello.
   
    ![Щелкните здесь tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. Hello, следующая команда toostart hello установщик командной строкой администратора, введите:
   
        start HybridConnectionManager.msi
4. После hello запускается программа установки, нажмите кнопку **не сейчас**, найдите папку %ProgramFiles%\Microsoft\HybridConnectionManager toohello, запустите HCMConfigWizard.exe и нажмите кнопку **Да** в hello **пользователя Управление учетными записями** диалогового окна.
5. Вставьте строку подключения гибридного hello, скопированное ранее и нажмите кнопку **ОК**. 
   
    ![Установка](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. После завершения установки hello, нажмите кнопку **закрыть**.
   
    ![Щелкните кнопку «Закрыть»](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    На hello **гибридных подключений** колонки, hello **состояние** столбец теперь показывает **подключен**. 
   
    ![Состояние «Подключено»](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

