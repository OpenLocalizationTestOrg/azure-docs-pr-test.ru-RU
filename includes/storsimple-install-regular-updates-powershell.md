<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="c8a1e-101">регулярные обновления tooinstall через Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="c8a1e-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="c8a1e-102">Откройте последовательной консоли устройства hello и выберите параметр 1 **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="c8a1e-103">Введите пароль hello.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-103">Type hello password.</span></span> <span data-ttu-id="c8a1e-104">пароль по умолчанию Hello — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="c8a1e-105">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c8a1e-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="c8a1e-106">При наличии обновлений и обновлений hello, нарушающие работу или нет ли вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="c8a1e-107">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c8a1e-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="c8a1e-108">начнется процесс обновления Hello.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="c8a1e-109">Данная команда применяется только tooregular обновления.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="c8a1e-110">Эта команда выполняется только на одном контроллере, но обновляться будут оба контроллера.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="c8a1e-111">Вы можете заметить отработки отказа для контроллера во время процесса обновления hello; Однако hello перехода на другой ресурс не повлияет на доступность или работу системы.</span><span class="sxs-lookup"><span data-stu-id="c8a1e-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

