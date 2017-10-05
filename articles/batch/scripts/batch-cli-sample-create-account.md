---
title: "Пример скрипта Azure CLI. Создание учетной записи пакетной службы | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание учетной записи пакетной службы"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="71472-103">Создание учетной записи пакетной службы с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="71472-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="71472-104">С помощью этого скрипта создается учетная запись пакетной службы Azure. Кроме того, в нем показано, как запрашивать и обновлять различные свойства учетной записи.</span><span class="sxs-lookup"><span data-stu-id="71472-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71472-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="71472-105">Prerequisites</span></span>

<span data-ttu-id="71472-106">Установите Azure CLI с помощью инструкций, приведенных в [руководстве по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="71472-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="71472-107">Пример скрипта учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="71472-107">Batch account sample script</span></span>

<span data-ttu-id="71472-108">Когда вы создаете учетную запись пакетной службы, по умолчанию ее вычислительные узлы назначаются внутри пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="71472-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="71472-109">К выделенным вычислительным узлам будет применяться отдельная квота на ядра, и учетная запись сможет проходить проверку подлинности с помощью учетных данных общего ключа или маркера Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71472-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="71472-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Создание учетной записи")]</span><span class="sxs-lookup"><span data-stu-id="71472-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="71472-111">Учетная запись пакетной службы с использованием примера скрипта подписки пользователя</span><span class="sxs-lookup"><span data-stu-id="71472-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="71472-112">Вы также можете разрешить пакетной службе создавать вычислительные узлы в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="71472-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="71472-113">Учетные записи, которые выделяют вычислительные узлы в подписке, должны пройти проверку подлинности с помощью маркера Azure Active Directory. Тогда выделенные вычислительные узлы будут учитываться в квоте вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="71472-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="71472-114">Чтобы создать учетную запись в этом режиме, необходимо указать ссылку хранилище ключей при создании учетной записи.</span><span class="sxs-lookup"><span data-stu-id="71472-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="71472-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Создание учетной записи с помощью подписки пользователя")]</span><span class="sxs-lookup"><span data-stu-id="71472-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="71472-116">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="71472-116">Clean up deployment</span></span>

<span data-ttu-id="71472-117">После выполнения одного из примеров скриптов, приведенных выше, выполните следующую команду, чтобы удалить группу ресурсов и все связанные с ней ресурсы (включая учетные записи пакетной службы, учетные записи хранения Azure и хранилища ключей Azure).</span><span class="sxs-lookup"><span data-stu-id="71472-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="71472-118">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="71472-118">Script explanation</span></span>

<span data-ttu-id="71472-119">Для создания группы ресурсов, учетной записи пакетной службы и всех связанных с ними ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="71472-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="71472-120">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="71472-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="71472-121">Команда</span><span class="sxs-lookup"><span data-stu-id="71472-121">Command</span></span> | <span data-ttu-id="71472-122">Примечания</span><span class="sxs-lookup"><span data-stu-id="71472-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="71472-123">az group create</span><span class="sxs-lookup"><span data-stu-id="71472-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="71472-124">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="71472-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="71472-125">az batch account create</span><span class="sxs-lookup"><span data-stu-id="71472-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="71472-126">Создает учетную запись пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="71472-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="71472-127">az batch account set</span><span class="sxs-lookup"><span data-stu-id="71472-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="71472-128">Обновляет свойства учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="71472-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="71472-129">az batch account show</span><span class="sxs-lookup"><span data-stu-id="71472-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="71472-130">Получает сведения об указанной учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="71472-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="71472-131">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="71472-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="71472-132">Получает ключи доступа указанной учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="71472-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="71472-133">az batch account login</span><span class="sxs-lookup"><span data-stu-id="71472-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="71472-134">Выполняет проверку подлинности с помощью указанной учетной записи пакетной службы для дальнейшего взаимодействия с интерфейсом командной строки.</span><span class="sxs-lookup"><span data-stu-id="71472-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="71472-135">az storage account create</span><span class="sxs-lookup"><span data-stu-id="71472-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="71472-136">Создание учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="71472-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="71472-137">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="71472-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="71472-138">Создает хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="71472-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="71472-139">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="71472-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="71472-140">Обновляет политику безопасности указанного хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="71472-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="71472-141">az group delete</span><span class="sxs-lookup"><span data-stu-id="71472-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="71472-142">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="71472-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="71472-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71472-143">Next steps</span></span>

<span data-ttu-id="71472-144">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="71472-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="71472-145">Дополнительные примеры скриптов для интерфейса командной строки пакетной службы см. в [документации по интерфейсу командной строки пакетной службы Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="71472-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
