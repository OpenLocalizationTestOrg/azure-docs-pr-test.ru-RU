---
title: "Использование пакета HBase .NET SDK для Azure HDInsight | Документация Майкрософт"
description: "Пакет SDK для .NET HBase позволяет создавать и удалять таблицы, а также считывать и записывать данные."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: ashishthaps
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/13/2017
ms.author: ashishth
ms.openlocfilehash: 083150fe5f8787ba791d3d692db73c5156f11e55
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="use-the-hbase-net-sdk"></a>Использование пакета SDK для .NET HBase

[HBase](apache-hbase-overview.md) предоставляет два основных способа работы с данными: [запросы Hive и вызовы RESTful API HBase](apache-hbase-tutorial-get-started-linux.md). Можно работать непосредственно с REST API, используя команду `curl` или подобную программу.

Для приложений C# и .NET [клиентская библиотека Microsoft HBase REST для .NET](https://www.nuget.org/packages/Microsoft.HBase.Client/) предоставляет клиентскую библиотеку на платформе REST API HBase.

## <a name="install-the-sdk"></a>Установка пакета SDK

Пакет SDK для .NET HBase предоставляется в виде пакета NuGet, который можно установить из **консоли диспетчера пакетов NuGet** в Visual Studio при помощи следующей команды:

    Install-Package Microsoft.HBase.Client

## <a name="instantiate-a-new-hbaseclient-object"></a>Создание нового экземпляра объекта HBaseClient

Чтобы использовать пакет SDK, создайте экземпляр объекта `HBaseClient`, передав в него данные `ClusterCredentials`, которые включают `Uri` вашего кластера, а также имя пользователя и пароль Hadoop.

```csharp
var credentials = new ClusterCredentials(new Uri("https://CLUSTERNAME.azurehdinsight.net"), "USERNAME", "PASSWORD");
client = new HBaseClient(credentials);
```

Замените CLUSTERNAME именем кластера HDInsight HBase, а USERNAME и PASSWORD — учетными данными Hadoop, указанными при создании кластера. Имя пользователя Hadoop по умолчанию — **admin**.

## <a name="create-a-new-table"></a>Создание таблицы

В HBase данные хранятся в таблицах. Таблица состоит из *Rowkey* — первичного ключа — и одной или нескольких групп столбцов, называемых *семействами столбцов*. Данные в каждой таблице горизонтально распределяются по диапазонам ключей Rowkey на *области*. У каждой области есть ключ начала и окончания. Таблица может содержать одну или несколько областей. По мере роста данных в таблице HBase большие области разбиваются на меньшие. Области хранятся на *серверах областей*. На одном сервере могут храниться несколько областей.

Физически данные хранятся в файлах *HFile*. Один файл HFile содержит данные для одной таблицы, одной области и одного семейства столбцов. Строки в файле HFile отсортированы по ключу Rowkey. Каждый файл HFile содержит индекс *дерева B+* для быстрого получения строк.

Чтобы создать новую таблицу, укажите `TableSchema` и столбцы. Следующий код проверяет, существует ли таблица RestSDKTable. Если нет, она создается.

```csharp
if (!client.ListTablesAsync().Result.name.Contains("RestSDKTable"))
{
    // Create the table
    var newTableSchema = new TableSchema {name = "RestSDKTable" };
    newTableSchema.columns.Add(new ColumnSchema() {name = "t1"});
    newTableSchema.columns.Add(new ColumnSchema() {name = "t2"});

    await client.CreateTableAsync(newTableSchema);
}
```

Эта новая таблица содержит два семейства столбцов — t1 и t2. Так как семейства столбцов хранятся отдельно в разных файлах HFile, есть смысл создать отдельное семейство столбцов для часто запрашиваемых данных. В следующем примере [вставки данных](#insert-data) столбцы добавляются в семейство столбцов t1.

## <a name="delete-a-table"></a>Удаление таблицы

Чтобы удалить таблицу, выполните следующую команду:

```csharp
await client.DeleteTableAsync("RestSDKTable");
```

## <a name="insert-data"></a>Добавление данных

Для вставки данных укажите уникальный ключ строки в качестве ее идентификатора. Все данные хранятся в массиве `byte[]`. Следующий код позволяет определить и добавить столбцы `title`, `director` и `release_date` в семейство столбцов t1, так как к ним наиболее часто осуществляется доступ. Столбцы `description` и `tagline` добавляются в семейство столбцов t2. При необходимости можно разделить данные на семейства столбцов.

```csharp
var key = "fifth_element";
var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };
var value = new Cell
{
    column = Encoding.UTF8.GetBytes("t1:title"),
    data = Encoding.UTF8.GetBytes("The Fifth Element")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t1:director"),
    data = Encoding.UTF8.GetBytes("Luc Besson")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t1:release_date"),
    data = Encoding.UTF8.GetBytes("1997")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t2:description"),
    data = Encoding.UTF8.GetBytes("In the colorful future, a cab driver unwittingly becomes the central figure in the search for a legendary cosmic weapon to keep Evil and Mr Zorg at bay.")
};
row.values.Add(value);
value = new Cell
{
    column = Encoding.UTF8.GetBytes("t2:tagline"),
    data = Encoding.UTF8.GetBytes("The Fifth is life")
};
row.values.Add(value);

var set = new CellSet();
set.rows.Add(row);

await client.StoreCellsAsync("RestSDKTable", set);
```

В HBase используется BigTable, поэтому формат данных выглядит следующим образом:

![Пользователь с ролью "Cluster User" (Пользователь кластера)](./media/apache-hbase-rest-sdk/table.png)

## <a name="select-data"></a>Выбор данных

Для чтения данных из таблицы HBase передайте имя таблицы и ключ строки в метод `GetCellsAsync`, который возвращает `CellSet`.

```csharp
var key = "fifth_element";

var cells = await client.GetCellsAsync("RestSDKTable", key);
// Get the first value from the row.
Console.WriteLine(Encoding.UTF8.GetString(cells.rows[0].values[0].data));
// Get the value for t1:title
Console.WriteLine(Encoding.UTF8.GetString(cells.rows[0].values
    .Find(c => Encoding.UTF8.GetString(c.column) == "t1:title").data));
// With the previous insert, it should yield: "The Fifth Element"
```

В этом случае код возвращает только первую совпадающую строку, так как уникальному ключу должна соответствовать только одна строка. Возвращаемое значение преобразуется в формат `string` из массива `byte[]`. Также это значение можно преобразовать в другие типы, например целочисленный для даты выпуска фильма:

```csharp
var releaseDateField = cells.rows[0].values
    .Find(c => Encoding.UTF8.GetString(c.column) == "t1:release_date");
int releaseDate = 0;

if (releaseDateField != null)
{
    releaseDate = Convert.ToInt32(Encoding.UTF8.GetString(releaseDateField.data));
}
Console.WriteLine(releaseDate);
// Should return 1997
```

## <a name="scan-over-rows"></a>Сканирование по строкам

В HBase используется `scan` для получения одной или нескольких строк. В этом примере запрашивается множество строк пакетами по 10 и возвращаются данные, значения ключей которых находятся в диапазоне от 25 до 35. После получения всех строк удалите сканер для освобождения ресурсов.

```csharp
var tableName = "mytablename";

// Assume the table has integer keys and we want data between keys 25 and 35
var scanSettings = new Scanner()
{
    batch = 10,
    startRow = BitConverter.GetBytes(25),
    endRow = BitConverter.GetBytes(35)
};
RequestOptions scanOptions = RequestOptions.GetDefaultOptions();
scanOptions.AlternativeEndpoint = "hbaserest0/";
ScannerInformation scannerInfo = null;
try
{
    scannerInfo = await client.CreateScannerAsync(tableName, scanSettings, scanOptions);
    CellSet next = null;
    while ((next = client.ScannerGetNextAsync(scannerInfo, scanOptions).Result) != null)
    {
        foreach (var row in next.rows)
        {
            // ... read the rows
        }
    }
}
finally
{
    if (scannerInfo != null)
    {
        await client.DeleteScannerAsync(tableName, scannerInfo, scanOptions);
    }
}
```

## <a name="next-steps"></a>Дополнительная информация

* [Начало работы с примером Apache HBase в HDInsight](apache-hbase-tutorial-get-started-linux.md)
* Создание полнофункционального приложения на основе руководства по [анализу мнений Twitter в режиме реального времени с помощью HBase](../hdinsight-hbase-analyze-twitter-sentiment.md)
