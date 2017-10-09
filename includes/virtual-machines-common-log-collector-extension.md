
<span data-ttu-id="8aac9-101">Диагностики проблем с облачной службы Microsoft Azure требуется сбор hello службы файлов журнала на виртуальных машинах при возникновении проблем hello.</span><span class="sxs-lookup"><span data-stu-id="8aac9-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="8aac9-102">Можно использовать hello AzureLogCollector расширение по требованию tooperfom однократного сбора журналов из одного или нескольких виртуальных машин облачной службы (из веб-ролей и рабочих ролей) и передачи hello собранные файлы tooan учетной записи хранилища Azure — все это без удаленного входа в систему tooany hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8aac9-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="8aac9-103">Описания большинства hello в журнал сведения можно найти в http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="8aac9-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="8aac9-104">Существует два режима коллекции, зависят от типов hello собранные toobe файлов.</span><span class="sxs-lookup"><span data-stu-id="8aac9-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="8aac9-105">Только журналы гостевого агента Azure (GA).</span><span class="sxs-lookup"><span data-stu-id="8aac9-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="8aac9-106">Этот режим коллекции включает все гостевые агенты связанные tooAzure hello журналов и других компонентах Azure.</span><span class="sxs-lookup"><span data-stu-id="8aac9-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="8aac9-107">Все журналы (Full).</span><span class="sxs-lookup"><span data-stu-id="8aac9-107">All Logs (Full).</span></span> <span data-ttu-id="8aac9-108">В этом режиме собираются все файлы, которые собираются в режиме GA, а также:</span><span class="sxs-lookup"><span data-stu-id="8aac9-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="8aac9-109">журналы событий системы и приложений;</span><span class="sxs-lookup"><span data-stu-id="8aac9-109">system and application event logs</span></span>
  * <span data-ttu-id="8aac9-110">журналы ошибок HTTP;</span><span class="sxs-lookup"><span data-stu-id="8aac9-110">HTTP error logs</span></span>
  * <span data-ttu-id="8aac9-111">Журналы IIS</span><span class="sxs-lookup"><span data-stu-id="8aac9-111">IIS Logs</span></span>
  * <span data-ttu-id="8aac9-112">журналы установки;</span><span class="sxs-lookup"><span data-stu-id="8aac9-112">Setup logs</span></span>
  * <span data-ttu-id="8aac9-113">другие системные журналы.</span><span class="sxs-lookup"><span data-stu-id="8aac9-113">other system logs</span></span>

<span data-ttu-id="8aac9-114">В обоих режимах сбора можно указать папки для сбора дополнительных данных с помощью коллекции hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="8aac9-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="8aac9-115">**Имя**: hello имя hello коллекцию, которая будет использоваться в качестве имени вложенной папки в toobe файла zip hello hello собраны.</span><span class="sxs-lookup"><span data-stu-id="8aac9-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="8aac9-116">**Расположение**: hello toohello папку на виртуальной машине hello где будут собираться файла.</span><span class="sxs-lookup"><span data-stu-id="8aac9-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="8aac9-117">**SearchPattern**: hello шаблон имен файлов toobe hello собраны.</span><span class="sxs-lookup"><span data-stu-id="8aac9-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="8aac9-118">Значение по умолчанию — *.</span><span class="sxs-lookup"><span data-stu-id="8aac9-118">Default is “*”</span></span>
* <span data-ttu-id="8aac9-119">**Рекурсивные**: Если hello файлы будут собраны рекурсивно папке hello.</span><span class="sxs-lookup"><span data-stu-id="8aac9-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8aac9-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8aac9-120">Prerequisites</span></span>
* <span data-ttu-id="8aac9-121">Для расширения toosave создан ZIP-файлы должны toohave учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="8aac9-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="8aac9-122">Командлеты Azure PowerShell 0.8.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8aac9-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="8aac9-123">Дополнительные сведения см. на странице [загрузок Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8aac9-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="8aac9-124">Добавьте расширение hello</span><span class="sxs-lookup"><span data-stu-id="8aac9-124">Add hello extension</span></span>
<span data-ttu-id="8aac9-125">Можно использовать [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) командлеты или [API REST управления службой](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello расширение AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="8aac9-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="8aac9-126">Для облачных служб hello существующий командлет Azure Powershell **Set-AzureServiceExtension**, может быть расширением hello используется tooenable на экземпляры роли облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8aac9-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="8aac9-127">При каждом включении этого расширения через этот командлет на hello выбранных экземплярах ролей выбранных ролей запускается сбор журналов.</span><span class="sxs-lookup"><span data-stu-id="8aac9-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="8aac9-128">Для виртуальных машин hello существующий командлет Azure Powershell **Set-AzureVMExtension**, могут быть только расширения hello используется tooenable на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="8aac9-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="8aac9-129">При каждом включении этого расширения hello командлетов запускается сбор журналов на каждом экземпляре.</span><span class="sxs-lookup"><span data-stu-id="8aac9-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="8aac9-130">На внутреннем уровне это расширение использует hello PublicConfiguration на основе JSON и PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="8aac9-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="8aac9-131">Hello Приведем hello структура примера JSON для общедоступной и частной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8aac9-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="8aac9-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="8aac9-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="8aac9-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8aac9-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="8aac9-134">Это расширение не требует наличия **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="8aac9-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="8aac9-135">Вы можете просто предоставить пустую структуру для hello **– PrivateConfiguration** аргумент.</span><span class="sxs-lookup"><span data-stu-id="8aac9-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="8aac9-136">Вы можете воспользоваться одним из двух hello следующие шаги tooadd hello AzureLogCollector tooone или более экземпляров облачной службы или виртуальной машины выбранных ролей, какие триггеры hello коллекций на каждой виртуальной Машины toorun и отправлять hello собранные файлы tooAzure учетной записи указано.</span><span class="sxs-lookup"><span data-stu-id="8aac9-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="8aac9-137">Добавление в качестве расширения службы</span><span class="sxs-lookup"><span data-stu-id="8aac9-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="8aac9-138">Выполните hello инструкции tooconnect Azure PowerShell tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="8aac9-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="8aac9-139">Укажите имя службы hello, слот, роли и toowhich экземпляры роли требуется tooadd и включить расширение AzureLogCollector hello.</span><span class="sxs-lookup"><span data-stu-id="8aac9-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="8aac9-140">Укажите папку hello дополнительных данных, для которого будут собираться файлы (этот шаг является необязательным).</span><span class="sxs-lookup"><span data-stu-id="8aac9-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="8aac9-141">Можно использовать токен `%roleroot%` toospecify hello корневой диск роли, так как она не использует фиксированный диск.</span><span class="sxs-lookup"><span data-stu-id="8aac9-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="8aac9-142">Укажите имя учетной записи хранилища Azure hello и ключа toowhich собранные файлы будут отправлены.</span><span class="sxs-lookup"><span data-stu-id="8aac9-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="8aac9-143">При вызове hello SetAzureServiceLogCollector.ps1 (входит в конце hello hello статьи) как расширение AzureLogCollector hello tooenable следующим облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8aac9-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="8aac9-144">После завершения выполнения hello можно найти hello отправить файл в папке`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="8aac9-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="8aac9-145">Hello приведем определение hello hello параметров, переданных toohello сценария.</span><span class="sxs-lookup"><span data-stu-id="8aac9-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="8aac9-146">(Эта часть кода дублируется ниже.)</span><span class="sxs-lookup"><span data-stu-id="8aac9-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="8aac9-147">*ServiceName*: имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8aac9-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="8aac9-148">*Roles*: список ролей, например WebRole1 или WorkerRole1.</span><span class="sxs-lookup"><span data-stu-id="8aac9-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="8aac9-149">*Экземпляры*: список приветствия имен экземпляров ролей, разделенных запятой--используйте строку с подстановочным знаком hello («*») для всех экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="8aac9-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="8aac9-150">*Slot*: имя слота.</span><span class="sxs-lookup"><span data-stu-id="8aac9-150">*Slot*: Slot name.</span></span> <span data-ttu-id="8aac9-151">Возможные значения: Production или Staging.</span><span class="sxs-lookup"><span data-stu-id="8aac9-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="8aac9-152">*Mode*: режим сбора данных.</span><span class="sxs-lookup"><span data-stu-id="8aac9-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="8aac9-153">Возможные значения: Full или GA.</span><span class="sxs-lookup"><span data-stu-id="8aac9-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="8aac9-154">*StorageAccountName*: имя учетной записи Azure для хранения собранных данных.</span><span class="sxs-lookup"><span data-stu-id="8aac9-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="8aac9-155">*StorageAccountKey*: имя ключа учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8aac9-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="8aac9-156">*AdditionalDataLocationList*: список hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="8aac9-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="8aac9-157">Добавление в качестве расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8aac9-157">Adding as a VM Extension</span></span>
<span data-ttu-id="8aac9-158">Выполните hello инструкции tooconnect Azure PowerShell tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="8aac9-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="8aac9-159">Укажите имя службы hello, виртуальных Машин и режим сбора hello.</span><span class="sxs-lookup"><span data-stu-id="8aac9-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="8aac9-160">Укажите имя учетной записи хранилища Azure hello и ключа toowhich собранные файлы будут отправлены.</span><span class="sxs-lookup"><span data-stu-id="8aac9-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="8aac9-161">При вызове hello SetAzureVMLogCollector.ps1 (входит в конце hello hello статьи) как расширение AzureLogCollector hello tooenable следующим облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8aac9-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="8aac9-162">После завершения выполнения hello можно найти hello отправить файл в папке https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="8aac9-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="8aac9-163">Hello приведем определение hello hello параметров, переданных toohello сценария.</span><span class="sxs-lookup"><span data-stu-id="8aac9-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="8aac9-164">(Эта часть кода дублируется ниже.)</span><span class="sxs-lookup"><span data-stu-id="8aac9-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="8aac9-165">ServiceName: имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8aac9-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="8aac9-166">Имя hello VMName hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8aac9-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="8aac9-167">Mode: режим сбора данных.</span><span class="sxs-lookup"><span data-stu-id="8aac9-167">Mode: Collection mode.</span></span> <span data-ttu-id="8aac9-168">Возможные значения: Full или GA.</span><span class="sxs-lookup"><span data-stu-id="8aac9-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="8aac9-169">StorageAccountName: имя учетной записи Azure для хранения собранных данных.</span><span class="sxs-lookup"><span data-stu-id="8aac9-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="8aac9-170">StorageAccountKey: имя ключа учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="8aac9-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="8aac9-171">AdditionalDataLocationList: Список hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="8aac9-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="8aac9-172">Файлы сценариев PowerShell для расширения</span><span class="sxs-lookup"><span data-stu-id="8aac9-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="8aac9-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="8aac9-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="8aac9-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="8aac9-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="8aac9-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8aac9-175">Next Steps</span></span>
<span data-ttu-id="8aac9-176">Теперь вы можете анализировать или копировать журналы, собранные в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="8aac9-176">Now you can examine or copy your logs from one very simple location.</span></span>

