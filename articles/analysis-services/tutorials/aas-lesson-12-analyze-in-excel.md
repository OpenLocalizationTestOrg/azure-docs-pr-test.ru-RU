---
Заголовок: aaa «занятие учебника Azure Analysis Services 12: анализ в Excel | Документы Microsoft» Описание: описание как toouse анализ в Excel в hello Azure служб Analysis Services учебного проекта. службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>Занятие 12. Анализ в Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии использовать hello анализ в Excel функции tooopen Microsoft Excel, автоматически создать рабочую область модели toohello подключения и автоматически добавлять на лист toohello сводной таблицы. Hello анализ в Excel предназначена tooprovide быстрый и простой способ tootest hello эффективность модели разрабатывается предыдущих toodeploying модель. В этом занятии выполнять анализ данных не нужно. Hello цель этого занятия — toofamiliarize, создавать модели hello, hello средства можно использовать tootest структуре модели.   
  
toocomplete этого занятия Excel должны быть установлены на hello же компьютере, что SSDT.
  
Предполагаемое время toocomplete на этом занятии: **пять минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятие 11: Создание ролей](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Просмотр с помощью перспективы по умолчанию и Интернет-продаж hello  
В этих первых задачах вы просмотрите модель как с помощью обоих hello Перспектива по умолчанию, которая включает все объекты модели, так и с использованием перспективы Internet Sales hello вы ранее. Hello перспективы Internet Sales исключает объект таблицы Customer hello.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse с помощью перспективы по умолчанию hello  
  
1.  Нажмите кнопку hello **модель** меню > **анализ в Excel**.  
  
2.  В hello **анализ в Excel** диалоговое окно, нажмите кнопку **ОК**.  
  
    В Excel открывается новая книга. Соединение с источником данных создается с использованием учетной записи текущего пользователя hello и hello Перспектива по умолчанию является toodefine используется для просмотра поля. Сводная таблица автоматически добавляется toohello листа.  
  
3.  В Excel в hello **список полей сводной таблицы**, уведомление hello **DimDate** и **FactInternetSales** отображаются группы мер. Hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, и **FactInternetSales** также отображаются в соответствующих столбцах таблицы.  
  
4.  Закройте Excel без сохранения книги hello.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse с помощью перспективы Internet Sales hello  
  
1.  Нажмите кнопку hello **модель** меню, а затем нажмите **анализ в Excel**.  
  
2.  В hello **анализ в Excel** диалоговое окно, оставьте **текущего пользователя Windows** выбрано в hello **перспективы** раскрывающемся списке выберите **продажи через Интернет** , а затем нажмите кнопку **ОК**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  В Excel в **полей сводной таблицы**, обратите внимание на то, таблица DimCustomer hello исключается из списка полей hello.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Закройте Excel без сохранения книги hello.  
  
## <a name="browse-by-using-roles"></a>Просмотр с помощью ролей  
Роли — это неотъемлемая часть любой табличной модели. Без хотя бы одну роль toowhich пользователи будут добавлены, пользователи не могут получить доступ к и анализировать данные с использованием модели. Hello анализ в Excel предоставляет способ для вас tootest hello роли, которые вы определили.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse с помощью роли пользователя менеджера по продажам hello  
  
1.  В SSDT выберите hello **модель** меню, а затем нажмите **анализ в Excel**.  
  
2.  В **укажите hello имя или роль toouse tooconnect toohello модели пользователя**выберите **роли**и выберите в раскрывающемся списке hello, **менеджера по продажам**и нажмите кнопку  **ОК**.  
  
    В Excel открывается новая книга. Автоматически создается сводная таблица. Hello список полей сводной таблицы включает все поля данных hello, доступные в новой модели.  
      
3.  Закройте Excel без сохранения книги hello.  
  
## <a name="whats-next"></a>Что дальше?
Последовательно выберите toohello занятию: [занятие 13: развертывание](../tutorials/aas-lesson-13-deploy.md).

  
  
  
