<span data-ttu-id="18d53-101">Теперь Azure поддерживает две функции отладки. Виртуальные машины Azure, созданные на основе модели развертывания с помощью Resource Manager, поддерживают выходные данные и снимки экрана консоли.</span><span class="sxs-lookup"><span data-stu-id="18d53-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="18d53-102">При повторном подключении tooAzure собственного образа или даже загрузки одного из образов платформы hello, может быть несколько причин, почему Возвращает виртуальную машину в состояние не является загрузочным.</span><span class="sxs-lookup"><span data-stu-id="18d53-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="18d53-103">Эти функции позволяют вам tooeasily Диагностика и восстановление сбоев загрузки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="18d53-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="18d53-104">Для виртуальных машин Linux можно легко просмотреть hello выходные данные журналов консоли из hello портала:</span><span class="sxs-lookup"><span data-stu-id="18d53-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Портал Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="18d53-106">Тем не менее для Windows и Linux виртуальных машин Azure также позволяет toosee снимок экрана приветствия виртуальных Машин из низкоуровневой оболочки hello:</span><span class="sxs-lookup"><span data-stu-id="18d53-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Ошибка](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="18d53-108">Обе эти функции доступны на виртуальных машинах Azure во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="18d53-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="18d53-109">Обратите внимание, снимки экрана и выходных данных может занять tooappear минут too10 вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="18d53-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="18d53-110">Распространенные ошибки загрузки</span><span class="sxs-lookup"><span data-stu-id="18d53-110">Common boot errors</span></span>

- [<span data-ttu-id="18d53-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="18d53-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="18d53-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="18d53-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="18d53-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="18d53-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="18d53-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="18d53-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="18d53-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="18d53-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="18d53-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="18d53-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="18d53-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="18d53-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="18d53-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="18d53-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="18d53-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="18d53-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="18d53-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="18d53-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="18d53-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="18d53-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="18d53-122">Операционная система не найдена</span><span class="sxs-lookup"><span data-stu-id="18d53-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="18d53-123">Сбой при загрузке или INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="18d53-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="18d53-124">Включение диагностики на новой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="18d53-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="18d53-125">При создании новой виртуальной машины из hello предварительной версии портала выберите hello **диспетчера ресурсов Azure** из раскрывающегося списка модели развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="18d53-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Диспетчер ресурсов](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="18d53-127">Настройте hello мониторинг параметр tooselect hello учетной записи хранилища куда tooplace эти файлы диагностики.</span><span class="sxs-lookup"><span data-stu-id="18d53-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Создание виртуальной машины](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="18d53-129">При развертывании на основе шаблона Azure Resource Manager перейдите tooyour ресурса виртуальной машины и добавить профиль раздел hello диагностики.</span><span class="sxs-lookup"><span data-stu-id="18d53-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="18d53-130">Не забывайте заголовок версии API «2015-06-15» hello toouse.</span><span class="sxs-lookup"><span data-stu-id="18d53-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="18d53-131">Hello диагностического профиля позволяет учетной записи хранилища hello tooselect место tooput эти журналы.</span><span class="sxs-lookup"><span data-stu-id="18d53-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="18d53-132">toodeploy образец виртуальной машины с включена, диагностика загрузки извлечение здесь нашей репозитория.</span><span class="sxs-lookup"><span data-stu-id="18d53-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="18d53-133">Обновление имеющейся виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="18d53-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="18d53-134">Диагностика загрузки tooenable через hello портала, можно также обновить существующую виртуальную машину через портал hello.</span><span class="sxs-lookup"><span data-stu-id="18d53-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="18d53-135">Выберите hello Диагностика загрузки и сохранить.</span><span class="sxs-lookup"><span data-stu-id="18d53-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="18d53-136">Перезапустите эффект tootake hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="18d53-136">Restart hello VM tootake effect.</span></span>

![Обновление имеющейся виртуальной машины](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

