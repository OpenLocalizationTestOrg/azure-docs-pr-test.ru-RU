---
title: "Как восстановить сервер в базе данных Azure для MySQL | Документация Майкрософт"
description: "В этой статье описывается, как восстановить сервер в базе данных Azure для MySQL с помощью портала Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="9125b-103">Как заархивировать и восстановить сервер в базе данных Azure для MySQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="9125b-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="9125b-104">Архивация выполняется автоматически</span><span class="sxs-lookup"><span data-stu-id="9125b-104">Backup happens Automatically</span></span>
<span data-ttu-id="9125b-105">При использовании базы данных Azure для MySQL служба базы данных автоматически создает резервную копию службы каждые 5 минут.</span><span class="sxs-lookup"><span data-stu-id="9125b-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="9125b-106">Для уровня "Базовый" доступны резервные копии за 7 дней, а для уровня "Стандартный" — за 35 дней.</span><span class="sxs-lookup"><span data-stu-id="9125b-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="9125b-107">Дополнительные сведения см. в разделе [Параметры и производительность базы данных Azure для MySQL: возможности разных уровней служб](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="9125b-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="9125b-108">С помощью этой функции автоматической архивации можно восстановить сервер и все его базы данных до более ранней точки во времени на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="9125b-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="9125b-109">Восстановление на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9125b-109">Restore in the Azure portal</span></span>
<span data-ttu-id="9125b-110">База данных Azure для MySQL позволяет восстановить сервер до точки во времени и восстановить сервер в виде новой копии сервера.</span><span class="sxs-lookup"><span data-stu-id="9125b-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="9125b-111">Вы можете восстановить данные с помощью этого нового сервера.</span><span class="sxs-lookup"><span data-stu-id="9125b-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="9125b-112">Например, если таблица была случайно удалена сегодня в полдень, ее можно восстановить до момента сразу перед полуднем и получить отсутствующие таблицы и данные из новой копии сервера.</span><span class="sxs-lookup"><span data-stu-id="9125b-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="9125b-113">Указанные ниже шаги позволяют восстановить пример сервера до определенной точки во времени.</span><span class="sxs-lookup"><span data-stu-id="9125b-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="9125b-114">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9125b-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="9125b-115">Найдите сервер базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="9125b-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="9125b-116">В левой области выберите **Все ресурсы**, затем выберите свой сервер из списка.</span><span class="sxs-lookup"><span data-stu-id="9125b-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="9125b-117">В верхней части колонки "Обзор" сервера нажмите кнопку **Восстановить** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="9125b-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="9125b-118">Откроется колонка "Восстановление".</span><span class="sxs-lookup"><span data-stu-id="9125b-118">The Restore blade opens.</span></span>
<span data-ttu-id="9125b-119">![Нажатие кнопки "Восстановить"](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="9125b-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="9125b-120">Заполните форму "Восстановление", указав следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="9125b-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="9125b-121">**Точка восстановления (в формате UTС)**: с помощью управляющих элементов выбора даты и времени выберите в точку во времени для восстановления.</span><span class="sxs-lookup"><span data-stu-id="9125b-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="9125b-122">Время указывается в формате UTC, поэтому, скорее всего, потребуется преобразовать местное время в формат UTC.</span><span class="sxs-lookup"><span data-stu-id="9125b-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="9125b-123">**Восстановить на новом сервере**: введите имя целевого сервера для восстановления имеющегося сервера.</span><span class="sxs-lookup"><span data-stu-id="9125b-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="9125b-124">**Расположение**: после выбора региона автоматически заполняется значение региона исходного сервера, которое не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="9125b-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="9125b-125">**Ценовая категория**: после выбора ценовой категории для исходного сервера автоматически указывается та же ценовая категория, и здесь ее невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="9125b-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="9125b-126">![Восстановление до точки во времени](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="9125b-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="9125b-127">Чтобы восстановить сервер до выбранной точки во времени, нажмите кнопку **OК**.</span><span class="sxs-lookup"><span data-stu-id="9125b-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="9125b-128">После завершения восстановления найдите созданный сервер, чтобы убедиться, что базы данных были восстановлены, как и ожидалось.</span><span class="sxs-lookup"><span data-stu-id="9125b-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9125b-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9125b-129">Next steps</span></span>
- [<span data-ttu-id="9125b-130">Библиотеки подключений для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="9125b-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)