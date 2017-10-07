---
title: "aaaAnalyze данные в хранилище Озера данных с помощью Power BI | Документы Microsoft"
description: "Использование данных tooanalyze Power BI в хранилище Озера данных Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Анализ данных в хранилище озера данных с помощью Power BI
В этой статье вы узнаете, как tooanalyze toouse Power BI Desktop и визуализации данных, хранящихся в хранилище Озера данных Azure.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись хранилища озера данных Azure**. Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md). В этой статье предполагается, что вы уже создали хранилища Озера данных учетную запись, **mybidatalakestore**и загрузить образец файла данных (**Drivers.txt**) tooit. Этот образец файла можно скачать в [репозитории Git для озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. Это средство можно скачать в [Центре загрузки Майкрософт](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Создание отчета в Power BI Desktop
1. Запустите Power BI Desktop на своем компьютере.
2. Из hello **Главная** ленты, нажмите кнопку **получить данные**и нажмите кнопку больше. В hello **получить данные** диалоговое окно, нажмите кнопку **Azure**, нажмите кнопку **хранилища Озера данных Azure**и нажмите кнопку **Connect**.
   
    ![Подключение хранилища Озера tooData](./media/data-lake-store-power-bi/get-data-lake-store-account.png "хранилища Озера tooData Connect")
3. Если отображается диалоговое окно о соединителе hello, он находится в стадии разработки, необязательно toocontinue.
4. В hello **хранилища Озера данных Microsoft Azure** диалоговое окно, укажите учетную запись хранилища Озера данных tooyour, hello URL-адрес и нажмите кнопку **ОК**.
   
    ![URL-адрес для Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL-адрес для Data Lake Store")
5. В следующем диалоговое окно «hello», щелкните **входа в** toosign в учетную запись хранилища Озера данных. Будет перенаправлен на страницу входа организации tooyour. Выполните запросы toosign hello учитывается hello.
   
    ![Вход в Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Вход в Data Lake Store")
6. Успешно выполнив вход, нажмите кнопку **Подключиться**.
   
    ![Подключение хранилища Озера tooData](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "хранилища Озера tooData Connect")
7. следующее окно Hello показан файл hello, отправленный учетной записи хранилища Озера данных tooyour. Проверьте сведения о hello и нажмите кнопку **нагрузки**.
   
    ![Скачивание данных из Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Скачивание данных из Data Lake Store")
8. После hello данных был успешно загружен в Power BI, вы увидите следующие поля в hello hello **поля** вкладки.
   
    ![Импортированные поля](./media/data-lake-store-power-bi/imported-fields.png "Импортированные поля")
   
    Тем не менее toovisualize и анализировать данные hello, желательно toobe hello данных, доступных для следующих полей hello
   
    ![Нужные поля](./media/data-lake-store-power-bi/desired-fields.png "Нужные поля")
   
    В следующих шагах hello мы обновим hello запроса tooconvert hello импорта данных в нужный формат hello.
9. Из hello **Главная** ленты, нажмите кнопку **изменить запросы**.
   
    ![Изменение запросов](./media/data-lake-store-power-bi/edit-queries.png "Изменение запросов")
10. В hello редактора запросов в группе hello **содержимого** столбец, нажмите кнопку **двоичных**.
    
    ![Изменение запросов](./media/data-lake-store-power-bi/convert-query1.png "Изменение запросов")
11. Появится значок файла, который представляет hello **Drivers.txt** загруженного файла. Щелкните правой кнопкой мыши файл hello и нажмите кнопку **CSV**.    
    
    ![Изменение запросов](./media/data-lake-store-power-bi/convert-query2.png "Изменение запросов")
12. В результате вы увидите выходные данные, приведенные ниже. Данные в формате, которые можно использовать визуализации toocreate теперь доступен.
    
    ![Изменение запросов](./media/data-lake-store-power-bi/convert-query3.png "Изменение запросов")
13. Из hello **Главная** ленты, нажмите кнопку **закрыть и применить**, а затем нажмите кнопку **закрыть и применить**.
    
    ![Изменение запросов](./media/data-lake-store-power-bi/load-edited-query.png "Изменение запросов")
14. После обновления запроса hello, hello **поля** вкладка отображает hello новые поля, доступные для визуализации.
    
    ![Обновление полей](./media/data-lake-store-power-bi/updated-query-fields.png "Обновление полей")
15. Давайте создадим toorepresent круговой диаграммы драйверы hello в каждом городе в каждой стране. Таким образом, toodo сделать hello следующих элементов.
    
    1. На вкладке визуализации hello щелкните символ hello для круговой диаграммы.
       
        ![Создание круговой диаграммы](./media/data-lake-store-power-bi/create-pie-chart.png "Создание круговой диаграммы")
    2. Hello столбцы, которые мы будем являются toouse **столбца 4** (имя hello Город) и **столбца 7** (имя страны hello). Перетащите следующие столбцы из **поля** вкладке слишком**визуализации** вкладки, как показано ниже.
       
        ![Создание визуализации](./media/data-lake-store-power-bi/create-visualizations.png "Создание визуализации")
    3. Круговая диаграмма Hello должен выглядеть как hello, показанной ниже.
       
        ![Круговая диаграмма](./media/data-lake-store-power-bi/pie-chart.png "Создание визуализаций")
16. Выбрав конкретной стране фильтры уровня страницы hello, теперь видно hello количество драйверов, в каждом городе hello выбранной страны. Например, в разделе hello **визуализации** в разделе **фильтры уровня страницы**выберите **Бразилия**.
    
    ![Выбор страны](./media/data-lake-store-power-bi/select-country.png "Выбор страны")
17. Круговая диаграмма Hello — драйверы hello toodisplay автоматически обновляются в городах hello Бразилии.
    
    ![Количество водителей в стране](./media/data-lake-store-power-bi/driver-per-country.png "Количество водителей в каждой стране")
18. Из hello **файл** меню, нажмите кнопку **Сохранить** toosave визуализации hello в файл Power BI Desktop.

## <a name="publish-report-toopower-bi-service"></a>Публикация отчетов tooPower бизнес-Аналитики службы
После создания hello визуализации в Power BI Desktop можно поделиться с другими, опубликовав toohello службы Power BI. Дополнительные сведения о toodo, в разделе [публикация из Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>См. также
* [Анализ данных в хранилище озера данных с помощью Аналитики озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

