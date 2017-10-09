<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7fa7d-101">регулярные исправления tooinstall через Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="7fa7d-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7fa7d-102">Подключение toohello последовательной консоли устройства.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-102">Connect toohello device serial console.</span></span> <span data-ttu-id="7fa7d-103">Дополнительные сведения см. в разделе [шаг 1: подключения последовательной консоли toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="7fa7d-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="7fa7d-104">В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="7fa7d-105">Введите пароль hello.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-105">Type hello password.</span></span> <span data-ttu-id="7fa7d-106">пароль по умолчанию Hello — **Password1**.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="7fa7d-107">Hello командной строки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7fa7d-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="7fa7d-108">Данная команда применяется только tooregular исправления.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="7fa7d-109">Эта команда выполняется только на одном контроллере, но обновляться будут оба контроллера.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="7fa7d-110">Вы можете заметить отработки отказа для контроллера во время процесса обновления hello; Однако hello перехода на другой ресурс не повлияет на доступность или работу системы.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="7fa7d-111">При появлении запроса укажите hello путь toohello общей сетевой папке, содержащей файлы исправлений hello.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="7fa7d-112">После этого введите подтверждение для применения этих исправлений.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="7fa7d-113">Тип **Y** tooproceed с установкой исправления hello.</span><span class="sxs-lookup"><span data-stu-id="7fa7d-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

