---
title: "aaaCreate и управления базой данных Azure для правила брандмауэра PostgreSQL, с помощью hello портал Azure | Документы Microsoft"
description: "Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="671ca-103">Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure</span><span class="sxs-lookup"><span data-stu-id="671ca-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="671ca-104">Правила брандмауэра уровня сервера включите tooaccess администраторы базы данных Azure для сервера PostgreSQL указанный IP-адрес или диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="671ca-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="671ca-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="671ca-105">Prerequisites</span></span>
<span data-ttu-id="671ca-106">toostep через этот как tooguide необходимо:</span><span class="sxs-lookup"><span data-stu-id="671ca-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="671ca-107">[сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-portal.md);</span><span class="sxs-lookup"><span data-stu-id="671ca-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="671ca-108">Создание правила брандмауэра уровня сервера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="671ca-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="671ca-109">В колонке сервера PostgreSQL hello в разделе Параметры щелкните **безопасности подключения** tooopen hello безопасности подключения колонке базы данных Azure для PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="671ca-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="671ca-111">Нажмите кнопку **добавить Мой IP** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="671ca-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="671ca-112">Это правило автоматически создаст hello IP-адрес компьютера, воспринимаемое, hello системы Azure.</span><span class="sxs-lookup"><span data-stu-id="671ca-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Портал Azure: нажатие кнопки "Добавить Мой IP-адрес"](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="671ca-114">Проверьте свой IP-адрес перед сохранением конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="671ca-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="671ca-115">В некоторых ситуациях hello IP-адрес, наблюдается порталом Azure отличается от hello IP-адрес используется при доступе к hello Интернета и серверы Azure.</span><span class="sxs-lookup"><span data-stu-id="671ca-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="671ca-116">Таким образом может потребоваться toochange hello начальный IP- и конечный IP-toomake правило функции hello должным образом.</span><span class="sxs-lookup"><span data-stu-id="671ca-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="671ca-117">Используйте поисковую систему или другие toocheck интерактивное средство собственный IP-адрес (например, поиск Bing «what is my IP»).</span><span class="sxs-lookup"><span data-stu-id="671ca-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Поиск текста "what is my IP" в Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="671ca-119">Добавьте дополнительные адресные пространства.</span><span class="sxs-lookup"><span data-stu-id="671ca-119">Add additional address ranges.</span></span> <span data-ttu-id="671ca-120">В правилах hello для hello базы данных Azure для брандмауэра PostgreSQL можно указать один IP-адрес или диапазон адресов.</span><span class="sxs-lookup"><span data-stu-id="671ca-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="671ca-121">Если вы хотите toolimit hello правило tooone один IP-адрес, тип hello же адрес в поле hello начальный IP- и конечный IP.</span><span class="sxs-lookup"><span data-stu-id="671ca-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="671ca-122">Открытие брандмауэра hello включает Администраторы и пользователи базу tooany toologin на hello toowhich сервера PostgreSQL, они имеют допустимые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="671ca-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="671ca-123">Портал Azure: правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="671ca-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="671ca-124">Нажмите кнопку **Сохранить** на hello инструментов toosave этого правила брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="671ca-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="671ca-125">Дождитесь подтверждения hello, правила брандмауэра toohello hello обновления успешно.</span><span class="sxs-lookup"><span data-stu-id="671ca-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Портал Azure: нажатие кнопки "Сохранить"](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="671ca-127">Управлять существующими правилами брандмауэра уровня сервера через портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="671ca-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="671ca-128">Повторите шаги toomanage hello hello-правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="671ca-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="671ca-129">tooadd hello данного компьютера, нажмите кнопку hello слишком + **добавить Мой IP**.</span><span class="sxs-lookup"><span data-stu-id="671ca-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="671ca-130">Нажмите кнопку **Сохранить** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="671ca-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="671ca-131">tooadd дополнительные IP-адреса, введите в hello имя правила, начальный IP-адрес и конечный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="671ca-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="671ca-132">Нажмите кнопку **Сохранить** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="671ca-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="671ca-133">toomodify существующее правило, щелкните любое из полей правила hello hello и изменения.</span><span class="sxs-lookup"><span data-stu-id="671ca-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="671ca-134">Нажмите кнопку **Сохранить** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="671ca-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="671ca-135">toodelete существующее правило, нажмите кнопку с многоточием hello [...] и щелкните Delete Удаление hello правило.</span><span class="sxs-lookup"><span data-stu-id="671ca-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="671ca-136">Нажмите кнопку **Сохранить** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="671ca-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="671ca-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="671ca-137">Next steps</span></span>
- <span data-ttu-id="671ca-138">Аналогичным образом, можно создать скрипт слишком[Создание и управление базы данных Azure для правила брандмауэра PostgreSQL, с помощью Azure CLI](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="671ca-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="671ca-139">Справку в подключении tooan базы данных Azure для сервера PostgreSQL см [библиотеки подключений к базе данных Azure для PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="671ca-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
