---
title: "aaaConnect tooAzure служб Analysis Services с помощью Power BI | Документы Microsoft"
description: "Узнайте, как tooconnect tooan Azure служб Analysis Services с помощью Power BI."
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
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Подключение с помощью Power BI

После создания сервера в Azure и развернуть tooit табличной модели, пользователи в вашей организации будут готовы tooconnect и приступить к изучению данных. 

> [!TIP]
> Убедиться, что последняя версия toouse hello объекта [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Подключение в Power BI Desktop

1. В Power BI Desktop выберите **Получить данные** > **Azure** > **База данных Azure Analysis Services**.

2. В **сервера**, введите имя сервера hello. 
    
    Быть убедиться, что tooinclude hello полный URL-адрес. Например, asazure://westcentralus.asazure.windows.net/advworks.

3. В **базы данных**, если известно имя hello hello базы данных табличной модели или перспективы требуется tooconnect для, вставьте его здесь. В противном случае вы можете оставить это поле пустым и выбрать базу данных или перспективу позже.

4. Оставьте по умолчанию hello **Connect live** параметр, а затем нажмите клавишу **Connect**. 

5. При отображении запроса введите свои учетные данные. 

6. В **Навигатор**, разверните сервер hello, а затем выберите hello модель или перспективу, нужно tooconnect для, нажмите кнопку **Connect**. Выберите модели или перспективы tooshow все объекты hello для этого представления.

    Hello модели в Power BI Desktop откроется пустой отчет в представлении отчета. Список полей Hello отображает все объекты модели не скрыты. Состояние подключения отображается в правом нижнем углу hello.

## <a name="connect-in-power-bi-service"></a>Подключение в Power BI (служба)

1. Создайте файл Power BI Desktop, имеет модель tooyour активное подключение на сервере.
2. В [Power BI](https://powerbi.microsoft.com) последовательно выберите **Получить данные** > **Файлы**. Найдите и выберите созданный файл.



## <a name="see-also"></a>См. также
[Подключение tooAzure Analysis Services](analysis-services-connect.md)   
[Клиентские библиотеки](analysis-services-data-providers.md)

