---
title: "Примеры кэша Redis для Azure CLI | Документы Майкрософт"
description: "Примеры Azure CLI для кэша Redis для Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="f7e35-103">Примеры Azure CLI для кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="f7e35-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="f7e35-104">В следующей таблице содержатся ссылки на скрипты Bash, созданные с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f7e35-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="f7e35-105">**Создание кэша**</span><span class="sxs-lookup"><span data-stu-id="f7e35-105">**Create cache**</span></span>||
| [<span data-ttu-id="f7e35-106">Создание кэша</span><span class="sxs-lookup"><span data-stu-id="f7e35-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="f7e35-107">Создает группу ресурсов и базовый уровень кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="f7e35-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="f7e35-108">Создание кэша уровня "Премиум" с кластеризацией</span><span class="sxs-lookup"><span data-stu-id="f7e35-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="f7e35-109">Создает группу ресурсов и кэш уровня "Премиум" с включенной кластеризацией.</span><span class="sxs-lookup"><span data-stu-id="f7e35-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="f7e35-110">Получение сведений о кэше</span><span class="sxs-lookup"><span data-stu-id="f7e35-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="f7e35-111">Возвращает сведения об экземпляре кэша Redis для Azure, включая состояние подготовки.</span><span class="sxs-lookup"><span data-stu-id="f7e35-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="f7e35-112">Получение имени узла, портов и ключей</span><span class="sxs-lookup"><span data-stu-id="f7e35-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="f7e35-113">Возвращает имя узла, порты и ключи для экземпляра кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="f7e35-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="f7e35-114">**Веб-приложение и кэш**</span><span class="sxs-lookup"><span data-stu-id="f7e35-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="f7e35-115">Подключение веб-приложения к кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="f7e35-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="f7e35-116">Создает веб-приложение Azure и кэш Redis, а затем добавляет сведения о подключении кэша Redis в параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="f7e35-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="f7e35-117">**Удаление кэша**</span><span class="sxs-lookup"><span data-stu-id="f7e35-117">**Delete cache**</span></span>||
| [<span data-ttu-id="f7e35-118">Удаление кэша</span><span class="sxs-lookup"><span data-stu-id="f7e35-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="f7e35-119">Удаляет экземпляр кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="f7e35-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="f7e35-120">Дополнительные сведения об Azure CLI 2.0 см. в статье [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Установка Azure CLI 2.0) и [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="f7e35-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>