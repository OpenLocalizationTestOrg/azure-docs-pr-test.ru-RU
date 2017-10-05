---
title: "Примеры Azure CLI для масштабирования сервера базы данных Azure для MySQL | Документация Майкрософт"
description: "Этот пример скрипта CLI масштабирует сервер базы данных Azure для MySQL до нужного уровня производительности после выполнения запроса к метрикам."
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
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="a8663-103">Мониторинг и масштабирование сервера базы данных Azure для MySQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8663-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="a8663-104">Этот пример скрипта CLI масштабирует отдельный сервер базы данных Azure для MySQL до нужного уровня производительности после выполнения запроса к метрикам.</span><span class="sxs-lookup"><span data-stu-id="a8663-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a8663-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a8663-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a8663-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="a8663-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a8663-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8663-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a8663-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a8663-108">Sample script</span></span>
<span data-ttu-id="a8663-109">В этом примере скрипта измените выделенные строки, чтобы настроить имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="a8663-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="a8663-110">Замените идентификатор подписки, используемый в командах мониторинга az, собственным.</span><span class="sxs-lookup"><span data-stu-id="a8663-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="a8663-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Создание и масштабирование базы данных Azure для MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="a8663-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a8663-112">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="a8663-112">Clean up deployment</span></span>
<span data-ttu-id="a8663-113">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a8663-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="a8663-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Удаление группы ресурсов.")]</span><span class="sxs-lookup"><span data-stu-id="a8663-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="a8663-115">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a8663-115">Script explanation</span></span>
<span data-ttu-id="a8663-116">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="a8663-116">This script uses the following commands.</span></span> <span data-ttu-id="a8663-117">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="a8663-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a8663-118">**Команда**</span><span class="sxs-lookup"><span data-stu-id="a8663-118">**Command**</span></span> | <span data-ttu-id="a8663-119">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="a8663-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="a8663-120">az group create</span><span class="sxs-lookup"><span data-stu-id="a8663-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="a8663-121">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a8663-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a8663-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="a8663-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="a8663-123">Создает сервер MySQL, на котором размещены базы данных.</span><span class="sxs-lookup"><span data-stu-id="a8663-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="a8663-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="a8663-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="a8663-125">Выводит список значений метрики для ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8663-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="a8663-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="a8663-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="a8663-127">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="a8663-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8663-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8663-128">Next steps</span></span>
- <span data-ttu-id="a8663-129">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a8663-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="a8663-130">Попробуйте использовать другие скрипты на основе [примеров Azure CLI для базы данных Azure для MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a8663-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="a8663-131">Дополнительные сведения о масштабировании см. в статьях об [уровнях служб](../concepts-service-tiers.md) и [единицах вычислений и единицах хранения](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a8663-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
