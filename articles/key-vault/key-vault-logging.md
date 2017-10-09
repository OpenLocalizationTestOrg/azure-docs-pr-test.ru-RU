---
title: "Ведение журнала хранилища ключей aaaAzure | Документы Microsoft"
description: "Использовать этот учебник toohelp приступить к работе с хранилищем ключей Azure ведения журнала."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="a1311-103">Ведение журнала хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="a1311-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="a1311-104">Хранилище ключей Azure доступно в большинстве регионов.</span><span class="sxs-lookup"><span data-stu-id="a1311-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="a1311-105">Дополнительные сведения см. в разделе hello [страница цен в хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="a1311-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="a1311-106">Введение</span><span class="sxs-lookup"><span data-stu-id="a1311-106">Introduction</span></span>
<span data-ttu-id="a1311-107">После создания одного или нескольких хранилищ ключей, вероятно, стоит toomonitor, как и когда хранилищ ключа доступа и кем.</span><span class="sxs-lookup"><span data-stu-id="a1311-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="a1311-108">Это можно сделать с помощью функции ведения журнала хранилища ключей, которая сохраняет информацию в указанной учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a1311-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="a1311-109">Для указанной учетной записи автоматически создается новый контейнер с именем **insights-logs-auditevent**. Эту же учетную запись можно использовать для сбора журналов нескольких хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="a1311-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="a1311-110">Данные ведения журнала доступны в журнал не чаще, 10 минут после hello ключ в хранилище операции.</span><span class="sxs-lookup"><span data-stu-id="a1311-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="a1311-111">В большинстве случаев это будет еще быстрее.</span><span class="sxs-lookup"><span data-stu-id="a1311-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="a1311-112">Он работает tooyou toomanage журналы в учетную запись хранилища:</span><span class="sxs-lookup"><span data-stu-id="a1311-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="a1311-113">Используйте журналы toosecure методы управления стандартного доступа Azure, ограничив доступ к ним.</span><span class="sxs-lookup"><span data-stu-id="a1311-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="a1311-114">Удалите журналы, которые больше не требуется tookeep вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1311-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="a1311-115">Использовать этот учебник toohelp приступить к работе с ведения журнала, хранилище ключей Azure toocreate учетной записи хранилища, включите ведение журнала и интерпретации собираемых hello ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="a1311-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="a1311-116">Этот учебник не содержит инструкций для как toocreate ключа хранилища, ключи и секретные данные.</span><span class="sxs-lookup"><span data-stu-id="a1311-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="a1311-117">Соответствующие сведения см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a1311-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="a1311-118">Инструкции по кроссплатформенному интерфейсу командной строки см. в [этом руководстве](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="a1311-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="a1311-119">В настоящее время вы не можете настроить хранилище ключей Azure hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a1311-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="a1311-120">Вместо этого используйте эти указания по работе с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1311-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="a1311-121">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a1311-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1311-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1311-122">Prerequisites</span></span>
<span data-ttu-id="a1311-123">toocomplete этого учебника необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="a1311-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a1311-124">Существующее хранилище ключей, которое вы используете.</span><span class="sxs-lookup"><span data-stu-id="a1311-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="a1311-125">Azure PowerShell, **начиная с версии 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="a1311-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="a1311-126">tooinstall Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a1311-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="a1311-127">Если вы уже установили Azure PowerShell и вы не знаете версии hello из консоли Azure PowerShell hello, введите `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="a1311-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="a1311-128">Достаточный объем хранилища в Azure для журналов хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="a1311-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="a1311-129"><a id="connect"></a>Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="a1311-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="a1311-130">Запустите сеанс Azure PowerShell и войдите в tooyour учетная запись Azure с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1311-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="a1311-131">В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль.</span><span class="sxs-lookup"><span data-stu-id="a1311-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="a1311-132">Azure PowerShell получит все подписки hello, которые связаны с этой учетной записью, а также по умолчанию, использует hello первое.</span><span class="sxs-lookup"><span data-stu-id="a1311-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="a1311-133">Если у вас несколько подписок, могут появиться toospecify одну из них, используемые toocreate вашего хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="a1311-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="a1311-134">Введите hello, следуя toosee hello подписки для учетной записи:</span><span class="sxs-lookup"><span data-stu-id="a1311-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="a1311-135">Затем toospecify hello подписки, связанной с хранилищу ключей, будет работать, тип:</span><span class="sxs-lookup"><span data-stu-id="a1311-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="a1311-136">Этот шаг очень важен и особенно полезен, если с учетной записью связано несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="a1311-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="a1311-137">Если этот шаг пропускается, может появиться ошибка tooregister помощью Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="a1311-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="a1311-138">Дополнительные сведения о настройке Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a1311-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="a1311-139"><a id="storage"></a>Создание учетной записи хранения для журналов</span><span class="sxs-lookup"><span data-stu-id="a1311-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="a1311-140">Несмотря на то, что можно использовать существующую учетную запись хранения для журналов, мы создадим новую учетную запись хранилища, выделенного tooKey хранилища журналов.</span><span class="sxs-lookup"><span data-stu-id="a1311-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="a1311-141">Для удобства работы, когда у нас есть toospecify это более поздней версии, мы будем хранить сведения hello в переменную с именем **sa**.</span><span class="sxs-lookup"><span data-stu-id="a1311-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="a1311-142">Для дополнительных легкость управления, мы также используем hello одну группу ресурсов, как hello, содержащий нашей хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="a1311-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="a1311-143">Из hello [учебник по началу работы](key-vault-get-started.md), эта группа ресурсов с именем **ContosoResourceGroup** и мы продолжим toouse hello Восточная Азия расположение.</span><span class="sxs-lookup"><span data-stu-id="a1311-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="a1311-144">Замените эти значения собственными.</span><span class="sxs-lookup"><span data-stu-id="a1311-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="a1311-145">Если вы решите toouse существующую учетную запись хранения, необходимо использовать hello той же подписке, как хранилище ключей и его необходимо использовать модель развертывания диспетчера ресурсов hello, а не hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1311-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="a1311-146"><a id="identify"></a>Определите hello хранилища ключей для журналов</span><span class="sxs-lookup"><span data-stu-id="a1311-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="a1311-147">В обучении началу работы был наш имя хранилища ключей **ContosoKeyVault**, поэтому мы продолжим, имени и сохранение сведений о hello в переменную с именем toouse **Кв**:</span><span class="sxs-lookup"><span data-stu-id="a1311-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="a1311-148"><a id="enable"></a>Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="a1311-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="a1311-149">tooenable ведения журнала для хранилища ключей, мы будем использовать hello AzureRmDiagnosticSetting набор командлетов, вместе с переменными hello мы создали для нашей новой учетной записи хранения и наши хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="a1311-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="a1311-150">Мы также настроить установим hello **-включена** флаг слишком**$true** и tooAuditEvent категории hello (hello только категория для ведения журнала хранилища ключей), задайте:</span><span class="sxs-lookup"><span data-stu-id="a1311-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="a1311-151">включает Hello выходные данные для этого:</span><span class="sxs-lookup"><span data-stu-id="a1311-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="a1311-152">Это позволит убедиться, что для хранилища ключей, сохранение сведений учетной записи хранилища tooyour теперь включено ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="a1311-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="a1311-153">При необходимости можно также задать политику хранения для журналов, например политику, в соответствии с которой старые журналы будут автоматически удаляться.</span><span class="sxs-lookup"><span data-stu-id="a1311-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="a1311-154">Например, задать политику хранения с помощью **- RetentionEnabled** флаг слишком**$true** и задайте **- RetentionInDays** параметр слишком**90** , что старше 90 дней журналы будут автоматически удалены.</span><span class="sxs-lookup"><span data-stu-id="a1311-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="a1311-155">Регистрируются следующие данные:</span><span class="sxs-lookup"><span data-stu-id="a1311-155">What's logged:</span></span>

* <span data-ttu-id="a1311-156">все прошедшие проверку подлинности запросы REST API, включая запросы, ставшие неудачными из-за определенных разрешений на доступ, системных ошибок или неправильных запросов;</span><span class="sxs-lookup"><span data-stu-id="a1311-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="a1311-157">Операции с ключом hello хранилище себя, включая создание, удаление, параметр политики доступа хранилища ключей, и теги, такие как обновление атрибутов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="a1311-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="a1311-158">Операции над ключи и секретные данные в хранилище ключей hello, включая создание, изменение или удаление эти ключи и секретные данные; операции, такие как знак, убедитесь, шифрования, расшифровки, перенос и распаковки ключей, секреты, список ключей и секреты и их версиями.</span><span class="sxs-lookup"><span data-stu-id="a1311-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="a1311-159">непроверенные запросы, которые приводят к появлению ответа 401</span><span class="sxs-lookup"><span data-stu-id="a1311-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="a1311-160">(например, запросы без токена носителя, с недействительным токеном, а также запросы неправильного формата или просроченные запросы).</span><span class="sxs-lookup"><span data-stu-id="a1311-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="a1311-161"><a id="access"></a>Доступ к журналам</span><span class="sxs-lookup"><span data-stu-id="a1311-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="a1311-162">Хранилище ключей журналы хранятся в hello **аналитики журналов auditevent** контейнера в учетной записи хранения hello, вы указали.</span><span class="sxs-lookup"><span data-stu-id="a1311-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="a1311-163">toolist все большие двоичные объекты hello в этом контейнере, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1311-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="a1311-164">Во-первых создайте переменную для имени контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="a1311-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="a1311-165">Он будет использоваться на протяжении hello остальной части пошагового hello.</span><span class="sxs-lookup"><span data-stu-id="a1311-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="a1311-166">toolist все большие двоичные объекты hello в этом контейнере, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1311-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="a1311-167">Hello результат будет выглядеть toothis что-нибудь подобное:</span><span class="sxs-lookup"><span data-stu-id="a1311-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="a1311-168">**Универсальный код ресурса (URI) контейнера: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="a1311-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="a1311-169">**Имя**</span><span class="sxs-lookup"><span data-stu-id="a1311-169">**Name**</span></span>

- - -
<span data-ttu-id="a1311-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="a1311-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="a1311-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="a1311-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="a1311-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="a1311-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="a1311-173">Как видно из этих выходных данных, hello больших двоичных объектов Следуйте соглашению об именах: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="a1311-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="a1311-174">Hello значений даты и времени используйте время UTC.</span><span class="sxs-lookup"><span data-stu-id="a1311-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="a1311-175">Так как hello учетную запись хранения может быть журналы toocollect используется для нескольких ресурсов, hello полный идентификатор ресурса в имени большого двоичного объекта hello является полезным tooaccess или загрузки только hello большие двоичные объекты, необходимые.</span><span class="sxs-lookup"><span data-stu-id="a1311-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="a1311-176">Но перед этим мы рассмотрим сначала как toodownload все hello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a1311-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="a1311-177">Создайте папку toodownload hello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a1311-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="a1311-178">Например:</span><span class="sxs-lookup"><span data-stu-id="a1311-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="a1311-179">Затем выведите список всех BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a1311-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="a1311-180">Передайте этот список при помощи «Get-AzureStorageBlobContent» toodownload hello BLOB-объектов в нашем папку назначения:</span><span class="sxs-lookup"><span data-stu-id="a1311-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="a1311-181">При выполнении этой команды второй hello  **/**  разделитель в именах blob hello создайте полный папки в папке назначения hello, и эта структура будет используется toodownload и хранилище hello большие двоичные объекты как файлы.</span><span class="sxs-lookup"><span data-stu-id="a1311-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="a1311-182">tooselectively загрузка больших двоичных объектов, использовать подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="a1311-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="a1311-183">Например:</span><span class="sxs-lookup"><span data-stu-id="a1311-183">For example:</span></span>

* <span data-ttu-id="a1311-184">Если имеется несколько хранилищ ключей и должны toodownload журналы для одной хранилища ключей, с именем CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="a1311-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="a1311-185">Если существует несколько групп ресурсов и будут toodownload журналы только одной группы ресурсов, используйте `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="a1311-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="a1311-186">Toodownload все журналы hello месяц hello: Январь 2016 г., используйте `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="a1311-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="a1311-187">Вы теперь готовы toostart, просмотрев возможности hello заносит в журнал.</span><span class="sxs-lookup"><span data-stu-id="a1311-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="a1311-188">Но до перехода, две дополнительные параметры для Get-AzureRmDiagnosticSetting, которые могут потребоваться tooknow:</span><span class="sxs-lookup"><span data-stu-id="a1311-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="a1311-189">состояние hello tooquery параметров диагностики для ресурса хранилища ключей:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="a1311-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="a1311-190">Ведение журнала toodisable для ресурса хранилища ключей:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="a1311-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="a1311-191"><a id="interpret"></a>Интерпретация журналов хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="a1311-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="a1311-192">Отдельные BLOB-объекты хранятся как текст в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="a1311-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="a1311-193">Вот пример записи журнала после выполнения команды `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="a1311-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="a1311-194">Hello следующей таблице перечислены имена полей hello и описания.</span><span class="sxs-lookup"><span data-stu-id="a1311-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="a1311-195">Имя поля</span><span class="sxs-lookup"><span data-stu-id="a1311-195">Field name</span></span> | <span data-ttu-id="a1311-196">Описание</span><span class="sxs-lookup"><span data-stu-id="a1311-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1311-197">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="a1311-197">time</span></span> |<span data-ttu-id="a1311-198">Дата и время (в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="a1311-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="a1311-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="a1311-199">resourceId</span></span> |<span data-ttu-id="a1311-200">Идентификатор ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="a1311-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="a1311-201">Для журналов хранилища ключей это значение всегда равно hello хранилище ключей, идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="a1311-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="a1311-202">operationName</span><span class="sxs-lookup"><span data-stu-id="a1311-202">operationName</span></span> |<span data-ttu-id="a1311-203">Имя операции hello, как описано в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="a1311-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="a1311-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="a1311-204">operationVersion</span></span> |<span data-ttu-id="a1311-205">Это версия интерфейса API REST hello, необходимая для клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a1311-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="a1311-206">category</span><span class="sxs-lookup"><span data-stu-id="a1311-206">category</span></span> |<span data-ttu-id="a1311-207">Для журналов хранилища ключей AuditEvent значение hello единый, доступны.</span><span class="sxs-lookup"><span data-stu-id="a1311-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="a1311-208">resultType</span><span class="sxs-lookup"><span data-stu-id="a1311-208">resultType</span></span> |<span data-ttu-id="a1311-209">Результат запроса REST API.</span><span class="sxs-lookup"><span data-stu-id="a1311-209">Result of REST API request.</span></span> |
| <span data-ttu-id="a1311-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="a1311-210">resultSignature</span></span> |<span data-ttu-id="a1311-211">Состояние HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1311-211">HTTP status.</span></span> |
| <span data-ttu-id="a1311-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="a1311-212">resultDescription</span></span> |<span data-ttu-id="a1311-213">Дополнительное описание о результате hello, если оно доступно.</span><span class="sxs-lookup"><span data-stu-id="a1311-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="a1311-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="a1311-214">durationMs</span></span> |<span data-ttu-id="a1311-215">Время, затраченное запроса REST API tooservice hello, в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="a1311-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="a1311-216">Это не включает hello задержки в сети, поэтому время hello мер на стороне клиента hello может не совпадать с этого времени.</span><span class="sxs-lookup"><span data-stu-id="a1311-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="a1311-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="a1311-217">callerIpAddress</span></span> |<span data-ttu-id="a1311-218">IP-адрес клиента hello, сделавшего запрос hello.</span><span class="sxs-lookup"><span data-stu-id="a1311-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="a1311-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="a1311-219">correlationId</span></span> |<span data-ttu-id="a1311-220">Необязательный идентификатор GUID, который hello клиента можно передать toocorrelate клиентские журналы с журналами (хранилище ключей) на стороне службы.</span><span class="sxs-lookup"><span data-stu-id="a1311-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="a1311-221">identity</span><span class="sxs-lookup"><span data-stu-id="a1311-221">identity</span></span> |<span data-ttu-id="a1311-222">Удостоверение из hello токена, который был предоставлен при выполнении запроса API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="a1311-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="a1311-223">Обычно это «пользователь», «субъект-служба» или комбинация «пользователь + идентификатор приложения» при запросе с помощью командлета Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1311-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="a1311-224">properties</span><span class="sxs-lookup"><span data-stu-id="a1311-224">properties</span></span> |<span data-ttu-id="a1311-225">Это поле будет содержать различные данные на основании hello операцию (Имя_операции).</span><span class="sxs-lookup"><span data-stu-id="a1311-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="a1311-226">В большинстве случаев содержит сведения о клиенте (hello useragent строка передается по hello клиента), hello точное URI запроса API-Интерфейс REST и код состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1311-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="a1311-227">Кроме того объект, возвращаемый в результате запроса (например, KeyCreate или VaultGet) он также содержит hello URI ключа (в виде «id»), хранилище URI или URI секрета.</span><span class="sxs-lookup"><span data-stu-id="a1311-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="a1311-228">Hello **Имя_операции** значения полей находятся в формате ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="a1311-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="a1311-229">Например:</span><span class="sxs-lookup"><span data-stu-id="a1311-229">For example:</span></span>

* <span data-ttu-id="a1311-230">Все операции хранилища ключей имеют hello "хранилище`<action>`" форматирования, такие как `VaultGet` и `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="a1311-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="a1311-231">Все операции с ключами имеют hello ' ключ`<action>`"форматирования, такие как `KeySign` и `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="a1311-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="a1311-232">Все операции с секретом имеют hello "секрет`<action>`" форматирования, такие как `SecretGet` и `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="a1311-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="a1311-233">Hello в следующей таблице перечислены Имя_операции hello и соответствующей команды REST API.</span><span class="sxs-lookup"><span data-stu-id="a1311-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="a1311-234">operationName</span><span class="sxs-lookup"><span data-stu-id="a1311-234">operationName</span></span> | <span data-ttu-id="a1311-235">Команда API REST</span><span class="sxs-lookup"><span data-stu-id="a1311-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="a1311-236">Authentication</span><span class="sxs-lookup"><span data-stu-id="a1311-236">Authentication</span></span> |<span data-ttu-id="a1311-237">Через конечную точку Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1311-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="a1311-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="a1311-238">VaultGet</span></span> |[<span data-ttu-id="a1311-239">Получение сведений о хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="a1311-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="a1311-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="a1311-240">VaultPut</span></span> |[<span data-ttu-id="a1311-241">Создание или обновление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="a1311-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="a1311-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="a1311-242">VaultDelete</span></span> |[<span data-ttu-id="a1311-243">Удаление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="a1311-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="a1311-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="a1311-244">VaultPatch</span></span> |[<span data-ttu-id="a1311-245">Update a key vault (Создание или обновление хранилища ключей)</span><span class="sxs-lookup"><span data-stu-id="a1311-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="a1311-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="a1311-246">VaultList</span></span> |[<span data-ttu-id="a1311-247">Список всех хранилищ ключей в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1311-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="a1311-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="a1311-248">KeyCreate</span></span> |[<span data-ttu-id="a1311-249">Создание ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="a1311-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="a1311-250">KeyGet</span></span> |[<span data-ttu-id="a1311-251">Получение сведений о ключе</span><span class="sxs-lookup"><span data-stu-id="a1311-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="a1311-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="a1311-252">KeyImport</span></span> |[<span data-ttu-id="a1311-253">Импорт ключа в хранилище</span><span class="sxs-lookup"><span data-stu-id="a1311-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="a1311-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="a1311-254">KeyBackup</span></span> |<span data-ttu-id="a1311-255">[Создание резервной копии ключа](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx)</span><span class="sxs-lookup"><span data-stu-id="a1311-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="a1311-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="a1311-256">KeyDelete</span></span> |[<span data-ttu-id="a1311-257">Удаление ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="a1311-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="a1311-258">KeyRestore</span></span> |[<span data-ttu-id="a1311-259">Восстановление ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="a1311-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="a1311-260">KeySign</span></span> |[<span data-ttu-id="a1311-261">Вход с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="a1311-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="a1311-262">KeyVerify</span></span> |[<span data-ttu-id="a1311-263">Проверка с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="a1311-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="a1311-264">KeyWrap</span></span> |[<span data-ttu-id="a1311-265">Перенос ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="a1311-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="a1311-266">KeyUnwrap</span></span> |[<span data-ttu-id="a1311-267">Развертывание ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="a1311-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="a1311-268">KeyEncrypt</span></span> |[<span data-ttu-id="a1311-269">Шифрование с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="a1311-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="a1311-270">KeyDecrypt</span></span> |[<span data-ttu-id="a1311-271">Расшифровка с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="a1311-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="a1311-272">KeyUpdate</span></span> |[<span data-ttu-id="a1311-273">Обновление ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="a1311-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="a1311-274">KeyList</span></span> |[<span data-ttu-id="a1311-275">Список ключей hello в хранилище</span><span class="sxs-lookup"><span data-stu-id="a1311-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="a1311-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="a1311-276">KeyListVersions</span></span> |[<span data-ttu-id="a1311-277">Список версий hello ключа</span><span class="sxs-lookup"><span data-stu-id="a1311-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="a1311-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="a1311-278">SecretSet</span></span> |[<span data-ttu-id="a1311-279">Создание секрета</span><span class="sxs-lookup"><span data-stu-id="a1311-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="a1311-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="a1311-280">SecretGet</span></span> |[<span data-ttu-id="a1311-281">Получение сведений о секрете</span><span class="sxs-lookup"><span data-stu-id="a1311-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="a1311-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="a1311-282">SecretUpdate</span></span> |[<span data-ttu-id="a1311-283">Обновление секрета</span><span class="sxs-lookup"><span data-stu-id="a1311-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="a1311-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="a1311-284">SecretDelete</span></span> |[<span data-ttu-id="a1311-285">Удаление секрета</span><span class="sxs-lookup"><span data-stu-id="a1311-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="a1311-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="a1311-286">SecretList</span></span> |[<span data-ttu-id="a1311-287">Список секретов в хранилище</span><span class="sxs-lookup"><span data-stu-id="a1311-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="a1311-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="a1311-288">SecretListVersions</span></span> |[<span data-ttu-id="a1311-289">Список версий секрета</span><span class="sxs-lookup"><span data-stu-id="a1311-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="a1311-290"><a id="loganalytics"></a>Использование Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a1311-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="a1311-291">Можно использовать решение хранилища ключей Azure hello в tooreview аналитики журналов, журналов AuditEvent хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="a1311-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="a1311-292">Дополнительные сведения, включая tooset это, см. в [решения хранилища ключей Azure в службе анализа журналов](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="a1311-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="a1311-293">В этой статье также содержит инструкции, если вам требуется toomigrate из hello старое хранилище ключей решение, предложенное во время предварительного просмотра анализа журналов hello, где сначала направляться к tooan журналы учетной записи хранилища Azure и настроены службы анализа журналов tooread оттуда.</span><span class="sxs-lookup"><span data-stu-id="a1311-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="a1311-294"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1311-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="a1311-295">Руководство по использованию хранилища ключей Azure в веб-приложении см. в статье [Использование хранилища ключей Azure из веб-приложения](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="a1311-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="a1311-296">Программирование ссылки, в разделе [hello хранилище ключей Azure в руководстве разработчика](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="a1311-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="a1311-297">Полный список командлетов Azure PowerShell 1.0 для хранилища ключей Azure см. в статье [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Командлеты хранилища ключей Azure).</span><span class="sxs-lookup"><span data-stu-id="a1311-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="a1311-298">Учебник по смены ключей и журнала аудита с хранилищем ключей Azure см. в разделе [как toosetup хранилище ключей с конечным tooend ключа аудит и поворота](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="a1311-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
