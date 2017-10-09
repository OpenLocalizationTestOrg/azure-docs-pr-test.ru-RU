---
title: "Использование кэша Redis aaaManaging hello обозреватель Azure для IntelliJ | Документы Microsoft"
description: "Узнайте, как toomanage redis для Azure кэширует с помощью hello обозреватель Azure для IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="17541-103">Управление кэшами Redis, с помощью hello обозреватель Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="17541-103">Managing Redis Caches using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="17541-104">Hello Explorer Azure, который является частью набора средств Azure для IntelliJ hello, обеспечивает разработчиков Java в использовании решения для управления redis кэши в его учетной записью Azure из внутри hello IntelliJ интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="17541-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="17541-105">Создание кэша Redis с помощью IntelliJ</span><span class="sxs-lookup"><span data-stu-id="17541-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="17541-106">Hello следующие шаги пошаговыми руководствами toocreate hello действия кэша redis с использованием hello обозреватель Azure.</span><span class="sxs-lookup"><span data-stu-id="17541-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="17541-107">Войдите в tooyour учетная запись Azure с помощью действия hello в hello [входа в инструкции для hello средств Azure для IntelliJ] статьи.</span><span class="sxs-lookup"><span data-stu-id="17541-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="17541-108">В hello **обозреватель Azure** окно инструментов, разверните hello **Azure** узел, щелкните правой кнопкой мыши **кэша Redis**и нажмите кнопку **создать кэш Redis**.</span><span class="sxs-lookup"><span data-stu-id="17541-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Меню создания кэша Redis][CR01]

1. <span data-ttu-id="17541-110">Здравствуйте, когда **новый кэш Redis** диалоговое окно, укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="17541-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Диалоговое окно New Redis Cache (Новый кэш Redis)][CR02]

   <span data-ttu-id="17541-112">а.</span><span class="sxs-lookup"><span data-stu-id="17541-112">a.</span></span> <span data-ttu-id="17541-113">**DNS-имя**: определяет поддомен hello DNS для hello новый кэш redis, который предваряются слишком». redis.cache.windows .net», например: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="17541-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which are prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="17541-114">b.</span><span class="sxs-lookup"><span data-stu-id="17541-114">b.</span></span> <span data-ttu-id="17541-115">**Подписки**: указывает hello подписки Azure, требуется toouse hello новый кэш redis.</span><span class="sxs-lookup"><span data-stu-id="17541-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="17541-116">c.</span><span class="sxs-lookup"><span data-stu-id="17541-116">c.</span></span> <span data-ttu-id="17541-117">**Группа ресурсов**: Определяет hello группы ресурсов для кэша redis; требуется toochoose один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="17541-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="17541-118">**Создать новое**: Указывает, что toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="17541-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="17541-119">**Использовать существующую**: указывает, что будет выбрана группа ресурсов, связанная с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="17541-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="17541-120">d.</span><span class="sxs-lookup"><span data-stu-id="17541-120">d.</span></span> <span data-ttu-id="17541-121">**Расположение**: Указывает расположение hello, где создается кэш redis; например, *Запад США*.</span><span class="sxs-lookup"><span data-stu-id="17541-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="17541-122">д.</span><span class="sxs-lookup"><span data-stu-id="17541-122">e.</span></span> <span data-ttu-id="17541-123">**Ценовая категория**: Определяет выбранной ценовой категории использует кэш redis; этот параметр определяет hello число клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="17541-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="17541-124">(Дополнительные сведения см. на [странице с ценами на кэш Redis].)</span><span class="sxs-lookup"><span data-stu-id="17541-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="17541-125">f.</span><span class="sxs-lookup"><span data-stu-id="17541-125">f.</span></span> <span data-ttu-id="17541-126">**Порт без SSL**: указывает, разрешает ли кэш Redis подключения без использования SSL. По умолчанию разрешены только SSL-подключения.</span><span class="sxs-lookup"><span data-stu-id="17541-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="17541-127">Когда вы введете значения для всех параметров кэша Redis, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17541-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="17541-128">После создания кэша redis отображается в обозревателе Azure hello.</span><span class="sxs-lookup"><span data-stu-id="17541-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Кэш Redis в Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="17541-130">Дополнительные сведения о настройке Azure параметры кэша redis см. в разделе [как tooconfigure кэш Azure Redis].</span><span class="sxs-lookup"><span data-stu-id="17541-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="17541-131">Отобразить свойства hello для кэша Redis в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="17541-131">Display hello properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="17541-132">В обозреватель Azure hello правой кнопкой мыши кэша redis и нажмите кнопку **Показать свойства**.</span><span class="sxs-lookup"><span data-stu-id="17541-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure свойства обозревателя контекстного меню toodisplay для кэша redis][SP01]

1. <span data-ttu-id="17541-134">Hello обозреватель Azure отображаются свойства hello для кэша redis.</span><span class="sxs-lookup"><span data-stu-id="17541-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Свойства кэша Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="17541-136">Удаление кэша Redis с помощью IntelliJ</span><span class="sxs-lookup"><span data-stu-id="17541-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="17541-137">В обозреватель Azure hello правой кнопкой мыши кэша redis и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="17541-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Обозреватель контекст меню toodelete кэш redis для Azure][DE01]

1. <span data-ttu-id="17541-139">Нажмите кнопку **Да** при запросе toodelete кэша redis.</span><span class="sxs-lookup"><span data-stu-id="17541-139">Click **Yes** when prompted toodelete your redis cache.</span></span>

   ![Запрос на удаление кэша Redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="17541-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17541-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="17541-142">Дополнительные сведения о кэш redis для Azure, параметры конфигурации и ценах см. в разделе hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="17541-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="17541-143">[кэш Azure Redis]</span><span class="sxs-lookup"><span data-stu-id="17541-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="17541-144">[Документация по кэшу Redis]</span><span class="sxs-lookup"><span data-stu-id="17541-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="17541-145">[странице с ценами на кэш Redis]</span><span class="sxs-lookup"><span data-stu-id="17541-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="17541-146">[как tooconfigure кэш Azure Redis]</span><span class="sxs-lookup"><span data-stu-id="17541-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[странице с ценами на кэш Redis]: https://azure.microsoft.com/pricing/details/cache/
[кэш Azure Redis]: https://azure.microsoft.com/services/cache/
[Документация по кэшу Redis]: ./redis-cache/index.md
[как tooconfigure кэш Azure Redis]: ./redis-cache/cache-configure.md
[входа в инструкции для hello средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
