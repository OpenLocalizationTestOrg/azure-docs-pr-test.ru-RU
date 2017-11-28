
1. <span data-ttu-id="4b638-101">В колонке **Гибридные подключения** щелкните только что созданное гибридное подключение, а затем нажмите **Настройка прослушивателя**.</span><span class="sxs-lookup"><span data-stu-id="4b638-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Щелкните «Установка прослушивателя»](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="4b638-103">Откроется выноска **Свойства гибридного подключения** .</span><span class="sxs-lookup"><span data-stu-id="4b638-103">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="4b638-104">В разделе **Локальный диспетчер гибридного подключения** выберите **Скачать и настроить вручную**, сохраните скачанный пакет HybridConnectionManager.msi и скопируйте строку подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="4b638-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span></span>
   
    ![Щелкните здесь, чтобы установить](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="4b638-106">Введите следующую команду в командной строке администратора, чтобы запустить установщик:</span><span class="sxs-lookup"><span data-stu-id="4b638-106">From an administrator command prompt, type the following command to start the installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="4b638-107">После запуска установщика щелкните **Не сейчас**, перейдите в папку %ProgramFiles%\Microsoft\HybridConnectionManager, запустите HCMConfigWizard.exe и нажмите кнопку **Да** в диалоговом окне **Контроль учетных записей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4b638-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span></span>
5. <span data-ttu-id="4b638-108">Вставьте заранее скопированную гибридную строку подключения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4b638-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Установка](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="4b638-110">После завершения установки щелкните кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="4b638-110">When the install completes, click **Close**.</span></span>
   
    ![Щелкните кнопку «Закрыть»](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="4b638-112">В колонке **Гибридные подключения** в столбце **Состояние** теперь отображается **Подключено**.</span><span class="sxs-lookup"><span data-stu-id="4b638-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Состояние «Подключено»](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

