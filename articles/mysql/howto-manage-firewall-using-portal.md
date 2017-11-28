---
title: "Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью портала Azure | Документация Майкрософт"
description: "Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью портала Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="779b8-103">Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="779b8-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="779b8-104">Правила брандмауэра уровня сервера позволяют администраторам обращаться к серверу базы данных Azure для MySQL с указанного IP-адреса или диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="779b8-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="779b8-105">Создание правила брандмауэра на уровне сервера с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="779b8-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="779b8-106">В колонке сервера MySQL в разделе "Параметры" щелкните **Безопасность подключения**, чтобы открыть колонку "Безопасность подключения" базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="779b8-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Портал Azure: щелчок пункта "Безопасность подключения"](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="779b8-108">Щелкните на панели инструментов **Добавить мой IP-адрес**, чтобы создать правило с IP-адресом компьютера, определенным системой Azure.</span><span class="sxs-lookup"><span data-stu-id="779b8-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Портал Azure: нажатие кнопки "Добавить Мой IP-адрес"](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="779b8-110">Проверьте IP-адрес перед сохранением конфигурации.</span><span class="sxs-lookup"><span data-stu-id="779b8-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="779b8-111">В некоторых случаях IP-адрес, определенный порталом Azure, может отличаться от IP-адреса, используемого для доступа к Интернету и серверам Azure.</span><span class="sxs-lookup"><span data-stu-id="779b8-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="779b8-112">Поэтому может потребоваться изменить начальный IP-адрес и конечный IP-адрес для правила, чтобы оно функционировало ожидаемым образом.</span><span class="sxs-lookup"><span data-stu-id="779b8-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="779b8-113">Используйте поисковую систему или другой сетевой инструмент, чтобы проверить собственный IP-адрес (например, выполните поиск текста "what is my IP").</span><span class="sxs-lookup"><span data-stu-id="779b8-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Поиск текста what is my IP в Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="779b8-115">Добавьте дополнительные адресные пространства.</span><span class="sxs-lookup"><span data-stu-id="779b8-115">Add additional address ranges.</span></span> <span data-ttu-id="779b8-116">В правилах брандмауэра базы данных Azure для MySQL можно указать отдельный IP-адрес или диапазон адресов.</span><span class="sxs-lookup"><span data-stu-id="779b8-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="779b8-117">Если вы хотите ограничить правило, указав отдельный IP-адрес, введите его в полях начального и конечного IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="779b8-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="779b8-118">Открытие брандмауэра позволит администраторам и пользователям входить в любую базу данных на сервере MySQL, для которой у них есть действительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="779b8-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="779b8-119">Портал Azure: правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="779b8-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="779b8-120">На панели инструментов нажмите кнопку **Сохранить**, чтобы сохранить это правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="779b8-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="779b8-121">Дождитесь подтверждения успешного обновления правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="779b8-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Портал Azure: нажатие кнопки "Сохранить"](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="779b8-123">Управление существующими правилами брандмауэра с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="779b8-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="779b8-124">Повторите действия для управлению правилами брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="779b8-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="779b8-125">Чтобы добавить текущий компьютер, нажмите кнопку **Добавить мой IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="779b8-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="779b8-126">Чтобы добавить дополнительные IP-адреса, введите **имя правила**, **начальный IP-адрес** и **конечный IP-адрес** в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="779b8-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="779b8-127">Чтобы изменить существующее правило, измените значения во всех полях в данном правиле.</span><span class="sxs-lookup"><span data-stu-id="779b8-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="779b8-128">Чтобы удалить существующее правило, щелкните многоточие [...] и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="779b8-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="779b8-129">Щелкните **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="779b8-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="779b8-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="779b8-130">Next steps</span></span>
- <span data-ttu-id="779b8-131">Справка по подключению к серверу базы данных Azure для MySQL доступна в разделе [Библиотеки подключений для базы данных Azure для MySQL](./concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="779b8-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
