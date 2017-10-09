## <a name="repeatability-during-copy"></a><span data-ttu-id="02cf1-101">Повторяемость во время копирования</span><span class="sxs-lookup"><span data-stu-id="02cf1-101">Repeatability during Copy</span></span>
<span data-ttu-id="02cf1-102">При копирование tooAzure данных SQL и SQL Server на основе других данных хранит один повторяемость tookeep потребности в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="02cf1-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="02cf1-103">При копировании данных tooAzure базы данных SQL и SQL Server, действие копирования будет по умолчанию APPEND hello набора данных toohello приемник таблицы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="02cf1-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="02cf1-104">Например при копировании данных из исходного файла CSV (данные значения с разделителями-запятыми), содержащий два записывает tooAzure базы данных SQL и SQL Server, это выглядит как hello таблиц:</span><span class="sxs-lookup"><span data-stu-id="02cf1-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="02cf1-105">Предположим, что обнаружены ошибки в исходном файле и обновленные hello количество для работы с 2 too4 в исходном файле hello.</span><span class="sxs-lookup"><span data-stu-id="02cf1-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="02cf1-106">При повторном запуске hello срез данных для этого периода, вы найдете две новые записи добавляются tooAzure базы данных SQL и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="02cf1-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="02cf1-107">Hello ниже предполагается, что hello столбцов в таблице hello не имеют hello первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="02cf1-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="02cf1-108">tooavoid это, вам потребуется toospecify семантику вставки-обновления, используя один из hello ниже 2 механизмы, указанной ниже.</span><span class="sxs-lookup"><span data-stu-id="02cf1-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="02cf1-109">Срез можно повторно выполняться автоматически в фабрике данных Azure согласно заданной политике hello повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="02cf1-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="02cf1-110">Механизм 1</span><span class="sxs-lookup"><span data-stu-id="02cf1-110">Mechanism 1</span></span>
<span data-ttu-id="02cf1-111">Можно использовать **sqlWriterCleanupScript** toofirst свойство Действие очистки при выполнении среза.</span><span class="sxs-lookup"><span data-stu-id="02cf1-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="02cf1-112">Hello скрипт очистки будет выполняться первой во время копирования для данного фрагмента, которой будет удалять данные hello из соответствующего среза toothat hello таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="02cf1-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="02cf1-113">Действие Hello впоследствии будет вставлять данные hello в hello таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="02cf1-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="02cf1-114">Если срез hello сейчас запустить повторно, то можно будет видеть, что количество hello обновляется как правильно.</span><span class="sxs-lookup"><span data-stu-id="02cf1-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="02cf1-115">Предположим, что hello плоский Шайба запись удаляется из исходной csv hello.</span><span class="sxs-lookup"><span data-stu-id="02cf1-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="02cf1-116">Затем повторным запуском срез hello приведет к получению hello следующий результат:</span><span class="sxs-lookup"><span data-stu-id="02cf1-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="02cf1-117">Ничего нового было сделано toobe.</span><span class="sxs-lookup"><span data-stu-id="02cf1-117">Nothing new had toobe done.</span></span> <span data-ttu-id="02cf1-118">Действие копирования Hello выполнялись hello очистки сценария toodelete hello соответствующих данных для этого среза.</span><span class="sxs-lookup"><span data-stu-id="02cf1-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="02cf1-119">Затем он считывают hello входные данные из CSV-файла hello (которое затем содержит всего одну запись) и вставлены hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="02cf1-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="02cf1-120">Механизм 2</span><span class="sxs-lookup"><span data-stu-id="02cf1-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="02cf1-121">В настоящее время sliceIdentifierColumnName не поддерживается для хранилища данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="02cf1-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="02cf1-122">Другой механизм tooachieve повторяемость является выделенный столбец (**sliceIdentifierColumnName**) в hello целевая таблица.</span><span class="sxs-lookup"><span data-stu-id="02cf1-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="02cf1-123">Этот столбец будет использоваться фабрики данных Azure tooensure hello источника и назначения Оставайтесь синхронизированы.</span><span class="sxs-lookup"><span data-stu-id="02cf1-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="02cf1-124">Такой подход работает, когда гибкие возможности изменения или определение схемы таблицы SQL hello назначения.</span><span class="sxs-lookup"><span data-stu-id="02cf1-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="02cf1-125">Этот столбец будет использоваться фабрики данных Azure в целях обеспечения и в процессе hello фабрики данных Azure не будет выполнять любую схему изменяет toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="02cf1-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="02cf1-126">Способ toouse этот подход:</span><span class="sxs-lookup"><span data-stu-id="02cf1-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="02cf1-127">Задать столбец двоичного типа (32) на целевом экземпляре hello таблицы SQL.</span><span class="sxs-lookup"><span data-stu-id="02cf1-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="02cf1-128">Для этого столбца не должно быть никаких ограничений.</span><span class="sxs-lookup"><span data-stu-id="02cf1-128">There should be no constraints on this column.</span></span> <span data-ttu-id="02cf1-129">Давайте в данном примере назовем столбец ColumnForADFuseOnly.</span><span class="sxs-lookup"><span data-stu-id="02cf1-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="02cf1-130">Используйте его в действие hello копирования следующим образом:</span><span class="sxs-lookup"><span data-stu-id="02cf1-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="02cf1-131">Фабрика данных Azure заполнит этот столбец согласно необходимости tooensure hello источника и назначения сохранить синхронизацию.</span><span class="sxs-lookup"><span data-stu-id="02cf1-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="02cf1-132">Hello значения этого столбца не используется за пределами этого контекста пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="02cf1-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="02cf1-133">Аналогичные toomechanism 1, действие копирования будет автоматически первой очистки данных hello для hello даны срез hello целевой таблицы SQL и запустите действие копирования hello обычно tooinsert hello данные из источника toodestination для этого среза.</span><span class="sxs-lookup"><span data-stu-id="02cf1-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

