---
title: "Учебник aaaPower бизнес-Аналитики для соединителя Azure Cosmos DB | Документы Microsoft"
description: "Использовать этот учебник tooimport Power BI JSON, создания полезных отчетов и визуализации данных с помощью соединителя Azure Cosmos DB и Power BI hello."
keywords: "учебник по Power BI, визуализация данных, соединитель Power BI"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Power BI учебник по Azure Cosmos DB: визуализировать данные с помощью hello соединитель Power BI
[PowerBI.com](https://powerbi.microsoft.com/) — это сетевая служба, в которой можно создавать и совместно использовать панели мониторинга и отчеты с данными, важные tooyou и вашей организации.  Power BI Desktop — выделенное средство разработки tooretrieve данные отчета из различных источников данных, слияния и преобразования данных hello, создавать мощные отчеты и визуализации и публиковать отчеты hello tooPower бизнес-Аналитики.  Hello последнюю версию Power BI Desktop теперь можно подключиться учетной записи Cosmos DB tooyour через соединитель Cosmos DB hello для Power BI.   

В этом учебнике Power BI мы перемещайтесь hello действия tooconnect tooa Cosmos DB учетной записи в Power BI Desktop, переходы tooa коллекции, где мы хотим tooextract hello данных, с помощью hello навигатор, преобразование данных JSON в табличном формате, с помощью Power BI Desktop запроса Редактор и сборки и повторно опубликовать tooPowerBI.com отчета.

После завершения этого учебника Power BI, вы будете иметь доступ tooanswer hello следующие вопросы:  

* Как создавать отчеты с данными из Azure Cosmos DB с помощью Power BI Desktop?
* Как подключаться учетной записи Cosmos DB tooa в Power BI Desktop?
* Как получить данные из коллекции в Power BI Desktop?
* Как преобразовывать вложенные данные JSON в Power BI Desktop?
* Как публиковать и совместно использовать отчеты в PowerBI.com?

> [!NOTE]
> Соединитель Power BI Hello для Azure Cosmos DB подключается tooPower BI Desktop для извлечения и преобразования данных. Отчеты, созданные в Power BI Desktop можно затем опубликованных tooPowerBI.com. Невозможно напрямую извлекать и преобразовывать данные Azure Cosmos DB на сайте PowerBI.com. 

## <a name="prerequisites"></a>Предварительные требования
Перед выполнением инструкции hello в этом учебнике Power BI, убедитесь, что доступ toohello следующие ресурсы:

* [последнюю версию Power BI Desktop Hello](https://powerbi.microsoft.com/desktop).
* Учетная запись доступа к tooour Демонстрация или данных в вашей учетной записи Cosmos DB.
  * Учетная запись Демонстрация Hello заполняется данными вулканов hello, показанными в данном руководстве. Использование этой демонстрационной учетной записи не регулируется соглашениями об уровне обслуживания. Она предназначена только для демонстрационных целей.  Мы оставляем за hello правой toomake изменения toothis демонстрационной учетной записи включая, но не ограничиваясь, завершается hello учетной записи, ключ hello, ограничивая доступ, изменение, изменение и удаление данных hello в любое время без уведомления или по причине.
    * URL-адрес: https://analytics.documents.azure.com
    * Ключ только для чтения: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * Или toocreate свою учетную запись в разделе [создать учетную запись базы данных Azure Cosmos DB hello портал Azure с помощью](https://azure.microsoft.com/documentation/articles/create-account/). Затем, используемые в этом учебнике tooget образец вулканов данные, аналогичные toowhat (но не содержит блоки GeoJSON hello) см. в разделе hello [сайта NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) , а затем импортировать данные hello, с помощью hello [переноса данных Azure Cosmos DB средство](import-data.md).

tooshare отчетов на сайте PowerBI.com, необходимо настроить учетную запись на сайте PowerBI.com.  Посетите toolearn Дополнительные сведения о Power BI для бесплатных и Power BI Pro [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Начало работы
В этом учебнике Предположим, что вы являетесь geologist, изучения вулканов вокруг Здравствуй, мир.  Hello вулканов данные хранятся в учетной записи Cosmos DB и документы JSON hello выглядят как hello следующий образец документа.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Вы хотите tooretrieve hello вулканов данные hello Cosmos DB учетной записи и визуализации данных в интерактивный отчет Power BI как hello, следуя отчета.

![Выполнив этот учебник Power BI, соединитель Power BI hello, вы будете может toovisualize данных с помощью hello вулканов отчет Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Все готово toogive ему try? Давайте приступим.

1. Запустите на своей рабочей станции Power BI Desktop.
2. После запуска Power BI Desktop появится экран *приветствия* .
   
    ![Экран приветствия в Power BI Desktop — соединитель Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. Вы можете **получить данные**, в разделе **последние источники**, или **открыть другие отчеты** непосредственно из hello *приветствия* экрана.  Щелкните hello X tooclose hello hello правом верхнем углу экрана. Hello **отчетов** появляется представление Power BI Desktop.
   
    ![Представление отчета в Power BI Desktop — соединитель Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Выберите hello **Главная** ленты, а затем нажмите **получение данных**.  Hello **получить данные** должно появиться окно.
5. Выберите **Azure**, затем — **Microsoft Azure DocumentDB (Beta)** и щелкните **Подключение**. 

    ![Получение данных в Power BI Desktop — соединитель Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. На hello **предварительной версии соединителя** щелкните **Продолжить**. Hello **Microsoft Azure DocumentDB Connect** появится окно.
7. Укажите hello Cosmos DB конечной точки URL-адреса будет как tooretrieve hello данные, как показано ниже и нажмите кнопку **ОК**. toouse свою учетную запись можно получить hello, введите URL-адрес из hello URI в hello  **[ключей](manage-account.md#keys)**  колонке hello портал Azure. toouse hello демонстрационных учетной записи, введите `https://analytics.documents.azure.com` для hello URL-адреса. 
   
    Не указывайте hello имя базы данных, имя коллекции и инструкцию SQL, как эти поля являются необязательными.  Вместо этого мы используем hello навигатор tooselect hello базу данных и коллекцию tooidentify источника данных hello.
   
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — окно подключения рабочего стола](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. При подключении toothis конечную точку для hello первый раз, появится для hello ключ учетной записи. Для собственной учетной записи, извлечь ключ hello из hello **первичного ключа** поле в hello  **[ключей только для чтения](manage-account.md#keys)**  колонке hello портал Azure. Учетной записи Демонстрация hello hello ключ является `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Введите соответствующий ключ hello и нажмите кнопку **Connect**.
   
    Мы рекомендуем использовать hello ключа, доступного только для чтения, при построении отчетов.  Это позволит избежать лишнего доступа угрозы безопасности toopotential hello главного ключа. из hello доступен только для чтения ключ Hello [ключей](manage-account.md#keys) колонке hello портал Azure, или можно использовать приведенные выше сведения учетной записи Демонстрация hello.
   
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — ключ учетной записи](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Если вы получаете сообщение об ошибке: «hello указанной базы данных не найден.» см. инструкции по решению hello шаги в этом [Power BI проблема](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Здравствуйте, когда учетная запись hello успешно подключен, **Навигатор** будут отображаться.  Hello **Навигатор** отобразит список баз данных под учетной записью hello.
10. Выберите и разверните hello базы данных, где данные hello hello отчетов будет получен из, если вы используете учетную запись Демонстрация hello, рекомендуется выбрать **volcanodb**.   
11. Теперь выберите коллекцию, который будет извлекать данные hello. Если вы используете учетную запись Демонстрация hello, выберите **volcano1**.
    
    Hello область просмотра отображается список **записи** элементов.  Документ представлен как тип **Запись** в Power BI. Точно так же вложенный блок JSON в документе является **Записью**.
    
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — окно навигатора](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Нажмите кнопку **изменить** toolaunch hello редактора запросов в новых данных hello tootransform окна.

## <a name="flattening-and-transforming-json-documents"></a>Преобразование документов JSON в плоскую структуру и их трансформация
1. Переключение окна редактора запросов Power BI toohello, где hello **документа** столбец в центральной области hello.
   ![Редактор запросов Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Щелкните расширитель hello в правой стороне hello hello **документа** заголовок столбца.  Появится контекстное меню Hello со списком полей.  Выберите hello поля, необходимые для отчета, например, вулканов имя, Страна, регион, расположение, повышение прав, тип, состояние и временем последнего знать и нажмите кнопку **ОК**.
   
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — раскрыть документы](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. Hello центральной области будут отображаться Предварительный просмотр результатов hello с выбранных полей hello.
   
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — сделать результаты более плоскими](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. В нашем примере hello свойство Location — это блок GeoJSON в документе.  Как видно, значение свойства «Расположение» представлено типом **Запись** в Power BI Desktop.  
5. Щелкните расширитель hello в правой стороне заголовок столбца расположения hello hello.  Появится контекстное меню Hello с полями типа и координаты.  Давайте выберите поля координат hello и нажмите кнопку **ОК**.
   
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — запись о расположении](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Hello center панели отображается столбец координаты **списка** типа.  Как показано в начале hello учебника hello hello данных GeoJSON в этом учебнике имеет тип точки с широты и долготы значениям, записанным в массиве координаты hello.
   
    элемент Hello координаты [0] представляет долготу, а координаты [1] представляет широту.
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — список координат](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Массив координат tooflatten hello, мы создадим **настраиваемый столбец** вызывается LatLong.  Выберите hello **добавить столбец** ленты и выберите команду **добавить настраиваемый столбец**.  Hello **добавить настраиваемый столбец** должно появиться окно.
8. Введите имя для нового столбца hello, например LatLong.
9. Затем укажите hello пользовательской формулы для нового столбца hello.  В нашем примере мы объединить hello широты и долготы значения, разделенные запятой, как показано ниже, с помощью hello следующую формулу: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Нажмите кнопку **ОК**.
   
    Дополнительные сведения о выражениях анализа данных (DAX), включая функции DAX, см. в статье [Основные сведения о DAX в Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — добавление пользовательского столбца](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Теперь hello центральной области отображается hello новый LatLong столбец заполняется hello широты и долготы значений, разделенных запятыми.
    
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — пользовательский столбец LatLong](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Если произошла ошибка в новом столбце hello, убедитесь, что, посвященный hello применены параметры запроса совпадают hello следующий рисунок:
    
    ![Примененные шаги должны быть такими: источник, навигация, развернут документ, развернуто расположение документа, добавлен настраиваемый элемент](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Если шагов не совпадают, удалить hello дополнительные действия и снова попробуйте добавить настраиваемый столбец hello. 
11. Теперь мы завершена обработки прозрачности hello данных в табличном формате.  Можно использовать все функции hello, доступные в hello tooshape редактора запросов и преобразования данных в базу данных, Cosmos.  Если вы используете образец hello, изменить hello тип данных для повышения прав слишком**целое число** , изменив hello **тип данных** на hello **Главная** ленты.
    
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — изменение типа столбца](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Нажмите кнопку **закрыть и применить** toosave hello данных модели.
    
    ![Руководство по Power BI для соединителя Power BI Azure Cosmos DB — закрыть и применить](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Построение отчетов hello
Power BI Desktop отчет является, где можно начать создание отчетов toovisualize данных.  Можно создавать отчеты путем перетаскивания полей в hello **отчетов** холст.

![Представление отчета в Power BI Desktop — соединитель Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

В hello представления отчета следует найти:

1. Hello **поля** области, это происходит, когда вы увидите список моделей данных с полями, которые можно использовать для создания отчета.
2. Hello **визуализации** области. Отчет может содержать одну или несколько визуализаций.  Выбрать типами visual hello соответствует вашим потребностям из hello **визуализации** области.
3. Hello **отчетов** холст, это где построит hello визуальных элементов отчета.
4. Hello **отчетов** страницы. В Power BI Desktop можно добавить несколько страниц отчета.

Hello ниже показан hello основные действия по созданию простого интерактивный просмотр отчета-карты.

1. В нашем примере мы создадим карты представление, показывающее расположение каждого вулканов hello.  В hello **визуализации** щелкните hello карты тип визуального элемента как видно на снимке экрана приветствия выше.  Вы увидите hello карты тип визуального элемента закраске hello **отчетов** холст.  Hello **визуализации** панели также следует отобразить набор связанных toohello свойства тип визуального элемента карты.
2. Теперь, путем перетаскивания поля LatLong hello из hello **поля** toohello панели **расположение** свойство в **визуализации** области.
3. Далее, путем перетаскивания поля toohello hello вулканов имя **условных обозначений** свойство.  
4. Затем, путем перетаскивания поля toohello hello повышение **размер** свойство.  
5. Теперь вы увидите hello визуальных элементов, отображающих набор пузырьков, указывающее расположение каждого вулканов hello hello размер пузырька hello корреляции повышение toohello вулканов hello карты.
6. Базовый отчет готов.  Hello отчетов можно настроить, добавив дополнительные визуализации.  В нашем случае мы добавили тип вулканов среза toomake hello отчета интерактивный.  
   
    ![Снимок экрана: hello окончательный отчет Power BI Desktop, после завершения учебника hello Power BI для Azure Cosmos DB](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Публикация и совместное использование отчета
tooshare отчет, необходимо настроить учетную запись на сайте PowerBI.com.

1. Hello Power BI Desktop, щелкнуть hello **Главная** ленты.
2. Щелкните **Опубликовать**.  Будет запрашиваемые tooenter hello имя и пароль пользователя для учетной записи PowerBI.com.
3. После проверки подлинности учетных данных hello hello отчет является опубликованной tooyour расположение.
4. Нажмите кнопку **откройте «PowerBITutorial.pbix» в Power BI** toosee и предоставить доступ к отчету, на сайте PowerBI.com.
   
    ![Публикация tooPower успех BI! Открыть учебник в Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Создание панели мониторинга на PowerBI.com
Теперь, когда у вас уже есть отчет, используйте его совместно с другими пользователями на сайте PowerBI.com.

При публикации отчета из Power BI Desktop tooPowerBI.com создает **отчетов** и **Dataset** в клиенте PowerBI.com. Например, после публикации отчета под названием **PowerBITutorial** tooPowerBI.com, вы увидите в обоих hello PowerBITutorial **отчеты** и **наборы данных** разделы на PowerBI.com.

   ![Снимок экрана: hello новый отчет и набор данных на сайте PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate общий панели мониторинга щелкните hello **закрепить активную страницу** кнопку на сайте PowerBI.com отчета.

   ![Снимок экрана: hello новый отчет и набор данных на сайте PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Следуйте инструкциям hello [закрепление плитки из отчета](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate панели мониторинга. 

Также можно сделать tooreport нерегламентированных изменения, прежде чем создавать панели мониторинга. Тем не менее рекомендуется использовать Power BI Desktop tooperform hello изменений и повторная публикация отчета tooPowerBI.com hello.

## <a name="refresh-data-in-powerbicom"></a>Обновление данных на сайте PowerBI.com
Существует два способа toorefresh данные, нерегламентированные и запланированное.

Для нерегламентированных обновления, просто щелкните затмения hello (...), hello **набора данных**, например PowerBITutorial. Отобразится список доступных действий, включая **Обновить**. Нажмите кнопку **Обновить сейчас** toorefresh hello данных.

![Снимок экрана действия "Обновить" на PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Запланированное обновление hello следующие.

1. Нажмите кнопку **запланировать обновление** в список действий hello. 

    ![Снимок экрана: hello расписание обновлений на сайте PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. В hello **параметры** разверните **учетные данные источника данных**. 
3. Щелкните **Изменить учетные данные**. 
   
    Появится всплывающее окно Настройка Hello. 
4. Введите hello ключа tooconnect toohello Cosmos DB запись для этого набора данных, а затем нажмите кнопку **входа**. 
5. Разверните **запланировать обновление** и настроить расписание hello требуется toorefresh hello dataset. 
6. Нажмите кнопку **применить** и больше не требуется настройка запланированного обновления hello.

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о Power BI в разделе [Приступая к работе с Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn Дополнительные сведения о Cosmos DB. в разделе hello [целевой страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

