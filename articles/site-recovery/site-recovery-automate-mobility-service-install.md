---
title: "hello aaaDeploy службы мобильности восстановления сайта с помощью DSC службы автоматизации Azure | Документы Microsoft"
description: "Описывает, как развертывать tooautomatically Azure Automation DSC toouse службу hello Mobility восстановления сайта Azure и Azure агент для виртуальной Машины VMware и tooAzure репликации физического сервера"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="89fda-103">Развертывание службы мобильности hello с DSC службы автоматизации Azure для репликации виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="89fda-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="89fda-104">В Operations Management Suite предоставляется комплексное решение для архивации и аварийного восстановления, которое можно использовать в плане обеспечения непрерывности бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="89fda-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="89fda-105">Мы начали этот путь с Hyper-V, используя реплику Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="89fda-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="89fda-106">Но у нас есть развернутой toosupport разнородных установки, так как клиенты имеют несколько низкоуровневых оболочках и платформ в своих облаках.</span><span class="sxs-lookup"><span data-stu-id="89fda-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="89fda-107">При выполнении рабочих нагрузок VMware и физических серверов сегодня, сервер управления запускает все hello компонентов Azure Site Recovery в вашей среде toohandle hello связью и передачи данных репликации в Azure, когда Azure — место.</span><span class="sxs-lookup"><span data-stu-id="89fda-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="89fda-108">Развертывание службы hello Mobility восстановления сайта с помощью DSC службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="89fda-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="89fda-109">Начнем с краткого разбора функций этого сервера управления.</span><span class="sxs-lookup"><span data-stu-id="89fda-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="89fda-110">сервер управления Hello выполняется несколько ролей сервера.</span><span class="sxs-lookup"><span data-stu-id="89fda-110">hello management server runs several server roles.</span></span> <span data-ttu-id="89fda-111">Одна из них, *роль конфигурации*, координирует обмен данными и управляет процессами репликации и восстановления данных.</span><span class="sxs-lookup"><span data-stu-id="89fda-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="89fda-112">Кроме того, hello *процесс* роли действует как шлюз репликации.</span><span class="sxs-lookup"><span data-stu-id="89fda-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="89fda-113">Эта роль передаются данные репликации из защищенного источника машин, выполняет оптимизацию для кэширования, сжатия и шифрования и отправляет его tooan учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="89fda-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="89fda-114">Одна из функций hello для hello процесс роли также установки toopush машин tooprotected службы мобильности hello и выполнить автоматическое обнаружение виртуальных машин VMware.</span><span class="sxs-lookup"><span data-stu-id="89fda-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="89fda-115">Если восстановление размещения из Azure, hello *главного целевого сервера* роль будет обрабатывать данные репликации hello в рамках этой операции.</span><span class="sxs-lookup"><span data-stu-id="89fda-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="89fda-116">Для машин, защищенных hello, мы полагаемся на hello *службы Mobility service*.</span><span class="sxs-lookup"><span data-stu-id="89fda-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="89fda-117">Этот компонент является компьютер развернутой tooevery (виртуальной Машины VMware или физических серверов), будет tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="89fda-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="89fda-118">Она фиксирует записи данных на компьютере hello и пересылает их toohello сервера управления (роль процесса).</span><span class="sxs-lookup"><span data-stu-id="89fda-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="89fda-119">При работе с непрерывность бизнес-процессов, это важно toounderstand рабочих нагрузок, инфраструктуры и компоненты hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="89fda-120">Можно затем требования hello для целевого времени восстановления (RTO) и целевую точку восстановления (RPO).</span><span class="sxs-lookup"><span data-stu-id="89fda-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="89fda-121">В данном контексте hello службы Mobility service — tooensuring ключа, как и следовало ожидать защищенных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="89fda-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="89fda-122">Как оптимальным образом можно обеспечить надежную защищенную конфигурацию, используя компоненты Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="89fda-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="89fda-123">В этой статье приведен пример того, как можно использовать Azure Automation требуемого состояния (DSC), вместе с Site Recovery, tooensure:</span><span class="sxs-lookup"><span data-stu-id="89fda-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="89fda-124">Служба мобильности Hello и агент ВМ Azure являются развернутой toohello компьютеров с Windows, которые должны tooprotect.</span><span class="sxs-lookup"><span data-stu-id="89fda-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="89fda-125">Служба мобильности Hello и агент ВМ Azure всегда запускаются при Azure — целевым объектом репликации hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89fda-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89fda-126">Prerequisites</span></span>
* <span data-ttu-id="89fda-127">В случае установки необходимых hello toostore репозитория</span><span class="sxs-lookup"><span data-stu-id="89fda-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="89fda-128">Репозиторий toostore hello требуется парольная фраза tooregister с сервером управления hello</span><span class="sxs-lookup"><span data-stu-id="89fda-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="89fda-129">Для каждого сервера управления создается уникальная парольная фраза.</span><span class="sxs-lookup"><span data-stu-id="89fda-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="89fda-130">Если вы собираетесь toodeploy несколько серверов управления, у вас есть tooensure, исправьте парольную фразу, хранится в файле passphrase.txt hello hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="89fda-131">Windows Management Framework (WMF) 5.0 установлено на компьютерах hello, что требуется tooenable для защиты (требование DSC службы автоматизации)</span><span class="sxs-lookup"><span data-stu-id="89fda-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="89fda-132">Если требуется, чтобы машины toouse DSC для Windows, имеющих установки WMF 4.0, см. раздел hello [использование DSC в отключенных средах](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="89fda-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="89fda-133">Служба мобильности Hello может устанавливаться через командную строку hello и нескольких аргументов.</span><span class="sxs-lookup"><span data-stu-id="89fda-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="89fda-134">Вот почему потребуется двоичные файлы hello toohave (после извлечения их из настройки программы установки) и сохранять их в том месте, где их можно получить с помощью конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="89fda-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="89fda-135">Шаг 1. Извлечение двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="89fda-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="89fda-136">tooextract hello файлы, необходимые для программы установки, откройте toohello следующий каталог на сервере управления.</span><span class="sxs-lookup"><span data-stu-id="89fda-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="89fda-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="89fda-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="89fda-138">В этой папке должен быть MSI-файл с таким именем.</span><span class="sxs-lookup"><span data-stu-id="89fda-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="89fda-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="89fda-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="89fda-140">Используйте следующие команды tooextract hello установщика hello:</span><span class="sxs-lookup"><span data-stu-id="89fda-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="89fda-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="89fda-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="89fda-142">Выберите все файлы и отправлять их tooa сжатые ZIP-папки.</span><span class="sxs-lookup"><span data-stu-id="89fda-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="89fda-143">Теперь у вас есть hello двоичные файлы, необходимые настройки hello tooautomate hello службы Mobility service с помощью DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="89fda-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="89fda-144">Парольная фраза</span><span class="sxs-lookup"><span data-stu-id="89fda-144">Passphrase</span></span>
<span data-ttu-id="89fda-145">Далее необходимо toodetermine место tooplace этот ZIP-папки.</span><span class="sxs-lookup"><span data-stu-id="89fda-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="89fda-146">Можно использовать учетную запись хранилища Azure, как показано далее, toostore hello парольную фразу, необходимое для установки hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="89fda-147">затем регистрирует Hello агента с сервером управления hello в рамках процесса hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="89fda-148">Парольная фраза Hello, полученный при развертывании сервера управления hello могут быть сохранены как passphrase.txt tooa текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="89fda-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="89fda-149">Поместите ZIP-папки hello и парольная фраза hello выделенного контейнера в учетной записи хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Расположение папки](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="89fda-151">Если вы предпочитаете tookeep эти файлы в общей папке в сети, это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="89fda-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="89fda-152">Необходимо просто tooensure, hello DSC ресурс, который будет использоваться позже имеет доступ и может получить установки hello и парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="89fda-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="89fda-153">Шаг 2: Создание конфигурации hello DSC</span><span class="sxs-lookup"><span data-stu-id="89fda-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="89fda-154">Программа установки Hello зависит от WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="89fda-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="89fda-155">Для компьютера toosuccessfully hello применить hello конфигурации с помощью DSC службы автоматизации, WMF 5.0 должен toobe присутствует.</span><span class="sxs-lookup"><span data-stu-id="89fda-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="89fda-156">Hello среде используется следующая конфигурация DSC пример hello:</span><span class="sxs-lookup"><span data-stu-id="89fda-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="89fda-157">Hello конфигурации будет выполнять hello следующее:</span><span class="sxs-lookup"><span data-stu-id="89fda-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="89fda-158">переменные Hello сообщает о конфигурации hello где tooget hello двоичных файлов для службы мобильности hello и hello агент ВМ Azure, которой tooget hello парольной фразы, а toostore hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="89fda-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="89fda-159">Hello конфигурации будут импортированы ресурсов xPSDesiredStateConfiguration DSC hello, чтобы можно было использовать `xRemoteFile` toodownload hello файлов из репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="89fda-160">Hello конфигурации создаст каталог место двоичные файлы toostore hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="89fda-161">ресурс archive Hello hello файлы будут извлечены из ZIP-папки hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="89fda-162">ресурс установки пакета Hello будет установлена служба Mobility hello из hello UNIFIEDAGENT. Exe-ФАЙЛ установщика hello определенных аргументов.</span><span class="sxs-lookup"><span data-stu-id="89fda-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="89fda-163">(переменные hello, составляющие hello аргументы требуют toobe изменить tooreflect среды)</span><span class="sxs-lookup"><span data-stu-id="89fda-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="89fda-164">Hello пакета ресурсов AzureAgent установить агент ВМ Azure hello, рекомендуется на каждой виртуальной Машине, запущенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="89fda-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="89fda-165">агент ВМ Azure Hello также упрощает toohello возможных tooadd расширения виртуальной Машины после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="89fda-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="89fda-166">Hello ресурсы, служба будет убедитесь, что мобильных служб, связанных с hello и hello Azure они всегда работают.</span><span class="sxs-lookup"><span data-stu-id="89fda-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="89fda-167">Сохранить конфигурацию hello как **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="89fda-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="89fda-168">Запомнить hello tooreplace CSIP в сервер управления фактическое hello tooreflect конфигурации для hello агент будет подключен и будет использовать правильную парольную фразу hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="89fda-169">Шаг 3: Отправка tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="89fda-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="89fda-170">Поскольку hello DSC настройки, сделанные будет импортировать требуемый модуль ресурсов DSC (xPSDesiredStateConfiguration), вам потребуется tooimport этот модуль в автоматизации перед отправкой конфигурации hello DSC.</span><span class="sxs-lookup"><span data-stu-id="89fda-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="89fda-171">Слишком Обзор входа в учетную запись автоматизации, tooyour**активы** > **модули**и нажмите кнопку **обзора коллекции**.</span><span class="sxs-lookup"><span data-stu-id="89fda-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="89fda-172">Здесь можно найти модуль hello и импортируйте его tooyour учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89fda-172">Here you can search for hello module and import it tooyour account.</span></span>

![Импорт модуля](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="89fda-174">После завершения, go tooyour машины при наличии hello модули диспетчера ресурсов Azure и продолжить конфигурацию DSC только что созданный hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="89fda-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="89fda-175">Импорт командлетов</span><span class="sxs-lookup"><span data-stu-id="89fda-175">Import cmdlets</span></span>
<span data-ttu-id="89fda-176">В PowerShell войдите в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="89fda-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="89fda-177">Изменения tooreflect командлеты hello среды и записывать данные учетной записи автоматизации в переменной.</span><span class="sxs-lookup"><span data-stu-id="89fda-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="89fda-178">Отправьте hello настройки tooAutomation DSC с помощью hello, выполнив командлет.</span><span class="sxs-lookup"><span data-stu-id="89fda-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="89fda-179">Компиляция конфигурации hello в DSC службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="89fda-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="89fda-180">Далее необходимо toocompile hello конфигурации в DSC службы автоматизации, так, чтобы можно было начать tooit tooregister узлов.</span><span class="sxs-lookup"><span data-stu-id="89fda-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="89fda-181">Для этого, выполнив следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="89fda-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="89fda-182">Это может занять несколько минут, так как по сути вы развертываете hello конфигурации toohello размещенных DSC опрашивающей службы.</span><span class="sxs-lookup"><span data-stu-id="89fda-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="89fda-183">После компиляции hello конфигурации можно получить сведения о задании hello с помощью PowerShell (Get-AzureRmAutomationDscCompilationJob) или с помощью hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="89fda-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Получение задания](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="89fda-185">Теперь успешно опубликован и отправки вашего tooAutomation конфигурации DSC DSC.</span><span class="sxs-lookup"><span data-stu-id="89fda-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="89fda-186">Шаг 4: Встроенный машины tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="89fda-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="89fda-187">Одним из hello необходимые условия для выполнения этого сценария является обновляются, компьютеры с Windows hello последнюю версию WMF.</span><span class="sxs-lookup"><span data-stu-id="89fda-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="89fda-188">Можно загрузить и установить правильную версию hello для вашей платформы из hello [центра загрузки](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="89fda-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="89fda-189">Теперь вы создадите metaconfig для DSC, что будет применять tooyour узлов.</span><span class="sxs-lookup"><span data-stu-id="89fda-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="89fda-190">toosucceed с этим необходимо tooretrieve hello конечной точки URL-адрес и hello первичный ключ для выбранной учетной записи автоматизации в Azure.</span><span class="sxs-lookup"><span data-stu-id="89fda-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="89fda-191">Можно найти эти значения в разделе **ключей** на hello **все параметры** колонке hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="89fda-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Значения ключей](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="89fda-193">В этом примере имеется физический сервер Windows Server 2012 R2, требуется tooprotect с помощью Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="89fda-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="89fda-194">Проверьте все ожидающие операции переименования файла в реестре hello</span><span class="sxs-lookup"><span data-stu-id="89fda-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="89fda-195">Прежде чем начать tooassociate hello server с конечной точкой hello DSC службы автоматизации, рекомендуется проверять наличие все ожидающие операции переименования файла в реестре hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="89fda-196">Они могут запретить hello установки завершить из-за tooa ожидается перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="89fda-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="89fda-197">Выполните следующий командлет tooverify, это не ожидается перезагрузка сервера hello hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="89fda-198">Это показывает пустым, имеется ли tooproceed ОК.</span><span class="sxs-lookup"><span data-stu-id="89fda-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="89fda-199">Если нет, вы должны обработать перезагрузка сервера hello в течение периода обслуживания.</span><span class="sxs-lookup"><span data-stu-id="89fda-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="89fda-200">tooapply hello конфигурации на сервере hello запустите hello PowerShell интегрированная среда сценариев (ISE) и выполните следующий скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="89fda-201">Это по сути локальной конфигурации DSC, указать tooregister engine hello локального диспетчера конфигураций с hello службы DSC службы автоматизации и получить определенную конфигурацию hello (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="89fda-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="89fda-202">Эта конфигурация приведет к tooregister engine сам hello локального диспетчера конфигураций с DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="89fda-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="89fda-203">Также определяет работу hello ядра, что нужно делать при изменении конфигурации (ApplyAndAutoCorrect) и как его следует продолжить настройку hello, если требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="89fda-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="89fda-204">После запуска этого сценария hello узел должен начинаться tooregister с Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="89fda-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Выполняется регистрация узла](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="89fda-206">Если вернуться toohello портал Azure, вы увидите этот узел вновь зарегистрированного hello теперь отображается на портале hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Зарегистрированный узел портала hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="89fda-208">На сервере hello можно выполнить следующий командлет tooverify, hello узел был зарегистрирован правильно PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="89fda-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="89fda-209">После настройки hello извлеченные и примененные toohello сервера, это можно проверить, выполнив следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="89fda-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="89fda-210">Hello выходные данные показывают, что этот сервер hello успешно извлечено конфигурации:</span><span class="sxs-lookup"><span data-stu-id="89fda-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Выходные данные](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="89fda-212">Кроме того, программа установки службы Mobility hello имеет свой собственный журнал, в котором можно найти в *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="89fda-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="89fda-213">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="89fda-213">That’s it.</span></span> <span data-ttu-id="89fda-214">Теперь успешно развернуты и зарегистрированы hello Mobility service на компьютере hello, требуется tooprotect с помощью Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="89fda-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="89fda-215">DSC будет убедитесь, что hello необходимые службы запущены всегда.</span><span class="sxs-lookup"><span data-stu-id="89fda-215">DSC will make sure that hello required services are always running.</span></span>

![Развертывание завершено успешно](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="89fda-217">После hello сервер управления обнаруживает hello успешному развертыванию, можно настроить защиту и включить репликацию на машине hello с помощью Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="89fda-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="89fda-218">Использование DSC в отключенных средах</span><span class="sxs-lookup"><span data-stu-id="89fda-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="89fda-219">Если компьютеры не подключенных toohello Интернета, можно по-прежнему полагаться на DSC toodeploy и настроить службу Mobility hello на hello рабочих нагрузок, которые должны tooprotect.</span><span class="sxs-lookup"><span data-stu-id="89fda-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="89fda-220">Можно создать собственные опрашивающего сервера DSC в вашей среде tooessentially предоставляют hello такие же возможности, которые получаются из DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="89fda-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="89fda-221">То есть hello клиентов будет получать hello конфигурации (после его регистрации) конечной точки toohello DSC.</span><span class="sxs-lookup"><span data-stu-id="89fda-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="89fda-222">Тем не менее другой вариант — toomanually принудительной hello DSC конфигурации tooyour машины, локально или удаленно.</span><span class="sxs-lookup"><span data-stu-id="89fda-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="89fda-223">Обратите внимание, что в этом примере добавленный параметр для имени компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="89fda-224">Hello удаленные файлы теперь находятся на удаленном ресурсе, который должен быть доступен, которые должны tooprotect машины hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="89fda-225">Hello конец скрипта hello вводит в действие hello конфигурации, а затем запускает tooapply hello DSC конфигурации toohello целевого компьютера.</span><span class="sxs-lookup"><span data-stu-id="89fda-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="89fda-226">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89fda-226">Prerequisites</span></span>
<span data-ttu-id="89fda-227">Убедитесь, что установлен модуль PowerShell xPSDesiredStateConfiguration, hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="89fda-228">Для компьютеров Windows с установленным WMF 5.0 вы можете установить модуль xPSDesiredStateConfiguration hello, выполнив следующий командлет на целевых компьютерах hello hello:</span><span class="sxs-lookup"><span data-stu-id="89fda-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="89fda-229">Можно также загрузить и сохранить модуль hello на случай необходимости toodistribute его tooWindows машин, имеющих WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="89fda-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="89fda-230">Выполните этот командлет на компьютере, на котором установлен компонент PowerShellGet (WMF 5.0).</span><span class="sxs-lookup"><span data-stu-id="89fda-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="89fda-231">Также для WMF 4.0, убедитесь, что hello [обновление Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) будет установлено на компьютерах hello.</span><span class="sxs-lookup"><span data-stu-id="89fda-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="89fda-232">Hello следующей конфигурации могут быть принудительно tooWindows машин, которые имеют WMF 5.0 и WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="89fda-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="89fda-233">Если tooinstantiate собственные опрашивающего сервера DSC на ваши возможности hello toomimic корпоративной сети, можно получить из DSC службы автоматизации, см. [Настройка опрашивающего веб-сервера DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="89fda-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="89fda-234">Развертывание конфигурации DSC с помощью шаблона Azure Resource Manager (необязательно)</span><span class="sxs-lookup"><span data-stu-id="89fda-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="89fda-235">В этой статье основное внимание уделяется созданию собственного tooautomatically конфигурации DSC развертывать службы мобильности hello и hello агента ВМ Azure — и убедитесь, что они работают на компьютерах hello, которые должны tooprotect.</span><span class="sxs-lookup"><span data-stu-id="89fda-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="89fda-236">У нас также есть шаблона Azure Resource Manager, которое будет выполнять развертывание этого DSC конфигурации tooa новую или существующую запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="89fda-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="89fda-237">Hello шаблон будет использовать ресурсы автоматизации toocreate входные параметры, содержащие переменные hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="89fda-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="89fda-238">После развертывания шаблона hello, можно просто ссылаться toostep 4 в tooonboard этого руководства компьютеры.</span><span class="sxs-lookup"><span data-stu-id="89fda-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="89fda-239">Hello шаблонов будет выполнять hello следующее:</span><span class="sxs-lookup"><span data-stu-id="89fda-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="89fda-240">Использует имеющуюся или создаст учетную запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="89fda-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="89fda-241">Примет входные параметры для:</span><span class="sxs-lookup"><span data-stu-id="89fda-241">Take input parameters for:</span></span>
   * <span data-ttu-id="89fda-242">ASRRemoteFile--hello расположение, где были сохранены hello установки службы Mobility</span><span class="sxs-lookup"><span data-stu-id="89fda-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="89fda-243">ASRPassphrase--hello расположение, где сохранили файл passphrase.txt hello</span><span class="sxs-lookup"><span data-stu-id="89fda-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="89fda-244">ASRCSEndpoint--hello IP-адрес сервера управления</span><span class="sxs-lookup"><span data-stu-id="89fda-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="89fda-245">Импортируйте модуль PowerShell xPSDesiredStateConfiguration hello</span><span class="sxs-lookup"><span data-stu-id="89fda-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="89fda-246">Создание и компиляция конфигурации DSC hello</span><span class="sxs-lookup"><span data-stu-id="89fda-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="89fda-247">Все hello в предыдущих шагах, произойдет в правильном порядке hello, для возможности запуска адаптации компьютеры для защиты.</span><span class="sxs-lookup"><span data-stu-id="89fda-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="89fda-248">Hello шаблона с помощью инструкции по развертыванию, находится на [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="89fda-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="89fda-249">Развертывание hello шаблона с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="89fda-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="89fda-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89fda-250">Next steps</span></span>
<span data-ttu-id="89fda-251">После развертывания агентов службы мобильности hello, вы можете [включить репликацию](site-recovery-vmware-to-azure.md) для hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="89fda-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
