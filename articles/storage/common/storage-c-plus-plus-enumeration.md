---
title: "aaaList ресурсов хранилища Azure с hello клиентская библиотека хранилища для C++ | Документы Microsoft"
description: "Узнайте, как toouse hello список интерфейсов API в клиентской библиотеке хранилища Microsoft Azure для C++ tooenumerate контейнеров больших двоичных объектов, очередей, таблиц и сущностей."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Перечисление ресурсов хранилища Azure в C++
Листинг операции выполняются сценарии разработки toomany ключа хранилища Azure. В этой статье описывается, как toomost эффективно перечисления объектов в хранилище Azure с помощью hello список интерфейсов API, входящих в hello клиентская библиотека хранилища Microsoft Azure для C++.

> [!NOTE]
> В этом руководстве обращается hello клиентская библиотека хранилища Azure для C++ версии 2.x, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Hello клиентской библиотеки хранилища предоставляет разнообразные методы toolist или запроса объектов в хранилище Azure. В этой статье рассматриваются hello следующие сценарии:

* перечисление контейнеров в учетной записи;
* перечисление больших двоичных объектов в контейнере или виртуальном каталоге больших двоичных объектов;
* перечисление очередей в учетной записи;
* перечисление таблиц в учетной записи;
* запрос сущностей в таблице.

Каждый из этих методов продемонстрирован с использованием различных перегрузок для разных сценариев.

## <a name="asynchronous-versus-synchronous"></a>Асинхронный или синхронный
Поскольку hello клиентская библиотека хранилища для C++ является надстройкой hello [библиотеки C++ REST](https://github.com/Microsoft/cpprestsdk), мы поддерживаем по своей природе асинхронных операций с помощью [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Например:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Синхронные операции wrap hello соответствующих асинхронных операций:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

При работе с несколькими приложениями или службами потоков, рекомендуется использовать hello асинхронные интерфейсы API, напрямую вместо создания синхронизации hello toocall поток API, которые существенно влияет на производительность.

## <a name="segmented-listing"></a>Сегментированное перечисление
Масштаб Hello облачного хранилища требуется листинг Сегментированные. Например, в контейнере больших двоичных объектов Azure может быть больше миллиона больших двоичных объектов, а в таблице Azure может быть больше миллиарда сущностей. Это не теоретические значения, а фактические примеры реальных пользователей.

Именно поэтому нецелесообразным toolist все объекты в одном ответе. Вместо этого можно получить список объектов с разбиением на страницы. Каждый список API-интерфейсы hello имеет *сегментированных* перегрузки.

Hello ответ для операции листинг Сегментированные включает:

* <i>_segment</i>, который содержит набор результатов, возвращенных за один вызов toohello, перечисление API hello.
* *continuation_token*, который передается следующему вызову toohello в порядке tooget hello следующей страницы результатов. Если нет дополнительных результатов tooreturn, токен продолжения hello имеет значение null.

Например типичный вызов toolist все большие двоичные объекты в контейнере может выглядеть как следующий фрагмент кода hello. Hello код находится в нашем [образцы](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

Обратите внимание, что hello количество результатов, возвращаемых на странице можно управлять параметром hello *max_results* в перегрузке hello каждый API, например:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Если вы не укажете hello *max_results* параметр, по умолчанию hello возвращается максимальное значение too5000 результатов на одной странице.

Также Обратите внимание, что запрос к хранилищу таблиц Azure может возвращать нет записей или записей меньше, чем значение hello hello *max_results* параметр, который вы указали, даже если токен продолжения hello не является пустым. Одна из причин может быть hello запроса не удалось завершить в течение пяти секунд. При условии, что токен продолжения hello не пуста, следует продолжить запрос hello и код не должен предполагать hello размер сегмента результатов.

Hello рекомендуется шаблона для большинства сценариев кодирования разбито перечисление, предоставляющее явную хода выполнения со списком или запросов, а также службы hello реакция tooeach запроса. Особенно для C++ приложений или служб управление hello со списком выполняется более низкого уровня могут помочь управления памятью и производительностью.

## <a name="greedy-listing"></a>Каскадное перечисление
Более ранних версиях hello клиентская библиотека хранилища для C++ (Предварительный просмотр версий 0.5.0 и более ранних версий) включены несегментированный список API-интерфейсы для таблиц и очередей, как следующий пример hello:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Эти методы были реализованы в виде оболочки сегментированных API-интерфейсов. В каждом ответе листинг Сегментированные кода hello добавлено вектор tooa результаты hello и вернуть все результаты, после полного контейнеры hello сканировались.

Этот подход может работать при hello учетной записи хранилища или таблица содержит небольшое количество объектов. Тем не менее увеличение hello число объектов, требуемый объем памяти hello удалось увеличить без ограничения, так как все результаты остаются в памяти. Одной операцией получения листинга может занять очень много времени, в которой hello вызывающего объекта, необходимо было отсутствует информация о ходе своего выполнения.

Эти жадном список интерфейсов API в hello SDK не существует в C#, Java, и hello среды JavaScript Node.js. tooavoid hello потенциальных проблем с помощью этих жадном API, мы удалили их в версии 0.6.0 предварительного просмотра.

Если ваш код вызывает эти каскадные API-интерфейсы:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Необходимо изменить код, а затем toouse hello сегментированных список API-интерфейсы:

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

Указав hello *max_results* параметр hello сегмента можно распределить между номерами hello запросов и использования памяти toomeet вопросы производительности приложения.

Кроме того, если выполняется с помощью листинг Сегментированные API-интерфейсы, но сохранить данные hello в локальную коллекцию в стиле «жадного», также настоятельно рекомендуется выполнить рефакторинг toohandle вашего кода, хранение данных в локальную коллекцию тщательно в масштабе.

## <a name="lazy-listing"></a>Отложенное перечисление
Несмотря на то, что жадном листинг возникает потенциальные проблемы, его удобно, если не слишком много объектов в контейнере hello.

Если вы также используете C# или Oracle Java SDK, необходимо ознакомиться с hello перечисляемую модель программирования, обеспечивающую отложенной стиля списка, где hello данные с определенным смещением только доставляются при необходимости. В C++ шаблон на основе итератора hello также предоставляет подобный подход.

Типичный API отложенного перечисления, использующий **list_blobs**, например, выглядит следующим образом:

```cpp
list_blob_item_iterator list_blobs() const;
```

Фрагмент обычного кода, который использует шаблон отложенной листинг hello может выглядеть следующим образом:

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

Обратите внимание, что отложенное перечисление доступно только в синхронном режиме.

По сравнению с каскадным перечислением отложенное перечисление извлекает данные только при необходимости. На деле hello он выбирает данные из хранилища Azure, только в том случае, когда перемещает hello следующего итератора в следующего сегмента. Таким образом использование памяти контролируется с помощью предельный размер и hello операция выполняется быстро.

Листинг отложенной API-интерфейсы, включаются в hello клиентская библиотека хранилища C++ в версии 2.2.0.

## <a name="conclusion"></a>Заключение
В этой статье мы рассмотрели разные перегрузки для перечисления API-интерфейсы для различных объектов в hello клиентской библиотеки хранилища для C++. toosummarize:

* Настоятельно рекомендуется использовать асинхронные интерфейсы API в сценариях с несколькими потоками.
* Для большинства сценариев рекомендуется сегментированное перечисление.
* Отложенная список приведен в библиотеке hello как удобный оболочка в синхронные сценарии.
* Жадное список не рекомендуется и был удален из библиотеки hello.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о хранилище Azure и клиентскую библиотеку C++ см. следующие ресурсы hello.

* [Как toouse хранилища BLOB-объектов из C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Как toouse хранилище таблиц из C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Как toouse хранилища очередей из C++](../storage-c-plus-plus-how-to-use-queues.md)
* [Документация по API-интерфейсам клиентской библиотеки хранилища Azure для C++.](http://azure.github.io/azure-storage-cpp/)
* [Блог рабочей группы службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Документация по хранилищу Azure](https://azure.microsoft.com/documentation/services/storage/)

