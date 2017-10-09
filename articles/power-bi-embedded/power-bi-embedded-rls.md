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
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="997ab-103">Безопасность на уровне строк в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="997ab-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="997ab-104">Безопасность на уровне строк (RLS) может быть tooparticular используется toorestrict пользователя доступ к данным внутри отчета или набора данных, позволяя для нескольких различных пользователей toouse hello того же отчета, когда все просматривают разные данные.</span><span class="sxs-lookup"><span data-stu-id="997ab-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="997ab-105">В Power BI Embedded теперь поддерживаются наборы данных, для которых настроена безопасность на уровне строк.</span><span class="sxs-lookup"><span data-stu-id="997ab-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="997ab-106">В порядке преимуществами tootake RLS важно понимать три основных понятия; Пользователи, роли и правила.</span><span class="sxs-lookup"><span data-stu-id="997ab-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="997ab-107">Давайте подробнее рассмотрим каждое из них.</span><span class="sxs-lookup"><span data-stu-id="997ab-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="997ab-108">**Пользователи** — эти фактическое hello конечным пользователям способа просмотра отчетов.</span><span class="sxs-lookup"><span data-stu-id="997ab-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="997ab-109">В Power BI Embedded пользователи определяются по hello свойство имени пользователя в токене приложений.</span><span class="sxs-lookup"><span data-stu-id="997ab-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="997ab-110">**Роли** — tooroles принадлежат пользователи.</span><span class="sxs-lookup"><span data-stu-id="997ab-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="997ab-111">Роль — это контейнер правил, которому можно присвоить имя "Менеджер по продажам" или "Торговый представитель".</span><span class="sxs-lookup"><span data-stu-id="997ab-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="997ab-112">В Power BI Embedded пользователи идентифицируются свойством hello роли в токен приложения.</span><span class="sxs-lookup"><span data-stu-id="997ab-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="997ab-113">**Правила** — роли имеют правила, и эти правила hello фактическое фильтры, которые будут применены toobe toohello данных.</span><span class="sxs-lookup"><span data-stu-id="997ab-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="997ab-114">Это может быть просто "Страна — США" или что-то гораздо более динамичное.</span><span class="sxs-lookup"><span data-stu-id="997ab-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="997ab-115">Пример</span><span class="sxs-lookup"><span data-stu-id="997ab-115">Example</span></span>

<span data-ttu-id="997ab-116">Hello оставшейся части этой статьи мы предоставим пример создания RLS и затем использует, внедренные приложения.</span><span class="sxs-lookup"><span data-stu-id="997ab-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="997ab-117">Наш пример использует hello [анализ розничной торговли](http://go.microsoft.com/fwlink/?LinkID=780547) pbix-файл.</span><span class="sxs-lookup"><span data-stu-id="997ab-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="997ab-118">Наш анализ розничной торговли показывает продаж для всех магазинов hello розничной определенной сети.</span><span class="sxs-lookup"><span data-stu-id="997ab-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="997ab-119">Без RLS независимо от того, какие Округ manager входит в и представления hello отчета, они видят hello и тех же данных.</span><span class="sxs-lookup"><span data-stu-id="997ab-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="997ab-120">Высшее руководство определяет, что каждый регионального менеджера должны видеть только hello продажи для hello магазинов, которыми они управляют и toodo это, мы можем использовать безопасность на уровне СТРОК.</span><span class="sxs-lookup"><span data-stu-id="997ab-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="997ab-121">Безопасность на уровне строк настраивается в Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="997ab-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="997ab-122">При открытии набора данных hello и отчета, мы можем переключиться toosee hello toodiagram представление схемы:</span><span class="sxs-lookup"><span data-stu-id="997ab-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="997ab-123">Ниже приведены несколько вещей toonotice с этой схемой.</span><span class="sxs-lookup"><span data-stu-id="997ab-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="997ab-124">Все меры, например **общего объема продаж**, хранятся в hello **Sales** таблицы фактов.</span><span class="sxs-lookup"><span data-stu-id="997ab-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="997ab-125">Есть четыре дополнительных связанных таблицы измерений: **Позиция**, **Время**, **Хранилище** и **Район**.</span><span class="sxs-lookup"><span data-stu-id="997ab-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="997ab-126">Hello стрелки на линии связи hello указывают, каким образом фильтры могут передаваться из одной таблицы tooanother.</span><span class="sxs-lookup"><span data-stu-id="997ab-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="997ab-127">Например, если фильтр помещается в **времени [Date]**, в текущей схеме hello он бы только отфильтровываются значения в hello **Sales** таблицы.</span><span class="sxs-lookup"><span data-stu-id="997ab-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="997ab-128">Поскольку все hello стрелки на таблицу продаж toohello точки линии связи hello и сейчас не будет влиять никаких других таблиц этот фильтр.</span><span class="sxs-lookup"><span data-stu-id="997ab-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="997ab-129">Hello **Округ** таблице указано, кто диспетчер hello — для всех регионов:</span><span class="sxs-lookup"><span data-stu-id="997ab-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="997ab-130">На основе этой схемы, если применить toohello фильтра **регионального менеджера** столбца в hello Округ таблицы, и если этот фильтр соответствует hello пользователя, просматривающего отчет hello, этот фильтр будет также отфильтровываются hello **хранилища**и **продажи** tooonly таблицы будут отображаться данные для этого конкретного Округ диспетчера.</span><span class="sxs-lookup"><span data-stu-id="997ab-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="997ab-131">Этот процесс описывается далее.</span><span class="sxs-lookup"><span data-stu-id="997ab-131">Here’s how:</span></span>

1. <span data-ttu-id="997ab-132">Откройте вкладку моделирования hello **управление ролями**.</span><span class="sxs-lookup"><span data-stu-id="997ab-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="997ab-133">Создайте роль с именем **Менеджер**.</span><span class="sxs-lookup"><span data-stu-id="997ab-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="997ab-134">В hello **District** таблицы введите следующее выражение DAX hello: **[регионального менеджера] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="997ab-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="997ab-135">Работа toomake убедиться, что правила hello на hello **моделирования** щелкните **просмотреть как роли**и затем введите следующие hello:</span><span class="sxs-lookup"><span data-stu-id="997ab-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="997ab-136">Hello отчетов теперь будут отображаться данные как если бы вы выполняли вход как **Ma Эндрю**.</span><span class="sxs-lookup"><span data-stu-id="997ab-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="997ab-137">Применение фильтра hello, мы сделали здесь способ hello отфильтрует вниз все записи из hello **Округ**, **хранилища**, и **Sales** таблиц.</span><span class="sxs-lookup"><span data-stu-id="997ab-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="997ab-138">Однако из-за направление фильтра hello в hello связи между **продажи** и **время**, **продажи** и **элемент**и **Элемент** и **время** таблицы не будут фильтроваться вниз.</span><span class="sxs-lookup"><span data-stu-id="997ab-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="997ab-139">Которые могут быть ОК для соответствия этому требованию, однако, если мы не хотим диспетчеры toosee элементы, для которых они не имеют ни одной продажи, мы может включить двунаправленной перекрестной фильтрации для hello связь и поток hello фильтр безопасности в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="997ab-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="997ab-140">Это можно сделать, изменив hello связь между **продажи** и **элемент**, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="997ab-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="997ab-141">Теперь фильтров может также распространяться и из таблицы toohello hello Sales **элемент** таблицы:</span><span class="sxs-lookup"><span data-stu-id="997ab-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="997ab-142">Если вы используете режим DirectQuery для данных, вам потребуется двунаправленной перекрестной tooenable фильтрации, выбрав следующие два варианта:</span><span class="sxs-lookup"><span data-stu-id="997ab-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="997ab-143">**Файл** -> **Параметры и настройки** -> **Функции предварительной версии** -> **Включить кроссфильтрацию в обоих направлениях для DirectQuery**;</span><span class="sxs-lookup"><span data-stu-id="997ab-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="997ab-144">**Файл** -> **Параметры и настройки** -> **DirectQuery** -> **Разрешить неограниченные меры в режиме DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="997ab-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="997ab-145">Дополнительные сведения о двунаправленной перекрестной фильтрации, hello загрузки toolearn [двунаправленной перекрестной фильтрации в SQL Server Analysis Services 2016 и Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) Технический документ.</span><span class="sxs-lookup"><span data-stu-id="997ab-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="997ab-146">Это перенесет все hello работу, необходимо сделать в Power BI Desktop toobe, но есть один дополнительные объем работы, который требуется сделать toobe toomake hello RLS правила, определенные работы в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="997ab-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="997ab-147">Пользователи с проверкой подлинности и авторизации для приложения и приложения токены, используемые toogrant пользователя доступ tooa конкретного Power BI Embedded отчета.</span><span class="sxs-lookup"><span data-stu-id="997ab-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="997ab-148">В Power BI Embedded нет сведений о том, кем является конкретный пользователь.</span><span class="sxs-lookup"><span data-stu-id="997ab-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="997ab-149">Для toowork RLS вам потребуется toopass некоторые дополнительный контекст как часть вашего приложения токена.</span><span class="sxs-lookup"><span data-stu-id="997ab-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="997ab-150">**имя пользователя** (необязательно) — при использовании RLS это строка, который может использоваться toohelp идентификации пользователя hello при применении правила RLS.</span><span class="sxs-lookup"><span data-stu-id="997ab-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="997ab-151">См. статью Using Row Level Security with Power BI Embedded (Использование безопасности на уровне строк в Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="997ab-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="997ab-152">**роли** — строка, содержащая hello ролей tooselect при применении правил безопасности уровня строк.</span><span class="sxs-lookup"><span data-stu-id="997ab-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="997ab-153">При выборе нескольких ролей их нужно передавать в виде массива строк.</span><span class="sxs-lookup"><span data-stu-id="997ab-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="997ab-154">Создать токен hello с помощью hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) метод.</span><span class="sxs-lookup"><span data-stu-id="997ab-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="997ab-155">Если присутствует свойство username hello, необходимо также передать в роли по крайней мере одно значение.</span><span class="sxs-lookup"><span data-stu-id="997ab-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="997ab-156">Например можно изменить hello EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="997ab-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="997ab-157">Строку 55 DashboardController можно изменить с</span><span class="sxs-lookup"><span data-stu-id="997ab-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="997ab-158">значение</span><span class="sxs-lookup"><span data-stu-id="997ab-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="997ab-159">маркер полного приложения Hello будет выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="997ab-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="997ab-160">Теперь с все составляющие hello вместе, при входе в систему в нашем tooview приложения в этом отчете, они будут только может toosee hello данных они могут toosee, в соответствии с определением безопасность на уровне строк.</span><span class="sxs-lookup"><span data-stu-id="997ab-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="997ab-161">См. также</span><span class="sxs-lookup"><span data-stu-id="997ab-161">See also</span></span>

[<span data-ttu-id="997ab-162">Безопасность на уровне строк (RLS) в Power BI</span><span class="sxs-lookup"><span data-stu-id="997ab-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="997ab-163">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="997ab-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="997ab-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="997ab-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="997ab-165">Пример внедрения JavaScript</span><span class="sxs-lookup"><span data-stu-id="997ab-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="997ab-166">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="997ab-166">More questions?</span></span> [<span data-ttu-id="997ab-167">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="997ab-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

