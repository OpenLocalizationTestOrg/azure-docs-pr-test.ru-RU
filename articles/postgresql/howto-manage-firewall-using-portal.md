---
title: "Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью портала Azure | Документация Майкрософт"
description: "Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью портала Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="259c3-103">Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="259c3-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="259c3-104">Правила брандмауэра уровня сервера позволяют администраторам обращаться к серверу базы данных Azure для PostgreSQL с указанного IP-адреса или диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="259c3-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="259c3-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="259c3-105">Prerequisites</span></span>
<span data-ttu-id="259c3-106">Прежде чем приступить к выполнению этого руководства, необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="259c3-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="259c3-107">[сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-portal.md);</span><span class="sxs-lookup"><span data-stu-id="259c3-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="259c3-108">Создание правила брандмауэра на уровне сервера с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="259c3-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="259c3-109">В колонке сервера PostgreSQL в разделе "Параметры" щелкните **Безопасность подключения**, чтобы открыть колонку "Безопасность подключения" базы данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="259c3-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="259c3-111">Нажмите кнопку **Добавить мой IP-адрес** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="259c3-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="259c3-112">Автоматически будет создано правило с IP-адресом компьютера, определенным системой Azure.</span><span class="sxs-lookup"><span data-stu-id="259c3-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Портал Azure: нажатие кнопки "Добавить Мой IP-адрес"](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="259c3-114">Проверьте IP-адрес перед сохранением конфигурации.</span><span class="sxs-lookup"><span data-stu-id="259c3-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="259c3-115">В некоторых случаях IP-адрес, определенный порталом Azure, может отличаться от IP-адреса, используемого для доступа к Интернету и серверам Azure.</span><span class="sxs-lookup"><span data-stu-id="259c3-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="259c3-116">Поэтому может потребоваться изменить начальный IP-адрес и конечный IP-адрес для правила, чтобы оно функционировало ожидаемым образом.</span><span class="sxs-lookup"><span data-stu-id="259c3-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="259c3-117">Используйте поисковую систему или другой сетевой инструмент, чтобы проверить собственный IP-адрес (например, выполните в Bing поиск текста "what is my IP").</span><span class="sxs-lookup"><span data-stu-id="259c3-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Поиск текста "what is my IP" в Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="259c3-119">Добавьте дополнительные адресные пространства.</span><span class="sxs-lookup"><span data-stu-id="259c3-119">Add additional address ranges.</span></span> <span data-ttu-id="259c3-120">В правилах брандмауэра базы данных Azure для PostgreSQL можно указать отдельный IP-адрес или диапазон адресов.</span><span class="sxs-lookup"><span data-stu-id="259c3-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="259c3-121">Если вы хотите ограничить правило, указав отдельный IP-адрес, введите его в полях начального и конечного IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="259c3-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="259c3-122">Открыв брандмауэр, вы дадите возможность администраторам и пользователям входить в любую базу данных на сервере PostgreSQL, для которой у них есть действительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="259c3-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="259c3-123">Портал Azure: правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="259c3-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="259c3-124">На панели инструментов нажмите кнопку **Сохранить**, чтобы сохранить это правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="259c3-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="259c3-125">Дождитесь подтверждения успешного обновления правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="259c3-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Портал Azure: нажатие кнопки "Сохранить"](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="259c3-127">Управление существующими правилами брандмауэра с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="259c3-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="259c3-128">Повторите действия для управлению правилами брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="259c3-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="259c3-129">Чтобы добавить текущий компьютер, нажмите кнопку **Добавить мой IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="259c3-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="259c3-130">Щелкните **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="259c3-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="259c3-131">Чтобы добавить дополнительные IP-адреса, введите имя правила, начальный IP-адрес и конечный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="259c3-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="259c3-132">Щелкните **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="259c3-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="259c3-133">Чтобы изменить существующее правило, измените значения во всех полях в данном правиле.</span><span class="sxs-lookup"><span data-stu-id="259c3-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="259c3-134">Щелкните **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="259c3-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="259c3-135">Чтобы удалить существующее правило, щелкните многоточие [...] и выберите "Удалить".</span><span class="sxs-lookup"><span data-stu-id="259c3-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="259c3-136">Щелкните **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="259c3-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="259c3-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="259c3-137">Next steps</span></span>
- <span data-ttu-id="259c3-138">Аналогичным образом можно [создать правила брандмауэра базы данных Azure для PostgreSQL и управлять ими с помощью Azure CLI](howto-manage-firewall-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="259c3-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="259c3-139">Справка по подключению к серверу базы данных Azure для PostgreSQL доступна в разделе [Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="259c3-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
