---
title: "aaaSSL подключения для базы данных Azure для MySQL | Документы Microsoft"
description: "Сведения о настройке базы данных Azure для MySQL и связанные с ними приложения tooproperly использовать подключения SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="e4dc9-103">SSL-соединения в базе данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="e4dc9-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="e4dc9-104">База данных Azure для MySQL поддерживает подключение приложения tooclient сервера базы данных с помощью Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="e4dc9-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="e4dc9-105">Принудительное SSL-подключений между сервером базы данных и клиентские приложения помогает защитить от атак «злоумышленник в середине hello» путем шифрования hello потока данных между сервером hello и приложения.</span><span class="sxs-lookup"><span data-stu-id="e4dc9-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="e4dc9-106">Параметры по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e4dc9-106">Default settings</span></span>
<span data-ttu-id="e4dc9-107">По умолчанию hello службы базы данных должно быть toorequire настроенный SSL-подключения при подключении tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="e4dc9-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="e4dc9-108">Рекомендуется избежать отключения hello параметр SSL, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="e4dc9-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="e4dc9-109">При подготовке новой базы данных Azure для сервера MySQL через портал Azure hello и интерфейс командной строки, принудительное выполнение SSL-соединений включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e4dc9-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="e4dc9-110">Аналогичным образом строки подключения, предварительно определенные в параметрах «Строки соединения» hello в области сервера в hello портал Azure включают hello необходимые параметры для общий языков tooconnect tooyour сервер баз данных с помощью протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="e4dc9-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="e4dc9-111">Hello SSL параметра различается в зависимости от соединителя hello, например «ssl = true» или «sslmode = требуют» или» sslmode = необходимые» и др..</span><span class="sxs-lookup"><span data-stu-id="e4dc9-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="e4dc9-112">как tooenable или отключите SSL-подключение при разработке приложения, см. слишком toolearn[как tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e4dc9-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4dc9-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4dc9-113">Next steps</span></span>
[<span data-ttu-id="e4dc9-114">Библиотеки подключений для базы данных Azure для MySQL</span><span class="sxs-lookup"><span data-stu-id="e4dc9-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
