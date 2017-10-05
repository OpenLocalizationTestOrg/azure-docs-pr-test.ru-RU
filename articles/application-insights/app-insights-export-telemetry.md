---
title: "Непрерывный экспорт данных телеметрии из Application Insights | Документация Майкрософт"
description: "Экспортируйте данные диагностики и использования в хранилище в Microsoft Azure и загрузите их оттуда."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="bbde6-103">Экспорт данных телеметрии из Application Insights</span><span class="sxs-lookup"><span data-stu-id="bbde6-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="bbde6-104">Хотите увеличить период удержания телеметрии</span><span class="sxs-lookup"><span data-stu-id="bbde6-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="bbde6-105">или анализировать ее особым образом?</span><span class="sxs-lookup"><span data-stu-id="bbde6-105">Or process it in some specialized way?</span></span> <span data-ttu-id="bbde6-106">Функция "Непрерывный экспорт" идеально подходит для этого.</span><span class="sxs-lookup"><span data-stu-id="bbde6-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="bbde6-107">События, которые отображаются на портале Application Insights, можно экспортировать в хранилище Microsoft Azure в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="bbde6-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="bbde6-108">Отсюда можно загрузить данные; также вы можете написать любой код, необходимый для их обработки.</span><span class="sxs-lookup"><span data-stu-id="bbde6-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="bbde6-109">За использование непрерывного экспорта может взиматься дополнительная плата.</span><span class="sxs-lookup"><span data-stu-id="bbde6-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="bbde6-110">Проверьте свою [модель ценообразования](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="bbde6-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="bbde6-111">Прежде чем настраивать функцию непрерывного экспорта, рассмотрите некоторые альтернативные варианты.</span><span class="sxs-lookup"><span data-stu-id="bbde6-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="bbde6-112">Кнопка "Экспорт" в верхней части колонки метрик или поиска позволяет передавать таблицы и диаграммы в электронную таблицу Excel.</span><span class="sxs-lookup"><span data-stu-id="bbde6-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="bbde6-113">[Аналитика](app-insights-analytics.md) предоставляет эффективный язык запросов для телеметрии</span><span class="sxs-lookup"><span data-stu-id="bbde6-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="bbde6-114">и позволяет экспортировать результаты.</span><span class="sxs-lookup"><span data-stu-id="bbde6-114">It can also export results.</span></span>
* <span data-ttu-id="bbde6-115">Если вы собираетесь [исследовать данные в Power BI](app-insights-export-power-bi.md), это можно сделать, не прибегая к непрерывному экспорту.</span><span class="sxs-lookup"><span data-stu-id="bbde6-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="bbde6-116">[REST API доступа к данным](https://dev.applicationinsights.io/) позволяет получить доступ к телеметрии программным образом.</span><span class="sxs-lookup"><span data-stu-id="bbde6-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="bbde6-117">После того, как во время непрерывного экспорта данные будут скопированы в хранилище (где они могут храниться столько, сколько необходимо), они по-прежнему будут доступны в Application Insights в течение обычного [периода хранения](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="bbde6-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="bbde6-118"><a name="setup"></a>Создание непрерывного экспорта</span><span class="sxs-lookup"><span data-stu-id="bbde6-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="bbde6-119">В ресурсе Application Insights для своего приложения откройте раздел непрерывного экспорта и выберите **Добавить**:</span><span class="sxs-lookup"><span data-stu-id="bbde6-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Прокрутите вниз и щелкните "Непрерывный экспорт"](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="bbde6-121">Выберите типы данных телеметрии, которые хотите экспортировать.</span><span class="sxs-lookup"><span data-stu-id="bbde6-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="bbde6-122">Создайте или выберите [учетную запись хранения Azure](../storage/common/storage-introduction.md), в которой необходимо сохранить данные.</span><span class="sxs-lookup"><span data-stu-id="bbde6-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="bbde6-123">По умолчанию учетная запись хранения будет относиться к тому же географическому региону, что и ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bbde6-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="bbde6-124">Если вы выберете другой регион, может взиматься плата за передачу данных.</span><span class="sxs-lookup"><span data-stu-id="bbde6-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Последовательно щелкните "Добавить", "Назначение экспорта", "Учетная запись хранения" и затем создайте новое хранилище или выберите существующее.](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="bbde6-126">Создайте или выберите контейнер в хранилище:</span><span class="sxs-lookup"><span data-stu-id="bbde6-126">Create or select a container in the storage:</span></span>

    ![Щелкните "Выбор типов событий".](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="bbde6-128">После создания параметров экспорта запускается процедура экспорта.</span><span class="sxs-lookup"><span data-stu-id="bbde6-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="bbde6-129">Вы получите только те данные, которые поступят после создания параметров экспорта.</span><span class="sxs-lookup"><span data-stu-id="bbde6-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="bbde6-130">Возможна задержка около часа до появления данных в хранилище.</span><span class="sxs-lookup"><span data-stu-id="bbde6-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="bbde6-131">Изменение непрерывного экспорта</span><span class="sxs-lookup"><span data-stu-id="bbde6-131">To edit continuous export</span></span>

<span data-ttu-id="bbde6-132">Если позднее потребуется изменить типы событий, просто изменить параметры экспорта:</span><span class="sxs-lookup"><span data-stu-id="bbde6-132">If you want to change the event types later, just edit the export:</span></span>

![Щелкните "Выбор типов событий".](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="bbde6-134">Остановка непрерывного экспорта</span><span class="sxs-lookup"><span data-stu-id="bbde6-134">To stop continuous export</span></span>

<span data-ttu-id="bbde6-135">Чтобы остановить экспорт, нажмите кнопку "Отключить".</span><span class="sxs-lookup"><span data-stu-id="bbde6-135">To stop the export, click Disable.</span></span> <span data-ttu-id="bbde6-136">При повторном нажатии кнопки включения экспорт будет повторно запущен с новыми данными.</span><span class="sxs-lookup"><span data-stu-id="bbde6-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="bbde6-137">Пока экспорт был отключен, вы не будете получать данные, которые поступают на портал.</span><span class="sxs-lookup"><span data-stu-id="bbde6-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="bbde6-138">Чтобы остановить экспорт навсегда, удалите его.</span><span class="sxs-lookup"><span data-stu-id="bbde6-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="bbde6-139">Это действие не повлечет удаление данных из хранилища.</span><span class="sxs-lookup"><span data-stu-id="bbde6-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="bbde6-140">Не удается добавить или изменить параметры экспорта?</span><span class="sxs-lookup"><span data-stu-id="bbde6-140">Can't add or change an export?</span></span>
* <span data-ttu-id="bbde6-141">Чтобы добавить или изменить параметры экспорта, необходимы права доступа владельца, участника или участника Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bbde6-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="bbde6-142">[Дополнительные сведения о ролях][roles].</span><span class="sxs-lookup"><span data-stu-id="bbde6-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="bbde6-143"><a name="analyze"></a> Какие события вы получаете?</span><span class="sxs-lookup"><span data-stu-id="bbde6-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="bbde6-144">Экспортированные данные представляют собой необработанные данные телеметрии, полученные из приложения, за исключением того, что мы добавляем данные расположения, которые следует вычислять по IP-адресу клиента.</span><span class="sxs-lookup"><span data-stu-id="bbde6-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="bbde6-145">Данные, которые были отклонены [выборкой](app-insights-sampling.md) , не включаются в экспортированные данные.</span><span class="sxs-lookup"><span data-stu-id="bbde6-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="bbde6-146">Другие вычисляемые метрики не включаются.</span><span class="sxs-lookup"><span data-stu-id="bbde6-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="bbde6-147">Например, мы не экспортируем показатель среднего использования ЦП, но мы экспортируем необработанные данные телеметрии, на основе которых можно вычислить это среднее значение.</span><span class="sxs-lookup"><span data-stu-id="bbde6-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="bbde6-148">Данные также содержат результаты любого настроенного [веб-теста доступности](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="bbde6-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="bbde6-149">**Выборка.**</span><span class="sxs-lookup"><span data-stu-id="bbde6-149">**Sampling.**</span></span> <span data-ttu-id="bbde6-150">Если ваше приложение отправляет большие объемы данных, может сработать функция выборки и отправить только часть вашей телеметрии.</span><span class="sxs-lookup"><span data-stu-id="bbde6-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="bbde6-151">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="bbde6-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="bbde6-152"><a name="get"></a> Изучение данных</span><span class="sxs-lookup"><span data-stu-id="bbde6-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="bbde6-153">Проверить хранилище можно непосредственно на портале.</span><span class="sxs-lookup"><span data-stu-id="bbde6-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="bbde6-154">Нажмите кнопку **Обзор**, выберите учетную запись хранения, а затем откройте раздел **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="bbde6-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="bbde6-155">Чтобы проверить службу хранилища Azure в Visual Studio, выберите меню **Представление** и щелкните **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bbde6-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="bbde6-156">(Если этой команды нет в меню, установите пакет SDK для Azure: откройте диалоговое окно **Создание проекта**, разверните узел "Visual C#/Облако" и выберите **Get Microsoft Azure SDK for .NET** (Получить пакет Microsoft Azure SDK для .NET).)</span><span class="sxs-lookup"><span data-stu-id="bbde6-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="bbde6-157">При открытии хранилища больших двоичных объектов вы увидите контейнер с набором файлов больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="bbde6-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="bbde6-158">URI для каждого файла основан на имени ресурса Application Insights, ключе инструментирования, типе телеметрии, дате и времени.</span><span class="sxs-lookup"><span data-stu-id="bbde6-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="bbde6-159">(Имя ресурса содержит только строчные буквы, в ключе инструментирования опускаются дефисы).</span><span class="sxs-lookup"><span data-stu-id="bbde6-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Проверьте хранилище больших двоичных объектов с помощью подходящего средства.](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="bbde6-161">Дата и время имеют формат UTC и соответствуют моменту, когда элемент телеметрии был внесен в хранилище (не моменту его создания).</span><span class="sxs-lookup"><span data-stu-id="bbde6-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="bbde6-162">Поэтому при написании кода для загрузки данных можно линейно перемещаться по данным.</span><span class="sxs-lookup"><span data-stu-id="bbde6-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="bbde6-163">Путь имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="bbde6-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="bbde6-164">Where</span><span class="sxs-lookup"><span data-stu-id="bbde6-164">Where</span></span>

* <span data-ttu-id="bbde6-165">`blobCreationTimeUtc` — время создания большого двоичного объекта во внутреннем промежуточном хранилище.</span><span class="sxs-lookup"><span data-stu-id="bbde6-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="bbde6-166">`blobDeliveryTimeUtc` — время копирования большого двоичного объекта в целевое хранилище экспорта.</span><span class="sxs-lookup"><span data-stu-id="bbde6-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="bbde6-167"><a name="format"></a> Формат данных</span><span class="sxs-lookup"><span data-stu-id="bbde6-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="bbde6-168">Каждый большой двоичный объект является текстовым файлом, который содержит несколько строк, разделенных символом новой строки "\n".</span><span class="sxs-lookup"><span data-stu-id="bbde6-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="bbde6-169">Он содержит данные телеметрии, обрабатываемые примерно раз в 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="bbde6-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="bbde6-170">Каждая строка представляет точку данных телеметрии, например просмотр страницы или запроса.</span><span class="sxs-lookup"><span data-stu-id="bbde6-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="bbde6-171">Каждая строка представляет собой неформатированный JSON-документ.</span><span class="sxs-lookup"><span data-stu-id="bbde6-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="bbde6-172">Если вы хотите просмотреть его, откройте документ в Visual Studio и последовательно выберите "Правка", "Дополнительно", "Формат файла":</span><span class="sxs-lookup"><span data-stu-id="bbde6-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Просмотрите данные телеметрии с помощью подходящего средства.](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="bbde6-174">Продолжительность времени измеряется в тактах, где 10 000 тактов составляют 1 мс.</span><span class="sxs-lookup"><span data-stu-id="bbde6-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="bbde6-175">Например, следующие значения показывают время 1 мс для отправки запроса из браузера, 3 мс для его получения и 1,8 с для обработки страницы в браузере:</span><span class="sxs-lookup"><span data-stu-id="bbde6-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="bbde6-176">Подробный справочник по модели данных типов и значений свойств.</span><span class="sxs-lookup"><span data-stu-id="bbde6-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="bbde6-177">Обработка данных</span><span class="sxs-lookup"><span data-stu-id="bbde6-177">Processing the data</span></span>
<span data-ttu-id="bbde6-178">Для небольших объемов данных можно написать код, который будет выделять элементы данных, записывать их в электронную таблицу и т. д.</span><span class="sxs-lookup"><span data-stu-id="bbde6-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="bbde6-179">Например:</span><span class="sxs-lookup"><span data-stu-id="bbde6-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="bbde6-180">Больший пример кода см. в статье [Пошаговое руководство. Экспорт в SQL из Application Insights с использованием Stream Analytics][exportasa].</span><span class="sxs-lookup"><span data-stu-id="bbde6-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="bbde6-181"><a name="delete"></a>Удаление старых данных</span><span class="sxs-lookup"><span data-stu-id="bbde6-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="bbde6-182">Обратите внимание на то, что вы несете ответственность за управление емкостью хранилища и удаление при необходимости старых данных.</span><span class="sxs-lookup"><span data-stu-id="bbde6-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="bbde6-183">При повторном создании ключа хранилища...</span><span class="sxs-lookup"><span data-stu-id="bbde6-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="bbde6-184">Если изменить ключ хранилища, непрерывный экспорт перестанет работать.</span><span class="sxs-lookup"><span data-stu-id="bbde6-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="bbde6-185">Вы увидите уведомление в учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="bbde6-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="bbde6-186">Откройте колонку непрерывного экспорта и измените параметры экспорта.</span><span class="sxs-lookup"><span data-stu-id="bbde6-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="bbde6-187">Измените параметр назначения экспорта, но оставьте выбранным то же самое хранилище.</span><span class="sxs-lookup"><span data-stu-id="bbde6-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="bbde6-188">Нажмите кнопку "ОК" для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="bbde6-188">Click OK to confirm.</span></span>

![Измените параметры непрерывного экспорта, откройте и закройте место назначения экспорта.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="bbde6-190">Непрерывный экспорт будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="bbde6-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="bbde6-191">Примеры экспорта</span><span class="sxs-lookup"><span data-stu-id="bbde6-191">Export samples</span></span>

* <span data-ttu-id="bbde6-192">[Экспорт в SQL с использованием Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="bbde6-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="bbde6-193">Пример 2 с использованием Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bbde6-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="bbde6-194">Для больших объемов данных рассмотрите возможность использования [HDInsight](https://azure.microsoft.com/services/hdinsight/) – кластеров Hadoop в облаке.</span><span class="sxs-lookup"><span data-stu-id="bbde6-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="bbde6-195">HDInsight предусматривает широкий набор технологий для анализа больших объемов данных и управления ими. Кроме того, решение можно использовать для обработки данных, экспортированных из Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bbde6-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="bbde6-196">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="bbde6-196">Q & A</span></span>
* <span data-ttu-id="bbde6-197">*Все, что мне требуется, – всего лишь один раз загрузить диаграмму.*</span><span class="sxs-lookup"><span data-stu-id="bbde6-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="bbde6-198">Да, это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="bbde6-198">Yes, you can do that.</span></span> <span data-ttu-id="bbde6-199">В верхней части колонки щелкните **Экспорт данных**.</span><span class="sxs-lookup"><span data-stu-id="bbde6-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="bbde6-200">*Параметры экспорта настроены, но в хранилище нет данных.*</span><span class="sxs-lookup"><span data-stu-id="bbde6-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="bbde6-201">Получала ли служба Application Insights какие-либо данные телеметрии из вашего приложения с момента настройки параметров экспорта?</span><span class="sxs-lookup"><span data-stu-id="bbde6-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="bbde6-202">Вы получите только новые данные.</span><span class="sxs-lookup"><span data-stu-id="bbde6-202">You'll only receive new data.</span></span>
* <span data-ttu-id="bbde6-203">*Я попытался настроить параметры экспорта, но было отказано в доступе.*</span><span class="sxs-lookup"><span data-stu-id="bbde6-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="bbde6-204">Если учетная запись принадлежит организации, необходимо быть членом группы владельцев или участников.</span><span class="sxs-lookup"><span data-stu-id="bbde6-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="bbde6-205">*Могу ли я экспортировать данные непосредственно в свое локальное хранилище?*</span><span class="sxs-lookup"><span data-stu-id="bbde6-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="bbde6-206">Нет.</span><span class="sxs-lookup"><span data-stu-id="bbde6-206">No, sorry.</span></span> <span data-ttu-id="bbde6-207">Наш механизм экспорта в настоящее время работает только для хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bbde6-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="bbde6-208">*Существует ли предел для объема данных, помещаемых в мое хранилище?*</span><span class="sxs-lookup"><span data-stu-id="bbde6-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="bbde6-209">Нет.</span><span class="sxs-lookup"><span data-stu-id="bbde6-209">No.</span></span> <span data-ttu-id="bbde6-210">Мы будем хранить переданные данные в хранилище, пока вы не удалите данные экспорта.</span><span class="sxs-lookup"><span data-stu-id="bbde6-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="bbde6-211">Мы остановим передачу данных, если столкнемся с внешними ограничениями для хранилища больших двоичных объектов, но хранилище очень большое.</span><span class="sxs-lookup"><span data-stu-id="bbde6-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="bbde6-212">Вы можете настроить объем используемого хранилища.</span><span class="sxs-lookup"><span data-stu-id="bbde6-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="bbde6-213">*Сколько больших двоичных объектов отображается в хранилище?*</span><span class="sxs-lookup"><span data-stu-id="bbde6-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="bbde6-214">Для каждого типа данных, выбранных для экспорта, каждую минуту создается новый большой двоичный объект (при наличии данных).</span><span class="sxs-lookup"><span data-stu-id="bbde6-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="bbde6-215">Кроме того, для приложений с высоким трафиком выделяются дополнительные единицы разделов.</span><span class="sxs-lookup"><span data-stu-id="bbde6-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="bbde6-216">В этом случае каждую минуту каждая единица создает большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="bbde6-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="bbde6-217">*После повторного создания ключа для моего хранилища или изменения имени контейнера экспорт больше не работает.*</span><span class="sxs-lookup"><span data-stu-id="bbde6-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="bbde6-218">Измените параметры экспорта и откройте колонку назначения экспорта.</span><span class="sxs-lookup"><span data-stu-id="bbde6-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="bbde6-219">Оставьте выбранным прежнее хранилище и нажмите кнопку "OK" для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="bbde6-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="bbde6-220">Экспорт будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="bbde6-220">Export will restart.</span></span> <span data-ttu-id="bbde6-221">Если это изменение было сделано в течение последних нескольких дней, данные не будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="bbde6-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="bbde6-222">*Можно ли приостановить экспорт?*</span><span class="sxs-lookup"><span data-stu-id="bbde6-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="bbde6-223">Да.</span><span class="sxs-lookup"><span data-stu-id="bbde6-223">Yes.</span></span> <span data-ttu-id="bbde6-224">Нажмите кнопку "Отключить".</span><span class="sxs-lookup"><span data-stu-id="bbde6-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="bbde6-225">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="bbde6-225">Code samples</span></span>

* <span data-ttu-id="bbde6-226">[Пример с использованием Stream Analytics](app-insights-export-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="bbde6-226">[Stream Analytics sample](app-insights-export-stream-analytics.md)</span></span>
* <span data-ttu-id="bbde6-227">[Экспорт в SQL с использованием Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="bbde6-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="bbde6-228">Подробный справочник по модели данных типов и значений свойств.</span><span class="sxs-lookup"><span data-stu-id="bbde6-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
