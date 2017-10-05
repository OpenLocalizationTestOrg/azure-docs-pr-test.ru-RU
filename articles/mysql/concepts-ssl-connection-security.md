---
title: "SSL-соединения в базе данных Azure для MySQL | Документация Майкрософт"
description: "Сведения о настройке базы данных Azure для MySQL и связанных приложений для правильного использования SSL-соединений."
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="32276-103">SSL-соединения в базе данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="32276-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="32276-104">База данных Azure для MySQL поддерживает подключение сервера базы данных к клиентским приложениям с помощью SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="32276-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="32276-105">Применение SSL-соединений между сервером базы данных и клиентскими приложениями обеспечивает защиту от атак "злоумышленник в середине" за счет шифрования потока данных между сервером и приложением.</span><span class="sxs-lookup"><span data-stu-id="32276-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="32276-106">Параметры по умолчанию</span><span class="sxs-lookup"><span data-stu-id="32276-106">Default settings</span></span>
<span data-ttu-id="32276-107">По умолчанию в службе базы данных должно быть настроено обязательное использование SSL-соединений при подключении к MySQL.</span><span class="sxs-lookup"><span data-stu-id="32276-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="32276-108">Рекомендуется не отключать параметр SSL без необходимости.</span><span class="sxs-lookup"><span data-stu-id="32276-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="32276-109">При подготовке нового сервера базы данных Azure для MySQL с помощью портала Azure и интерфейса командной строки применение SSL-соединений включается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="32276-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="32276-110">Аналогичным образом предопределенные строки подключения в разделе "Строки подключения" в настройках сервера на портале Azure содержат необходимые параметры для распространенных языков, что позволяет подключиться к серверу базы данных с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="32276-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="32276-111">Значение параметра SSL зависит от соединителя. Например, может использоваться "ssl=true", "sslmode=require", "sslmode=required" или другой вариант.</span><span class="sxs-lookup"><span data-stu-id="32276-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="32276-112">Чтобы узнать, как включить или отключить SSL-соединение при разработке приложения, ознакомьтесь со [статьей, посвященной настройке SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="32276-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32276-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32276-113">Next steps</span></span>
[<span data-ttu-id="32276-114">Библиотеки подключений для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="32276-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
