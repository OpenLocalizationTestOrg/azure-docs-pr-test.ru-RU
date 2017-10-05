---
title: "Как восстановить сервер в базе данных Azure для PostgreSQL | Документация Майкрософт"
description: "В этой статье описывается, как восстановить сервер в базе данных Azure для PostgreSQL с помощью портала Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="d6f92-103">Как заархивировать и восстановить сервер в базе данных Azure для PostgreSQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="d6f92-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="d6f92-104">Архивация выполняется автоматически</span><span class="sxs-lookup"><span data-stu-id="d6f92-104">Backup happens Automatically</span></span>
<span data-ttu-id="d6f92-105">При использовании базы данных Azure для PostgreSQL служба базы данных автоматически создает резервную копию службы каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="d6f92-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="d6f92-106">Для уровня "Базовый" доступны резервные копии за 7 дней, а для уровня "Стандартный" — за 35 дней.</span><span class="sxs-lookup"><span data-stu-id="d6f92-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="d6f92-107">Дополнительные сведения см. в разделе [Параметры и производительность базы данных Azure для PostgreSQL: возможности разных уровней служб](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="d6f92-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="d6f92-108">С помощью этой функции автоматической архивации можно восстановить сервер и все его базы данных до более ранней точки во времени на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="d6f92-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="d6f92-109">Восстановление на портале Azure</span><span class="sxs-lookup"><span data-stu-id="d6f92-109">Restore in the Azure portal</span></span>
<span data-ttu-id="d6f92-110">База данных Azure для PostgreSQL позволяет восстановить сервер до точки во времени и восстановить сервер в виде новой копии сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f92-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="d6f92-111">Вы можете восстановить данные с помощью этого нового сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f92-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="d6f92-112">Например, если таблица была случайно удалена сегодня в полдень, ее можно восстановить до момента сразу перед полуднем и получить отсутствующие таблицы и данные из новой копии сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f92-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="d6f92-113">Указанные ниже шаги позволяют восстановить пример сервера до определенной точки во времени.</span><span class="sxs-lookup"><span data-stu-id="d6f92-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="d6f92-114">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6f92-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="d6f92-115">Найдите сервер базы данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d6f92-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="d6f92-116">На портале Azure щелкните **Все ресурсы** в меню слева и введите имя, например **mypgserver-20170401**, чтобы найти существующий сервер.</span><span class="sxs-lookup"><span data-stu-id="d6f92-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="d6f92-117">Щелкните имя сервера в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="d6f92-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="d6f92-118">После этого откроется страница **Обзор** сервера с параметрами для дальнейшей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6f92-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Портал Azure: поиск сервера](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="d6f92-120">В верхней части колонки "Обзор" сервера нажмите кнопку **Восстановить** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="d6f92-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="d6f92-121">Откроется колонка "Восстановление".</span><span class="sxs-lookup"><span data-stu-id="d6f92-121">The Restore blade opens.</span></span>

   ![База данных Azure для PostgreSQL: колонка "Восстановление" в колонке "Обзор"](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="d6f92-123">Заполните форму "Восстановление", указав следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="d6f92-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="d6f92-124">База данных Azure для PostgreSQL: информация для восстановления</span><span class="sxs-lookup"><span data-stu-id="d6f92-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="d6f92-125">**Точка восстановления**: выберите время до того момента, когда был изменен сервер.</span><span class="sxs-lookup"><span data-stu-id="d6f92-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="d6f92-126">**Целевой сервер**: укажите новое имя сервера, который нужно восстановить.</span><span class="sxs-lookup"><span data-stu-id="d6f92-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="d6f92-127">**Расположение**: вы не сможете выбрать регион, по умолчанию он совпадает с регионом исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f92-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="d6f92-128">**Ценовая категория**: это значение нельзя изменить при восстановлении сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f92-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="d6f92-129">Она совпадает с ценовой категорией исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="d6f92-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="d6f92-130">Чтобы восстановить сервер до выбранной точки во времени, нажмите кнопку **OК**.</span><span class="sxs-lookup"><span data-stu-id="d6f92-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="d6f92-131">После завершения восстановления найдите созданный сервер, чтобы убедиться, что данные были восстановлены, как и ожидалось.</span><span class="sxs-lookup"><span data-stu-id="d6f92-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6f92-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6f92-132">Next steps</span></span>
- [<span data-ttu-id="d6f92-133">Библиотеки подключений для базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d6f92-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
