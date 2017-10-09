1. <span data-ttu-id="2f5e4-101">Скопируйте hello установщика tooa локальную папку (например, C:\Temp) на сервере hello, которое следует tooprotect.</span><span class="sxs-lookup"><span data-stu-id="2f5e4-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="2f5e4-102">Выполните следующие команды от имени администратора, в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="2f5e4-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="2f5e4-103">tooinstall службы Mobility Service, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2f5e4-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="2f5e4-104">Теперь агент hello должен toobe зарегистрирована hello сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2f5e4-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="2f5e4-105">Команда установщика службы Mobility Service: аргументы строки</span><span class="sxs-lookup"><span data-stu-id="2f5e4-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="2f5e4-106">Параметр</span><span class="sxs-lookup"><span data-stu-id="2f5e4-106">Parameter</span></span>|<span data-ttu-id="2f5e4-107">Тип</span><span class="sxs-lookup"><span data-stu-id="2f5e4-107">Type</span></span>|<span data-ttu-id="2f5e4-108">Описание</span><span class="sxs-lookup"><span data-stu-id="2f5e4-108">Description</span></span>|<span data-ttu-id="2f5e4-109">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="2f5e4-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="2f5e4-110">/Role</span><span class="sxs-lookup"><span data-stu-id="2f5e4-110">/Role</span></span>|<span data-ttu-id="2f5e4-111">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2f5e4-111">Mandatory</span></span>|<span data-ttu-id="2f5e4-112">Указывает службу, которую нужно установить: Mobility Service (MS) или MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="2f5e4-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="2f5e4-113">MS</span><span class="sxs-lookup"><span data-stu-id="2f5e4-113">MS</span></span> </br> <span data-ttu-id="2f5e4-114">MT</span><span class="sxs-lookup"><span data-stu-id="2f5e4-114">MT</span></span>|
|<span data-ttu-id="2f5e4-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="2f5e4-115">/InstallLocation</span></span>|<span data-ttu-id="2f5e4-116">Необязательно</span><span class="sxs-lookup"><span data-stu-id="2f5e4-116">Optional</span></span>|<span data-ttu-id="2f5e4-117">Расположение, в котором установлена служба Mobility Service</span><span class="sxs-lookup"><span data-stu-id="2f5e4-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="2f5e4-118">Любой папке на компьютере hello</span><span class="sxs-lookup"><span data-stu-id="2f5e4-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="2f5e4-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="2f5e4-119">/Platform</span></span>|<span data-ttu-id="2f5e4-120">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2f5e4-120">Mandatory</span></span>|<span data-ttu-id="2f5e4-121">Указывает платформу hello, на какие hello начало установлена служба Mobility</span><span class="sxs-lookup"><span data-stu-id="2f5e4-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="2f5e4-122">- **VMware.** Используйте это значение при установке службы Mobility Service на виртуальной машине под управлением *узлов VMware vSphere ESXi*, *узлов Hyper-V* или *физических серверов*</span><span class="sxs-lookup"><span data-stu-id="2f5e4-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="2f5e4-123">- **Azure.** Используйте это значение при установке агента на виртуальной машине Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="2f5e4-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="2f5e4-124">VMware</span><span class="sxs-lookup"><span data-stu-id="2f5e4-124">VMware</span></span> </br> <span data-ttu-id="2f5e4-125">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="2f5e4-125">Azure</span></span>|
|<span data-ttu-id="2f5e4-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="2f5e4-126">/Silent</span></span>|<span data-ttu-id="2f5e4-127">Необязательно</span><span class="sxs-lookup"><span data-stu-id="2f5e4-127">Optional</span></span>|<span data-ttu-id="2f5e4-128">Задает установщик toorun hello в автоматическом режиме</span><span class="sxs-lookup"><span data-stu-id="2f5e4-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="2f5e4-129">Нет данных</span><span class="sxs-lookup"><span data-stu-id="2f5e4-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="2f5e4-130">журналы установки Hello можно найти в разделе %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="2f5e4-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="2f5e4-131">Аргументы командной строки регистрации службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="2f5e4-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="2f5e4-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="2f5e4-132">Parameter</span></span>|<span data-ttu-id="2f5e4-133">Тип</span><span class="sxs-lookup"><span data-stu-id="2f5e4-133">Type</span></span>|<span data-ttu-id="2f5e4-134">Описание</span><span class="sxs-lookup"><span data-stu-id="2f5e4-134">Description</span></span>|<span data-ttu-id="2f5e4-135">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="2f5e4-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="2f5e4-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="2f5e4-136">/CSEndPoint</span></span> |<span data-ttu-id="2f5e4-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2f5e4-137">Mandatory</span></span>|<span data-ttu-id="2f5e4-138">IP-адрес сервера конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="2f5e4-138">IP address of hello configuration server</span></span>| <span data-ttu-id="2f5e4-139">Любой допустимый IP-адрес</span><span class="sxs-lookup"><span data-stu-id="2f5e4-139">Any valid IP address</span></span>|
  |<span data-ttu-id="2f5e4-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="2f5e4-140">/PassphraseFilePath</span></span>|<span data-ttu-id="2f5e4-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2f5e4-141">Mandatory</span></span>|<span data-ttu-id="2f5e4-142">Расположение hello парольная фраза</span><span class="sxs-lookup"><span data-stu-id="2f5e4-142">Location of hello passphrase</span></span> |<span data-ttu-id="2f5e4-143">Любой допустимый локальный путь к файлу или UNC</span><span class="sxs-lookup"><span data-stu-id="2f5e4-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="2f5e4-144">Hello AgentConfiguration журналы можно найти в разделе %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="2f5e4-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
