---
title: "Использование кэша Redis aaaManaging hello обозреватель Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toomanage redis для Azure кэширует с помощью hello обозреватель Azure для Eclipse."
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
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a>Управление кэшами Redis, с помощью hello обозреватель Azure для Eclipse

Hello Explorer Azure, который является частью hello средств Azure для Eclipse, обеспечивает разработчиков Java в использовании решения для управления redis кэши в его учетной записью Azure из внутри hello интегрированной среды разработки Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Создание кэша Redis с помощью Eclipse

Hello следующие шаги пошаговыми руководствами toocreate hello действия кэша redis с использованием hello обозреватель Azure.

1. Войдите в tooyour учетная запись Azure с помощью действия hello в hello [входа в инструкции для средств Azure для Eclipse hello] статьи.

1. В hello **обозреватель Azure** окно инструментов, разверните hello **Azure** узел, щелкните правой кнопкой мыши **кэша Redis**и нажмите кнопку **создать кэш Redis**.

   ![Меню создания кэша Redis][CR01]

1. Здравствуйте, когда **новый кэш Redis** диалоговое окно, укажите hello следующие параметры:

   ![Диалоговое окно создания кэша Redis][CR02]

   а. **DNS-имя**: определяет поддомен hello DNS для hello новый кэш redis, который добавляется слишком». redis.cache.windows .net», например: *wingtiptoys.redis.cache.windows.net*.

   b. **Подписки**: указывает hello подписки Azure, требуется toouse hello новый кэш redis.

   c. **Группа ресурсов**: Определяет hello группы ресурсов для кэша redis; требуется toochoose один из следующих вариантов hello:
      * **Создать новое**: Указывает, что toocreate новую группу ресурсов.
      * **Использовать существующую**: указывает, что будет выбрана группа ресурсов, связанная с учетной записью Azure.

   d. **Расположение**: Указывает расположение hello, где создается кэш redis; например, *Запад США*.

   д. **Ценовая категория**: Определяет выбранной ценовой категории использует кэш redis; этот параметр определяет hello число клиентских подключений. (Дополнительные сведения см. на [странице с ценами на кэш Redis].)

   f. **Порт без SSL**: указывает, разрешает ли кэш Redis подключения без использования SSL. По умолчанию разрешены только SSL-подключения.

1. Когда вы введете значения для всех параметров кэша Redis, нажмите кнопку **ОК**.

После создания кэша redis отображается в обозревателе Azure hello.

   ![Кэш Redis в Azure Explorer][CR03]

> [!NOTE]
>
> Дополнительные сведения о настройке Azure параметры кэша redis см. в разделе [как tooconfigure кэш Azure Redis].
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a>Отобразить свойства hello для кэша Redis в Eclipse

1. В обозреватель Azure hello правой кнопкой мыши кэша redis и нажмите кнопку **Показать свойства**.

   ![Azure свойства обозревателя контекстного меню toodisplay для кэша redis][SP01]

1. Hello обозреватель Azure отображаются свойства hello для кэша redis.

   ![Свойства кэша Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Удаление кэша Redis с помощью Eclipse

1. В обозреватель Azure hello правой кнопкой мыши кэша redis и нажмите кнопку **удалить**.

   ![Обозреватель контекст меню toodelete кэш redis для Azure][DE01]

1. Нажмите кнопку **ОК** при запросе toodelete кэша redis.

   ![Запрос на удаление кэша Redis][DE02]

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Дополнительные сведения о кэш redis для Azure, параметры конфигурации и ценах см. в разделе hello ссылкам:

* [кэш Azure Redis]
* [Документация по кэшу Redis]
* [странице с ценами на кэш Redis]
* [как tooconfigure кэш Azure Redis]

<!-- URL List -->

[странице с ценами на кэш Redis]: https://azure.microsoft.com/pricing/details/cache/
[кэш Azure Redis]: https://azure.microsoft.com/services/cache/
[Документация по кэшу Redis]: ./redis-cache/index.md
[как tooconfigure кэш Azure Redis]: ./redis-cache/cache-configure.md
[входа в инструкции для средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
