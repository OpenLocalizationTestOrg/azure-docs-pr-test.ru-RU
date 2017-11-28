1. <span data-ttu-id="14d7d-101">Скопируйте установщик в локальную папку (например, /tmp) на сервере, который необходимо защитить.</span><span class="sxs-lookup"><span data-stu-id="14d7d-101">Copy the installer to a local folder (for example, /tmp) on the server that you want to protect.</span></span> <span data-ttu-id="14d7d-102">Выполните следующие команды в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="14d7d-102">In a terminal, run the following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="14d7d-103">Чтобы установить службу Mobility Service, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="14d7d-103">To install Mobility Service, run the following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="14d7d-104">После завершения установки службу Mobility Service необходимо зарегистрировать на сервере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14d7d-104">Once installation is complete, the Mobility Service needs to get registered to the configuration server.</span></span> <span data-ttu-id="14d7d-105">Выполните следующую команду, чтобы зарегистрировать службу Mobility Service на сервере конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14d7d-105">Run the following command to register the Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="14d7d-106">Командная строка установщика Mobility Service</span><span class="sxs-lookup"><span data-stu-id="14d7d-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="14d7d-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="14d7d-107">Parameter</span></span>|<span data-ttu-id="14d7d-108">Тип</span><span class="sxs-lookup"><span data-stu-id="14d7d-108">Type</span></span>|<span data-ttu-id="14d7d-109">Описание</span><span class="sxs-lookup"><span data-stu-id="14d7d-109">Description</span></span>|<span data-ttu-id="14d7d-110">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="14d7d-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="14d7d-111">-r</span><span class="sxs-lookup"><span data-stu-id="14d7d-111">-r</span></span> |<span data-ttu-id="14d7d-112">Обязательно</span><span class="sxs-lookup"><span data-stu-id="14d7d-112">Mandatory</span></span>|<span data-ttu-id="14d7d-113">Указывает службу, которую нужно установить: Mobility Service (MS) или MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="14d7d-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="14d7d-114">MS</span><span class="sxs-lookup"><span data-stu-id="14d7d-114">MS</span></span> </br> <span data-ttu-id="14d7d-115">MT</span><span class="sxs-lookup"><span data-stu-id="14d7d-115">MT</span></span>|
|<span data-ttu-id="14d7d-116">-d</span><span class="sxs-lookup"><span data-stu-id="14d7d-116">-d</span></span> |<span data-ttu-id="14d7d-117">Необязательно</span><span class="sxs-lookup"><span data-stu-id="14d7d-117">Optional</span></span>|<span data-ttu-id="14d7d-118">Расположение, в котором будет установлена служба Mobility Service</span><span class="sxs-lookup"><span data-stu-id="14d7d-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="14d7d-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="14d7d-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="14d7d-120">-v</span><span class="sxs-lookup"><span data-stu-id="14d7d-120">-v</span></span>|<span data-ttu-id="14d7d-121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="14d7d-121">Mandatory</span></span>|<span data-ttu-id="14d7d-122">Указывает платформу, на которой будет установлена служба Mobility Service</span><span class="sxs-lookup"><span data-stu-id="14d7d-122">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="14d7d-123">- **VMware.** Используйте это значение при установке службы Mobility Service на виртуальной машине под управлением *узлов VMware vSphere ESXi*, *узлов Hyper-V* или *физических серверов*</span><span class="sxs-lookup"><span data-stu-id="14d7d-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="14d7d-124">- **Azure.** Используйте это значение при установке агента на виртуальной машине Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="14d7d-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="14d7d-125">VMware</span><span class="sxs-lookup"><span data-stu-id="14d7d-125">VMware</span></span> </br> <span data-ttu-id="14d7d-126">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="14d7d-126">Azure</span></span>|
|<span data-ttu-id="14d7d-127">-q</span><span class="sxs-lookup"><span data-stu-id="14d7d-127">-q</span></span>|<span data-ttu-id="14d7d-128">Необязательно</span><span class="sxs-lookup"><span data-stu-id="14d7d-128">Optional</span></span>|<span data-ttu-id="14d7d-129">Используется для запуска установщика в автоматическом режиме</span><span class="sxs-lookup"><span data-stu-id="14d7d-129">Specifies to run installer in silent mode</span></span>| <span data-ttu-id="14d7d-130">Недоступно</span><span class="sxs-lookup"><span data-stu-id="14d7d-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="14d7d-131">Командная строка конфигурации службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="14d7d-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="14d7d-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="14d7d-132">Parameter</span></span>|<span data-ttu-id="14d7d-133">Тип</span><span class="sxs-lookup"><span data-stu-id="14d7d-133">Type</span></span>|<span data-ttu-id="14d7d-134">Описание</span><span class="sxs-lookup"><span data-stu-id="14d7d-134">Description</span></span>|<span data-ttu-id="14d7d-135">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="14d7d-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="14d7d-136">-i</span><span class="sxs-lookup"><span data-stu-id="14d7d-136">-i</span></span> |<span data-ttu-id="14d7d-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="14d7d-137">Mandatory</span></span>|<span data-ttu-id="14d7d-138">IP-адрес сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="14d7d-138">IP of the Configuration Server</span></span>|<span data-ttu-id="14d7d-139">Любой допустимый IP-адрес</span><span class="sxs-lookup"><span data-stu-id="14d7d-139">Any valid IP Address</span></span>|
|<span data-ttu-id="14d7d-140">-P</span><span class="sxs-lookup"><span data-stu-id="14d7d-140">-P</span></span> |<span data-ttu-id="14d7d-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="14d7d-141">Mandatory</span></span>|<span data-ttu-id="14d7d-142">Полный путь к файлу, в котором хранится парольная фраза для подключения</span><span class="sxs-lookup"><span data-stu-id="14d7d-142">Full file path the file where the connection passphrase is saved</span></span>|<span data-ttu-id="14d7d-143">Любая допустимая папка</span><span class="sxs-lookup"><span data-stu-id="14d7d-143">Any valid folder</span></span>|
