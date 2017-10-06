---
title: "aaaConnect tooAzure Excel в службах Analysis Services | Документы Microsoft"
description: "Узнайте, как tooconnect tooan Azure служб Analysis Services с помощью Excel."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Подключение с помощью Excel

После создания сервера в Azure и развернуть tooit табличной модели, вы будете готовы tooconnect и приступить к изучению данных.


## <a name="connect-in-excel"></a>Подключение в Excel

Соединение сервера tooa в Excel поддерживается с помощью получения данных в Excel 2016. Подключение с помощью мастера импорта таблиц hello в PowerPivot не поддерживается. 

**tooconnect в Excel 2016**

1. В Excel 2016 hello **данные** ленты, нажмите кнопку **внешние данные** > **из других источников** > **из служб Analysis Services** .

2. В hello мастер подключения данных, в **имя сервера**, введите имя сервера hello, включая протокол и URI. Затем в **учетные данные входа в систему**выберите **hello используйте следующие имя пользователя и пароль**, а затем введите имя пользователя организации hello, например nancy@adventureworks.comи пароль.

    ![Подключение из Excel: вход](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. В **Выбор базы данных и таблицы**, выберите hello базы данных и модели или перспективе и нажмите кнопку **Готово**.
   
    ![Подключение из Excel: выбор модели](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>См. также
[Клиентские библиотеки](analysis-services-data-providers.md)   
[Управление службами Analysis Services](analysis-services-manage.md)     


