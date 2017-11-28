---
title: "При экспорте данных телеметрии Application Insights aaaContinuous | Документы Microsoft"
description: "Экспорт toostorage данных диагностики и использования в Microsoft Azure и загрузить его оттуда."
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="966f7-103">Экспорт данных телеметрии из Application Insights</span><span class="sxs-lookup"><span data-stu-id="966f7-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="966f7-104">Требуется tookeep телеметрии дольше, чем стандартный срок hello?</span><span class="sxs-lookup"><span data-stu-id="966f7-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="966f7-105">или анализировать ее особым образом?</span><span class="sxs-lookup"><span data-stu-id="966f7-105">Or process it in some specialized way?</span></span> <span data-ttu-id="966f7-106">Функция "Непрерывный экспорт" идеально подходит для этого.</span><span class="sxs-lookup"><span data-stu-id="966f7-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="966f7-107">Hello события, отображаемые на портале Application Insights hello могут быть экспортированного toostorage в Microsoft Azure в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="966f7-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="966f7-108">Из него можно загрузить данные и записи, независимо от кода, которые должны tooprocess его.</span><span class="sxs-lookup"><span data-stu-id="966f7-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="966f7-109">За использование непрерывного экспорта может взиматься дополнительная плата.</span><span class="sxs-lookup"><span data-stu-id="966f7-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="966f7-110">Проверьте свою [модель ценообразования](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="966f7-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="966f7-111">Перед настройкой непрерывный экспорт, существуют некоторые альтернативные решения, может потребоваться tooconsider:</span><span class="sxs-lookup"><span data-stu-id="966f7-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="966f7-112">Кнопка "экспортировать" Hello вверху hello показателей или поиска колонке позволяет передавать электронную таблицу Excel tooan таблиц и диаграмм.</span><span class="sxs-lookup"><span data-stu-id="966f7-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="966f7-113">[Аналитика](app-insights-analytics.md) предоставляет эффективный язык запросов для телеметрии</span><span class="sxs-lookup"><span data-stu-id="966f7-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="966f7-114">и позволяет экспортировать результаты.</span><span class="sxs-lookup"><span data-stu-id="966f7-114">It can also export results.</span></span>
* <span data-ttu-id="966f7-115">Если вы рассматриваете возможность слишком[изучение данных в Power BI](app-insights-export-power-bi.md), это можно сделать без использования непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="966f7-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="966f7-116">Hello [REST API доступа к данным](https://dev.applicationinsights.io/) позволяет программно получить доступ к телеметрии.</span><span class="sxs-lookup"><span data-stu-id="966f7-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="966f7-117">После экспорта непрерывного копирует вашей toostorage данных (где он может оставаться при условии, что вам нравится), по-прежнему доступен в Application Insights для hello обычные [срок хранения](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="966f7-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="966f7-118"><a name="setup"></a>Создание непрерывного экспорта</span><span class="sxs-lookup"><span data-stu-id="966f7-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="966f7-119">В hello ресурс Application Insights для своего приложения, откройте непрерывный Экспорт и выберите **добавить**:</span><span class="sxs-lookup"><span data-stu-id="966f7-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Прокрутите вниз и щелкните "Непрерывный экспорт"](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="966f7-121">Выберите типы данных телеметрии hello требуется tooexport.</span><span class="sxs-lookup"><span data-stu-id="966f7-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="966f7-122">Создайте или выберите [учетной записи хранилища Azure](../storage/common/storage-introduction.md) место toostore hello данных.</span><span class="sxs-lookup"><span data-stu-id="966f7-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="966f7-123">По умолчанию место хранения hello задается toohello одном географическом регионе ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="966f7-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="966f7-124">Если вы выберете другой регион, может взиматься плата за передачу данных.</span><span class="sxs-lookup"><span data-stu-id="966f7-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Последовательно щелкните "Добавить", "Назначение экспорта", "Учетная запись хранения" и затем создайте новое хранилище или выберите существующее.](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="966f7-126">Создайте или выберите контейнер хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="966f7-126">Create or select a container in hello storage:</span></span>

    ![Щелкните "Выбор типов событий".](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="966f7-128">После создания параметров экспорта запускается процедура экспорта.</span><span class="sxs-lookup"><span data-stu-id="966f7-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="966f7-129">Можно получить только данных, поступающих после создания hello экспорта.</span><span class="sxs-lookup"><span data-stu-id="966f7-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="966f7-130">Может быть задержка до одного часа до появления данных в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="966f7-131">непрерывный Экспорт tooedit</span><span class="sxs-lookup"><span data-stu-id="966f7-131">tooedit continuous export</span></span>

<span data-ttu-id="966f7-132">Типы событий toochange hello позже, просто измените hello экспорта:</span><span class="sxs-lookup"><span data-stu-id="966f7-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Щелкните "Выбор типов событий".](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="966f7-134">непрерывный Экспорт toostop</span><span class="sxs-lookup"><span data-stu-id="966f7-134">toostop continuous export</span></span>

<span data-ttu-id="966f7-135">Экспорт toostop hello, отключить.</span><span class="sxs-lookup"><span data-stu-id="966f7-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="966f7-136">При нажатии кнопки включения экспорта hello перезапустится с новыми данными.</span><span class="sxs-lookup"><span data-stu-id="966f7-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="966f7-137">Вы не сможете получить данные hello, поступивших в портал hello во время отключения экспорта.</span><span class="sxs-lookup"><span data-stu-id="966f7-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="966f7-138">Экспорт hello toostop навсегда, удалите его.</span><span class="sxs-lookup"><span data-stu-id="966f7-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="966f7-139">Это действие не повлечет удаление данных из хранилища.</span><span class="sxs-lookup"><span data-stu-id="966f7-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="966f7-140">Не удается добавить или изменить параметры экспорта?</span><span class="sxs-lookup"><span data-stu-id="966f7-140">Can't add or change an export?</span></span>
* <span data-ttu-id="966f7-141">tooadd или измените экспортов, необходимы права доступа владельца, участника или участников аналитики приложений.</span><span class="sxs-lookup"><span data-stu-id="966f7-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="966f7-142">[Дополнительные сведения о ролях][roles].</span><span class="sxs-lookup"><span data-stu-id="966f7-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="966f7-143"><a name="analyze"></a> Какие события вы получаете?</span><span class="sxs-lookup"><span data-stu-id="966f7-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="966f7-144">Hello экспортированных данных — hello необработанные телеметрии, полученных из своего приложения, за исключением того, что мы добавляем расположение данных, которые мы можем вычислить из IP-адрес клиента hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="966f7-145">Данные были отклонены, [выборки](app-insights-sampling.md) не включается в hello экспортированы данные.</span><span class="sxs-lookup"><span data-stu-id="966f7-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="966f7-146">Другие вычисляемые метрики не включаются.</span><span class="sxs-lookup"><span data-stu-id="966f7-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="966f7-147">Например мы не экспортирует среднее использование ЦП, но мы экспортировать hello необработанные данные телеметрии, из которого вычисляется среднее hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="966f7-148">Hello данных также включает hello результаты любого [доступности веб-тесты](app-insights-monitor-web-app-availability.md) , были установлены.</span><span class="sxs-lookup"><span data-stu-id="966f7-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="966f7-149">**Выборка.**</span><span class="sxs-lookup"><span data-stu-id="966f7-149">**Sampling.**</span></span> <span data-ttu-id="966f7-150">Если приложение отправляет большой объем данных, функция выборки hello может работать и отправьте лишь часть телеметрии hello создан.</span><span class="sxs-lookup"><span data-stu-id="966f7-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="966f7-151">Дополнительная информация о выборке.</span><span class="sxs-lookup"><span data-stu-id="966f7-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="966f7-152"><a name="get"></a>Проверки данных hello</span><span class="sxs-lookup"><span data-stu-id="966f7-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="966f7-153">Рекомендуется проверить hello хранения непосредственно на портале hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="966f7-154">Нажмите кнопку **Обзор**, выберите учетную запись хранения, а затем откройте раздел **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="966f7-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="966f7-155">tooinspect хранилища Azure в Visual Studio откройте **представление**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="966f7-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="966f7-156">(Если у вас нет этой команды меню, необходимо tooinstall hello Azure SDK: Привет открыть **новый проект** диалоговое окно, откройте Visual C# / облака и выберите **получить Microsoft Azure SDK для .NET**.)</span><span class="sxs-lookup"><span data-stu-id="966f7-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="966f7-157">При открытии хранилища больших двоичных объектов вы увидите контейнер с набором файлов больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="966f7-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="966f7-158">Hello URI каждого файла на основе ваше имя ресурса Application Insights, ключ инструментирования, телеметрии тип, дату и время.</span><span class="sxs-lookup"><span data-stu-id="966f7-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="966f7-159">(имя ресурса hello только нижний регистр, и ключ инструментирования hello не содержит тире).</span><span class="sxs-lookup"><span data-stu-id="966f7-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Проверять hello хранилища больших двоичных объектов с помощью подходящего средства](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="966f7-161">Hello Дата и время UTC и при телеметрии hello был внесен в хранилище hello — не hello время его создания.</span><span class="sxs-lookup"><span data-stu-id="966f7-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="966f7-162">Поэтому при написании кода toodownload hello данных, его можно перемещать линейно через hello данных.</span><span class="sxs-lookup"><span data-stu-id="966f7-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="966f7-163">Вот формы hello hello пути:</span><span class="sxs-lookup"><span data-stu-id="966f7-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="966f7-164">Where</span><span class="sxs-lookup"><span data-stu-id="966f7-164">Where</span></span>

* <span data-ttu-id="966f7-165">`blobCreationTimeUtc`При создании BLOB-объект был в hello внутренней промежуточного хранения хранилища</span><span class="sxs-lookup"><span data-stu-id="966f7-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="966f7-166">`blobDeliveryTimeUtc`— время hello при скопированный toohello экспорта конечное хранилище BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="966f7-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="966f7-167"><a name="format"></a> Формат данных</span><span class="sxs-lookup"><span data-stu-id="966f7-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="966f7-168">Каждый большой двоичный объект является текстовым файлом, который содержит несколько строк, разделенных символом новой строки "\n".</span><span class="sxs-lookup"><span data-stu-id="966f7-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="966f7-169">Он содержит телеметрии hello, обработанных за период времени, половина около минуты.</span><span class="sxs-lookup"><span data-stu-id="966f7-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="966f7-170">Каждая строка представляет точку данных телеметрии, например просмотр страницы или запроса.</span><span class="sxs-lookup"><span data-stu-id="966f7-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="966f7-171">Каждая строка представляет собой неформатированный JSON-документ.</span><span class="sxs-lookup"><span data-stu-id="966f7-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="966f7-172">Toosit и stare его, откройте его в Visual Studio и выберите изменение, Дополнительно, файл форматирования:</span><span class="sxs-lookup"><span data-stu-id="966f7-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Представление hello телеметрии с помощью подходящего средства](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="966f7-174">Продолжительность времени измеряется в тактах, где 10 000 тактов составляют 1 мс.</span><span class="sxs-lookup"><span data-stu-id="966f7-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="966f7-175">Например, эти значения показывают время 1 мс toosend запроса в браузере hello мс tooreceive и 1.8s tooprocess hello страницы в браузере hello:</span><span class="sxs-lookup"><span data-stu-id="966f7-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="966f7-176">Подробные данные модели ссылок для значений и типы свойств hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="966f7-177">Обработка данных hello</span><span class="sxs-lookup"><span data-stu-id="966f7-177">Processing hello data</span></span>
<span data-ttu-id="966f7-178">Небольших масштабах записи данных друг от друга, некоторые toopull кода, его чтение в электронную таблицу и так далее.</span><span class="sxs-lookup"><span data-stu-id="966f7-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="966f7-179">Например:</span><span class="sxs-lookup"><span data-stu-id="966f7-179">For example:</span></span>

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

<span data-ttu-id="966f7-180">Больший пример кода см. в статье [Пошаговое руководство. Экспорт в SQL из Application Insights с использованием Stream Analytics][exportasa].</span><span class="sxs-lookup"><span data-stu-id="966f7-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="966f7-181"><a name="delete"></a>Удаление старых данных</span><span class="sxs-lookup"><span data-stu-id="966f7-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="966f7-182">Обратите внимание на то, что вы несете ответственность за управление емкость хранилища и удаление старых данных hello, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="966f7-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="966f7-183">При повторном создании ключа хранилища...</span><span class="sxs-lookup"><span data-stu-id="966f7-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="966f7-184">При изменении хранилища ключей tooyour hello непрерывный Экспорт перестанут работать.</span><span class="sxs-lookup"><span data-stu-id="966f7-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="966f7-185">Вы увидите уведомление в учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="966f7-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="966f7-186">Откройте колонку непрерывный Экспорт hello и отредактируйте экспорта.</span><span class="sxs-lookup"><span data-stu-id="966f7-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="966f7-187">Редактировать hello назначения экспорта, но просто оставьте hello выбран же хранилище.</span><span class="sxs-lookup"><span data-stu-id="966f7-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="966f7-188">Нажмите кнопку ОК tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="966f7-188">Click OK tooconfirm.</span></span>

![Hello изменить непрерывный экспорт, открыть и закрыть три назначение экспорта.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="966f7-190">Hello непрерывный экспорт будет перезапущена.</span><span class="sxs-lookup"><span data-stu-id="966f7-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="966f7-191">Примеры экспорта</span><span class="sxs-lookup"><span data-stu-id="966f7-191">Export samples</span></span>

* <span data-ttu-id="966f7-192">[С помощью Stream Analytics tooSQL экспорта][exportasa]</span><span class="sxs-lookup"><span data-stu-id="966f7-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="966f7-193">Пример 2 с использованием Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="966f7-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="966f7-194">На больших масштабах, рассмотрите возможность [HDInsight](https://azure.microsoft.com/services/hdinsight/) -кластеров Hadoop в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="966f7-195">HDInsight предоставляет широкий набор технологий для управления и анализа больших данных, и его можно использовать tooprocess данные, которые были экспортированы из Application Insights.</span><span class="sxs-lookup"><span data-stu-id="966f7-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="966f7-196">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="966f7-196">Q & A</span></span>
* <span data-ttu-id="966f7-197">*Все, что мне требуется, – всего лишь один раз загрузить диаграмму.*</span><span class="sxs-lookup"><span data-stu-id="966f7-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="966f7-198">Да, это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="966f7-198">Yes, you can do that.</span></span> <span data-ttu-id="966f7-199">Hello верхней части колонки hello, нажмите кнопку **Экспорт данных**.</span><span class="sxs-lookup"><span data-stu-id="966f7-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="966f7-200">*Параметры экспорта настроены, но в хранилище нет данных.*</span><span class="sxs-lookup"><span data-stu-id="966f7-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="966f7-201">Был Application Insights получен все данные телеметрии из приложения, так как настроено hello экспорта?</span><span class="sxs-lookup"><span data-stu-id="966f7-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="966f7-202">Вы получите только новые данные.</span><span class="sxs-lookup"><span data-stu-id="966f7-202">You'll only receive new data.</span></span>
* <span data-ttu-id="966f7-203">*Я попытался tooset копирование экспорт, но было отказано в доступе*</span><span class="sxs-lookup"><span data-stu-id="966f7-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="966f7-204">Если hello учетная запись принадлежит вашей организации, у вас toobe членом hello владельцев или участники групп.</span><span class="sxs-lookup"><span data-stu-id="966f7-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="966f7-205">*Можно экспортировать прямой toomy собственные к локальному хранилищу*</span><span class="sxs-lookup"><span data-stu-id="966f7-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="966f7-206">Нет.</span><span class="sxs-lookup"><span data-stu-id="966f7-206">No, sorry.</span></span> <span data-ttu-id="966f7-207">Наш механизм экспорта в настоящее время работает только для хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="966f7-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="966f7-208">*Есть ли все toohello ограничить объем данных, помещаемых в хранилище my?*</span><span class="sxs-lookup"><span data-stu-id="966f7-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="966f7-209">Нет.</span><span class="sxs-lookup"><span data-stu-id="966f7-209">No.</span></span> <span data-ttu-id="966f7-210">Мы будем хранить Принудительная отправка данных до момента удаления экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="966f7-211">Мы будем останавливаться, если мы получаем hello ограничений на внешнее хранилище BLOB-объектов, но это довольно большой.</span><span class="sxs-lookup"><span data-stu-id="966f7-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="966f7-212">Он работает tooyou toocontrol объем хранилища используется.</span><span class="sxs-lookup"><span data-stu-id="966f7-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="966f7-213">*Сколько большие двоичные объекты должны увидеть в хранилище hello*</span><span class="sxs-lookup"><span data-stu-id="966f7-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="966f7-214">Для каждого данные из выбранного tooexport, новый большой двоичный объект создается каждую минуту (при наличии данных).</span><span class="sxs-lookup"><span data-stu-id="966f7-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="966f7-215">Кроме того, для приложений с высоким трафиком выделяются дополнительные единицы разделов.</span><span class="sxs-lookup"><span data-stu-id="966f7-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="966f7-216">В этом случае каждую минуту каждая единица создает большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="966f7-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="966f7-217">*Я повторно хранилища ключей toomy hello или изменено имя hello hello контейнера, а теперь hello экспорта не работает.*</span><span class="sxs-lookup"><span data-stu-id="966f7-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="966f7-218">Изменить Экспорт hello и откройте колонку назначения экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="966f7-219">Оставьте hello, как и ранее выбранные же хранилище и нажмите кнопку ОК tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="966f7-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="966f7-220">Экспорт будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="966f7-220">Export will restart.</span></span> <span data-ttu-id="966f7-221">В случае изменения hello в hello за последние несколько дней сохранности данных.</span><span class="sxs-lookup"><span data-stu-id="966f7-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="966f7-222">*Можно приостановить hello экспорта*</span><span class="sxs-lookup"><span data-stu-id="966f7-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="966f7-223">Да.</span><span class="sxs-lookup"><span data-stu-id="966f7-223">Yes.</span></span> <span data-ttu-id="966f7-224">Нажмите кнопку "Отключить".</span><span class="sxs-lookup"><span data-stu-id="966f7-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="966f7-225">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="966f7-225">Code samples</span></span>

* <span data-ttu-id="966f7-226">[Пример с использованием Stream Analytics](app-insights-export-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="966f7-226">[Stream Analytics sample](app-insights-export-stream-analytics.md)</span></span>
* <span data-ttu-id="966f7-227">[С помощью Stream Analytics tooSQL экспорта][exportasa]</span><span class="sxs-lookup"><span data-stu-id="966f7-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="966f7-228">Подробные данные модели ссылок для значений и типы свойств hello.</span><span class="sxs-lookup"><span data-stu-id="966f7-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
