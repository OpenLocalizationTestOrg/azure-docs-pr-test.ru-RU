---
title: "Правила брандмауэра сервера базы данных Azure для MySQL | Документация Майкрософт"
description: "Описываются правила брандмауэра сервера базы данных Azure для MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 7456cef7a5da665ee3d70df64265b8186a79f9b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a><span data-ttu-id="320b3-103">Правила брандмауэра сервера базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="320b3-103">Azure Database for MySQL server firewall rules</span></span>
<span data-ttu-id="320b3-104">Брандмауэр запрещает любой доступ к серверу базы данных, пока вы не укажете компьютеры, у которых есть разрешение на доступ.</span><span class="sxs-lookup"><span data-stu-id="320b3-104">Firewalls prevent all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="320b3-105">Брандмауэр предоставляет доступ к серверу на основе исходного IP-адреса каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="320b3-105">The firewall grants access to the server based on the originating IP address of each request.</span></span>

<span data-ttu-id="320b3-106">Для настройки брандмауэра можно создать правила брандмауэра, которые указывают диапазон допустимых IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="320b3-106">To configure your firewall, you create firewall rules that specify ranges of acceptable IP addresses.</span></span> <span data-ttu-id="320b3-107">Правила брандмауэра можно создавать на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="320b3-107">You can create firewall rules at the server level.</span></span>

<span data-ttu-id="320b3-108">**Правила брандмауэра:** эти правила разрешают клиентам доступ ко всему серверу базы данных Azure для MySQL, то есть ко всем базам данных на одном логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="320b3-108">**Firewall rules:** These rules enable clients to access your entire Azure Database for MySQL server, that is, all the databases within the same logical server.</span></span> <span data-ttu-id="320b3-109">Правила брандмауэра уровня сервера можно настроить на портале Azure или с помощью команд Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="320b3-109">Server-level firewall rules can be configured by using the Azure portal or using Azure CLI commands.</span></span> <span data-ttu-id="320b3-110">Для создания правил брандмауэра уровня сервера необходимо быть владельцем или участником подписки.</span><span class="sxs-lookup"><span data-stu-id="320b3-110">To create server-level firewall rules, you must be the subscription owner or a subscription contributor.</span></span>

## <a name="firewall-overview"></a><span data-ttu-id="320b3-111">Общие сведения о брандмауэре</span><span class="sxs-lookup"><span data-stu-id="320b3-111">Firewall overview</span></span>
<span data-ttu-id="320b3-112">По умолчанию весь доступ к базам данных на сервере базы данных Azure для MySQL блокируется брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="320b3-112">All database access to your Azure Database for MySQL server is blocked by the firewall by default.</span></span> <span data-ttu-id="320b3-113">Чтобы использовать сервер с другого компьютера, сначала необходимо указать одно или несколько правил брандмауэра уровня сервера для обеспечения доступа к этому серверу.</span><span class="sxs-lookup"><span data-stu-id="320b3-113">To begin using your server from another computer, you need to specify one or more server-level firewall rules to enable access to your server.</span></span> <span data-ttu-id="320b3-114">Используйте правила брандмауэра, чтобы определить разрешенные диапазоны IP-адресов из Интернета.</span><span class="sxs-lookup"><span data-stu-id="320b3-114">Use the firewall rules to specify which IP address ranges from the Internet to allow.</span></span> <span data-ttu-id="320b3-115">Правила брандмауэра не повлияют на доступ к самому веб-сайту портала Azure.</span><span class="sxs-lookup"><span data-stu-id="320b3-115">Access to the Azure portal website itself is not impacted by the firewall rules.</span></span>

<span data-ttu-id="320b3-116">Запросы на подключение из Интернета и Azure должны сначала обрабатываться брандмауэром и только потом достигать базы данных Azure для MySQL, как показано на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="320b3-116">Connection attempts from the Internet and Azure must first pass through the firewall before they can reach your Azure Database for MySQL database, as shown in the following diagram:</span></span>

![Пример рабочего потока брандмауэра](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a><span data-ttu-id="320b3-118">Подключение через Интернет</span><span class="sxs-lookup"><span data-stu-id="320b3-118">Connecting from the Internet</span></span>
<span data-ttu-id="320b3-119">Правила брандмауэра уровня сервера применяются ко всем базам данных на сервере базы данных Azure для MySQL.</span><span class="sxs-lookup"><span data-stu-id="320b3-119">Server-level firewall rules apply to all databases on the Azure Database for MySQL server.</span></span>

<span data-ttu-id="320b3-120">Если IP-адрес запроса находится в одном из диапазонов, указанных в правилах брандмауэра уровня сервера, подключение предоставляется.</span><span class="sxs-lookup"><span data-stu-id="320b3-120">If the IP address of the request is within one of the ranges specified in the server-level firewall rules, the connection is granted.</span></span>

<span data-ttu-id="320b3-121">Если IP-адрес запроса находится за пределами диапазонов, указанных в любом из правил брандмауэра уровня базы данных или уровня сервера, то запрос на подключение отклоняется.</span><span class="sxs-lookup"><span data-stu-id="320b3-121">If the IP address of the request is not within the ranges specified in any of the database-level or server-level firewall rules, the connection request fails.</span></span>

## <a name="programmatically-managing-firewall-rules"></a><span data-ttu-id="320b3-122">Программное управление правилами брандмауэра</span><span class="sxs-lookup"><span data-stu-id="320b3-122">Programmatically managing firewall rules</span></span>
<span data-ttu-id="320b3-123">Помимо портала Azure правилами брандмауэра можно управлять программно с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="320b3-123">In addition to the Azure portal, firewall rules can be managed programmatically using Azure CLI.</span></span> <span data-ttu-id="320b3-124">Ознакомьтесь также со статьей [Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью Azure CLI](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="320b3-124">See also [Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>

## <a name="troubleshooting-the-database-firewall"></a><span data-ttu-id="320b3-125">Устранение неполадок брандмауэра базы данных</span><span class="sxs-lookup"><span data-stu-id="320b3-125">Troubleshooting the database firewall</span></span>
<span data-ttu-id="320b3-126">Если доступ к службе сервера базы данных Microsoft Azure для MySQL не работает должным образом, необходимо учитывать следующее:</span><span class="sxs-lookup"><span data-stu-id="320b3-126">Consider the following points when access to the Microsoft Azure Database for MySQL server service does not behave as you expect:</span></span>

* <span data-ttu-id="320b3-127">**Изменения в списке разрешенных адресов еще не вступили в силу.** До вступления в силу изменений конфигурации брандмауэра сервера базы данных Azure для MySQL может присутствовать задержка до пяти минут.</span><span class="sxs-lookup"><span data-stu-id="320b3-127">**Changes to the allow list have not taken effect yet:** There may be as much as a five-minute delay for changes to the Azure Database for MySQL Server firewall configuration to take effect.</span></span>

* <span data-ttu-id="320b3-128">**Имя для входа не авторизовано, или использован неправильный пароль.** Если имя для входа не имеет разрешений на сервере базы данных Azure для MySQL или введен неправильный пароль, то подключение к серверу базы данных Azure для MySQL отклоняется.</span><span class="sxs-lookup"><span data-stu-id="320b3-128">**The login is not authorized or an incorrect password was used:** If a login does not have permissions on the Azure Database for MySQL server or the password used is incorrect, the connection to the Azure Database for MySQL server is denied.</span></span> <span data-ttu-id="320b3-129">Создание параметра брандмауэра только предоставляет клиентам возможность подключения к серверу. Каждый клиент должен предоставить необходимые учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="320b3-129">Creating a firewall setting only provides clients with an opportunity to attempt connecting to your server; each client must provide the necessary security credentials.</span></span>

* <span data-ttu-id="320b3-130">**Динамический IP-адрес:** при наличии подключения к Интернету с динамическим предоставлением IP-адресов и возникновении проблем с прохождением через брандмауэр попробуйте одно из описанных ниже решений.</span><span class="sxs-lookup"><span data-stu-id="320b3-130">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through the firewall, you could try one of the following solutions:</span></span>

* <span data-ttu-id="320b3-131">Попросите поставщика услуг Интернета (ISP) назначить диапазон IP-адресов тем клиентским компьютерам, с которых осуществляется доступ к серверу базы данных Azure для MySQL, а затем добавьте диапазон IP-адресов в качестве правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="320b3-131">Ask your Internet Service Provider (ISP) for the IP address range assigned to your client computers that access the Azure Database for MySQL server, and then add the IP address range as a firewall rule.</span></span>

* <span data-ttu-id="320b3-132">Получите статические IP-адреса для клиентских компьютеров, а затем добавьте IP-адреса как правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="320b3-132">Get static IP addressing instead for your client computers, and then add the IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="320b3-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="320b3-133">Next steps</span></span>

<span data-ttu-id="320b3-134">[Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью портала Azure](./howto-manage-firewall-using-portal.md)
[Создание правил брандмауэра базы данных Azure для MySQL и управление ими с помощью Azure CLI](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="320b3-134">[Create and manage Azure Database for MySQL firewall rules using the Azure portal](./howto-manage-firewall-using-portal.md)
[Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>
