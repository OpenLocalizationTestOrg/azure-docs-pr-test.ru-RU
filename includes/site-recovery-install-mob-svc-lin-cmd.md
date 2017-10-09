1. <span data-ttu-id="3dfbe-101">Скопируйте hello установщика tooa локальную папку (например, / TMP) на сервере hello, которое следует tooprotect.</span><span class="sxs-lookup"><span data-stu-id="3dfbe-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="3dfbe-102">В конечном выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="3dfbe-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="3dfbe-103">tooinstall службы Mobility Service, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3dfbe-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="3dfbe-104">После завершения установки hello службы Mobility Service должна tooget зарегистрированных toohello конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="3dfbe-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="3dfbe-105">Запустите hello, следующая команда tooregister hello службы Mobility Service с сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3dfbe-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="3dfbe-106">Командная строка установщика Mobility Service</span><span class="sxs-lookup"><span data-stu-id="3dfbe-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="3dfbe-107">Параметр</span><span class="sxs-lookup"><span data-stu-id="3dfbe-107">Parameter</span></span>|<span data-ttu-id="3dfbe-108">Тип</span><span class="sxs-lookup"><span data-stu-id="3dfbe-108">Type</span></span>|<span data-ttu-id="3dfbe-109">Описание</span><span class="sxs-lookup"><span data-stu-id="3dfbe-109">Description</span></span>|<span data-ttu-id="3dfbe-110">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="3dfbe-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="3dfbe-111">-r</span><span class="sxs-lookup"><span data-stu-id="3dfbe-111">-r</span></span> |<span data-ttu-id="3dfbe-112">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-112">Mandatory</span></span>|<span data-ttu-id="3dfbe-113">Указывает службу, которую нужно установить: Mobility Service (MS) или MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="3dfbe-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="3dfbe-114">MS</span><span class="sxs-lookup"><span data-stu-id="3dfbe-114">MS</span></span> </br> <span data-ttu-id="3dfbe-115">MT</span><span class="sxs-lookup"><span data-stu-id="3dfbe-115">MT</span></span>|
|<span data-ttu-id="3dfbe-116">-d</span><span class="sxs-lookup"><span data-stu-id="3dfbe-116">-d</span></span> |<span data-ttu-id="3dfbe-117">Необязательно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-117">Optional</span></span>|<span data-ttu-id="3dfbe-118">Расположение, в котором будет установлена служба Mobility Service</span><span class="sxs-lookup"><span data-stu-id="3dfbe-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="3dfbe-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="3dfbe-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="3dfbe-120">-v</span><span class="sxs-lookup"><span data-stu-id="3dfbe-120">-v</span></span>|<span data-ttu-id="3dfbe-121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-121">Mandatory</span></span>|<span data-ttu-id="3dfbe-122">Указывает платформу hello, на какие hello начало установлена служба Mobility</span><span class="sxs-lookup"><span data-stu-id="3dfbe-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="3dfbe-123">- **VMware.** Используйте это значение при установке службы Mobility Service на виртуальной машине под управлением *узлов VMware vSphere ESXi*, *узлов Hyper-V* или *физических серверов*</span><span class="sxs-lookup"><span data-stu-id="3dfbe-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="3dfbe-124">- **Azure.** Используйте это значение при установке агента на виртуальной машине Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="3dfbe-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="3dfbe-125">VMware</span><span class="sxs-lookup"><span data-stu-id="3dfbe-125">VMware</span></span> </br> <span data-ttu-id="3dfbe-126">Таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="3dfbe-126">Azure</span></span>|
|<span data-ttu-id="3dfbe-127">-q</span><span class="sxs-lookup"><span data-stu-id="3dfbe-127">-q</span></span>|<span data-ttu-id="3dfbe-128">Необязательно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-128">Optional</span></span>|<span data-ttu-id="3dfbe-129">Указывает toorun установки в автоматическом режиме</span><span class="sxs-lookup"><span data-stu-id="3dfbe-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="3dfbe-130">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="3dfbe-131">Командная строка конфигурации службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="3dfbe-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="3dfbe-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="3dfbe-132">Parameter</span></span>|<span data-ttu-id="3dfbe-133">Тип</span><span class="sxs-lookup"><span data-stu-id="3dfbe-133">Type</span></span>|<span data-ttu-id="3dfbe-134">Описание</span><span class="sxs-lookup"><span data-stu-id="3dfbe-134">Description</span></span>|<span data-ttu-id="3dfbe-135">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="3dfbe-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="3dfbe-136">-i</span><span class="sxs-lookup"><span data-stu-id="3dfbe-136">-i</span></span> |<span data-ttu-id="3dfbe-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-137">Mandatory</span></span>|<span data-ttu-id="3dfbe-138">IP-адрес сервера конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="3dfbe-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="3dfbe-139">Любой допустимый IP-адрес</span><span class="sxs-lookup"><span data-stu-id="3dfbe-139">Any valid IP Address</span></span>|
|<span data-ttu-id="3dfbe-140">-P</span><span class="sxs-lookup"><span data-stu-id="3dfbe-140">-P</span></span> |<span data-ttu-id="3dfbe-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3dfbe-141">Mandatory</span></span>|<span data-ttu-id="3dfbe-142">Hello полный путь к файлу, сохранения парольной фразы подключения hello</span><span class="sxs-lookup"><span data-stu-id="3dfbe-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="3dfbe-143">Любая допустимая папка</span><span class="sxs-lookup"><span data-stu-id="3dfbe-143">Any valid folder</span></span>|
