---
title: "aaaCreate и управления базой данных Azure для MySQL правила брандмауэра, с помощью hello портал Azure | Документы Microsoft"
description: "Создание и управление для MySQL правила брандмауэра, с помощью портала Azure hello базы данных Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="fc462-103">Создание и управление для MySQL правила брандмауэра, с помощью портала Azure hello базы данных Azure</span><span class="sxs-lookup"><span data-stu-id="fc462-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="fc462-104">Правила брандмауэра уровня сервера включите tooaccess администраторы базы данных Azure для сервера MySQL из указанный IP-адрес или диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="fc462-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="fc462-105">Создание правила брандмауэра уровня сервера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="fc462-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="fc462-106">В колонке сервера MySQL hello в разделе Параметры щелкните **безопасности подключения** tooopen hello безопасности подключения колонке hello базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="fc462-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="fc462-108">Нажмите кнопку **добавить Мой IP** на toocreate инструментов hello правило с hello IP-адрес компьютера, с точки зрения hello системы Azure.</span><span class="sxs-lookup"><span data-stu-id="fc462-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Портал Azure: нажатие кнопки "Добавить Мой IP-адрес"](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="fc462-110">Проверьте свой IP-адрес перед сохранением конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="fc462-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="fc462-111">В некоторых ситуациях hello IP-адрес, наблюдается порталом Azure отличается от hello IP-адрес используется при доступе к hello Интернета и серверы Azure.</span><span class="sxs-lookup"><span data-stu-id="fc462-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="fc462-112">Таким образом может потребоваться toochange hello начальный IP- и конечный IP-toomake правило функции hello должным образом.</span><span class="sxs-lookup"><span data-stu-id="fc462-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="fc462-113">Используйте поисковую систему или другие интерактивное средство toocheck IP-адреса (например, выполните поиск «what is my IP-адрес»).</span><span class="sxs-lookup"><span data-stu-id="fc462-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Поиск текста what is my IP в Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="fc462-115">Добавьте дополнительные адресные пространства.</span><span class="sxs-lookup"><span data-stu-id="fc462-115">Add additional address ranges.</span></span> <span data-ttu-id="fc462-116">В правилах hello для hello базы данных Azure для MySQL брандмауэра можно указать один IP-адрес или диапазон адресов.</span><span class="sxs-lookup"><span data-stu-id="fc462-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="fc462-117">Если вы хотите toolimit hello правило tooone один IP-адрес, тип hello же адрес в поле hello начальный IP- и конечный IP.</span><span class="sxs-lookup"><span data-stu-id="fc462-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="fc462-118">Открытие брандмауэра hello позволяет Администраторы и пользователи tooaccess любой базы данных на hello toowhich MySQL server, они имеют допустимые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fc462-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="fc462-119">Портал Azure: правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="fc462-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="fc462-120">Нажмите кнопку **Сохранить** на hello инструментов toosave этого правила брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="fc462-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="fc462-121">Дождитесь подтверждения hello, правила брандмауэра toohello hello обновления успешно.</span><span class="sxs-lookup"><span data-stu-id="fc462-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Портал Azure: нажатие кнопки "Сохранить"](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="fc462-123">Управлять существующими правилами брандмауэра уровня сервера через портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="fc462-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="fc462-124">Повторите шаги toomanage hello hello-правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="fc462-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="fc462-125">tooadd hello данного компьютера, нажмите кнопку **+ добавить Мой IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="fc462-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="fc462-126">tooadd дополнительные IP-адреса, введите в hello **имя ПРАВИЛА**, **НАЧАЛЬНЫЙ IP-**, и **конечным IP**.</span><span class="sxs-lookup"><span data-stu-id="fc462-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="fc462-127">toomodify существующее правило, щелкните любое из полей правила hello hello и изменения.</span><span class="sxs-lookup"><span data-stu-id="fc462-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="fc462-128">правило toodelete существующего, нажмите кнопку с многоточием hello [...] и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="fc462-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="fc462-129">Нажмите кнопку **Сохранить** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="fc462-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc462-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc462-130">Next steps</span></span>
- <span data-ttu-id="fc462-131">Справку в подключении tooan базы данных Azure для MySQL server в разделе [библиотеки подключений к базе данных Azure для MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="fc462-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
