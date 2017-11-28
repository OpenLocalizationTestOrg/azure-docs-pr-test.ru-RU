---
title: "Как сервер в базе данных Azure для PostgreSQL tooRestore | Документы Microsoft"
description: "В этой статье описывается как toorestore сервера в базе данных Azure для использования PostgreSQL hello портал Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="14dcf-103">Как tooBackup и восстановления сервера в базе данных Azure для использования PostgreSQL hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="14dcf-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="14dcf-104">Архивация выполняется автоматически</span><span class="sxs-lookup"><span data-stu-id="14dcf-104">Backup happens Automatically</span></span>
<span data-ttu-id="14dcf-105">При использовании базы данных Azure для PostgreSQL, hello служба базы данных автоматически создает резервную копию службы hello каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="14dcf-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="14dcf-106">Hello резервные копии доступны в течение 7 дней, при использовании базового уровня и на 35 дней при использовании стандартного уровня.</span><span class="sxs-lookup"><span data-stu-id="14dcf-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="14dcf-107">Дополнительные сведения см. в разделе [Параметры и производительность базы данных Azure для PostgreSQL: возможности разных уровней служб](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="14dcf-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="14dcf-108">С помощью этой функции автоматического резервного копирования вы можете восстановить сервер hello и все его базы данных на новый сервер tooan ранее в определенный момент.</span><span class="sxs-lookup"><span data-stu-id="14dcf-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="14dcf-109">Восстановление в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="14dcf-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="14dcf-110">Базы данных Azure для PostgreSQL позволяет toorestore hello server задней tooa точки на время и в новой копии tooa сервера hello.</span><span class="sxs-lookup"><span data-stu-id="14dcf-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="14dcf-111">Этот новый toorecover сервера можно использовать данные.</span><span class="sxs-lookup"><span data-stu-id="14dcf-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="14dcf-112">Например если таблица была случайно удалены в полдень в настоящее время можно восстановить время toohello только до полудня и получить hello отсутствует таблицы и данные из этой новой копии сервера hello.</span><span class="sxs-lookup"><span data-stu-id="14dcf-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="14dcf-113">Hello следующее моментов hello образец server tooa времени:</span><span class="sxs-lookup"><span data-stu-id="14dcf-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="14dcf-114">Вход в hello [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="14dcf-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="14dcf-115">Найдите сервер базы данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14dcf-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="14dcf-116">В hello портал Azure, щелкните **все ресурсы** из hello левого меню и введите имя hello, таких как **mypgserver 20170401**, toosearch для существующего сервера.</span><span class="sxs-lookup"><span data-stu-id="14dcf-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="14dcf-117">Щелкните имя сервера hello, перечисленные в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="14dcf-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="14dcf-118">Hello **Обзор** страница сервера открывает и предоставляет параметры для дальнейшей настройки.</span><span class="sxs-lookup"><span data-stu-id="14dcf-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Портал Azure — поиск toolocate сервера](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="14dcf-120">Щелкните hello верхней части колонки Обзор сервера hello, **восстановить** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="14dcf-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="14dcf-121">Открывает колонку восстановления Hello.</span><span class="sxs-lookup"><span data-stu-id="14dcf-121">hello Restore blade opens.</span></span>

   ![База данных Azure для PostgreSQL: колонка "Восстановление" в колонке "Обзор"](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="14dcf-123">Заполните форму восстановления hello hello необходимые сведения:</span><span class="sxs-lookup"><span data-stu-id="14dcf-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="14dcf-124">База данных Azure для PostgreSQL: информация для восстановления</span><span class="sxs-lookup"><span data-stu-id="14dcf-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="14dcf-125">**Точка восстановления**: выберите в момент, выполняемой до hello сервер был изменен</span><span class="sxs-lookup"><span data-stu-id="14dcf-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="14dcf-126">**Целевой сервер**: Введите имя нового сервера требуется toorestore для</span><span class="sxs-lookup"><span data-stu-id="14dcf-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="14dcf-127">**Расположение**: не удается выбрать область hello, по умолчанию его значение совпадает hello исходного сервера</span><span class="sxs-lookup"><span data-stu-id="14dcf-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="14dcf-128">**Ценовая категория**: это значение нельзя изменить при восстановлении сервера.</span><span class="sxs-lookup"><span data-stu-id="14dcf-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="14dcf-129">Это то же, что hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="14dcf-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="14dcf-130">Нажмите кнопку **ОК** toorestore hello server toorestore tooa моменту времени.</span><span class="sxs-lookup"><span data-stu-id="14dcf-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="14dcf-131">После завершения выполнения hello восстановления, найдите hello новый сервер, который создается приветствия tooverify восстановления данных должным образом.</span><span class="sxs-lookup"><span data-stu-id="14dcf-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14dcf-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14dcf-132">Next steps</span></span>
- [<span data-ttu-id="14dcf-133">Библиотеки подключений для базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="14dcf-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
