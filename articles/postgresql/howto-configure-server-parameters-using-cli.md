---
title: "Параметры службы aaaConfigure hello в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "В этой статье описывается, как параметры службы tooconfigure hello в базе данных Azure для использования PostgreSQL hello Azure CLI командной строки."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="75f24-103">Настройка параметров конфигурации сервера с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="75f24-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="75f24-104">Можно перечислить, отображения и обновить параметры конфигурации для сервера Azure PostgreSQL, с помощью hello командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="75f24-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="75f24-105">Однако только подмножество конфигураций ядра предоставляется на уровне сервера и может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="75f24-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="75f24-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="75f24-106">Prerequisites</span></span>
<span data-ttu-id="75f24-107">toostep через этот как tooguide необходимо:</span><span class="sxs-lookup"><span data-stu-id="75f24-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="75f24-108">[сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);</span><span class="sxs-lookup"><span data-stu-id="75f24-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="75f24-109">Установка [Azure CLI 2.0](/cli/azure/install-azure-cli) командной строки программы или используйте hello оболочки облако Azure в обозревателе hello.</span><span class="sxs-lookup"><span data-stu-id="75f24-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="75f24-110">Получение списка параметров конфигурации сервера для базы данных Azure для сервера PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="75f24-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="75f24-111">Запустите все изменяемые параметры сервера и соответствующие значения toolist hello [список конфигураций сервера postgres az](/cli/azure/postgres/server/configuration#list) команды.</span><span class="sxs-lookup"><span data-stu-id="75f24-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="75f24-112">Список параметров конфигурации сервера hello hello сервера можно **mypgserver 20170401.postgres.database.azure.com** группе ресурсов **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="75f24-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="75f24-113">Отображение сведений о параметре конфигурации сервера</span><span class="sxs-lookup"><span data-stu-id="75f24-113">Show server configuration parameter details</span></span>
<span data-ttu-id="75f24-114">tooshow сведения о параметре конкретной конфигурации для сервера, запустите hello [az postgres сервера конфигурации show](/cli/azure/postgres/server/configuration#show) команды.</span><span class="sxs-lookup"><span data-stu-id="75f24-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="75f24-115">В этом примере отображаются подробные сведения об hello **журнала\_min\_сообщений** параметр конфигурации сервера для сервера **mypgserver 20170401.postgres.database.azure.com** в группе Группа ресурсов **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="75f24-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="75f24-116">Изменение значения параметра конфигурации сервера</span><span class="sxs-lookup"><span data-stu-id="75f24-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="75f24-117">Можно также изменить значение hello определенного параметра конфигурации сервера, и это обновляет hello базовое значение конфигурации для hello PostgreSQL server engine.</span><span class="sxs-lookup"><span data-stu-id="75f24-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="75f24-118">конфигурации используйте tooupdate hello hello [набор конфигурации сервера postgres az](/cli/azure/postgres/server/configuration#set) команды.</span><span class="sxs-lookup"><span data-stu-id="75f24-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="75f24-119">tooupdate hello **журнала\_min\_сообщений** параметр конфигурации сервера, сервера **mypgserver 20170401.postgres.database.azure.com** группересурсов**myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="75f24-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="75f24-120">Если требуется tooreset hello значение параметра конфигурации, нужно просто выбрать tooleave out hello необязательно `--value` параметр и hello службы будет применяться значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="75f24-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="75f24-121">В приведенном выше примере это может выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="75f24-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="75f24-122">Это приведет к сбросу hello **журнала\_min\_сообщений** по умолчанию значения конфигурации toohello **предупреждение**.</span><span class="sxs-lookup"><span data-stu-id="75f24-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="75f24-123">Дополнительные сведения о конфигурации сервера и допустимых значениях приведены в документации PostgreSQL по [конфигурации сервера](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="75f24-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75f24-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75f24-124">Next steps</span></span>
- <span data-ttu-id="75f24-125">журналы сервера tooconfigure и доступа в разделе [журналы сервера в базе данных Azure для PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="75f24-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
