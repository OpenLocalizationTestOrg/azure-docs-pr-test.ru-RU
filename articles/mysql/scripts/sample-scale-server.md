---
title: "aaaAzure CLI образцы базы данных Azure для сервера MySQL tooscale | Документы Microsoft"
description: "Этот пример скрипта CLI масштабирует базы данных Azure для MySQL server tooa разных уровнях производительности после выполнения запроса к hello метрики."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="7c87d-103">Мониторинг и масштабирование сервера базы данных Azure для MySQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c87d-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="7c87d-104">Этот пример скрипта CLI масштабируется в одной базе данных Azure MySQL server tooa разных уровнях производительности после выполнения запроса к hello метрики.</span><span class="sxs-lookup"><span data-stu-id="7c87d-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7c87d-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7c87d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7c87d-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7c87d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7c87d-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c87d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7c87d-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="7c87d-108">Sample script</span></span>
<span data-ttu-id="7c87d-109">В этот образец скрипта измените hello выделенной строки toocustomize hello имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="7c87d-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="7c87d-110">Замените идентификатор подписки hello, используемый в командах монитор az hello своим идентификатором подписки.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="7c87d-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7c87d-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="7c87d-111">Clean up deployment</span></span>
<span data-ttu-id="7c87d-112">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="7c87d-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="7c87d-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="7c87d-113">Script explanation</span></span>
<span data-ttu-id="7c87d-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="7c87d-114">This script uses hello following commands.</span></span> <span data-ttu-id="7c87d-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="7c87d-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7c87d-116">**Команда**</span><span class="sxs-lookup"><span data-stu-id="7c87d-116">**Command**</span></span> | <span data-ttu-id="7c87d-117">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="7c87d-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="7c87d-118">az group create</span><span class="sxs-lookup"><span data-stu-id="7c87d-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="7c87d-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7c87d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c87d-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="7c87d-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="7c87d-121">Создает сервер MySQL, содержащий hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="7c87d-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="7c87d-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="7c87d-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="7c87d-123">Список hello значение метрики для hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c87d-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="7c87d-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="7c87d-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="7c87d-125">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="7c87d-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c87d-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c87d-126">Next steps</span></span>
- <span data-ttu-id="7c87d-127">Дополнительные сведения о hello Azure CLI: [документации Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c87d-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="7c87d-128">Попробуйте использовать другие скрипты на основе [примеров Azure CLI для базы данных Azure для MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7c87d-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="7c87d-129">Дополнительные сведения о масштабировании см. в статьях об [уровнях служб](../concepts-service-tiers.md) и [единицах вычислений и единицах хранения](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7c87d-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
