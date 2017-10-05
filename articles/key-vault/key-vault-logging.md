---
title: "Ведение журнала хранилища ключей Azure | Документация Майкрософт"
description: "Это руководство поможет вам приступить к работе с журналами хранилища ключей Azure."
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
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="5c1bf-103">Ведение журнала хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="5c1bf-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="5c1bf-104">Хранилище ключей Azure доступно в большинстве регионов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="5c1bf-105">Дополнительные сведения см. на странице [цен на хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="5c1bf-106">Введение</span><span class="sxs-lookup"><span data-stu-id="5c1bf-106">Introduction</span></span>
<span data-ttu-id="5c1bf-107">Создав одно или несколько хранилищ ключей вы, вероятно, захотите знать, кто, как и когда осуществлял доступ к этим хранилищам.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="5c1bf-108">Это можно сделать с помощью функции ведения журнала хранилища ключей, которая сохраняет информацию в указанной учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="5c1bf-109">Для указанной учетной записи автоматически создается новый контейнер с именем **insights-logs-auditevent**. Эту же учетную запись можно использовать для сбора журналов нескольких хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="5c1bf-110">Регистрируемые в журналах сведения доступны не позже, чем через 10 минут после выполнения операции с хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="5c1bf-111">В большинстве случаев это будет еще быстрее.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="5c1bf-112">Способ управления журналами в своей учетной записи хранения вы выбираете сами.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="5c1bf-113">Используйте стандартные методы контроля доступа, предоставляемые Azure, для защиты журналов путем ограничения доступа к ним.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="5c1bf-114">Удаляйте журналы, которые больше не нужно хранить в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="5c1bf-115">Это руководство поможет вам приступить к работе с журналами хранилища ключей Azure. В нем описывается создание учетной записи хранения, включение функции ведения журналов, а также интерпретация собранных зарегистрированных сведений.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="5c1bf-116">В этом руководстве нет инструкций по созданию хранилищ ключей, ключей и секретов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="5c1bf-117">Соответствующие сведения см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="5c1bf-118">Инструкции по кроссплатформенному интерфейсу командной строки см. в [этом руководстве](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="5c1bf-119">В настоящее время нельзя настроить хранилище ключей Azure на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="5c1bf-120">Вместо этого используйте эти указания по работе с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="5c1bf-121">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="5c1bf-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c1bf-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c1bf-122">Prerequisites</span></span>
<span data-ttu-id="5c1bf-123">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5c1bf-124">Существующее хранилище ключей, которое вы используете.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="5c1bf-125">Azure PowerShell, **начиная с версии 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="5c1bf-126">Чтобы установить решение Azure PowerShell и связать его с подпиской Azure, см. статью [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5c1bf-127">Если средство Azure PowerShell у вас установлено, но вы не знаете его версию, в консоли Azure PowerShell введите `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="5c1bf-128">Достаточный объем хранилища в Azure для журналов хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="5c1bf-129"><a id="connect"></a>Подключение к подпискам</span><span class="sxs-lookup"><span data-stu-id="5c1bf-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="5c1bf-130">Запустите сеанс Azure PowerShell и войдите в учетную запись Azure, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="5c1bf-131">Во всплывающем окне браузера введите имя пользователя и пароль учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="5c1bf-132">Azure PowerShell получит все подписки, связанные с этой учетной записью, и по умолчанию будет использовать первую из них.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="5c1bf-133">Если у вас есть несколько подписок, возможно, вам нужно будет указать ту, которая использовалась для создания хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="5c1bf-134">Чтобы увидеть подписки для своей учетной записи, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="5c1bf-135">Затем укажите подписку, связанную с хранилищем ключей, данные которого будут регистрироваться. Для этого введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="5c1bf-136">Этот шаг очень важен и особенно полезен, если с учетной записью связано несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="5c1bf-137">Если вы пропустите этот шаг, то при регистрации Microsoft.Insights может появиться сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="5c1bf-138">Дополнительные сведения о настройке Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="5c1bf-139"><a id="storage"></a>Создание учетной записи хранения для журналов</span><span class="sxs-lookup"><span data-stu-id="5c1bf-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="5c1bf-140">Хотя вы можете использовать и существующую учетную запись хранения для журналов, мы создадим новую учетную запись, которая будет использоваться для сбора данных хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="5c1bf-141">Эти сведения нам нужно будет указать позже. Сейчас же для удобства работы мы сохраним их в переменной с именем **sa**.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="5c1bf-142">Чтобы упростить управление, мы также будем использовать ту же группу ресурсов, которая содержит наше хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="5c1bf-143">Согласно инструкциям из руководства [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md) эта группа ресурсов называется **ContosoResourceGroup**. Кроме того, мы будем продолжать использовать регион "Восточная Азия".</span><span class="sxs-lookup"><span data-stu-id="5c1bf-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="5c1bf-144">Замените эти значения собственными.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="5c1bf-145">Если вы планируете использовать существующую учетную запись хранения, для нее должна использоваться та же подписка, что и для хранилища ключей. Кроме того, она должна быть создана с помощью модели развертывания Resource Manager, а не классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="5c1bf-146"><a id="identify"></a>Определение хранилища ключей для журналов</span><span class="sxs-lookup"><span data-stu-id="5c1bf-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="5c1bf-147">В руководстве по началу работы мы присвоили хранилищу ключей имя **ContosoKeyVault**. Мы продолжим использовать это имя, сохранив данные в переменной с именем **kv**.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="5c1bf-148"><a id="enable"></a>Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="5c1bf-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="5c1bf-149">Мы включим ведение журналов хранилища ключей с помощью командлета Set-AzureRmDiagnosticSetting и переменных, которые мы создали для новой учетной записи хранения и хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="5c1bf-150">Мы также установим для флага **-Enabled** значение **$true** и зададим категорию AuditEvent (единственная категория для ведения журнала хранилища ключей):</span><span class="sxs-lookup"><span data-stu-id="5c1bf-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="5c1bf-151">Результат будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="5c1bf-152">Это подтверждает включение регистрации данных для хранилища ключей и сохранение этих данных в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="5c1bf-153">При необходимости можно также задать политику хранения для журналов, например политику, в соответствии с которой старые журналы будут автоматически удаляться.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="5c1bf-154">Например, задайте политику хранения, установив для флага **-RetentionEnabled** значение **$true**, а для параметра **-RetentionInDays** — значение **90**, чтобы автоматически удалять журналы, которые хранятся более 90 дней.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="5c1bf-155">Регистрируются следующие данные:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-155">What's logged:</span></span>

* <span data-ttu-id="5c1bf-156">все прошедшие проверку подлинности запросы REST API, включая запросы, ставшие неудачными из-за определенных разрешений на доступ, системных ошибок или неправильных запросов;</span><span class="sxs-lookup"><span data-stu-id="5c1bf-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="5c1bf-157">операции с хранилищем ключей, включая создание, удаление и настройку политик доступа к нему, а также обновление таких его атрибутов, как теги;</span><span class="sxs-lookup"><span data-stu-id="5c1bf-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="5c1bf-158">операции с ключами и секретами в хранилище ключей, включая создание, изменение или удаление этих ключей и секретов; операции подписания, проверки, шифрования, расшифровки, упаковки и распаковки ключей; операции получения секретов, списка ключей, а также секретов и их версий.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="5c1bf-159">непроверенные запросы, которые приводят к появлению ответа 401</span><span class="sxs-lookup"><span data-stu-id="5c1bf-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="5c1bf-160">(например, запросы без токена носителя, с недействительным токеном, а также запросы неправильного формата или просроченные запросы).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="5c1bf-161"><a id="access"></a>Доступ к журналам</span><span class="sxs-lookup"><span data-stu-id="5c1bf-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="5c1bf-162">Журналы хранилища ключей хранятся в контейнере **insights-logs-auditevent** в указанной вами учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="5c1bf-163">Чтобы получить список всех больших двоичных объектов (BLOB-объектов) в этом контейнере, введите следующее.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="5c1bf-164">Сначала создайте переменную для имени контейнера.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-164">First, create a variable for the container name.</span></span> <span data-ttu-id="5c1bf-165">Она будет использоваться для выполнения действий в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="5c1bf-166">Чтобы получить список всех больших двоичных объектов (BLOB-объектов) в этом контейнере, введите следующее.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="5c1bf-167">Вы получите приблизительно такой результат:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-167">The output will look something similar to this:</span></span>

<span data-ttu-id="5c1bf-168">**Универсальный код ресурса (URI) контейнера: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="5c1bf-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="5c1bf-169">**Имя**</span><span class="sxs-lookup"><span data-stu-id="5c1bf-169">**Name**</span></span>

- - -
<span data-ttu-id="5c1bf-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="5c1bf-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="5c1bf-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="5c1bf-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="5c1bf-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="5c1bf-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="5c1bf-173">Как видно из этих выходных данных, имена больших двоичных объектов соответствуют соглашению об именовании: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="5c1bf-174">Для значений даты и времени используется время в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-174">The date and time values use UTC.</span></span>

<span data-ttu-id="5c1bf-175">Поскольку ту же учетную запись можно использовать при сборе журналов для нескольких ресурсов, для доступа к нужным BLOB-объектам (или для их загрузки) рекомендуется использовать полный идентификатор ресурса в имени BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="5c1bf-176">Но сначала мы рассмотрим загрузку всех BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="5c1bf-177">Во-первых, создайте папку для загрузки BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="5c1bf-178">Например:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="5c1bf-179">Затем выведите список всех BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="5c1bf-180">Передайте этот список с помощью команды Get-AzureStorageBlobContent, чтобы загрузить BLOB-объекты в папку назначения.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="5c1bf-181">При выполнении второй команды разделитель **/** в именах больших двоичных объектов используется для создания полной структуры папки в конечной папке. Эта структура будет использоваться для скачивания и хранения больших двоичных объектов в виде файлов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="5c1bf-182">Для выборочной загрузки BLOB-объектов используйте подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="5c1bf-183">Например:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-183">For example:</span></span>

* <span data-ttu-id="5c1bf-184">Если у вас есть несколько хранилищ ключей, но вы хотите загрузить журналы только для одного хранилища с именем CONTOSOKEYVAULT3.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="5c1bf-185">Если у вас есть несколько групп ресурсов, но вы хотите загрузить журналы только для одной из них, используйте `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="5c1bf-186">Если вы хотите загрузить все журналы за январь 2016 г., используйте `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="5c1bf-187">Теперь можно переходить к анализу содержимого журналов.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="5c1bf-188">Но перед этим мы рассмотрим еще два дополнительных параметра для команды Get-AzureRmDiagnosticSetting:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="5c1bf-189">Запрос состояния параметров диагностики для ресурса хранилища ключей: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="5c1bf-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="5c1bf-190">Отключение ведения журнала для ресурса хранилища ключей: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="5c1bf-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="5c1bf-191"><a id="interpret"></a>Интерпретация журналов хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5c1bf-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="5c1bf-192">Отдельные BLOB-объекты хранятся как текст в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="5c1bf-193">Вот пример записи журнала после выполнения команды `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="5c1bf-194">В следующей таблице перечислены имена полей и описания.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="5c1bf-195">Имя поля</span><span class="sxs-lookup"><span data-stu-id="5c1bf-195">Field name</span></span> | <span data-ttu-id="5c1bf-196">Описание</span><span class="sxs-lookup"><span data-stu-id="5c1bf-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c1bf-197">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="5c1bf-197">time</span></span> |<span data-ttu-id="5c1bf-198">Дата и время (в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="5c1bf-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="5c1bf-199">resourceId</span></span> |<span data-ttu-id="5c1bf-200">Идентификатор ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="5c1bf-201">Для журналов хранилища ключей это всегда идентификатор ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="5c1bf-202">operationName</span><span class="sxs-lookup"><span data-stu-id="5c1bf-202">operationName</span></span> |<span data-ttu-id="5c1bf-203">Имя операции, как описано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="5c1bf-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="5c1bf-204">operationVersion</span></span> |<span data-ttu-id="5c1bf-205">Запрошенная клиентом версия REST API.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="5c1bf-206">category</span><span class="sxs-lookup"><span data-stu-id="5c1bf-206">category</span></span> |<span data-ttu-id="5c1bf-207">Для журналов хранилища ключей единственным доступным значением является AuditEvent.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="5c1bf-208">resultType</span><span class="sxs-lookup"><span data-stu-id="5c1bf-208">resultType</span></span> |<span data-ttu-id="5c1bf-209">Результат запроса REST API.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-209">Result of REST API request.</span></span> |
| <span data-ttu-id="5c1bf-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="5c1bf-210">resultSignature</span></span> |<span data-ttu-id="5c1bf-211">Состояние HTTP.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-211">HTTP status.</span></span> |
| <span data-ttu-id="5c1bf-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="5c1bf-212">resultDescription</span></span> |<span data-ttu-id="5c1bf-213">Дополнительное описание результата, если доступно.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="5c1bf-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="5c1bf-214">durationMs</span></span> |<span data-ttu-id="5c1bf-215">Время обслуживания запроса REST API в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="5c1bf-216">Сюда не входит задержка сети, поэтому время, зарегистрированное на стороне клиента, может не соответствовать этому значению.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="5c1bf-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="5c1bf-217">callerIpAddress</span></span> |<span data-ttu-id="5c1bf-218">IP-адрес клиента, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="5c1bf-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="5c1bf-219">correlationId</span></span> |<span data-ttu-id="5c1bf-220">Необязательный GUID, который клиент может передавать для сопоставления журналов на стороне клиента с журналами на стороне службы (хранилища ключей).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="5c1bf-221">identity</span><span class="sxs-lookup"><span data-stu-id="5c1bf-221">identity</span></span> |<span data-ttu-id="5c1bf-222">Удостоверение из маркера, предоставляемое при выполнении запроса REST API.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="5c1bf-223">Обычно это «пользователь», «субъект-служба» или комбинация «пользователь + идентификатор приложения» при запросе с помощью командлета Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="5c1bf-224">properties</span><span class="sxs-lookup"><span data-stu-id="5c1bf-224">properties</span></span> |<span data-ttu-id="5c1bf-225">Это поле будет содержать разные сведения об операции (operationName).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="5c1bf-226">В большинстве случаев оно содержит сведения о клиенте (передаваемая клиентом строка useragent), точный URI запроса REST API и код состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="5c1bf-227">Кроме того, когда объект возвращается в результате запроса (например, KeyCreate или VaultGet), это поле будет содержать URI ключа (как id), URI хранилища или URI секрета.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="5c1bf-228">Значения поля **operationName** отображаются в формате ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="5c1bf-229">Например:</span><span class="sxs-lookup"><span data-stu-id="5c1bf-229">For example:</span></span>

* <span data-ttu-id="5c1bf-230">Все операции с хранилищем ключей отображаются в формате Vault`<action>`, например `VaultGet` и `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="5c1bf-231">Все операции с ключами отображаются в формате Key`<action>`, например `KeySign` и `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="5c1bf-232">Все операции с секретами отображаются в формате Secret`<action>`, например `SecretGet` и `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="5c1bf-233">В следующей таблице перечислены значения operationName и соответствующие команды REST API.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="5c1bf-234">operationName</span><span class="sxs-lookup"><span data-stu-id="5c1bf-234">operationName</span></span> | <span data-ttu-id="5c1bf-235">Команда API REST</span><span class="sxs-lookup"><span data-stu-id="5c1bf-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="5c1bf-236">Authentication</span><span class="sxs-lookup"><span data-stu-id="5c1bf-236">Authentication</span></span> |<span data-ttu-id="5c1bf-237">Через конечную точку Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c1bf-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="5c1bf-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="5c1bf-238">VaultGet</span></span> |[<span data-ttu-id="5c1bf-239">Получение сведений о хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="5c1bf-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="5c1bf-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="5c1bf-240">VaultPut</span></span> |[<span data-ttu-id="5c1bf-241">Создание или обновление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5c1bf-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="5c1bf-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="5c1bf-242">VaultDelete</span></span> |[<span data-ttu-id="5c1bf-243">Удаление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5c1bf-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="5c1bf-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="5c1bf-244">VaultPatch</span></span> |[<span data-ttu-id="5c1bf-245">Update a key vault (Создание или обновление хранилища ключей)</span><span class="sxs-lookup"><span data-stu-id="5c1bf-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="5c1bf-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="5c1bf-246">VaultList</span></span> |[<span data-ttu-id="5c1bf-247">Список всех хранилищ ключей в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="5c1bf-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="5c1bf-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="5c1bf-248">KeyCreate</span></span> |[<span data-ttu-id="5c1bf-249">Создание ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="5c1bf-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="5c1bf-250">KeyGet</span></span> |[<span data-ttu-id="5c1bf-251">Получение сведений о ключе</span><span class="sxs-lookup"><span data-stu-id="5c1bf-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="5c1bf-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="5c1bf-252">KeyImport</span></span> |[<span data-ttu-id="5c1bf-253">Импорт ключа в хранилище</span><span class="sxs-lookup"><span data-stu-id="5c1bf-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="5c1bf-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="5c1bf-254">KeyBackup</span></span> |<span data-ttu-id="5c1bf-255">[Создание резервной копии ключа](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx)</span><span class="sxs-lookup"><span data-stu-id="5c1bf-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="5c1bf-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="5c1bf-256">KeyDelete</span></span> |[<span data-ttu-id="5c1bf-257">Удаление ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="5c1bf-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="5c1bf-258">KeyRestore</span></span> |[<span data-ttu-id="5c1bf-259">Восстановление ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="5c1bf-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="5c1bf-260">KeySign</span></span> |[<span data-ttu-id="5c1bf-261">Вход с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="5c1bf-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="5c1bf-262">KeyVerify</span></span> |[<span data-ttu-id="5c1bf-263">Проверка с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="5c1bf-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="5c1bf-264">KeyWrap</span></span> |[<span data-ttu-id="5c1bf-265">Перенос ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="5c1bf-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="5c1bf-266">KeyUnwrap</span></span> |[<span data-ttu-id="5c1bf-267">Развертывание ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="5c1bf-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="5c1bf-268">KeyEncrypt</span></span> |[<span data-ttu-id="5c1bf-269">Шифрование с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="5c1bf-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="5c1bf-270">KeyDecrypt</span></span> |[<span data-ttu-id="5c1bf-271">Расшифровка с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="5c1bf-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="5c1bf-272">KeyUpdate</span></span> |[<span data-ttu-id="5c1bf-273">Обновление ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="5c1bf-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="5c1bf-274">KeyList</span></span> |[<span data-ttu-id="5c1bf-275">Перечисление ключей в хранилище</span><span class="sxs-lookup"><span data-stu-id="5c1bf-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="5c1bf-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="5c1bf-276">KeyListVersions</span></span> |[<span data-ttu-id="5c1bf-277">Перечисление версий ключа</span><span class="sxs-lookup"><span data-stu-id="5c1bf-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="5c1bf-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="5c1bf-278">SecretSet</span></span> |[<span data-ttu-id="5c1bf-279">Создание секрета</span><span class="sxs-lookup"><span data-stu-id="5c1bf-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="5c1bf-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="5c1bf-280">SecretGet</span></span> |[<span data-ttu-id="5c1bf-281">Получение сведений о секрете</span><span class="sxs-lookup"><span data-stu-id="5c1bf-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="5c1bf-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="5c1bf-282">SecretUpdate</span></span> |[<span data-ttu-id="5c1bf-283">Обновление секрета</span><span class="sxs-lookup"><span data-stu-id="5c1bf-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="5c1bf-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="5c1bf-284">SecretDelete</span></span> |[<span data-ttu-id="5c1bf-285">Удаление секрета</span><span class="sxs-lookup"><span data-stu-id="5c1bf-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="5c1bf-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="5c1bf-286">SecretList</span></span> |[<span data-ttu-id="5c1bf-287">Список секретов в хранилище</span><span class="sxs-lookup"><span data-stu-id="5c1bf-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="5c1bf-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="5c1bf-288">SecretListVersions</span></span> |[<span data-ttu-id="5c1bf-289">Список версий секрета</span><span class="sxs-lookup"><span data-stu-id="5c1bf-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="5c1bf-290"><a id="loganalytics"></a>Использование Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5c1bf-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="5c1bf-291">Решение хранилища ключей Azure в Log Analytics позволяет просматривать журналы AuditEvent хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="5c1bf-292">Дополнительные сведения, включая инструкции по настройке, см. в статье [Решение Azure Key Vault Analytics в Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="5c1bf-293">В этой статье также содержатся инструкции на случай переноса из старого решения Key Vault, которое предлагалось в предварительной версии Log Analytics, где сначала требовалось направить журналы в учетную запись хранения Azure и настроить Log Analytics для чтения из этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5c1bf-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="5c1bf-294"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c1bf-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="5c1bf-295">Руководство по использованию хранилища ключей Azure в веб-приложении см. в статье [Использование хранилища ключей Azure из веб-приложения](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="5c1bf-296">Справочные материалы по программированию см. в статье [Руководство разработчика хранилища ключей Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="5c1bf-297">Полный список командлетов Azure PowerShell 1.0 для хранилища ключей Azure см. в статье [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Командлеты хранилища ключей Azure).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="5c1bf-298">Руководство по смене ключей и аудиту журналов с помощью хранилища ключей Azure см. в статье [Как настроить полную смену ключей и аудит в хранилище ключей](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="5c1bf-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
