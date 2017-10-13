---
title: "Клиентские библиотеки, требуемые для подключения к службам Azure Analysis Services | Документы Майкрософт"
description: "Описываются клиентские библиотеки, необходимые для подключения клиентских приложений и средств к службам Azure Analysis Services"
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
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a>Клиентские библиотеки для подключения к службам Azure Analysis Services

Клиентские библиотеки требуются клиентским приложениям и средствам для подключения к серверам служб Analysis Services. 

Службы Analysis Services используют три типа клиентских библиотек. ADOMD.NET и объекты управления служб Analysis Services — это управляемые клиентские библиотеки. Поставщик OLE DB служб Analysis Services (MSOLAP DLL) — это собственная клиентская библиотека. Как правило, все три библиотеки устанавливаются одновременно. Службам Azure Analysis Services требуются последние версии библиотек. 

Клиентские приложения Майкрософт, такие как Power BI Desktop и Excel, устанавливают все три клиентские библиотеки. Однако в зависимости от версии или частоты обновлений могут устанавливаться устаревшие, а не новые версии клиентских библиотек, необходимые для служб Azure Analysis Services. Это же касается и пользовательских приложений или других интерфейсов, таких как AsCmd, TOM, ADOMD.NET. Для этих приложений клиентские библиотеки требуется устанавливать вручную. Клиентские библиотеки, устанавливаемые вручную, включены в пакеты дополнительных компонентов SQL Server в качестве распространяемых пакетов. Однако они зависят от версии SQL Server, поэтому версия в пакетах может быть не последней.  

Клиентские библиотеки для клиентских подключений отличаются от поставщиков данных, требуемых для подключения с сервера служб Azure Analysis Services к источнику данных. Дополнительные сведения о подключениях к источнику данных см. в [этой статье](analysis-services-datasource.md).

## <a name="download-the-latest-client-libraries"></a>Скачивание последних версий клиентских библиотек  
Используйте перечисленные ниже клиентские библиотеки, если в рабочей среде требуются полностью выпущенные и поддерживаемые версии.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Дальнейшие действия
[Подключение с помощью Excel](analysis-services-connect-excel.md)    
[Подключение с помощью Power BI](analysis-services-connect-pbi.md)
