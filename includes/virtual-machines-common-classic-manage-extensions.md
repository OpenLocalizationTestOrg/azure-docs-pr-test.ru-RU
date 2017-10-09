


## <a name="using-vm-extensions"></a><span data-ttu-id="1efdb-101">Использование расширений виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1efdb-101">Using VM Extensions</span></span>
<span data-ttu-id="1efdb-102">Расширений ВМ Azure реализуют поведение и функции, которые либо помогают другие программы, которые работают на виртуальных машинах Azure (например, hello **WebDeployForVSDevTest** расширение позволяет развернуть решения Visual Studio tooWeb на ВМ Azure) или укажите Здравствуйте, возможность toointeract с toosupport ВМ hello другие правила поведения (например, можно использовать расширения Access ВМ hello из hello Azure CLI, tooreset клиентов REST и PowerShell или изменения значений удаленного доступа на ВМ Azure).</span><span class="sxs-lookup"><span data-stu-id="1efdb-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1efdb-103">Полный список расширений по поддерживаемым ими функциям hello см. в разделе [расширений ВМ Azure и компоненты](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1efdb-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1efdb-104">Поскольку каждое расширение ВМ поддерживает конкретную функцию, именно то, что можно и нельзя выполнить с помощью расширения зависит от расширения hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="1efdb-105">Таким образом перед изменением ВМ, убедитесь, что вы прочитали hello документацию для расширения виртуальной Машины требуется toouse hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="1efdb-106">Одни расширения ВМ нельзя удалить, а другие имеют такие свойства, изменение которых радикальным образом меняет реакцию ВМ на события.</span><span class="sxs-lookup"><span data-stu-id="1efdb-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="1efdb-107">Ниже перечислены наиболее распространенные задачи Hello:</span><span class="sxs-lookup"><span data-stu-id="1efdb-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="1efdb-108">Поиск доступных расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="1efdb-109">Обновление загруженных расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="1efdb-110">Добавление расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-110">Adding Extensions</span></span>
4. <span data-ttu-id="1efdb-111">Удаление расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="1efdb-112">Поиск доступных расширений</span><span class="sxs-lookup"><span data-stu-id="1efdb-112">Find Available Extensions</span></span>
<span data-ttu-id="1efdb-113">Вы можете найти расширения и дополнительную информацию, используя:</span><span class="sxs-lookup"><span data-stu-id="1efdb-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="1efdb-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1efdb-114">PowerShell</span></span>
* <span data-ttu-id="1efdb-115">Использование кросс-платформенного интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="1efdb-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="1efdb-116">Интерфейс API REST управления службой</span><span class="sxs-lookup"><span data-stu-id="1efdb-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1efdb-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1efdb-117">Azure PowerShell</span></span>
<span data-ttu-id="1efdb-118">Некоторые модули имеют командлетов PowerShell, которые являются определенной toothem, что упрощает их конфигурации из PowerShell; но hello следующие командлеты действуют для всех расширений ВМ.</span><span class="sxs-lookup"><span data-stu-id="1efdb-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="1efdb-119">Можно использовать следующие командлеты tooobtain сведения о доступных расширениях hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="1efdb-120">Для экземпляров веб-ролей или рабочих ролей, можно использовать hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="1efdb-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="1efdb-121">Для экземпляров виртуальных машин можно использовать hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="1efdb-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="1efdb-122">Здравствуйте, например, следующая примере кода показано, как toolist сведения для hello **IaaSDiagnostics** расширение с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1efdb-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="1efdb-123">Интерфейс командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="1efdb-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="1efdb-124">Некоторые модули имеют Azure CLI-команд, определенных toothem (hello расширение ВМ Docker является одним из примеров), который может упростить их конфигурации; но hello следующие команды работают для всех расширений ВМ.</span><span class="sxs-lookup"><span data-stu-id="1efdb-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="1efdb-125">Можно использовать hello **список расширений ВМ azure** tooobtain сведения о доступных расширениях команды и использовать hello **–-json** параметр toodisplay все доступные сведения о одно или несколько расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="1efdb-126">Если вы не используете расширение, hello команда возвращает JSON-описание всех доступных расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="1efdb-127">Привет, в следующем примере кода показано, как toolist hello сведения для hello **IaaSDiagnostics** расширение с помощью Azure CLI "hello" **список расширений ВМ azure** команда и использует hello **–-json** параметр tooreturn полные сведения.</span><span class="sxs-lookup"><span data-stu-id="1efdb-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="1efdb-128">REST API управления службой</span><span class="sxs-lookup"><span data-stu-id="1efdb-128">Service Management REST APIs</span></span>
<span data-ttu-id="1efdb-129">Можно использовать следующие API-интерфейс REST tooobtain сведения о доступных расширениях hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="1efdb-130">Для экземпляров веб-ролей или рабочих ролей, можно использовать hello [перечисления доступных расширений](https://msdn.microsoft.com/library/dn169559.aspx) операции.</span><span class="sxs-lookup"><span data-stu-id="1efdb-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="1efdb-131">версии hello toolist доступных расширений, можно использовать [перечисление версий расширения](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="1efdb-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="1efdb-132">Для экземпляров виртуальных машин можно использовать hello [перечисления расширений ресурсов](https://msdn.microsoft.com/library/dn495441.aspx) операции.</span><span class="sxs-lookup"><span data-stu-id="1efdb-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="1efdb-133">версии hello toolist доступных расширений, можно использовать [перечисление версий расширения ресурса](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="1efdb-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="1efdb-134">Добавление, обновление или отключение расширений</span><span class="sxs-lookup"><span data-stu-id="1efdb-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="1efdb-135">Расширения можно добавить при создании экземпляра или могут быть добавлены tooa, на котором запущен экземпляр.</span><span class="sxs-lookup"><span data-stu-id="1efdb-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="1efdb-136">Расширения можно обновить, отключить или удалить.</span><span class="sxs-lookup"><span data-stu-id="1efdb-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="1efdb-137">Эти действия можно выполнять с помощью командлетов Azure PowerShell или с помощью операций API REST управления службами hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="1efdb-138">Tooinstall необходимые параметры и настройки некоторых расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="1efdb-139">Для расширений поддерживаются общедоступные и частные параметры.</span><span class="sxs-lookup"><span data-stu-id="1efdb-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1efdb-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1efdb-140">Azure PowerShell</span></span>
<span data-ttu-id="1efdb-141">С помощью командлетов Azure PowerShell — hello простым способом tooadd и обновления расширений.</span><span class="sxs-lookup"><span data-stu-id="1efdb-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="1efdb-142">При использовании командлетов расширения hello, большая часть конфигурации hello hello расширения выполняется за вас.</span><span class="sxs-lookup"><span data-stu-id="1efdb-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="1efdb-143">В некоторых случаях может потребоваться tooprogrammatically добавить расширение.</span><span class="sxs-lookup"><span data-stu-id="1efdb-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="1efdb-144">При необходимости toodo это, необходимо предоставить hello конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="1efdb-145">Можно использовать следующие командлеты tooknow, требуется ли для расширения Настройка общедоступных и частных параметров hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="1efdb-146">Для экземпляров веб-ролей или рабочих ролей, можно использовать hello **Get-AzureServiceAvailableExtension** командлета.</span><span class="sxs-lookup"><span data-stu-id="1efdb-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="1efdb-147">Для экземпляров виртуальных машин можно использовать hello **Get-AzureVMAvailableExtension** командлета.</span><span class="sxs-lookup"><span data-stu-id="1efdb-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="1efdb-148">REST API управления службой</span><span class="sxs-lookup"><span data-stu-id="1efdb-148">Service Management REST APIs</span></span>
<span data-ttu-id="1efdb-149">При получении списка доступных расширений с помощью API-интерфейсов REST hello, вы получите информацию о том, как настроить toobe hello расширения.</span><span class="sxs-lookup"><span data-stu-id="1efdb-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="1efdb-150">Возвращаемая информация Hello может показывать сведения о параметрах, представленных общедоступной схемы и частной схемы.</span><span class="sxs-lookup"><span data-stu-id="1efdb-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="1efdb-151">Значения общедоступных параметров возвращаются в запросах об экземплярах hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="1efdb-152">Значения частных параметров не возвращаются.</span><span class="sxs-lookup"><span data-stu-id="1efdb-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="1efdb-153">Можно использовать следующие API-интерфейс REST tooknow, требуется ли для расширения Настройка общедоступных и частных параметров hello.</span><span class="sxs-lookup"><span data-stu-id="1efdb-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="1efdb-154">Для экземпляров веб-ролей или рабочих ролей hello **PublicConfigurationSchema** и **PrivateConfigurationSchema** элементы содержат данные hello в ответ hello из hello [списка Доступные расширения](https://msdn.microsoft.com/library/dn169559.aspx) операции.</span><span class="sxs-lookup"><span data-stu-id="1efdb-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="1efdb-155">Для экземпляров виртуальных машин hello **PublicConfigurationSchema** и **PrivateConfigurationSchema** элементы содержат данные hello в ответ hello из hello [списка Расширения ресурсов](https://msdn.microsoft.com/library/dn495441.aspx) операции.</span><span class="sxs-lookup"><span data-stu-id="1efdb-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="1efdb-156">Кроме того, расширения могут использовать конфигурации, заданные с помощью JSON.</span><span class="sxs-lookup"><span data-stu-id="1efdb-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="1efdb-157">Если такие типы расширений используются, только hello **SampleConfig** используется элемент.</span><span class="sxs-lookup"><span data-stu-id="1efdb-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

