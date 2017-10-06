---
title: "aaaAzure образец скрипта CLI - Создание учетной записи пакетного | Документы Microsoft"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="ae893-103">Создать пакетную учетную запись с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae893-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="ae893-104">Этот сценарий создает учетную запись пакетной службы Azure и показано, как различные свойства учетной записи hello можно запрашивать и обновлены.</span><span class="sxs-lookup"><span data-stu-id="ae893-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae893-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae893-105">Prerequisites</span></span>

<span data-ttu-id="ae893-106">Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.</span><span class="sxs-lookup"><span data-stu-id="ae893-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="ae893-107">Пример скрипта учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="ae893-107">Batch account sample script</span></span>

<span data-ttu-id="ae893-108">При создании учетной записи пакетной по умолчанию ее вычислительные узлы назначения внутренне hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ae893-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="ae893-109">Выделенных вычислительных узлов будет субъекта tooa отдельное ядро квоту и может проверить подлинность учетной записи hello, или с помощью Shared Key учетные данные или Azure Active Dirctory токена.</span><span class="sxs-lookup"><span data-stu-id="ae893-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="ae893-110">Учетная запись пакетной службы с использованием примера скрипта подписки пользователя</span><span class="sxs-lookup"><span data-stu-id="ae893-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="ae893-111">Вы можете также выбрать toohave пакетного создания его вычислительных узлов в своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="ae893-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="ae893-112">Учетные записи, которые распределяют вычислительные узлы в подписке должны пройти проверку подлинности посредством маркера Azure Active Directory и hello вычислительные узлы выделенной будут приниматься Квота вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="ae893-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="ae893-113">toocreate учетную запись в этом режиме один необходимо указать ссылку хранилище ключей при создании учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="ae893-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ae893-114">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ae893-114">Clean up deployment</span></span>

<span data-ttu-id="ae893-115">После выполнения любого из hello выше примеры сценариев запуска hello, следующая команда tooremove группы ресурсов и все связанные ресурсы (включая массовых учетных записей, учетных записей хранилища Azure и Azure хранилищ ключей).</span><span class="sxs-lookup"><span data-stu-id="ae893-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ae893-116">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ae893-116">Script explanation</span></span>

<span data-ttu-id="ae893-117">Этот скрипт использует hello следующие команды toocreate группы ресурсов, пакетную учетную запись и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ae893-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="ae893-118">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="ae893-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ae893-119">Команда</span><span class="sxs-lookup"><span data-stu-id="ae893-119">Command</span></span> | <span data-ttu-id="ae893-120">Примечания</span><span class="sxs-lookup"><span data-stu-id="ae893-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ae893-121">az group create</span><span class="sxs-lookup"><span data-stu-id="ae893-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ae893-122">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ae893-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ae893-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="ae893-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="ae893-124">Создает учетную запись пакетной hello.</span><span class="sxs-lookup"><span data-stu-id="ae893-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="ae893-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="ae893-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="ae893-126">Обновляет свойства hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ae893-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="ae893-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="ae893-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="ae893-128">Извлекает сведения о hello указана учетная запись пакета.</span><span class="sxs-lookup"><span data-stu-id="ae893-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="ae893-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="ae893-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="ae893-130">Получает ключи доступа hello hello указана учетная запись пакета.</span><span class="sxs-lookup"><span data-stu-id="ae893-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="ae893-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="ae893-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="ae893-132">Подлинность hello указан пакетная учетная запись для дальнейшего взаимодействия CLI.</span><span class="sxs-lookup"><span data-stu-id="ae893-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="ae893-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="ae893-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="ae893-134">Создание учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ae893-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="ae893-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="ae893-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="ae893-136">Создает хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="ae893-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="ae893-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="ae893-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="ae893-138">Измените политику безопасности hello hello указанного ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="ae893-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="ae893-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="ae893-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="ae893-140">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="ae893-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae893-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae893-141">Next steps</span></span>

<span data-ttu-id="ae893-142">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae893-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ae893-143">Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ae893-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
