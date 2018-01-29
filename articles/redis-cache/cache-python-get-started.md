---
title: "Как использовать кэш Redis для Azure с Python | Документация Майкрософт"
description: "Приступая к работе с кэшем Redis для Azure с использованием Python"
services: redis-cache
documentationcenter: 
author: wesmc7777
manager: cfowler
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: wesmc
ms.openlocfilehash: 17a22dc7a18931e368c7f2e61c563e0d99c3a7ac
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-use-azure-redis-cache-with-python"></a>Использование кэша Redis для Azure с Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

В этой статье показано, как приступить к работе с кэшем Redis для Azure, используя Python.

## <a name="prerequisites"></a>предварительным требованиям
Установка [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Создание кэша Redis в Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a>Получение имени узла и ключей доступа
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a>Включение конечной точки без SSL
Некоторые клиенты Redis не поддерживают SSL. [Все порты, кроме SSL, отключены для новых экземпляров кэша Redis для Azure](cache-configure.md#access-ports) по умолчанию. На момент написания этой статьи клиент [redis-py](https://github.com/andymccurdy/redis-py) не поддерживает SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a>Добавление данных в кэш и их извлечение
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


Замените значение `<name>` именем своего кэша, а значение `key` — ключом доступа.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
