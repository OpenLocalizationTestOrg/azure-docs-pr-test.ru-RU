---
title: "Интеграция журналов из Azure Key Vault с помощью концентраторов событий | Документы Майкрософт"
description: "Руководство, в котором приводятся необходимые действия для обеспечения доступности журналов Key Vault для SIEM с помощью интеграции журналов Azure."
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
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="108c4-103">Руководство по интеграции журналов Azure. Обработка событий Azure Key Vault с помощью концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="108c4-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="108c4-104">Службу интеграции журналов Azure можно использовать для получения зарегистрированных событий журнала и обеспечения их доступности для системы SIEM.</span><span class="sxs-lookup"><span data-stu-id="108c4-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="108c4-105">В этом руководстве предоставляется поэтапный пример использования службы интеграции журналов Azure для обработки журналов, полученных из концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="108c4-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="108c4-106">Это руководство поможет вам ознакомиться с данными о совместной работе службы интеграции журналов Azure и концентраторов событий, выполнить шаги для примера и понять, как каждый шаг поддерживает решение.</span><span class="sxs-lookup"><span data-stu-id="108c4-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="108c4-107">Затем вы сможете применить полученные здесь знания для создания собственной процедуры обеспечения соответствия уникальным требованиям компании.</span><span class="sxs-lookup"><span data-stu-id="108c4-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="108c4-108">Действия и команды, используемые в этом руководстве, не предназначены для копирования и вставки.</span><span class="sxs-lookup"><span data-stu-id="108c4-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="108c4-109">Они предоставляются только в качестве примеров.</span><span class="sxs-lookup"><span data-stu-id="108c4-109">They're examples only.</span></span> <span data-ttu-id="108c4-110">Не используйте команды PowerShell "как есть" в динамической среде.</span><span class="sxs-lookup"><span data-stu-id="108c4-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="108c4-111">Их необходимо настраивать с учетом уникальной среды.</span><span class="sxs-lookup"><span data-stu-id="108c4-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="108c4-112">В этом руководстве описывается процесс использования действия Azure Key Vault, записанного в журнал концентратора событий, и обеспечения его доступности для системы SIEM в виде JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="108c4-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="108c4-113">Затем можно настроить систему SIEM для обработки JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="108c4-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="108c4-114">В большинстве шагов в этом руководстве выполняется настройка хранилищ ключей, учетных записей хранения и концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="108c4-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="108c4-115">Шаги по работе с интеграцией журналов Azure приводятся в конце руководства.</span><span class="sxs-lookup"><span data-stu-id="108c4-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="108c4-116">Не выполняйте следующие действия в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="108c4-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="108c4-117">Они предназначены для работы в лабораторной среде.</span><span class="sxs-lookup"><span data-stu-id="108c4-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="108c4-118">Прежде чем выполнять эти действия в рабочей среде, их нужно настроить.</span><span class="sxs-lookup"><span data-stu-id="108c4-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="108c4-119">Сведения, предоставляемые по ходу процедур, помогут понять причины выполнения каждого шага.</span><span class="sxs-lookup"><span data-stu-id="108c4-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="108c4-120">Перейдя по ссылкам на другие статьи, вы сможете получить более подробные сведения о конкретных разделах.</span><span class="sxs-lookup"><span data-stu-id="108c4-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="108c4-121">Дополнительные сведения о службах, которые упоминаются в этом учебнике, см. в указанных ниже разделах.</span><span class="sxs-lookup"><span data-stu-id="108c4-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="108c4-122">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="108c4-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="108c4-123">Концентраторы событий Azure</span><span class="sxs-lookup"><span data-stu-id="108c4-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="108c4-124">Интеграция журналов Azure</span><span class="sxs-lookup"><span data-stu-id="108c4-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="108c4-125">Начальная настройка</span><span class="sxs-lookup"><span data-stu-id="108c4-125">Initial setup</span></span>

<span data-ttu-id="108c4-126">Чтобы выполнить действия, описанные в этой статье, необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="108c4-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="108c4-127">Подписка Azure и учетная запись для этой подписки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="108c4-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="108c4-128">Если у вас нет подписки, вы можете [создать бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="108c4-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="108c4-129">Система с доступом к Интернету, отвечающая требованиям к установке интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="108c4-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="108c4-130">Система может быть размещена в облачной службе или в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="108c4-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="108c4-131">Установленная служба [интеграции журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="108c4-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="108c4-132">Чтобы установить службу:</span><span class="sxs-lookup"><span data-stu-id="108c4-132">To install it:</span></span>

   <span data-ttu-id="108c4-133">а.</span><span class="sxs-lookup"><span data-stu-id="108c4-133">a.</span></span> <span data-ttu-id="108c4-134">Подключитесь к системе, упомянутой в шаге 2, через удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="108c4-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="108c4-135">b.</span><span class="sxs-lookup"><span data-stu-id="108c4-135">b.</span></span> <span data-ttu-id="108c4-136">Скопируйте в систему установщик интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="108c4-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="108c4-137">Можно [скачать файлы установки](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="108c4-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="108c4-138">c.</span><span class="sxs-lookup"><span data-stu-id="108c4-138">c.</span></span> <span data-ttu-id="108c4-139">Запустите установщик и примите условия лицензионного соглашения на использование программного обеспечения корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="108c4-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="108c4-140">d.</span><span class="sxs-lookup"><span data-stu-id="108c4-140">d.</span></span> <span data-ttu-id="108c4-141">Если вы указываете данные телеметрии, оставьте флажок установленным.</span><span class="sxs-lookup"><span data-stu-id="108c4-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="108c4-142">Если вы не хотите отправлять сведения об использовании в корпорацию Майкрософт, снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="108c4-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="108c4-143">Дополнительные сведения о службе интеграции журналов Azure и действиях по ее установке см. в статье [Интеграция журналов Azure с ведением журнала системы диагностики Azure и пересылкой событий Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="108c4-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="108c4-144">Последняя версия PowerShell.</span><span class="sxs-lookup"><span data-stu-id="108c4-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="108c4-145">Если у вас установлен Windows Server 2016, по меньшей мере у вас есть PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="108c4-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="108c4-146">Если вы используете другие версии Windows Server, может потребоваться установить более раннюю версию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="108c4-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="108c4-147">Чтобы проверить используемую версию, в окне PowerShell введите ```get-host```.</span><span class="sxs-lookup"><span data-stu-id="108c4-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="108c4-148">Если версия PowerShell 5.0 не установлена, ее можно [скачать](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="108c4-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="108c4-149">При наличии PowerShell 5.0 (как минимум) перейдите к установке последней версии.</span><span class="sxs-lookup"><span data-stu-id="108c4-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="108c4-150">а.</span><span class="sxs-lookup"><span data-stu-id="108c4-150">a.</span></span> <span data-ttu-id="108c4-151">В окне PowerShell введите команду ```Install-Module Azure```.</span><span class="sxs-lookup"><span data-stu-id="108c4-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="108c4-152">Выполните действия по установке.</span><span class="sxs-lookup"><span data-stu-id="108c4-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="108c4-153">b.</span><span class="sxs-lookup"><span data-stu-id="108c4-153">b.</span></span> <span data-ttu-id="108c4-154">Введите команду ```Install-Module AzureRM```.</span><span class="sxs-lookup"><span data-stu-id="108c4-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="108c4-155">Выполните действия по установке.</span><span class="sxs-lookup"><span data-stu-id="108c4-155">Complete the installation steps.</span></span>

   <span data-ttu-id="108c4-156">Дополнительные сведения см. в статье [Установка Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="108c4-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="108c4-157">Создание вспомогательных элементов инфраструктуры</span><span class="sxs-lookup"><span data-stu-id="108c4-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="108c4-158">Откройте окно PowerShell с повышенными привилегиями и перейдите в каталог **C:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="108c4-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="108c4-159">Импортируйте командлеты AzLog, выполнив сценарий LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="108c4-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="108c4-160">Введите команду `.\LoadAzLogModule.ps1`.</span><span class="sxs-lookup"><span data-stu-id="108c4-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="108c4-161">(Обратите внимание на ".\" в этой команде.) Вы увидите нечто вроде этого:</span><span class="sxs-lookup"><span data-stu-id="108c4-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Список загруженных модулей](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="108c4-163">Введите команду `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="108c4-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="108c4-164">В окне входа введите учетные данные для подписки, которая будет использоваться в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="108c4-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="108c4-165">Если вы выполняете вход в Azure с этого компьютера впервые, появится сообщение о предоставлении корпорации Майкрософт разрешения на сбор данных об использовании PowerShell.</span><span class="sxs-lookup"><span data-stu-id="108c4-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="108c4-166">Рекомендуется включить эту функцию сбора данных, так как она будет использоваться для внесения улучшений в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="108c4-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="108c4-167">После успешной проверки подлинности вы войдете в систему и увидите сведения, аналогичные приведенным на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="108c4-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="108c4-168">Запишите идентификатор подписки и имя подписки, так как они потребуются вам на следующих этапах.</span><span class="sxs-lookup"><span data-stu-id="108c4-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![Окно PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="108c4-170">Создайте переменные для хранения значений, которые будут использоваться дальше.</span><span class="sxs-lookup"><span data-stu-id="108c4-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="108c4-171">Введите следующие строки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="108c4-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="108c4-172">Может потребоваться настроить параметры в соответствии с вашей средой.</span><span class="sxs-lookup"><span data-stu-id="108c4-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="108c4-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (У вашей подписки может быть другое имя.</span><span class="sxs-lookup"><span data-stu-id="108c4-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="108c4-174">Вы увидите его в составе выходных данных предыдущей команды.)</span><span class="sxs-lookup"><span data-stu-id="108c4-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="108c4-175">```$location = 'West US'``` (Эта переменная будет использоваться для передачи расположения, в котором должны быть созданы ресурсы.</span><span class="sxs-lookup"><span data-stu-id="108c4-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="108c4-176">Эту переменную можно изменить на любое необходимое расположение.)</span><span class="sxs-lookup"><span data-stu-id="108c4-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="108c4-177">``` $name = 'azlogtest' + $random``` (Имя может быть любым, но оно должно включать только строчные буквы и цифры.)</span><span class="sxs-lookup"><span data-stu-id="108c4-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="108c4-178">``` $storageName = $name``` (Эта переменная будет использоваться для имени учетной записи хранения.)</span><span class="sxs-lookup"><span data-stu-id="108c4-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="108c4-179">```$rgname = $name ``` (Эта переменная будет использоваться для имени группы ресурсов.)</span><span class="sxs-lookup"><span data-stu-id="108c4-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="108c4-180">``` $eventHubNameSpaceName = $name``` (Это имя пространства имен концентратора событий.)</span><span class="sxs-lookup"><span data-stu-id="108c4-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="108c4-181">Укажите подписку, с которой вы будете работать:</span><span class="sxs-lookup"><span data-stu-id="108c4-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="108c4-182">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="108c4-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="108c4-183">Если на этом этапе вы введете `$rg`, вы должны увидеть следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="108c4-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Выходные данные после создания группы ресурсов](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="108c4-185">Создайте учетную запись хранения, которая будет использоваться для отслеживания сведений о состоянии:</span><span class="sxs-lookup"><span data-stu-id="108c4-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="108c4-186">Создайте пространство имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="108c4-186">Create the event hub namespace.</span></span> <span data-ttu-id="108c4-187">Это необходимо для создания концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="108c4-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="108c4-188">Получите идентификатор правила, который будет использоваться с поставщиком Insights:</span><span class="sxs-lookup"><span data-stu-id="108c4-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="108c4-189">Получите все возможные расположения Azure и добавьте имена в переменную, которая может использоваться в дальнейшем:</span><span class="sxs-lookup"><span data-stu-id="108c4-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="108c4-190">а.</span><span class="sxs-lookup"><span data-stu-id="108c4-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="108c4-191">b.</span><span class="sxs-lookup"><span data-stu-id="108c4-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="108c4-192">Если на этом этапе вы введете `$locations`, вы увидите имена расположений без дополнительных сведений, возвращенных командлетом Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="108c4-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="108c4-193">Создайте профиль журнала Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="108c4-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="108c4-194">Дополнительные сведения о профиле журнала Azure см. в статье [Общие сведения о журнале действий Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="108c4-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="108c4-195">При попытке создания профиля журнала может появиться сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="108c4-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="108c4-196">Затем можно просмотреть в документацию по командлетам Get-AzureRmLogProfile и Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="108c4-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="108c4-197">При запуске командлета Get-AzureRmLogProfile будут выведены сведения о профиле журнала.</span><span class="sxs-lookup"><span data-stu-id="108c4-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="108c4-198">Чтобы удалить имеющийся профиль журнала, введите команду ```Remove-AzureRmLogProfile -name 'Log Profile Name' ```.</span><span class="sxs-lookup"><span data-stu-id="108c4-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Ошибка профиля Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="108c4-200">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="108c4-200">Create a key vault</span></span>

1. <span data-ttu-id="108c4-201">Создайте хранилище ключей:</span><span class="sxs-lookup"><span data-stu-id="108c4-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="108c4-202">Настройте ведение журнала для хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="108c4-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="108c4-203">Создание действия журнала</span><span class="sxs-lookup"><span data-stu-id="108c4-203">Generate log activity</span></span>

<span data-ttu-id="108c4-204">Для создания действия журнала требуется отправка запросов в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="108c4-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="108c4-205">Действия, например создание ключей, хранение секретов или чтение секретов из Key Vault, будут создавать записи в журнале.</span><span class="sxs-lookup"><span data-stu-id="108c4-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="108c4-206">Отобразите текущие ключи хранилища:</span><span class="sxs-lookup"><span data-stu-id="108c4-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="108c4-207">Создайте ключ **key2**:</span><span class="sxs-lookup"><span data-stu-id="108c4-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="108c4-208">Отобразите ключи снова и обратите внимание, что ключ **key2** содержит другое значение:</span><span class="sxs-lookup"><span data-stu-id="108c4-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="108c4-209">Задайте и считайте секрет для создания дополнительных записей журнала:</span><span class="sxs-lookup"><span data-stu-id="108c4-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="108c4-210">а.</span><span class="sxs-lookup"><span data-stu-id="108c4-210">a.</span></span> <span data-ttu-id="108c4-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` Б.</span><span class="sxs-lookup"><span data-stu-id="108c4-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Возвращенный секрет](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="108c4-213">Настройка интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="108c4-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="108c4-214">После того как для всех необходимых элементов настроено ведение журнала Key Vault в концентраторе событий, следует настроить интеграцию журнала Azure.</span><span class="sxs-lookup"><span data-stu-id="108c4-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="108c4-215">Выполните команду AzLog для каждого концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="108c4-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="108c4-216">Приблизительно через минуту после выполнения двух последних команд вы должны увидеть созданные JSON-файлы.</span><span class="sxs-lookup"><span data-stu-id="108c4-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="108c4-217">Их наличие можно проверить в каталоге **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="108c4-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="108c4-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="108c4-218">Next steps</span></span>

- [<span data-ttu-id="108c4-219">Интеграция журналов Azure: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="108c4-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="108c4-220">Приступая к работе со службой интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="108c4-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="108c4-221">Интеграция журналов из ресурсов Azure в системы SIEM</span><span class="sxs-lookup"><span data-stu-id="108c4-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
