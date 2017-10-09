---
title: "aaaControl поведение кэширования Azure CDN со строками запроса - Premium | Документы Microsoft"
description: "Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования Azure строки запроса CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Управление режимом кэширования Azure CDN с помощью строк запросов (ценовая категория "Премиум")
> [!div class="op_single_selector"]
> * [Стандартный](cdn-query-string.md)
> * [Azure CDN уровня "Премиум" от Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Обзор
Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования строки запроса.

> [!IMPORTANT]
> Hello Standard и Premium CDN продукты содержат hello же кэширования функциональные возможности строку запроса, но отличается hello пользовательского интерфейса.  В этом документе описывается интерфейс hello для **Azure CDN Premium из Verizon**.  Дополнительные сведения о кэшировании строк запроса с помощью **Azure CDN уровня "Стандартный" от Akamai** и **Azure CDN уровня "Стандартный" от Verizon** см. в статье [Управление режимом кэширования запросов CDN с использованием строк запроса](cdn-query-string.md).
> 
> 

Доступны три режима:

* **кэш Standard**: это режим по умолчанию hello.  на первый запрос hello и активов hello кэша Hello CDN граничного узла передаст строку hello запроса из исходной toohello hello запрашивающей стороны.  Все последующие запросы для этого ресурса, которые обслуживаются hello граничного узла будет пропускать строки запроса hello до истечения срока действия кэшированного активов hello.
* **Нет-cache**: В этом режиме запросы со строками запроса не кэшируются на hello CDN граничного узла.  Hello граничного узла извлекает активов hello непосредственно из источника hello и передает его toohello запрашивающей стороне с каждым запросом.
* **уникальный кэш**: этот режим обрабатывает каждый запрос со строкой запроса как уникальный ресурс с собственным кэшем.  Например, hello ответа от источника hello для запроса на *foo.ashx?q=bar* бы кэшированный на hello граничного узла и возвращается для последующих кэшей с такой же строки запроса.  Запрос *foo.ashx?q=somethingelse* как отдельный ресурс с свой собственный toolive времени будет кэшироваться.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Изменение параметров кэширования строки запроса для профилей CDN уровня "Премиум"
1. В колонке профиля CDN hello выберите hello **управление** кнопки.
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    Открытие портала управления CDN Hello.
2. Наведите указатель мыши hello **HTTP больших** , а затем наведите указатель мыши hello **параметры кэша** всплывающим меню.  Щелкните **Кэширование строк запроса**.
   
    Появятся параметры кэширования строк запроса.
   
    ![Параметры кэширования строк запроса CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. После выбора нажмите кнопку hello **обновление** кнопки.

> [!IMPORTANT]
> изменения параметров Hello может оказаться сразу же отображается, сколько потребуется времени для hello toopropagate регистрации через hello CDN.  Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.
> 
> 

