---
title: "Как tooback копировании и восстановлении сервера базы данных Azure для PostgreSQL | Документы Microsoft"
description: "Узнайте, как tooback копирование и восстановление сервера в базе данных Azure для PostgreSQL с помощью hello Azure CLI."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="aeb69-103">Здравствуйте как tooback копирование и восстановление сервера в базе данных Azure для PostgreSQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aeb69-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="aeb69-104">Использование базы данных Azure для PostgreSQL toorestore tooan сервера базы данных более ранней даты, охватывающий 7 дней too35.</span><span class="sxs-lookup"><span data-stu-id="aeb69-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aeb69-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aeb69-105">Prerequisites</span></span>
<span data-ttu-id="aeb69-106">toocomplete как tooguide, необходимо:</span><span class="sxs-lookup"><span data-stu-id="aeb69-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="aeb69-107">[сервер и база данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);</span><span class="sxs-lookup"><span data-stu-id="aeb69-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="aeb69-108">Если установить и использовать hello Azure CLI локально, это как tooguide требует использования Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="aeb69-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aeb69-109">версия tooconfirm hello, hello Azure CLI командной строки, введите `az --version`.</span><span class="sxs-lookup"><span data-stu-id="aeb69-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="aeb69-110">tooinstall или обновления, см. в [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aeb69-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="aeb69-111">Резервное копирование выполняется автоматически</span><span class="sxs-lookup"><span data-stu-id="aeb69-111">Back up happens automatically</span></span>
<span data-ttu-id="aeb69-112">При использовании базы данных Azure для PostgreSQL hello служба базы данных автоматически создает резервную копию службы hello каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="aeb69-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="aeb69-113">Для базового уровня hello резервные копии доступны в течение 7 дней.</span><span class="sxs-lookup"><span data-stu-id="aeb69-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="aeb69-114">Для уровня Standard hello доступны архивы 35 дней.</span><span class="sxs-lookup"><span data-stu-id="aeb69-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="aeb69-115">Дополнительные сведения см. в статье [Параметры и производительность базы данных Azure для PostgreSQL: возможности, доступные в каждой ценовой категории](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="aeb69-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="aeb69-116">Благодаря этому автоматического резервного копирования восстановления сервера hello и его tooan баз данных более ранней датой или на определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="aeb69-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="aeb69-117">Восстановление базы данных предыдущей точки tooa времени с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aeb69-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="aeb69-118">Использование базы данных Azure для PostgreSQL toorestore hello server tooa предыдущий момент времени.</span><span class="sxs-lookup"><span data-stu-id="aeb69-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="aeb69-119">Hello восстановить данные копируются tooa новый сервер, и существующий сервер hello оставляется.</span><span class="sxs-lookup"><span data-stu-id="aeb69-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="aeb69-120">Например если таблица случайно удалена в полдень сегодня, можно восстановить время toohello только до полудня.</span><span class="sxs-lookup"><span data-stu-id="aeb69-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="aeb69-121">Затем можно получить hello отсутствует таблицы и данные из копии восстановить hello hello server.</span><span class="sxs-lookup"><span data-stu-id="aeb69-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="aeb69-122">toorestore hello server, используйте hello Azure CLI [восстановление server postgres az](/cli/azure/postgres/server#restore) команды.</span><span class="sxs-lookup"><span data-stu-id="aeb69-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="aeb69-123">Выполните команду restore hello</span><span class="sxs-lookup"><span data-stu-id="aeb69-123">Run hello restore command</span></span>

<span data-ttu-id="aeb69-124">сервер hello toorestore, hello Azure CLI командной строки, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="aeb69-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="aeb69-125">Hello `az postgres server restore` команды необходим hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="aeb69-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="aeb69-126">Настройка</span><span class="sxs-lookup"><span data-stu-id="aeb69-126">Setting</span></span> | <span data-ttu-id="aeb69-127">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="aeb69-127">Suggested value</span></span> | <span data-ttu-id="aeb69-128">Описание</span><span class="sxs-lookup"><span data-stu-id="aeb69-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="aeb69-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="aeb69-129">resource-group</span></span> |  <span data-ttu-id="aeb69-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="aeb69-130">myResourceGroup</span></span> |  <span data-ttu-id="aeb69-131">Группа ресурсов, где существует hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="aeb69-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="aeb69-132">name</span><span class="sxs-lookup"><span data-stu-id="aeb69-132">name</span></span> | <span data-ttu-id="aeb69-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="aeb69-133">mypgserver-restored</span></span> | <span data-ttu-id="aeb69-134">Имя Hello hello новый сервер, созданный команды restore hello.</span><span class="sxs-lookup"><span data-stu-id="aeb69-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="aeb69-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="aeb69-135">restore-point-in-time</span></span> | <span data-ttu-id="aeb69-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="aeb69-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="aeb69-137">Выберите конкретное время toorestore для.</span><span class="sxs-lookup"><span data-stu-id="aeb69-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="aeb69-138">Дата и время должны находиться в hello исходного сервера резервное копирование срока хранения.</span><span class="sxs-lookup"><span data-stu-id="aeb69-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="aeb69-139">Использование формата hello ISO8601 даты и времени.</span><span class="sxs-lookup"><span data-stu-id="aeb69-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="aeb69-140">Можно использовать местный часовой пояс, например `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="aeb69-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="aeb69-141">Можно также использовать hello, формат UTC Zulu, например, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="aeb69-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="aeb69-142">source-server</span><span class="sxs-lookup"><span data-stu-id="aeb69-142">source-server</span></span> | <span data-ttu-id="aeb69-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="aeb69-143">mypgserver-20170401</span></span> | <span data-ttu-id="aeb69-144">Hello имя или идентификатор hello исходного сервера toorestore из.</span><span class="sxs-lookup"><span data-stu-id="aeb69-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="aeb69-145">При восстановлении tooan сервера более раннего момента времени, создается новый сервер.</span><span class="sxs-lookup"><span data-stu-id="aeb69-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="aeb69-146">Hello исходного сервера и баз данных из hello указанные точки во времени, скопированный toohello новый сервер.</span><span class="sxs-lookup"><span data-stu-id="aeb69-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="aeb69-147">значения уровня место и ценах Hello для сервера восстановления hello оставаться hello таким же как hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="aeb69-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="aeb69-148">Hello `az postgres server restore` команда является синхронным.</span><span class="sxs-lookup"><span data-stu-id="aeb69-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="aeb69-149">После восстановления сервера hello вы можно использовать снова toorepeat hello процесс для другой момент времени.</span><span class="sxs-lookup"><span data-stu-id="aeb69-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="aeb69-150">После hello завершения процесса восстановления, найдите новый сервер hello и убедитесь, что hello данные восстанавливаются должным образом.</span><span class="sxs-lookup"><span data-stu-id="aeb69-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb69-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aeb69-151">Next steps</span></span>
[<span data-ttu-id="aeb69-152">Библиотеки подключений для базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="aeb69-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
