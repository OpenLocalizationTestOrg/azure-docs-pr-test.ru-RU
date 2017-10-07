---
title: "aaaUpgrading toohello API REST службы поиска Azure версии 2016-09-01 | Документы Microsoft"
description: "Обновление toohello API REST службы поиска Azure версии 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Обновление toohello API REST службы поиска Azure версии 2016-09-01
Если вы используете версию 2015-02-28 или 2015-02-28-Preview из hello [API REST службы поиска Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), эта статья поможет вам обновить приложения toouse hello Далее общедоступной API версии, 2016-09-01.

Версии 2016-09-01 из API-интерфейса REST hello содержит некоторые изменения из более ранних версий. Эти отличия в основном обратно совместимы, поэтому изменение кода потребует минимальных усилий в зависимости от версии, которая использовался ранее. В разделе [tooupgrade действия](#UpgradeSteps) инструкции toochange новой версии API код toouse hello.

> [!NOTE]
> Экземпляр службы поиска Azure поддерживает несколько версий API-Интерфейс REST, включая hello последнюю версию. Вы можете продолжить toouse версии, когда он больше не hello последнюю версию, но рекомендуется перейти к toouse кода hello последнюю версию.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Новые возможности в версии 2016-09-01
Версии 2016-09-01 — второй общедоступной версии hello hello API REST службы поиска Azure. Новые возможности в этой версии API:

* [Пользовательские анализаторы](https://aka.ms/customanalyzers), которая разрешает tootake контроль над процессом hello преобразования текста в токены индексируемых и с возможностью поиска.
* [Хранилище больших двоичных объектов Azure](search-howto-indexing-azure-blob-storage.md) и [табличного хранилища Azure](search-howto-indexing-azure-tables.md) индексаторы, которые позволяют вам tooeasily импортировать данные из хранилища Azure в поиске Azure, по расписанию или по требованию.
* [Поля сопоставления](search-indexer-field-mappings.md), которая разрешает toocustomize как индексаторов в поиске Azure для импорта данных.
* Теги eTag, разрешающих tooupdate hello определений индексов, индексаторов и источников данных в режиме параллелизма. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Tooupgrade действия
При обновлении с версии 2015-02-28, скорее всего, будут toomake tooyour любого изменения кода, кроме номера версии toochange hello. Hello только ситуации, в которых может потребоваться toochange кода, когда:

* Код завершается ошибкой, если в ответе API возвращаются нераспознанные свойства. По умолчанию приложение должно игнорировать свойства, которые не распознаются.
* Код сохраняет запросы API-интерфейса и пытается tooresend их toohello новой версии API. Например, это может произойти, если приложение сохраняет токены продолжения, возвращенный API поиска hello (Дополнительные сведения см. по `@search.nextPageParameters` в hello [Справочник по API поиска](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Если любой из этих ситуаций применить tooyou, затем может потребоваться toochange код соответствующим образом. В противном случае никаких изменений не требуется Если не требуется, чтобы с помощью hello toostart [новые функции](#WhatsNew) версии 2016-09-01.

При обновлении с версии 2015-02-28-Preview hello выше также применяется, но также следует иметь в виду, что некоторые функции предварительной версии не доступны в версии 2016-09-01:

* Поддержка индексатора хранилища BLOB-объектов Azure для CSV-файлов и больших двоичных объектов, содержащих массивы JSON.
* синонимы;
* Запросы "Скорее всего".

Если ваш код использует эти функции, нельзя будет tooupgrade too2016-09-01 без удаления их использования.

> [!IMPORTANT]
> Помните, что предварительные версии API предназначены для тестирования и ознакомления. Они не должны использоваться в рабочей среде.
> 
> 

## <a name="conclusion"></a>Заключение
Если требуются дополнительные сведения об использовании hello API REST службы поиска Azure, см. раздел hello недавно обновленного [Справочник по API](https://msdn.microsoft.com/library/azure/dn798935.aspx) на сайте MSDN.

Будем рады вашим отзывам о службе поиска Azure. Если возникли проблемы, вы бесплатно tooask нам для получения справки по hello [форум MSDN поиска Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) или [StackOverflow](http://stackoverflow.com/). Если вы требуете вопрос о Azure поиск на сайте StackOverflow, убедитесь, что tootag с `azure-search`.

Благодарим вас за использование поиска Azure!

