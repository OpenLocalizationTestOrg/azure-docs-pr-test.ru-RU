
1. <span data-ttu-id="827a4-101">В hello **гибридных подключений** колонке hello гибридного подключения только что созданные выберите **установки прослушивателя**.</span><span class="sxs-lookup"><span data-stu-id="827a4-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Щелкните «Установка прослушивателя»](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="827a4-103">Hello **свойства гибридного подключения** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="827a4-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="827a4-104">В разделе **на локальный диспетчер гибридного подключения**, выберите **загрузить и настроить вручную**, сохранение пакета HybridConnectionManager.msi загружаются hello и скопируйте строку подключения для шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="827a4-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Щелкните здесь tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="827a4-106">Hello, следующая команда toostart hello установщик командной строкой администратора, введите:</span><span class="sxs-lookup"><span data-stu-id="827a4-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="827a4-107">После hello запускается программа установки, нажмите кнопку **не сейчас**, найдите папку %ProgramFiles%\Microsoft\HybridConnectionManager toohello, запустите HCMConfigWizard.exe и нажмите кнопку **Да** в hello **пользователя Управление учетными записями** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="827a4-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="827a4-108">Вставьте строку подключения гибридного hello, скопированное ранее и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="827a4-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Установка](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="827a4-110">После завершения установки hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="827a4-110">When hello install completes, click **Close**.</span></span>
   
    ![Щелкните кнопку «Закрыть»](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="827a4-112">На hello **гибридных подключений** колонки, hello **состояние** столбец теперь показывает **подключен**.</span><span class="sxs-lookup"><span data-stu-id="827a4-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Состояние «Подключено»](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

