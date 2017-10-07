---
title: "aaaScale копии приложения в Azure | Документы Microsoft"
description: "Узнайте, как tooscale копирование приложения службы приложений Azure tooadd возможностей и функций."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Увеличение масштаба приложения в Azure
В этой статье показано, как tooscale приложения в службе приложений Azure. Есть два рабочих процесса для масштабирования, масштабирования вверх и масштабирование и в этой статье объясняется hello масштабирования рабочего процесса.

* [Увеличение масштаба](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) — получение дополнительных ресурсов, в частности ЦП, памяти и места на диске, и дополнительных возможностей, таких как выделенные виртуальные машины, пользовательские домены и сертификаты, промежуточные слоты, автоматическое масштабирование и т. д. Можно масштабировать, изменяя Ценовая категория плана служб приложений, к которой принадлежит приложения hello.
* [Горизонтальное масштабирование](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): увеличьте число hello экземпляров виртуальной Машины, запуск приложения.
  Можно масштабировать tooas многие как 20 экземпляров в зависимости от ценовой категории. [Среды службы приложения](../app-service/app-service-app-service-environments-readme.md) в **Premium** будет повышать уровень too50 ваших масштабирование числа экземпляров. Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md). Приведены out, как автоматическое масштабирование toouse, который автоматически tooscale число экземпляров на основе предварительно определенные правила и расписания.

Здравствуйте шкалы параметры принимают только секунд tooapply и влияют на все приложения в вашей [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Они не требуют кода вы toochange или повторного развертывания приложения.

Сведения о ценах hello и функциональных возможностях отдельных планы служб приложений см. в разделе [сведения о ценах на приложение службы](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Перед переключением план служб приложений из hello **Free** уровня, необходимо сначала удалить hello [лимиты оплаты,](https://azure.microsoft.com/pricing/spending-limits/) на месте для вашей подписки Azure. tooview или измените параметры для вашей подписки службу приложений Microsoft Azure в разделе [подписки Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Увеличение масштаба ценовой категории
1. Откройте в браузере, hello [портал Azure][portal].
2. В колонке приложения щелкните **Все параметры**, а затем — **Увеличить масштаб**.
   
    ![Перейдите tooscale копии приложения Azure.][ChooseWHP]
3. Выберите нужную категорию, а затем щелкните **Выбрать**.
   
    Hello **уведомления** вкладка будет мигать зеленым **успех** после завершения операции hello.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Масштабирование связанных ресурсов
Если приложение зависит от других служб, таких как база данных SQL Azure или служба хранилища Azure, их масштаб также можно увеличить в зависимости от ваших потребностей. Эти ресурсы не масштабируются hello план служб приложений и должен быть масштабирована отдельно.

1. В **Essentials**, нажмите кнопку hello **группы ресурсов** ссылку.
   
    ![Увеличение масштаба связанных ресурсов приложения Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. В hello **Сводка** частью hello **группы ресурсов** колонка, щелкните ресурс, что tooscale. Следующий снимок экрана приветствия показаны ресурс базы данных SQL и ресурса хранилища Azure.
   
    ![Перейдите tooscale колонке группы tooresource копии приложения Azure](./media/web-sites-scale/ResourceGroup.png)
3. Ресурс базы данных SQL, щелкните **параметры** > **Ценовая категория** tooscale hello ценовой категории.
   
    ![Вертикальное масштабирование hello серверной базы данных SQL для приложения Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    Можно также включить [георепликацию](../sql-database/sql-database-geo-replication-overview.md) для экземпляра базы данных SQL.
   
    Для ресурса хранилища Azure, нажмите кнопку **параметры** > **конфигурации** tooscale копирование возможности хранения данных.
   
    ![Вертикальное масштабирование учетной записи хранилища Azure hello, используемые приложением Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Возможности для разработчика
В зависимости от ценового уровня hello hello ориентированные на разработчиков доступны следующие функции:

### <a name="bitness"></a>Разрядность
* Hello **основные**, **Стандартная**, и **Premium** уровни поддержки 64-разрядных и 32-разрядных приложений.
* Hello **Free** и **Shared** плана уровней поддерживает только 32-разрядных приложений.

### <a name="debugger-support"></a>Поддержка отладчика
* Поддержка отладчика для hello **Free**, **Shared**, и **основные** режимов в одно подключение для каждого плана служб приложений.
* Поддержка отладчика для hello **Стандартная** и **Premium** режимов в пяти одновременных подключений на план служб приложений.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Дополнительные возможности
* Подробные сведения обо всех hello оставшихся возможности службы приложения hello схем, включая цены и признаки пользователей tooall процентов (включая разработчиков), см. [сведения о ценах на приложение службы](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/) где немедленно создать кратковременных начальный веб-приложения в службе приложений. Не требуется никаких кредитных карт и обязательств.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Дальнейшие действия
* tooget работу с Azure, в разделе [бесплатная пробная версия Microsoft](https://azure.microsoft.com/pricing/free-trial/).
* Сведения о ценах, поддержка и соглашение об уровне ОБСЛУЖИВАНИЯ посетите следующие ссылки hello.
  
    [Сведения о ценах — передача данных](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Планы поддержки Microsoft Azure](https://azure.microsoft.com/support/plans/)
  
    [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/)
  
    [Сведения о ценах — база данных SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Размеры виртуальных машин и облачных служб для Microsoft Azure][vmsizes]
  
    [Сведения о ценах на службу приложений](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Сведения о ценах на службу приложений — SSL-соединения](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Рекомендации по использованию службы приложений Azure, в том числе по созданию масштабируемой и устойчивой архитектуры, см. [здесь](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Видео о масштабировании приложения служб приложений см. следующие ресурсы hello.
  
  * [Если tooScale веб-сайтов Azure - с (Stefan Schackow)](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Стефан Шаков (Stefan Schackow). Автоматическое масштабирование веб-сайтов Azure, ЦП или по расписанию](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Стефан Шаков (Stefan Schackow). Как масштабируются веб-сайты Azure](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
