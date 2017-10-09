---
title: "aaaUse Power BI с хранилищем данных SQL | Документы Microsoft"
description: "Советы по использованию Power BI с хранилищем данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="8ec7a-103">Использование Power BI с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="8ec7a-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="8ec7a-104">Как и в базе данных SQL Azure SQL хранилища прямого подключения к данным позволяет пользователя tooleverage мощные логических Включение наряду с hello аналитических возможностей Power BI.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="8ec7a-105">При использовании Direct Connect запросы отправляются назад tooyour хранилище данных SQL Azure в реальном времени при просмотре данных hello.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="8ec7a-106">Это, в сочетании с hello масштабирования хранилища данных SQL, позволяет пользователям toocreate динамических отчетов в минутах терабайтов данных.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="8ec7a-107">Кроме того, пользователи hello появлением Привет открыть в Power BI кнопку toodirectly подключения Power BI tootheir хранилище данных SQL не собирая сведения из других частей Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="8ec7a-108">При использовании прямого соединения следует обратить внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="8ec7a-109">Укажите hello полное имя сервера, при подключении (см. ниже дополнительные сведения)</span><span class="sxs-lookup"><span data-stu-id="8ec7a-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="8ec7a-110">Убедитесь, правила брандмауэра для базы данных hello настроены слишком «разрешать доступ tooAzure служб».</span><span class="sxs-lookup"><span data-stu-id="8ec7a-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="8ec7a-111">Каждое действие, например Выбор столбца или Добавление фильтра, отправляет запрос непосредственно hello хранилища данных</span><span class="sxs-lookup"><span data-stu-id="8ec7a-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="8ec7a-112">Плитки обновляются примерно каждые 15 минут, (обновления не требуются toobe запланировано)</span><span class="sxs-lookup"><span data-stu-id="8ec7a-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="8ec7a-113">Раздел вопросов и ответов недоступен для наборов данных прямого соединения.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="8ec7a-114">Изменения схемы не выбираются автоматически.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="8ec7a-115">Время ожидания любых запросов на прямое соединение истекает через две минуты.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="8ec7a-116">Эти ограничения и примечания может измениться по мере возможности tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="8ec7a-117">Ниже описаны шаги tooconnect Hello.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="8ec7a-118">С помощью кнопки «Открыть в Power BI» hello</span><span class="sxs-lookup"><span data-stu-id="8ec7a-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="8ec7a-119">toomove простым способом Hello между хранилищем данных SQL и Power BI — с Привет открыть в Power BI кнопку.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="8ec7a-120">Эта кнопка позволяет tooseamlessly начать создание новых панелей мониторинга в Power BI.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="8ec7a-121">tooget работы перейдите tooyour экземпляр хранилища данных SQL в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="8ec7a-122">Нажмите кнопку «Открыть в Power BI» hello.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="8ec7a-123">Если мы не может toosign в напрямую, или если у вас учетная запись Power BI, вам потребуется в toosign.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="8ec7a-124">Вы будете направлены подставлен toohello страницы подключения хранилища данных SQL, hello данными с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="8ec7a-125">После ввода учетных данных будет полностью соединенными tooyour хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="8ec7a-126">Подключение через портал hello Power BI</span><span class="sxs-lookup"><span data-stu-id="8ec7a-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="8ec7a-127">В добавление toousing Привет открыть кнопку Power BI пользователи также могут подключаться tootheir хранилище данных SQL через hello портале Power BI.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="8ec7a-128">Нажмите кнопку «Получить данные» hello нижней части панели навигации hello.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="8ec7a-129">Выберите «Базы данных».</span><span class="sxs-lookup"><span data-stu-id="8ec7a-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="8ec7a-130">Один раз на странице приветствия базами данных, выберите «Хранилище данных SQL Azure» и нажмите кнопку «Подключиться».</span><span class="sxs-lookup"><span data-stu-id="8ec7a-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="8ec7a-131">Введите hello необходимые сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="8ec7a-132">Имя сервера и имя базы данных можно найти в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="8ec7a-133">Вы будете перенаправлены обратно с именем hello экземпляра появится toohello главной странице Power BI, а после подключения к новой записи в разделе «Наборы данных».</span><span class="sxs-lookup"><span data-stu-id="8ec7a-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="8ec7a-134">Можно щелкнуть на новый набор данных tooexplore hello все hello таблиц и представлений в базе данных.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="8ec7a-135">При выборе столбца будет отправлено назад toohello источника запроса, динамически создается визуальный.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="8ec7a-136">Эти визуальные элементы можно сохранить в новом отчете и закрепить tooyour панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8ec7a-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
