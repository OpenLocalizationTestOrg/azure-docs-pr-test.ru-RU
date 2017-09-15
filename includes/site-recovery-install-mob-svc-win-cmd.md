1. <span data-ttu-id="dac57-101">Скопируйте установщик в локальную папку (например, C:\Temp) на сервере, который необходимо защитить.</span><span class="sxs-lookup"><span data-stu-id="dac57-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span></span> <span data-ttu-id="dac57-102">В командной строке выполните следующие команды от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="dac57-102">Run the following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="dac57-103">Чтобы установить службу Mobility Service, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="dac57-103">To install Mobility Service, run the following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="dac57-104">Теперь необходимо зарегистрировать агент на сервере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dac57-104">Now the agent needs to be registered with the Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="dac57-105">Команда установщика службы Mobility Service: аргументы строки</span><span class="sxs-lookup"><span data-stu-id="dac57-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="dac57-106">Параметр</span><span class="sxs-lookup"><span data-stu-id="dac57-106">Parameter</span></span>|<span data-ttu-id="dac57-107">Тип</span><span class="sxs-lookup"><span data-stu-id="dac57-107">Type</span></span>|<span data-ttu-id="dac57-108">Описание</span><span class="sxs-lookup"><span data-stu-id="dac57-108">Description</span></span>|<span data-ttu-id="dac57-109">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="dac57-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="dac57-110">/Role</span><span class="sxs-lookup"><span data-stu-id="dac57-110">/Role</span></span>|<span data-ttu-id="dac57-111">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dac57-111">Mandatory</span></span>|<span data-ttu-id="dac57-112">Указывает службу, которую нужно установить: Mobility Service (MS) или MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="dac57-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="dac57-113">MS</span><span class="sxs-lookup"><span data-stu-id="dac57-113">MS</span></span> </br> <span data-ttu-id="dac57-114">MT</span><span class="sxs-lookup"><span data-stu-id="dac57-114">MT</span></span>|
|<span data-ttu-id="dac57-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="dac57-115">/InstallLocation</span></span>|<span data-ttu-id="dac57-116">Необязательно</span><span class="sxs-lookup"><span data-stu-id="dac57-116">Optional</span></span>|<span data-ttu-id="dac57-117">Расположение, в котором установлена служба Mobility Service</span><span class="sxs-lookup"><span data-stu-id="dac57-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="dac57-118">Любая папка на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dac57-118">Any folder on the computer</span></span>|
|<span data-ttu-id="dac57-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="dac57-119">/Platform</span></span>|<span data-ttu-id="dac57-120">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dac57-120">Mandatory</span></span>|<span data-ttu-id="dac57-121">Указывает платформу, на которой будет установлена служба Mobility Service</span><span class="sxs-lookup"><span data-stu-id="dac57-121">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="dac57-122">- **VMware.** Используйте это значение при установке службы Mobility Service на виртуальной машине под управлением *узлов VMware vSphere ESXi*, *узлов Hyper-V* или *физических серверов*</span><span class="sxs-lookup"><span data-stu-id="dac57-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="dac57-123">- **Azure.** Используйте это значение при установке агента на виртуальной машине Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="dac57-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="dac57-124">VMware</span><span class="sxs-lookup"><span data-stu-id="dac57-124">VMware</span></span> </br> <span data-ttu-id="dac57-125">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="dac57-125">Azure</span></span>|
|<span data-ttu-id="dac57-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="dac57-126">/Silent</span></span>|<span data-ttu-id="dac57-127">Необязательно</span><span class="sxs-lookup"><span data-stu-id="dac57-127">Optional</span></span>|<span data-ttu-id="dac57-128">Используется для запуска установщика в автоматическом режиме</span><span class="sxs-lookup"><span data-stu-id="dac57-128">Specifies to run the installer in silent mode</span></span>| <span data-ttu-id="dac57-129">Нет данных</span><span class="sxs-lookup"><span data-stu-id="dac57-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="dac57-130">Журналы установки находятся в папке %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="dac57-130">The setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="dac57-131">Аргументы командной строки регистрации службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="dac57-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="dac57-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="dac57-132">Parameter</span></span>|<span data-ttu-id="dac57-133">Тип</span><span class="sxs-lookup"><span data-stu-id="dac57-133">Type</span></span>|<span data-ttu-id="dac57-134">Описание</span><span class="sxs-lookup"><span data-stu-id="dac57-134">Description</span></span>|<span data-ttu-id="dac57-135">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="dac57-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="dac57-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="dac57-136">/CSEndPoint</span></span> |<span data-ttu-id="dac57-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dac57-137">Mandatory</span></span>|<span data-ttu-id="dac57-138">IP-адрес сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="dac57-138">IP address of the configuration server</span></span>| <span data-ttu-id="dac57-139">Любой допустимый IP-адрес</span><span class="sxs-lookup"><span data-stu-id="dac57-139">Any valid IP address</span></span>|
  |<span data-ttu-id="dac57-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="dac57-140">/PassphraseFilePath</span></span>|<span data-ttu-id="dac57-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dac57-141">Mandatory</span></span>|<span data-ttu-id="dac57-142">Расположение файла с парольной фразой</span><span class="sxs-lookup"><span data-stu-id="dac57-142">Location of the passphrase</span></span> |<span data-ttu-id="dac57-143">Любой допустимый локальный путь к файлу или UNC</span><span class="sxs-lookup"><span data-stu-id="dac57-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="dac57-144">Журналы AgentConfiguration находятся в папке %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="dac57-144">The AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
