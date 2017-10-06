---
title: "поведение кэширования Azure CDN со строками запроса aaaControl | Документы Microsoft"
description: "Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования Azure строки запроса CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Управление режимом кэширования Azure CDN с помощью строк запросов
> [!div class="op_single_selector"]
> * [Стандартный](cdn-query-string.md)
> * [Azure CDN уровня "Премиум" от Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Обзор
Элементы управления, как файлы, если они содержат строки запросов в кэше toobe кэширования строки запроса.

> [!IMPORTANT]
> Hello Standard и Premium CDN продукты содержат hello же кэширования функциональные возможности строку запроса, но отличается hello пользовательского интерфейса.  В этом документе описывается интерфейс hello для **Azure CDN Standard из Akamai** и **Azure CDN Standard из Verizon**.  Дополнительные сведения о кэшировании строк запроса с помощью **Azure CDN уровня "Премиум" от Verizon** см. в статье [Управление поведением кэширования запросов CDN с помощью строк запроса — уровень Premium](cdn-query-string-premium.md).
> 
> 

Доступны три режима:

* **Пропускать строки запросов**: это режим по умолчанию hello.  на первый запрос hello и активов hello кэша Hello CDN граничного узла передаст строку hello запроса из исходной toohello hello запрашивающей стороны.  Все последующие запросы для этого ресурса, которые обслуживаются hello граничного узла будет пропускать строки запроса hello до истечения срока действия кэшированного активов hello.
* **Обойти кэширование для URL-адреса со строками запроса**: В этом режиме запросы со строками запроса не кэшируются на hello CDN граничного узла.  Hello граничного узла извлекает активов hello непосредственно из источника hello и передает его toohello запрашивающей стороне с каждым запросом.
* **Кэширование каждого уникального URL-адреса**: этот режим обрабатывает каждый запрос со строкой запроса как уникальный ресурс-контейнер с собственным кэшем.  Например, hello ответа от источника hello для запроса на *foo.ashx?q=bar* бы кэшированный на hello граничного узла и возвращается для последующих кэшей с такой же строки запроса.  Запрос *foo.ashx?q=somethingelse* как отдельный ресурс с свой собственный toolive времени будет кэшироваться.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Изменение параметров кэширования строки запроса для профилей CDN уровня "Стандартный"
1. Из колонки профиля CDN hello щелкните hello конечной точкой CDN необходимо toomanage.
   
    ![Конечные точки в колонке профиля CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    Открывает колонку конечной точки CDN Hello.
2. Нажмите кнопку hello **Настройка** кнопки.
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    Открывает колонку конфигурации CDN Hello.
3. Выберите значение из hello **режим кэширования строк запросов** раскрывающегося списка.
   
    ![Параметры кэширования строк запроса CDN](./media/cdn-query-string/cdn-query-string.png)
4. После выбора нажмите кнопку hello **Сохранить** кнопки.

> [!IMPORTANT]
> изменения параметров Hello может оказаться сразу же отображается, сколько потребуется времени для hello toopropagate регистрации через hello CDN.  Для профилей <b>Azure CDN от Akamai</b> распространение обычно занимает не более минуты.  Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.
> 
> 

