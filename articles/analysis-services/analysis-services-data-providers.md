---
title: "aaaClient библиотеки, необходимые для соединения служб Analysis Services tooAzure | Документы Microsoft"
description: "Описывает клиентские библиотеки, необходимые для клиентского приложения и средства tooconnect Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Клиентские библиотеки для соединения служб Analysis Services tooAzure

Клиентские библиотеки необходимы для клиентских приложений и серверов служб tooAnalysis tooconnect средства. 

Службы Analysis Services используют три типа клиентских библиотек. ADOMD.NET и объекты управления служб Analysis Services — это управляемые клиентские библиотеки. Поставщик OLE DB служб Analysis Services Hello (MSOLAP DLL) — это библиотека собственного клиента. Как правило, все три устанавливаются в hello то же время. Azure Analysis Services требует hello последних версий. 

Клиентские приложения Майкрософт, такие как Power BI Desktop и Excel, устанавливают все три клиентские библиотеки. Тем не менее в зависимости от версии hello или частота обновления, клиентские библиотеки не может быть hello последние версии необходимых служб Azure Analysis Services. Hello применимо и к toocustom приложений или другие интерфейсы, такие как AsCmd TOM, ADOMD.NET. Эти приложения требуют установки библиотеки hello вручную. Hello клиентские библиотеки для ручной установки включаются в пакеты дополнительных компонентов SQL Server в качестве распространяемых пакетов. Однако эти клиентские библиотеки равноценных toohello версии SQL Server и не может быть hello последняя версия.  

Клиентские библиотеки для клиентских подключений, отличаются от tooconnect необходимые поставщики данных из источника данных tooa сервера Azure Analysis Services. toolearn Дополнительные сведения о подключения источника данных, в разделе [подключения источника данных](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Загрузить последние библиотеки клиента hello  
Используйте следующие клиентские библиотеки, если в рабочей среде и требующих полностью выпущенных и поддерживаемых версий hello.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Дальнейшие действия
[Подключение с помощью Excel](analysis-services-connect-excel.md)    
[Подключение с помощью Power BI](analysis-services-connect-pbi.md)
