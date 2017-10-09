---
title: "aaaHow toouse кэша Redis с Python | Документы Microsoft"
description: "Приступая к работе с кэшем Redis для Azure с использованием Python"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a><span data-ttu-id="72c65-103">Как toouse Redis для Azure кэш с Python</span><span class="sxs-lookup"><span data-stu-id="72c65-103">How toouse Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72c65-104">.NET</span><span class="sxs-lookup"><span data-stu-id="72c65-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="72c65-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="72c65-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="72c65-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="72c65-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="72c65-107">Java</span><span class="sxs-lookup"><span data-stu-id="72c65-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="72c65-108">Python</span><span class="sxs-lookup"><span data-stu-id="72c65-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="72c65-109">В этом разделе рассказывается, как tooget работу с кэша Redis для Azure с помощью Python.</span><span class="sxs-lookup"><span data-stu-id="72c65-109">This topic shows you how tooget started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72c65-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="72c65-110">Prerequisites</span></span>
<span data-ttu-id="72c65-111">Установка [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="72c65-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="72c65-112">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="72c65-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="72c65-113">Получить ключи hello узла имя и доступа</span><span class="sxs-lookup"><span data-stu-id="72c65-113">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a><span data-ttu-id="72c65-114">Включить конечную точку hello не SSL</span><span class="sxs-lookup"><span data-stu-id="72c65-114">Enable hello non-SSL endpoint</span></span>
<span data-ttu-id="72c65-115">Некоторые клиенты Redis не поддерживает протокол SSL и по умолчанию hello [порт не SSL отключен для новых экземпляров кэша Azure Redis](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="72c65-115">Some Redis clients don't support SSL, and by default hello [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="72c65-116">Во время написания этой статьи hello hello [redis py](https://github.com/andymccurdy/redis-py) клиент не поддерживает SSL.</span><span class="sxs-lookup"><span data-stu-id="72c65-116">At hello time of this writing, hello [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="72c65-117">Добавить что-нибудь toohello кэш и извлечь его</span><span class="sxs-lookup"><span data-stu-id="72c65-117">Add something toohello cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="72c65-118">Замените значение `<name>` именем своего кэша, а значение `key` — ключом доступа.</span><span class="sxs-lookup"><span data-stu-id="72c65-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
