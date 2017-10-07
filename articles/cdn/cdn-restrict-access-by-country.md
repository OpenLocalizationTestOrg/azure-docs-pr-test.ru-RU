---
title: "aaaRestrict содержимого Azure CDN по странам | Документы Microsoft"
description: "Узнайте, как функция фильтрации Geo toorestrict доступа tooyour Azure CDN содержимого с помощью hello."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Ограничение доступности содержимого Azure CDN по странам

## <a name="overview"></a>Обзор
Когда пользователь запрашивает контент, по умолчанию, независимо от того, где пользователь hello сделан этот запрос из обслуживается hello содержимого. В некоторых случаях может потребоваться toorestrict доступа к содержимому tooyour по странам. В этом разделе объясняется как toouse hello **географическая фильтрация** компонентов в порядке tooconfigure hello tooallow или блокировать доступ к службе по странам.

> [!IMPORTANT]
> Hello Verizon и Akamai продукты содержат hello же функциональные возможности фильтрации geo, но имеют небольшими различиями в коды стран te, они поддерживают. Различия toohello связи см. шаг 3.


Этот тип ограничения, сведения о вопросы, касающиеся tooconfiguring разделе hello [вопросы](cdn-restrict-access-by-country.md#considerations) раздел в конце hello hello раздела.  

![фильтрации по стране](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Шаг 1: Определение путь к каталогу hello
Выберите конечную точку на портале hello и эта функция находится hello географическая фильтрация вкладка на левой навигационной toofind hello.

При настройке фильтра страны, необходимо указать hello относительный путь toohello расположение toowhich пользователей будет разрешен или запрещен доступ. Геофильтрацию можно применить ко всем файлам в корневом каталоге ("/") или к выбранным каталогам, указав к ним пути, например "/pictures/". Также можно применить фильтрацию geo tooa отдельных файлов, указав файл hello и пропускают hello завершающей косой черты «/ pictures/city.png».

Пример фильтра по каталогу:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Шаг 2: Определение действие hello: блокирующие или разрешающие
**Блокировать:** пользователям hello указан странах будет запрещен доступ tooassets, запрашиваемый с этого пути рекурсивной. Если для этого пути не было настроено другой фильтрации по стране, то доступ для всех остальных пользователей будет разрешен.

**Разрешить:** пользователям hello указан странах может tooassets доступа, запрашиваемый с этого пути рекурсивной.

## <a name="step-3-define-hello-countries"></a>Шаг 3: Определение странах hello
Выберите hello странах, вы должны быть tooblock или разрешить для hello пути. 

Например правило hello блокировки /Photos/Strasbourg/отфильтрует файлы в том числе:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Коды стран
Hello **географическая фильтрация** функция использует toodefine hello коды страны стран, из которых будут разрешены или заблокированы запрос для защищенной каталога. Вы найдете hello коды стран в [коды стран CDN Azure](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Рекомендации
* Он может занять too90 минут Verizon, или на несколько минут с Akamai, для изменения tooyour страны конфигурации tootake влияние фильтра.
* Эта функция не поддерживает символы-шаблоны (например, *).
* Конфигурация географическая фильтрация Hello, связанные с относительным путем hello будет путь toothat применяются рекурсивно.
* Только одно правило может быть применен toohello же относительный путь (не может создавать несколько фильтров, страны, toohello точки же относительный путь. Однако к одному и тому же каталогу могут применяться несколько фильтров стран. Это происходит из-за характера рекурсивные toohello фильтры страны. Другими словами, подкаталогу ранее настроенного каталога можно назначить другой фильтр страны.

