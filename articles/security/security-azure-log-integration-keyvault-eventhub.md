---
title: "журналы aaaIntegrate из хранилища ключей Azure с помощью концентраторов событий | Документы Microsoft"
description: "Учебник, в котором предоставляет необходимые шаги hello toomake хранилище ключей журналы доступны tooa SIEM с помощью интеграции журналов Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="fd7b9-103">Руководство по интеграции журналов Azure. Обработка событий Azure Key Vault с помощью концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="fd7b9-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="fd7b9-104">Можно использовать tooretrieve в журнал события журнала интеграции Azure и сделать их tooyour доступные сведения и событий системы управления безопасностью (SIEM).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="fd7b9-105">Этот учебник является примером как интеграции журналов Azure можно использовать tooprocess журналы, полученные через концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="fd7b9-106">С помощью этого учебника tooget изучать как рабочих журналов интеграции Azure и концентраторов событий друг с другом, выполнив hello примеры действий и основные сведения о поддержке решений hello каждого шага.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="fd7b9-107">Затем вы сможете, что вы узнали здесь toocreate toosupport свои собственные шаги уникальные требования вашей компании.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="fd7b9-108">шаги Hello и команды в этом учебнике не предполагаемого toobe операций копирования и вставки.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="fd7b9-109">Они предоставляются только в качестве примеров.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-109">They're examples only.</span></span> <span data-ttu-id="fd7b9-110">Не используйте команды PowerShell hello «как есть» в динамической среде.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="fd7b9-111">Их необходимо настраивать с учетом уникальной среды.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="fd7b9-112">Этот учебник поможет выполнить процесс hello получения концентратора событий регистрируется tooan действие хранилища ключей Azure и делая ее доступной в качестве системы SIEM tooyour файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="fd7b9-113">Затем можно настроить SIEM системы tooprocess hello JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="fd7b9-114">Большая часть hello шагах данного учебника включают Настройка хранилищ ключей, учетные записи хранения и концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="fd7b9-115">конкретные шаги интеграции Azure журнала Hello, hello конце этого учебника.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="fd7b9-116">Не выполняйте следующие действия в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="fd7b9-117">Они предназначены для работы в лабораторной среде.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="fd7b9-118">Перед использованием их в рабочей среде необходимо настроить действия hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="fd7b9-119">Сведения предоставлены вдоль hello способ помогает понять hello лежит в основе каждого шага.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="fd7b9-120">Статьи tooother ссылки предоставляют подробные сведения на определенных разделов.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="fd7b9-121">Дополнительные сведения о службах hello, которые упоминаются в этом учебнике см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="fd7b9-122">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="fd7b9-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="fd7b9-123">Концентраторы событий Azure</span><span class="sxs-lookup"><span data-stu-id="fd7b9-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="fd7b9-124">Интеграция журналов Azure</span><span class="sxs-lookup"><span data-stu-id="fd7b9-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="fd7b9-125">Начальная настройка</span><span class="sxs-lookup"><span data-stu-id="fd7b9-125">Initial setup</span></span>

<span data-ttu-id="fd7b9-126">Перед выполнением действия hello в этой статье, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="fd7b9-127">Подписка Azure и учетная запись для этой подписки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="fd7b9-128">Если у вас нет подписки, вы можете [создать бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="fd7b9-129">В системе с toohello доступа Интернета, отвечающий требованиям hello для интеграции Azure журнала установки.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="fd7b9-130">Hello системы может размещаться в облачной службе или в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="fd7b9-131">Установленная служба [интеграции журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="fd7b9-132">tooinstall его:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-132">tooinstall it:</span></span>

   <span data-ttu-id="fd7b9-133">а.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-133">a.</span></span> <span data-ttu-id="fd7b9-134">Использование удаленного рабочего стола tooconnect toohello системы, упомянутых в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="fd7b9-135">b.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-135">b.</span></span> <span data-ttu-id="fd7b9-136">Скопируйте hello Azure журнала установщика toohello системы интеграции.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="fd7b9-137">Вы можете [загружать файлы установки hello](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="fd7b9-138">c.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-138">c.</span></span> <span data-ttu-id="fd7b9-139">Запустите установщик hello и примите условия лицензии программного обеспечения Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="fd7b9-140">d.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-140">d.</span></span> <span data-ttu-id="fd7b9-141">При указании данные телеметрии, оставьте hello флажок установлен.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="fd7b9-142">Если вы предпочитаете не отправлять tooMicrosoft сведения об использовании, снимите флажок "hello".</span><span class="sxs-lookup"><span data-stu-id="fd7b9-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="fd7b9-143">Дополнительные сведения об интеграции журналов Azure и как tooinstall, в разделе [интеграции Azure журнала с помощью ведения журнала диагностики Azure и пересылки событий Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="fd7b9-144">Последняя версия PowerShell Hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="fd7b9-145">Если у вас установлен Windows Server 2016, по меньшей мере у вас есть PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="fd7b9-146">Если вы используете другие версии Windows Server, может потребоваться установить более раннюю версию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="fd7b9-147">Можно проверить версии hello, введя ```get-host``` в окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="fd7b9-148">Если версия PowerShell 5.0 не установлена, ее можно [скачать](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="fd7b9-149">После того как вы по крайней мере PowerShell 5.0, можно продолжить tooinstall hello последней версии:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="fd7b9-150">а.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-150">a.</span></span> <span data-ttu-id="fd7b9-151">В окне PowerShell, введите hello ```Install-Module Azure``` команды.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="fd7b9-152">Выполните действия по установке hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="fd7b9-153">b.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-153">b.</span></span> <span data-ttu-id="fd7b9-154">Введите hello ```Install-Module AzureRM``` команды.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="fd7b9-155">Выполните действия по установке hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="fd7b9-156">Дополнительные сведения см. в статье [Установка Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="fd7b9-157">Создание вспомогательных элементов инфраструктуры</span><span class="sxs-lookup"><span data-stu-id="fd7b9-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="fd7b9-158">Откройте окно PowerShell с повышенными привилегиями и перейдите слишком**интеграции журнала C:\Program Files\Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="fd7b9-159">Импортируйте командлеты AzLog hello, выполнив сценарий hello LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="fd7b9-160">Введите hello `.\LoadAzLogModule.ps1` команды.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="fd7b9-161">(Обратите внимание hello «. \» в этой команде.) Вы увидите нечто вроде этого:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Список загруженных модулей](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="fd7b9-163">Введите hello `Login-AzureRmAccount` команды.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="fd7b9-164">В окне приветствия входа введите hello учетные данные для подписки hello, который будет использоваться для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fd7b9-165">Если это впервые hello, заносимых в журнал в tooAzure на данном компьютере, появится сообщение о разрешении данные об использовании PowerShell toocollect Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="fd7b9-166">Рекомендуется включить эту коллекцию, так как они будут использоваться tooimprove Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="fd7b9-167">После успешной проверки подлинности выполнен вход, и вы увидите сведения hello в следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="fd7b9-168">Запишите имя идентификатора и подписки подписка hello, так как они потребуются позднее шаги toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Окно PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="fd7b9-170">Создайте переменные toostore значения, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="fd7b9-171">Введите каждый из следующих строк PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="fd7b9-172">Может потребоваться tooadjust hello значения toomatch вашей среде.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="fd7b9-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (У вашей подписки может быть другое имя.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="fd7b9-174">Вы увидите его как часть hello выходные данные предыдущей команды hello.)</span><span class="sxs-lookup"><span data-stu-id="fd7b9-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="fd7b9-175">```$location = 'West US'```(Эта переменная будет расположение используемых toopass hello, которой должен быть создан ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="fd7b9-176">Можно изменить этот переменной toobe любой папку по своему усмотрению.)</span><span class="sxs-lookup"><span data-stu-id="fd7b9-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="fd7b9-177">``` $name = 'azlogtest' + $random```(имя hello может быть любым, но оно должно включать только строчные буквы и цифры).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="fd7b9-178">``` $storageName = $name```(Эта переменная будет использоваться hello имени учетной записи хранения.)</span><span class="sxs-lookup"><span data-stu-id="fd7b9-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="fd7b9-179">```$rgname = $name ```(Эта переменная будет использоваться для имени группы ресурсов hello.)</span><span class="sxs-lookup"><span data-stu-id="fd7b9-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="fd7b9-180">``` $eventHubNameSpaceName = $name```(Это имя hello hello пространство имен концентратора событий).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="fd7b9-181">Укажите hello подписку, которая будет использоваться с:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="fd7b9-182">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="fd7b9-183">Если ввести `$rg` на этом этапе вы увидите примерно toothis экрана выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Выходные данные после создания группы ресурсов](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="fd7b9-185">Создайте учетную запись хранилища, который будет использоваться tookeep отслеживания сведений о состоянии:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="fd7b9-186">Создайте пространство имен концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-186">Create hello event hub namespace.</span></span> <span data-ttu-id="fd7b9-187">Это обязательный toocreate концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="fd7b9-188">Получите идентификатор правила hello, который будет использоваться с поставщиком аналитики hello:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="fd7b9-189">Получить все возможные местоположения Azure и добавьте hello имена tooa переменную, которая может использоваться в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="fd7b9-190">а.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="fd7b9-191">b.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="fd7b9-192">Если ввести `$locations` на этом этапе имена можно увидеть hello расположение без hello дополнительные данные, возвращаемые командлетом Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="fd7b9-193">Создайте профиль журнала Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="fd7b9-194">Дополнительные сведения о hello Azure log профиль в разделе [Обзор hello журнал действий Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="fd7b9-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fd7b9-195">Может появиться сообщение об ошибке при попытке toocreate профиля журнала.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="fd7b9-196">Затем можно просматривать документацию hello для Get-AzureRmLogProfile и Remove AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="fd7b9-197">При выполнении Get-AzureRmLogProfile появиться сведения о профиле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="fd7b9-198">Можно удалить существующий профиль журнала hello, введя hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` команды.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Ошибка профиля Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="fd7b9-200">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-200">Create a key vault</span></span>

1. <span data-ttu-id="fd7b9-201">Создание хранилища ключей hello:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="fd7b9-202">Настройка ведения журнала для хранилища ключей hello:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="fd7b9-203">Создание действия журнала</span><span class="sxs-lookup"><span data-stu-id="fd7b9-203">Generate log activity</span></span>

<span data-ttu-id="fd7b9-204">Запросы должны toobe отправлено tooKey хранилище toogenerate журнала действий.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="fd7b9-205">Действия, например создание ключей, хранение секретов или чтение секретов из Key Vault, будут создавать записи в журнале.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="fd7b9-206">Для отображения текущего хранилища ключей hello:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="fd7b9-207">Создайте ключ **key2**:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="fd7b9-208">Показывать ключи hello и видеть, что **key2** содержит другое значение:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="fd7b9-209">Установка и считывание секретный toogenerate дополнительные записи журнала:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="fd7b9-210">а.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-210">a.</span></span> <span data-ttu-id="fd7b9-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` Б.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Возвращенный секрет](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="fd7b9-213">Настройка интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="fd7b9-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="fd7b9-214">Настройки всех концентратора событий tooan ведения журнала хранилища ключей hello обязательные элементы toohave требуется tooconfigure интеграции журнала Azure:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="fd7b9-215">Выполните команду AzLog hello для каждого концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="fd7b9-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="fd7b9-216">После минуты или это выполнения hello последние две команды вы должны увидеть создаваемых файлов JSON.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="fd7b9-217">Подтвердите отслеживания каталога hello **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="fd7b9-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd7b9-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd7b9-218">Next steps</span></span>

- [<span data-ttu-id="fd7b9-219">Интеграция журналов Azure: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="fd7b9-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="fd7b9-220">Приступая к работе со службой интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="fd7b9-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="fd7b9-221">Интеграция журналов из ресурсов Azure в системы SIEM</span><span class="sxs-lookup"><span data-stu-id="fd7b9-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
