


<span data-ttu-id="cbb06-101">В этом разделе описываются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cbb06-101">This topic describes how to:</span></span>

* <span data-ttu-id="cbb06-102">включение данных в виртуальную машину Azure при ее подготовке;</span><span class="sxs-lookup"><span data-stu-id="cbb06-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="cbb06-103">извлечение их для Windows и Linux;</span><span class="sxs-lookup"><span data-stu-id="cbb06-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="cbb06-104">использование специальных средств, доступных в некоторых системах, для автоматического обнаружения и обработки пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="cbb06-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="cbb06-105">В этой статье рассказывается, как вставить пользовательские данные с помощью виртуальной машины, созданной с помощью API управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb06-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="cbb06-106">Чтобы узнать, как использовать API управления ресурсами Azure, см. [этот пример шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="cbb06-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="cbb06-107">Включение пользовательских данных в виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="cbb06-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="cbb06-108">В настоящее время эта функция поддерживается только в [интерфейсе командной строки Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="cbb06-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="cbb06-109">Создадим файл `custom-data.txt` , содержащий наши данные, и вставим ее в виртуальную машину в процессе подготовки.</span><span class="sxs-lookup"><span data-stu-id="cbb06-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="cbb06-110">Хотя для команды `azure vm create` можно использовать любой из вариантов, следующий подход демонстрирует самый простой способ.</span><span class="sxs-lookup"><span data-stu-id="cbb06-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="cbb06-111">Использование пользовательских данных в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="cbb06-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="cbb06-112">Если на виртуальной машине Azure используется платформа Windows, то пользовательские данные сохраняются в файл `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="cbb06-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="cbb06-113">Хотя для передачи с локального компьютера на новую виртуальную машину эти данные были зашифрованы с помощью кодировки base64, они автоматически расшифровываются и могут немедленно открываться и использоваться.</span><span class="sxs-lookup"><span data-stu-id="cbb06-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cbb06-114">Если такой файл существует, он перезаписывается.</span><span class="sxs-lookup"><span data-stu-id="cbb06-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="cbb06-115">В каталоге устанавливается защита **System:Full Control** и **Administrators:Full Control**.</span><span class="sxs-lookup"><span data-stu-id="cbb06-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="cbb06-116">Если на виртуальной машине Azure используется платформа Linux, файл пользовательских данных размещается в одном из следующих двух мест (в зависимости от вашего дистрибутива):</span><span class="sxs-lookup"><span data-stu-id="cbb06-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="cbb06-117">Данные будут в кодировке Base64, поэтому их необходимо сначала расшифровать:</span><span class="sxs-lookup"><span data-stu-id="cbb06-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="cbb06-118">Cloud-Init в Azure</span><span class="sxs-lookup"><span data-stu-id="cbb06-118">Cloud-init on Azure</span></span>
<span data-ttu-id="cbb06-119">Если виртуальная машина Azure создана из образа Ubuntu или CoreOS, то с помощью CustomData вы можете отправить файл cloud-config в пакет cloud-init.</span><span class="sxs-lookup"><span data-stu-id="cbb06-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="cbb06-120">Если же файл пользовательских данных является сценарием, пакет cloud-init может просто выполнить его.</span><span class="sxs-lookup"><span data-stu-id="cbb06-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="cbb06-121">Образы облаков Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cbb06-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="cbb06-122">В большинстве образов Azure Linux вы изменяете /etc/waagent.conf, чтобы настроить временный диск ресурсов и файл подкачки.</span><span class="sxs-lookup"><span data-stu-id="cbb06-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="cbb06-123">Дополнительные сведения см. в [руководстве пользователя агента Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbb06-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="cbb06-124">В образах Ubuntu Cloud для настройки диска ресурсов (который также называется временным) и раздела подкачки необходимо использовать пакет cloud-init.</span><span class="sxs-lookup"><span data-stu-id="cbb06-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="cbb06-125">Дополнительные сведения см. [здесь](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="cbb06-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="cbb06-126">Дальнейшие действия: использование пакета cloud-init</span><span class="sxs-lookup"><span data-stu-id="cbb06-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="cbb06-127">Дополнительные сведения см. в [документации по cloud-init для Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="cbb06-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="cbb06-128">Справочник по REST API управления добавлением службы роли</span><span class="sxs-lookup"><span data-stu-id="cbb06-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="cbb06-129">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="cbb06-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

