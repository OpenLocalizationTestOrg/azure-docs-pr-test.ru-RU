


<span data-ttu-id="28203-101">В этом разделе описываются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="28203-101">This topic describes how to:</span></span>

* <span data-ttu-id="28203-102">включение данных в виртуальную машину Azure при ее подготовке;</span><span class="sxs-lookup"><span data-stu-id="28203-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="28203-103">извлечение их для Windows и Linux;</span><span class="sxs-lookup"><span data-stu-id="28203-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="28203-104">Использование специальных средств, доступных в некоторых системах toodetect и автоматически обрабатывать пользовательские данные.</span><span class="sxs-lookup"><span data-stu-id="28203-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="28203-105">В этой статье описывается, как пользовательские данные могут быть добавлены с помощью виртуальных Машин, созданных с помощью hello API управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="28203-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="28203-106">toouse hello Azure ресурсов API-интерфейса управления. в статье toosee [hello пример шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="28203-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="28203-107">Включение пользовательских данных в виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="28203-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="28203-108">Эта функция в настоящее время поддерживается только в hello [интерфейса командной строки Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="28203-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="28203-109">Здесь мы создадим `custom-data.txt` файл, который содержит ваши данные, затем вставить, в toohello виртуальной Машины во время инициализации.</span><span class="sxs-lookup"><span data-stu-id="28203-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="28203-110">Однако вы можете использовать любой из параметров hello для hello `azure vm create` команды hello следующий код демонстрирует один подход очень простой:</span><span class="sxs-lookup"><span data-stu-id="28203-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="28203-111">Использование пользовательских данных в виртуальной машине hello</span><span class="sxs-lookup"><span data-stu-id="28203-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="28203-112">Если ВМ Azure виртуальной Машины на основе Windows, то файл hello пользовательских данных сохраняется слишком`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="28203-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="28203-113">Несмотря на то, что она была tootransfer кодировке base64 из локального компьютера toohello hello новой виртуальной Машины, она будет автоматически декодировать и можно открыть или использовать немедленно.</span><span class="sxs-lookup"><span data-stu-id="28203-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="28203-114">Если hello файл существует, он будет переопределен.</span><span class="sxs-lookup"><span data-stu-id="28203-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="28203-115">безопасность Hello в каталоге hello задано слишком**System: Full Control** и **Administrators: Full Control**.</span><span class="sxs-lookup"><span data-stu-id="28203-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="28203-116">Если ВМ Azure представляет собой виртуальную Машину под управлением Linux, то hello пользовательских данных файл будет находиться в одно из следующих hello помещает в зависимости от вашей дистрибутив.</span><span class="sxs-lookup"><span data-stu-id="28203-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="28203-117">Hello данные могут быть кодировке base64, поэтому может потребоваться сначала toodecode hello данных:</span><span class="sxs-lookup"><span data-stu-id="28203-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="28203-118">Cloud-Init в Azure</span><span class="sxs-lookup"><span data-stu-id="28203-118">Cloud-init on Azure</span></span>
<span data-ttu-id="28203-119">Если из Ubuntu или CoreOS образа ВМ Azure, можно использовать toosend CustomData облачной конфигурации toocloud-init.</span><span class="sxs-lookup"><span data-stu-id="28203-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="28203-120">Если же файл пользовательских данных является сценарием, пакет cloud-init может просто выполнить его.</span><span class="sxs-lookup"><span data-stu-id="28203-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="28203-121">Образы облаков Ubuntu</span><span class="sxs-lookup"><span data-stu-id="28203-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="28203-122">В большинстве изображений Azure Linux изменение «/ etc/waagent.conf» tooconfigure hello временный диск и замены файла ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28203-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="28203-123">Дополнительные сведения см. в [руководстве пользователя агента Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28203-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="28203-124">Тем не менее, на изображениях облака Ubuntu hello, необходимо использовать облака init tooconfigure hello ресурсов диск (т. е hello «эфемерных») и переключения секций.</span><span class="sxs-lookup"><span data-stu-id="28203-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="28203-125">См. следующие страницы на вики-сайте Ubuntu hello подробнее hello: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="28203-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="28203-126">Дальнейшие действия: использование пакета cloud-init</span><span class="sxs-lookup"><span data-stu-id="28203-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="28203-127">Дополнительные сведения см. в разделе hello [документации init облака для Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="28203-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="28203-128">Справочник по REST API управления добавлением службы роли</span><span class="sxs-lookup"><span data-stu-id="28203-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="28203-129">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="28203-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

