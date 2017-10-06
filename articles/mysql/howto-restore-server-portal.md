---
title: "aaaHow tooRestore сервера в базе данных Azure для MySQL | Документы Microsoft"
description: "В этой статье описывается как toorestore сервера в базе данных Azure для использования MySQL hello портал Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="a0eca-103">Здравствуйте как tooBackup и восстановления сервера в базе данных Azure для MySQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="a0eca-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="a0eca-104">Архивация выполняется автоматически</span><span class="sxs-lookup"><span data-stu-id="a0eca-104">Backup happens Automatically</span></span>
<span data-ttu-id="a0eca-105">При использовании базы данных Azure для MySQL, hello служба базы данных автоматически создает резервную копию службы hello каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="a0eca-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="a0eca-106">Hello резервные копии доступны в течение 7 дней, при использовании базового уровня и на 35 дней при использовании стандартного уровня.</span><span class="sxs-lookup"><span data-stu-id="a0eca-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="a0eca-107">Дополнительные сведения см. в разделе [Параметры и производительность базы данных Azure для MySQL: возможности разных уровней служб](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="a0eca-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="a0eca-108">С помощью этой функции автоматического резервного копирования вы можете восстановить сервер hello и все его базы данных на новый сервер tooan ранее в определенный момент.</span><span class="sxs-lookup"><span data-stu-id="a0eca-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="a0eca-109">Восстановление в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a0eca-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="a0eca-110">Базы данных Azure для MySQL позволяет toorestore hello server задней tooa точки на время и в новой копии tooa сервера hello.</span><span class="sxs-lookup"><span data-stu-id="a0eca-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="a0eca-111">Этот новый toorecover сервера можно использовать данные.</span><span class="sxs-lookup"><span data-stu-id="a0eca-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="a0eca-112">Например если таблица была случайно удалены в полдень в настоящее время можно восстановить время toohello только до полудня и получить hello отсутствует таблицы и данные из этой новой копии сервера hello.</span><span class="sxs-lookup"><span data-stu-id="a0eca-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="a0eca-113">Hello следующее моментов hello образец server tooa времени:</span><span class="sxs-lookup"><span data-stu-id="a0eca-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="a0eca-114">Вход в hello [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="a0eca-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="a0eca-115">Найдите сервер базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="a0eca-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="a0eca-116">Выберите в левой области hello **все ресурсы**, затем выберите сервер из списка hello.</span><span class="sxs-lookup"><span data-stu-id="a0eca-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="a0eca-117">Щелкните hello верхней части колонки Обзор сервера hello, **восстановить** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="a0eca-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="a0eca-118">Открывает колонку восстановления Hello.</span><span class="sxs-lookup"><span data-stu-id="a0eca-118">hello Restore blade opens.</span></span>
<span data-ttu-id="a0eca-119">![Нажатие кнопки "Восстановить"](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="a0eca-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="a0eca-120">Заполните форму восстановления hello hello необходимые сведения:</span><span class="sxs-lookup"><span data-stu-id="a0eca-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="a0eca-121">**(UTC) точку восстановления**: с помощью выбора даты hello и выбор времени выберите в момент toorestore для.</span><span class="sxs-lookup"><span data-stu-id="a0eca-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="a0eca-122">Hello указано в формате UTC, поэтому вы скорее всего, потребуется tooconvert hello местное время в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="a0eca-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="a0eca-123">**Восстановление сервера toonew**: укажите имя toorestore hello существующий сервер в новый сервер.</span><span class="sxs-lookup"><span data-stu-id="a0eca-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="a0eca-124">**Расположение**: Выбор региона hello автоматически заполняет регион сервера hello источника и не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="a0eca-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="a0eca-125">**Ценовая категория**: hello ценовой уровень выбора автоматически заполняет hello одинаковые цены уровня hello и исходный сервер и здесь нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="a0eca-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="a0eca-126">![Восстановление до точки во времени](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="a0eca-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="a0eca-127">Нажмите кнопку **ОК** toorestore hello server toorestore tooa моменту времени.</span><span class="sxs-lookup"><span data-stu-id="a0eca-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="a0eca-128">После завершения восстановления hello, найдите hello новый сервер, который был создан приветствия tooverify базы данных были восстановлены должным образом.</span><span class="sxs-lookup"><span data-stu-id="a0eca-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0eca-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0eca-129">Next steps</span></span>
- [<span data-ttu-id="a0eca-130">Библиотеки подключений для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="a0eca-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)