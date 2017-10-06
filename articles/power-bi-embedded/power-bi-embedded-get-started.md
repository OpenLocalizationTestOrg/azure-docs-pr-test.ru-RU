---
title: "aaaGet работы с Microsoft Power BI Embedded"
description: "Power BI Embedded, добавление интерактивных отчетов Power BI в приложение бизнес-аналитики"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Начало работы с Microsoft Power BI Embedded

**Power BI Embedded** — это служба Azure, tooadd разработчики приложений включает интерактивных отчетов Power BI в собственные приложения. **Power BI Embedded** входа работает с существующие приложения без необходимости переработки и изменение пользователей hello.

Ресурсы для **Microsoft Power BI Embedded** подготовленные в hello [API-интерфейсов Azure ARM](https://msdn.microsoft.com/library/mt712306.aspx). В этом случае является подготовка ресурсов hello **коллекции рабочей области Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Создание коллекции рабочей области

Объект **коллекции рабочей** hello верхнего уровня ресурсов Azure и контейнер для содержимого hello, который будет внедрен в приложении. **Коллекцию рабочей области** можно создать двумя способами:

* Вручную с помощью портала Azure hello
* Программно с помощью API-интерфейсов Manager(ARM) ресурсов Azure hello

Давайте рассмотрим hello действия toobuild **коллекции рабочей** с помощью портала Azure "hello".

1. Войдите на **портал Azure**по адресу [http://portal.azure.com](http://portal.azure.com).
2. Нажмите кнопку **+ создать** на верхней панели hello.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. В разделе **Данные+аналитика** щелкните **Power BI Embedded**.
4. На hello **колонке коллекции рабочей**, введите hello необходимые сведения. Дополнительные сведения о **ценообразовании** см. на странице с информацией о [ценах на Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Щелкните **Создать**.

Hello **коллекции рабочей** займет несколько секунд tooprovision. После завершения вы будете перенаправлены toohello **колонке коллекции рабочей**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Hello **создания колонке** содержит hello информацию, необходимую hello toocall API-интерфейсы, создание рабочих областей и развертывание содержимого toothem.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Просмотр ключей доступа для вызова API Power BI

Одно из наиболее важные части информации, необходимой toocall hello интерфейсы API REST Power BI hello, hello **клавиши доступа**. Ниже перечислены используемые toogenerate hello **токенов приложения** таблицы, используемые tooauthenticate запросов API. tooview вашей **клавиши доступа**, нажмите кнопку **клавиши доступа** на hello **колонку параметров**. Дополнительные сведения о **маркерах приложений** см. в статье [Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Обратите внимание: у вас есть два ключа.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Скопируйте эти ключи и надежно сохраните их в приложении. Очень важно, можно обработать эти ключи как пароль, так как они будут позволяют получать доступ к содержимому hello tooall в вашей **рабочей коллекции**.

Хотя указаны два ключа, в один момент времени используется только один из них. второй ключ Hello предоставляется, можно периодически повторного создания ключей без прерывания работы служб toohello доступа.

Теперь, когда у вас есть экземпляр Power BI для приложения и **ключи доступа**, вы можете импортировать отчет в свое приложение. Прежде чем вы узнаете, как tooimport отчет hello следующий раздел описывает создание tooembed наборы данных и отчеты Power BI в приложение.

## <a name="working-with-workspaces"></a>Работа с рабочими областями

После создания коллекции рабочей области потребуется toocreate рабочей области, где будет размещена отчеты и наборы данных. toocreate рабочей области потребуется toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Создание tooembed наборы данных и отчеты Power BI в приложение с помощью Power BI Desktop

Вы создали экземпляр Power BI для приложения и наличии **клавиши доступа**, вам понадобится toocreate hello Power BI, наборы данных и отчеты, которые должны tooembed. Наборы данных и отчеты можно создавать с помощью **Power BI Desktop**. [Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662) можно скачать бесплатно. Или, tooquickly приступить к работе, вы можете загрузить hello [PBIX пример анализа розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> Дополнительные сведения о том, как toolearn toouse **Power BI Desktop**, в разделе [Приступая к работе с Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

С **Power BI Desktop**, подключите tooyour источника данных путем импорта копии данных hello в **Power BI Desktop** или непосредственное подключение toohello данных источника с помощью **DirectQuery**.

Ниже приведены hello различия между использованием **импорта** и **DirectQuery**.

| Импорт | DirectQuery |
| --- | --- |
| Таблицы, столбцы *и данные* импортируются или копируются в **Power BI Desktop**. При работе с визуализациями, **Power BI Desktop** запрашивает копию данных hello. toosee всех изменений, произошедших toohello базовых данных, необходимо обновить или импортировать завершения, текущее набора данных еще раз. |В *Power BI Desktop* импортируются или копируются только **таблицы и столбцы**. При работе с визуализациями, **Power BI Desktop** запросы hello базового источника данных, поэтому вы всегда просматриваете актуальные данные. |

Дополнительные сведения о подключении источника данных tooa см. в разделе [подключить источник данных tooa](power-bi-embedded-connect-datasource.md).

Когда вы сохраните документ в **Power BI Desktop**, будет создан PBIX-файл. Этот файл содержит ваш отчет. Кроме того, при импорте данных hello pbix-ФАЙЛ содержит hello всего набора данных, или если вы используете **DirectQuery**, hello pbix-ФАЙЛ содержит только схему набора данных. Программным способом развертывания hello pbix-ФАЙЛ в рабочую область с помощью hello [импорта API Power BI](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** имеет дополнительные интерфейсы API toochange hello сервера и базы данных, что набор данных указывает tooand набор учетных данных учетной записи службы, hello набор данных будет использовать базу данных tooyour tooconnect. Дополнительные сведения см. в статьях [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) (Публикация SetAllConnections) и [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (Исправление источника данных шлюза).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Создание наборов данных и отчетов Power BI с помощью API

### <a name="datsets"></a>Наборы данных

Можно создать наборы данных в Power BI Embedded с помощью API-интерфейса REST hello. Затем данные можно передать в свой набор данных. Это позволяет toowork с данными без необходимости hello Power BI Desktop. Дополнительные сведения см. в статье о [публикации наборов данных](https://msdn.microsoft.com/library/azure/mt778875.aspx).

### <a name="reports"></a>Отчеты

Можно создать отчет из набора данных непосредственно в приложение с помощью hello JavaScript API. Дополнительные сведения см. в статье [Создание отчета из набора данных в Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).

## <a name="see-also"></a>См. также

[Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Внедрение отчета в Power BI Embedded](power-bi-embedded-embed-report.md)  
[Создание отчета из набора данных в Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Сохранение отчетов в Power BI Embedded](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)

