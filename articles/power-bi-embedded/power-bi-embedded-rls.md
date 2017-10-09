---
title: "безопасность на уровне aaaRow в Power BI Embedded"
description: "Сведения о безопасности на уровне строк в Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Безопасность на уровне строк в Power BI Embedded

Безопасность на уровне строк (RLS) может быть tooparticular используется toorestrict пользователя доступ к данным внутри отчета или набора данных, позволяя для нескольких различных пользователей toouse hello того же отчета, когда все просматривают разные данные. В Power BI Embedded теперь поддерживаются наборы данных, для которых настроена безопасность на уровне строк.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

В порядке преимуществами tootake RLS важно понимать три основных понятия; Пользователи, роли и правила. Давайте подробнее рассмотрим каждое из них.

**Пользователи** — эти фактическое hello конечным пользователям способа просмотра отчетов. В Power BI Embedded пользователи определяются по hello свойство имени пользователя в токене приложений.

**Роли** — tooroles принадлежат пользователи. Роль — это контейнер правил, которому можно присвоить имя "Менеджер по продажам" или "Торговый представитель". В Power BI Embedded пользователи идентифицируются свойством hello роли в токен приложения.

**Правила** — роли имеют правила, и эти правила hello фактическое фильтры, которые будут применены toobe toohello данных. Это может быть просто "Страна — США" или что-то гораздо более динамичное.

### <a name="example"></a>Пример

Hello оставшейся части этой статьи мы предоставим пример создания RLS и затем использует, внедренные приложения. Наш пример использует hello [анализ розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547) pbix-файл.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Наш анализ розничной торговли показывает продаж для всех магазинов hello розничной определенной сети. Без RLS независимо от того, какие Округ manager входит в и представления hello отчета, они видят hello и тех же данных. Высшее руководство определяет, что каждый регионального менеджера должны видеть только hello продажи для hello магазинов, которыми они управляют и toodo это, мы можем использовать безопасность на уровне СТРОК.

Безопасность на уровне строк настраивается в Power BI Desktop. При открытии набора данных hello и отчета, мы можем переключиться toosee hello toodiagram представление схемы:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Ниже приведены несколько вещей toonotice с этой схемой.

* Все меры, например **общего объема продаж**, хранятся в hello **Sales** таблицы фактов.
* Есть четыре дополнительных связанных таблицы измерений: **Позиция**, **Время**, **Хранилище** и **Район**.
* Hello стрелки на линии связи hello указывают, каким образом фильтры могут передаваться из одной таблицы tooanother. Например, если фильтр помещается в **времени [Date]**, в текущей схеме hello он бы только отфильтровываются значения в hello **Sales** таблицы. Поскольку все hello стрелки на таблицу продаж toohello точки линии связи hello и сейчас не будет влиять никаких других таблиц этот фильтр.
* Hello **Округ** таблице указано, кто диспетчер hello — для всех регионов:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

На основе этой схемы, если применить toohello фильтра **регионального менеджера** столбца в hello Округ таблицы, и если этот фильтр соответствует hello пользователя, просматривающего отчет hello, этот фильтр будет также отфильтровываются hello **хранилища**и **продажи** tooonly таблицы будут отображаться данные для этого конкретного Округ диспетчера.

Этот процесс описывается далее.

1. Откройте вкладку моделирования hello **управление ролями**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Создайте роль с именем **Менеджер**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. В hello **District** таблицы введите следующее выражение DAX hello: **[регионального менеджера] = USERNAME()**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. Работа toomake убедиться, что правила hello на hello **моделирования** щелкните **просмотреть как роли**и затем введите следующие hello:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Hello отчетов теперь будут отображаться данные как если бы вы выполняли вход как **Ma Эндрю**.

Применение фильтра hello, мы сделали здесь способ hello отфильтрует вниз все записи из hello **Округ**, **хранилища**, и **Sales** таблиц. Однако из-за направление фильтра hello в hello связи между **продажи** и **время**, **продажи** и **элемент**и **Элемент** и **время** таблицы не будут фильтроваться вниз.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Которые могут быть ОК для соответствия этому требованию, однако, если мы не хотим диспетчеры toosee элементы, для которых они не имеют ни одной продажи, мы может включить двунаправленной перекрестной фильтрации для hello связь и поток hello фильтр безопасности в обоих направлениях. Это можно сделать, изменив hello связь между **продажи** и **элемент**, следующим образом:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Теперь фильтров может также распространяться и из таблицы toohello hello Sales **элемент** таблицы:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Если вы используете режим DirectQuery для данных, вам потребуется двунаправленной перекрестной tooenable фильтрации, выбрав следующие два варианта:

1. **Файл** -> **Параметры и настройки** -> **Функции предварительной версии** -> **Включить кроссфильтрацию в обоих направлениях для DirectQuery**;
2. **Файл** -> **Параметры и настройки** -> **DirectQuery** -> **Разрешить неограниченные меры в режиме DirectQuery**.

Дополнительные сведения о двунаправленной перекрестной фильтрации, hello загрузки toolearn [двунаправленной перекрестной фильтрации в SQL Server Analysis Services 2016 и Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) Технический документ.

Это перенесет все hello работу, необходимо сделать в Power BI Desktop toobe, но есть один дополнительные объем работы, который требуется сделать toobe toomake hello RLS правила, определенные работы в Power BI Embedded. Пользователи с проверкой подлинности и авторизации для приложения и приложения токены, используемые toogrant пользователя доступ tooa конкретного Power BI Embedded отчета. В Power BI Embedded нет сведений о том, кем является конкретный пользователь. Для toowork RLS вам потребуется toopass некоторые дополнительный контекст как часть вашего приложения токена.

* **имя пользователя** (необязательно) — при использовании RLS это строка, который может использоваться toohelp идентификации пользователя hello при применении правила RLS. См. статью Using Row Level Security with Power BI Embedded (Использование безопасности на уровне строк в Power BI Embedded).
* **роли** — строка, содержащая hello ролей tooselect при применении правил безопасности уровня строк. При выборе нескольких ролей их нужно передавать в виде массива строк.

Создать токен hello с помощью hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) метод. Если присутствует свойство username hello, необходимо также передать в роли по крайней мере одно значение.

Например можно изменить hello EmbedSample. Строку 55 DashboardController можно изменить с

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

значение

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

маркер полного приложения Hello будет выглядеть примерно следующим образом:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Теперь с все составляющие hello вместе, при входе в систему в нашем tooview приложения в этом отчете, они будут только может toosee hello данных они могут toosee, в соответствии с определением безопасность на уровне строк.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>См. также

[Безопасность на уровне строк (RLS) в Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Аутентификация и авторизация в Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Пример внедрения JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)

