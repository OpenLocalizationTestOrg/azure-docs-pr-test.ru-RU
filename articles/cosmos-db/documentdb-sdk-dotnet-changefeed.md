---
title: "Пакет SDK и ресурсы обработчика веб-канала изменений в .NET для Azure DocumentDB | Документы Майкрософт"
description: "Сведения об API и пакете SDK для обработчика веб-канала изменений, включая даты выхода, даты выбытия и изменения, внесенные в каждую версию пакета SDK для обработчика веб-канала изменений в .NET для DocumentDB."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2017
ms.author: maquaran
ms.openlocfilehash: 239b590a1e3a83fe0205dd8169697db745d7f75e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a>Пакет SDK для обработчика веб-канала изменений для DocumentDB .NET: скачивание и заметки о выпуске
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Веб-канал изменений в .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Поставщик ресурсов REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Скачивание пакета SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td>**Документация по API**</td><td>[Справочная документация по изменению API библиотеки обработчика веб-каналов](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td>**Приступая к работе**</td><td>[Приступая к работе с пакетом SDK для обработчика веб-канала изменений в .NET для DocumentDB](change-feed.md)</td></tr>

<tr><td>**Текущая поддерживаемая платформа**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Заметки о выпуске

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1
* Устраняет проблему при расчете оставшейся работы, если канал изменений был пуст или никакие действия не ожидались.
* Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.13.2 и выше.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Добавлен метод для оценки оставшейся работы для обработки в веб-канале изменений.
* Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.13.2 и выше.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* Пакет SDK общей доступности.
* Совместимость с [пакетом SDK для .NET для DocumentDB](documentdb-sdk-dotnet.md) версии 1.14.1 и ниже.

## <a name="release--retirement-dates"></a>Даты выпуска и выбытия
Корпорация Майкрософт отправит уведомление минимум за **12 месяцев** до вывода пакета SDK из эксплуатации, чтобы обеспечить более плавный переход на новую или поддерживаемую версию.

Новые функции, возможности и оптимизации добавляются только в текущую версию пакета SDK, поэтому рекомендуется как можно раньше обновлять пакет SDK до последней версии. 

Любые запросы к Cosmos DB с помощью выведенного из эксплуатации пакета SDK будут отклонены службой.

<br/>

| Version (версия) | Дата выпуска | Дата вывода |
| --- | --- | --- |
| [1.1.1](#1.1.1) |29 августа 2017 г. |--- |
| [1.1.0](#1.1.0) |13 августа 2017 г. |--- |
| [1.0.0](#1.0.0) |7 июля 2017 г. |--- |


## <a name="faq"></a>Часто задаваемые вопросы
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>См. также
Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

