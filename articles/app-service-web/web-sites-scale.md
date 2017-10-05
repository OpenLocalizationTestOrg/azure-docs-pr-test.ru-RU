---
title: "Увеличение масштаба приложения в Azure | Документация Майкрософт"
description: "Узнайте, как увеличить масштаб приложения в службе приложений Azure для добавления емкости и расширения функций."
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a>Увеличение масштаба приложения в Azure
В этой статье показано, как масштабировать приложение в службе приложений Azure. Существует два рабочих процесса масштабирования (увеличение масштаба и развертывание), и в этой статье рассматривается первый из них.

* [Увеличение масштаба](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) — получение дополнительных ресурсов, в частности ЦП, памяти и места на диске, и дополнительных возможностей, таких как выделенные виртуальные машины, пользовательские домены и сертификаты, промежуточные слоты, автоматическое масштабирование и т. д. Чтобы увеличить масштаб приложения, следует изменить ценовую категорию плана службы приложений, к которому относится ваше приложение.
* [Развертывание](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling) — увеличение количества экземпляров виртуальных машин, на которых работает приложение.
  В зависимости от ценовой категории вы можете развернуть приложение на виртуальных машинах в количестве до 20 экземпляров. Использование [сред службы приложений](../app-service/app-service-app-service-environments-readme.md) на уровне **Премиум** позволит увеличить количество экземпляров до 50. Дополнительные сведения см. в статье [Масштабирование числа экземпляров вручную или автоматически](../monitoring-and-diagnostics/insights-how-to-scale.md). В ней вы узнаете, как использовать автомасштабирование, которое позволяет масштабировать число экземпляров автоматически на основе предварительно определенных правил и расписаний.

Применение этих параметров масштаба занимает всего несколько секунд, но они влияют на все приложения в вашем [плане службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Для этого не требуется вносить изменения в код или повторно развертывать приложение.

Сведения о ценах и функциях отдельных планов службы приложений см. [здесь](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Прежде чем сменить уровень **Бесплатный** для плана службы приложений, следует снять имеющиеся [ограничения на расходы](https://azure.microsoft.com/pricing/spending-limits/), установленные для вашей подписки Azure. Просмотреть или изменить параметры подписки на службу приложений Microsoft Azure можно на странице [подписок Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Увеличение масштаба ценовой категории
1. В браузере откройте [портал Azure][portal].
2. В колонке приложения щелкните **Все параметры**, а затем — **Увеличить масштаб**.
   
    ![Переход для увеличения масштаба приложения Azure][ChooseWHP]
3. Выберите нужную категорию, а затем щелкните **Выбрать**.
   
    После завершения операции на вкладке **Уведомления** появится зеленая надпись **Выполнено**.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Масштабирование связанных ресурсов
Если приложение зависит от других служб, таких как база данных SQL Azure или служба хранилища Azure, их масштаб также можно увеличить в зависимости от ваших потребностей. Эти ресурсы не масштабируется с планом службы приложений и должны масштабироваться отдельно.

1. В разделе **Основное** щелкните ссылку **Группа ресурсов**.
   
    ![Увеличение масштаба связанных ресурсов приложения Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. В области **Сводка** колонки**Группа ресурсов** щелкните ресурс, который нужно масштабировать. На приведенном ниже снимке экрана показаны ресурс базы данных SQL и ресурс службы хранилища Azure.
   
    ![Переход в колонку группы ресурсов для увеличения масштаба приложения Azure](./media/web-sites-scale/ResourceGroup.png)
3. Для ресурса базы данных SQL щелкните **Параметры** > **Ценовая категория**, чтобы изменить ценовую категорию.
   
    ![Увеличение масштаба внутреннего сервера базы данных SQL для приложения Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    Можно также включить [георепликацию](../sql-database/sql-database-geo-replication-overview.md) для экземпляра базы данных SQL.
   
    Для ресурса службы хранилища Azure щелкните **Параметры** > **Конфигурация**, чтобы изменить возможности хранилища.
   
    ![Увеличение масштаба учетной записи хранения Azure, используемой приложением Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Возможности для разработчика
В зависимости от ценовой категории будут доступны следующие возможности для разработчиков.

### <a name="bitness"></a>Разрядность
* Уровни **Базовый**, **Стандартный** и **Премиум** поддерживают 64-разрядные и 32-разрядные приложения.
* Уровни **Бесплатный** и **Общий** поддерживают только 32-разрядные приложения.

### <a name="debugger-support"></a>Поддержка отладчика
* Отладчик поддерживается на уровнях **Бесплатный**, **Общий** и **Базовый** для одного подключения на план службы приложений.
* Отладчик поддерживается на уровнях **Стандартный** и **Премиум** для пяти одновременных подключений на план службы приложений.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Дополнительные возможности
* Подробные сведения обо всех оставшихся функциях в планах службы приложений, включая цены и функции, интересующие всех пользователей (в том числе разработчиков), см. [здесь](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Try App Service](https://azure.microsoft.com/try/app-service/) (Пробное использование службы приложений), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений. Не требуется никаких кредитных карт и обязательств.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Дальнейшие действия
* Чтобы начать работу с Azure, [создайте бесплатную пробную учетную запись Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).
* Сведения о ценах, поддержке и соглашениях об уровне обслуживания см. по следующим ссылкам:
  
    [Сведения о ценах — передача данных](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Планы поддержки Microsoft Azure](https://azure.microsoft.com/support/plans/)
  
    [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/)
  
    [Сведения о ценах — база данных SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Размеры виртуальных машин и облачных служб для Microsoft Azure][vmsizes]
  
    [Сведения о ценах на службу приложений](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Сведения о ценах на службу приложений — SSL-соединения](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Рекомендации по использованию службы приложений Azure, в том числе по созданию масштабируемой и устойчивой архитектуры, см. [здесь](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Видео о масштабировании приложений службы приложений см. на следующих ресурсах:
  
  * [Стефан Шаков (Stefan Schackow). Когда следует масштабировать веб-сайты Azure](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
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
