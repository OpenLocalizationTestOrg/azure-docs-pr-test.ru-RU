---
Заголовок: aaa «занятие учебника Azure Analysis Services 13: развертывание | Документы Microsoft» Описание: описание как учебника hello toodeploy проекта служб Analysis Services tooAzure.
службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''

MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: ms.author 07-17/2017 г.: owend
---
# <a name="lesson-13-deploy"></a>Занятие 13. Развертывание

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

На этом занятии вы настройку свойств развертывания; Указание tooand toodeploy сервера Azure Analysis Services имя модели hello. Затем можно развернуть экземпляр toothat hello модели. После развертывания модели, пользователи могут подключаться tooit с помощью клиентского приложения создания отчетов. toolearn более, в разделе [развертывания служб Analysis Services tooAzure](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Предполагаемое время toocomplete на этом занятии: **5 минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 12: анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Необходимо иметь [разрешения администратора](../analysis-services-server-admins.md) on hello удаленных служб Analysis Services server toodeploy по порядку tooit.  

> [!IMPORTANT]  
> Если вы установили hello AdventureWorksDW2014 образца базы данных на локальном сервере SQL, и вы развертываете tooan служб Azure Analysis server модели, [локального шлюза данных](../analysis-services-gateway.md) является обязательным.
  
## <a name="deploy-hello-model"></a>Развертывание модели hello  
  
#### <a name="tooconfigure-deployment-properties"></a>Свойства развертывания tooconfigure  

  
1.  В **обозревателе решений**, щелкните правой кнопкой мыши hello **Интернет-продаж AW** проекта, а затем нажмите кнопку **свойства**.  
  
2.  В hello **страницы свойств Интернет-продаж AW** диалогового **сервер развертывания**, в hello **сервера** свойство, введите полный адрес сервера hello.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  В hello **базы данных** введите **Интернет-продаж Adventure Works**.  
  
4.  В hello **Имя_модели** введите **модель Интернет-продаж Adventure Works**.  
  
5.  Проверьте выбранные параметры и нажмите кнопку **ОК**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>hello toodeploy Интернет-продаж Adventure Works
  
1.  В **обозревателе решений**, щелкните правой кнопкой мыши hello **Интернет-продаж AW** проекта > **сборки**.  

2.  Щелкните правой кнопкой мыши hello **Интернет-продаж AW** проекта > **развернуть**.

    При развертывании служб Analysis Services tooAzure, может быть запрос tooenter вашей учетной записи. Укажите свою учетную запись в организации и пароль, например nancy@adventureworks.com. Это учетная запись должна быть в "Администраторы" на сервере hello.
  
    Развернуть Hello-диалоговое окно появляется и отображает состояние развертывания метаданных hello hello и каждая таблица, включенная в модель hello.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. После успешного завершения развертывания нажмите кнопку **Закрыть**.  
  
## <a name="conclusion"></a>Заключение  
Поздравляем! Вы создали и развернули свою первую табличную модель служб Analysis Services. Этот учебник помог вам выполнения типичных задач hello при создании табличной модели. Теперь, когда модель Интернет-продаж Adventure Works развернута, можно использовать SQL Server Management Studio toomanage hello модели; Создание скриптов обработки и плана резервного копирования. Теперь также позволяет пользователям подключаться toohello модели, с помощью клиентского приложения создания отчетов, таких как Microsoft Excel или Power BI.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Что дальше?
[Подключение с помощью Power BI](../analysis-services-connect-pbi.md)   
[Дополнительное занятие. Динамическая безопасность](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Дополнительное занятие. Строки детализации](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Дополнительное занятие. Неоднородные иерархии](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
