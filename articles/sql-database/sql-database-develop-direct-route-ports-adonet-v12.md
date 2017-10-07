---
title: "aaaPorts за пределы 1433 для базы данных SQL | Документы Microsoft"
description: "Подключения клиентов из tooAzure ADO.NET базы данных SQL иногда использование прокси-сервера hello и взаимодействовать непосредственно с базой данных hello. Порты, отличные от 1433, становятся важными."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>Порты для ADO.NET 4.5, отличные от порта 1433
В этом разделе описываются hello работу подключения к базе данных SQL Azure для клиентов, использующих ADO.NET 4.5 или более поздней версии. 

> [!IMPORTANT]
> Сведения об архитектуре подключения см. в статье [Azure SQL Database Connectivity Architecture](sql-database-connectivity-architecture.md) (Архитектура подключения базы данных SQL Azure).
>

## <a name="outside-vs-inside"></a>Снаружи или внутри
Для подключения tooAzure базы данных SQL, мы должны запросить запускается ли клиентская программа *за пределами* или *внутри* границ hello облако Azure. Hello подразделах рассматриваются два распространенных сценария.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Внешняя программа.* Клиент работает на настольном компьютере
Порт 1433 — hello только порт, который должен быть открыт на компьютере, на котором размещена база данных SQL клиентское приложение.

#### <a name="inside-client-runs-on-azure"></a>*Внутренняя программа.* Клиент работает в Azure
При запуске клиента внутри границы hello облако Azure использует так мы называем *прямого маршрута* toointeract с hello базы данных SQL server. После установления соединения для дальнейшего взаимодействия между клиентом hello и базы данных включает в себя без прокси-сервера по промежуточного слоя.

последовательность Hello выглядит следующим образом:

1. ADO.NET 4.5 (или более поздней версии) инициирует краткое взаимодействие с hello облако Azure и получает номер динамически определенного порта.
   
   * Hello динамически определяемого используется порт в диапазоне hello 11000 11999 или 14000 14999.
2. ADO.NET затем подключается toohello базы данных SQL server напрямую, не по промежуточного слоя между ними.
3. Запросы отправляются напрямую toohello базы данных, а результаты возвращаются непосредственно toohello клиента.

Убедитесь, что порта hello, диапазонов 11000 11999 и 14000-14999 на компьютере клиента Azure, остаются доступными для взаимодействия клиента ADO.NET 4.5 с базой данных SQL.

* В частности должно быть никаких других исходящих препятствия порты из диапазона hello.
* На ВМ Azure, hello **брандмауэр Windows в режиме повышенной безопасности** элементы управления hello параметры порта.
  
  * Можно использовать hello [брандмауэра пользовательский интерфейс](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a правило, для которого указывается hello **TCP** как протокол, а также диапазон портов с синтаксисом hello **11000 11999**.

## <a name="version-clarifications"></a>Уточнение версии
В этом разделе поясняются моникеров hello, которые ссылаются tooproduct версии. В нем также перечисляются некоторые пары версий продуктов.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 поддерживает протокол TDS 7.3 hello, но не 7.4.
* ADO.NET 4.5 и более поздних версий поддерживает протокол TDS 7.4 hello.

## <a name="related-links"></a>Связанные ссылки
* 20 июля 2015 г. был выпущен ADO.NET 4.6. Доступно с извещение блога от службы технической поддержки .NET hello [здесь](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* 15 августа 2012 г. был выпущен ADO.NET 4.5. Доступно с извещение блога от службы технической поддержки .NET hello [здесь](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * Запись блога об ADO.NET 4.5.1 доступна [здесь](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Список версий протокола TDS](http://www.freetds.org/userguide/tdshistory.htm)
* [Общие сведения о разработке базы данных SQL](sql-database-develop-overview.md)
* [Брандмауэр базы данных SQL Azure](sql-database-firewall-configure.md)
* [Практическое руководство. Настройка параметров брандмауэра для Базы данных SQL](sql-database-configure-firewall-settings.md)

