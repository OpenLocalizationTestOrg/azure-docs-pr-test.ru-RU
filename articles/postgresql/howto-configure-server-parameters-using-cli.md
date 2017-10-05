---
title: "Настройка параметров службы в базе данных Azure для PostgreSQL | Документация Майкрософт"
description: "В этой статье описывается настройка параметров службы в базе данных Azure для PostgreSQL с помощью командной строки CLI Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="2a3f2-103">Настройка параметров конфигурации сервера с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2a3f2-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="2a3f2-104">С помощью интерфейса командной строки (Azure CLI) можно вывести список параметров конфигурации для сервера Azure PostgreSQL, а также отобразить и обновить их.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="2a3f2-105">Однако только подмножество конфигураций ядра предоставляется на уровне сервера и может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2a3f2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2a3f2-106">Prerequisites</span></span>
<span data-ttu-id="2a3f2-107">Прежде чем приступить к выполнению этого руководства, необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="2a3f2-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="2a3f2-108">[сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);</span><span class="sxs-lookup"><span data-stu-id="2a3f2-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="2a3f2-109">Установите служебную программу командной строки [Azure CLI 2.0](/cli/azure/install-azure-cli) или используйте Azure Cloud Shell в браузере.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="2a3f2-110">Получение списка параметров конфигурации сервера для базы данных Azure для сервера PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2a3f2-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="2a3f2-111">Чтобы перечислить все изменяемые параметры на сервере и их значения, выполните команду [az postgres server configuration list](/cli/azure/postgres/server/configuration#list).</span><span class="sxs-lookup"><span data-stu-id="2a3f2-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="2a3f2-112">Например, можно вывести список параметров конфигурации сервера для сервера **mypgserver-20170401.postgres.database.azure.com** в группе ресурсов **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="2a3f2-113">Отображение сведений о параметре конфигурации сервера</span><span class="sxs-lookup"><span data-stu-id="2a3f2-113">Show server configuration parameter details</span></span>
<span data-ttu-id="2a3f2-114">Чтобы отобразить сведения об определенном параметре конфигурации для сервера, выполните команду [az postgres server configuration show](/cli/azure/postgres/server/configuration#show).</span><span class="sxs-lookup"><span data-stu-id="2a3f2-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="2a3f2-115">Этот пример отображает сведения параметра конфигурации сервера **log\_min\_messages** для сервера **mypgserver-20170401.postgres.database.azure.com** в группе ресурсов **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="2a3f2-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="2a3f2-116">Изменение значения параметра конфигурации сервера</span><span class="sxs-lookup"><span data-stu-id="2a3f2-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="2a3f2-117">Вы также можете изменить значение определенного параметра конфигурации сервера. При этом обновляется базовое значение конфигурации для ядра сервера.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="2a3f2-118">Чтобы обновить конфигурацию, выполните команду [az postgres server configuration set](/cli/azure/postgres/server/configuration#set).</span><span class="sxs-lookup"><span data-stu-id="2a3f2-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="2a3f2-119">Обновите параметр конфигурации сервера **log\_min\_messages** для сервера **mypgserver-20170401.postgres.database.azure.com** в группе ресурсов **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="2a3f2-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="2a3f2-120">Если вы хотите сбросить значение параметра конфигурации, нужно просто убрать необязательный параметр `--value`, и служба применит значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="2a3f2-121">В приведенном выше примере это может выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="2a3f2-122">Данная команда восстановит значение по умолчанию **WARNING** для параметра конфигурации **log\_min\_messages**.</span><span class="sxs-lookup"><span data-stu-id="2a3f2-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="2a3f2-123">Дополнительные сведения о конфигурации сервера и допустимых значениях приведены в документации PostgreSQL по [конфигурации сервера](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="2a3f2-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a3f2-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2a3f2-124">Next steps</span></span>
- <span data-ttu-id="2a3f2-125">Чтобы настроить журналы сервера и получать к ним доступ, ознакомьтесь с разделом [Журналы сервера в базе данных Azure для PostgreSQL](concepts-server-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2a3f2-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
