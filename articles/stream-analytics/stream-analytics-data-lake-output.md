---
title: "выходные данные для хранилища Озера данных Analytics aaaStream | Документы Microsoft"
description: "Настройка проверки подлинности и авторизации хранилища озера данных в задании Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="da83b-103">Выходные данные хранилища озера данных в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="da83b-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="da83b-104">Задания Stream Analytics поддерживают несколько методов вывода, одним из которых является [хранилище озера данных Azure](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="da83b-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="da83b-105">Хранилище озера данных Azure — это крупномасштабный репозиторий корпоративного уровня для рабочих нагрузок анализа больших данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="da83b-106">Хранилище Озера данных позволяет toostore данных любого размера, типа и приема скорости для ведения операционной и исследовательской аналитики.</span><span class="sxs-lookup"><span data-stu-id="da83b-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="da83b-107">Авторизация учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="da83b-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="da83b-108">При выборе хранилища Озера данных как выходные данные в hello Azure portal предложит tooauthorize использовать существующее хранилище Озера данных или toorequest доступ к хранилищу Озера данных toohello через hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="da83b-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="da83b-109">Если у вас уже есть доступ к хранилищу Озера tooData, нажмите кнопку «авторизовать» и на короткое время, в течение которых страница появится всплывающее окно, показывающее, «Перенаправление tooauthorization».</span><span class="sxs-lookup"><span data-stu-id="da83b-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="da83b-110">Страница приветствия автоматически закроется и откроется страница hello, позволит tooconfigure hello хранилища Озера данных вывода.</span><span class="sxs-lookup"><span data-stu-id="da83b-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="da83b-111">Если вы еще не зарегистрировались для хранилища Озера данных, выполните tooinitiate «Зарегистрироваться» связь hello hello запроса или выполните hello [получить работы инструкции](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="da83b-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="da83b-112">Настройка свойств вывода hello хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="da83b-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="da83b-113">Получив hello учетной записи хранилища Озера данных с проверкой подлинности, можно настроить свойства hello для получения выходных данных в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="da83b-114">в следующей таблице Hello — hello список имен свойств и их описание tooconfigure, которые выходные данные в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="da83b-115"><B>Имя свойства</B></span><span class="sxs-lookup"><span data-stu-id="da83b-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="da83b-116"><B>Описание</B></span><span class="sxs-lookup"><span data-stu-id="da83b-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-117">Псевдоним выходных данных</span><span class="sxs-lookup"><span data-stu-id="da83b-117">Output Alias</span></span></td>
<td><span data-ttu-id="da83b-118">Это понятное имя, используемое в выходных данных запроса toothis хранилища Озера данных запросов toodirect hello.</span><span class="sxs-lookup"><span data-stu-id="da83b-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-119">Учетная запись хранилища озера данных</span><span class="sxs-lookup"><span data-stu-id="da83b-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="da83b-120">Имя учетной записи хранения hello, где вы отправляете выходными данными Hello.</span><span class="sxs-lookup"><span data-stu-id="da83b-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="da83b-121">Появится список hello, пользователь имеет доступ к учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-122">Шаблон префикса пути [<I>необязательное свойство</I>]</span><span class="sxs-lookup"><span data-stu-id="da83b-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="da83b-123">Здравствуйте, toowrite путь, используемый файл файлов в пределах hello указан учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="da83b-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="da83b-124">{date}, {time}</span></span><BR><span data-ttu-id="da83b-125">Пример 1. folder1/logs/{дата}/{время}</span><span class="sxs-lookup"><span data-stu-id="da83b-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="da83b-126">Пример 2. folder1/logs/{дата}</span><span class="sxs-lookup"><span data-stu-id="da83b-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-127">Формат даты [<I>необязательное свойство</I>]</span><span class="sxs-lookup"><span data-stu-id="da83b-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="da83b-128">Если маркер hello даты используется hello префикс пути, можно выбрать формат даты hello, в котором упорядочены файлов.</span><span class="sxs-lookup"><span data-stu-id="da83b-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="da83b-129">Пример: ГГГГ/ММ/ДД</span><span class="sxs-lookup"><span data-stu-id="da83b-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-130">Формат времени [<I>необязательное свойство</I>]</span><span class="sxs-lookup"><span data-stu-id="da83b-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="da83b-131">Если токен hello времени используется в hello префикс пути, укажите hello формат времени, в котором упорядочены файлов.</span><span class="sxs-lookup"><span data-stu-id="da83b-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="da83b-132">В настоящее время поддерживается только hello значение — HH.</span><span class="sxs-lookup"><span data-stu-id="da83b-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-133">Формат сериализации событий</span><span class="sxs-lookup"><span data-stu-id="da83b-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="da83b-134">Формат сериализации для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-134">Serialization format for output data.</span></span> <span data-ttu-id="da83b-135">Поддерживаются форматы JSON, CSV и Avro.</span><span class="sxs-lookup"><span data-stu-id="da83b-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-136">Кодирование</span><span class="sxs-lookup"><span data-stu-id="da83b-136">Encoding</span></span></td>
<td><span data-ttu-id="da83b-137">Если используется формат CSV или JSON, необходимо указать формат кодирования.</span><span class="sxs-lookup"><span data-stu-id="da83b-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="da83b-138">UTF-8 является hello поддерживается только формат кодировки в данный момент.</span><span class="sxs-lookup"><span data-stu-id="da83b-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-139">Разделитель</span><span class="sxs-lookup"><span data-stu-id="da83b-139">Delimiter</span></span></td>
<td><span data-ttu-id="da83b-140">Применяется только для сериализации CSV-файлов.</span><span class="sxs-lookup"><span data-stu-id="da83b-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="da83b-141">Служба Stream Analytics позволяет использовать ряд распространенных разделителей для сериализации данных в формате CSV.</span><span class="sxs-lookup"><span data-stu-id="da83b-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="da83b-142">Поддерживаются такие разделители: запятая, точка с запятой, пробел, табуляция и вертикальная черта.</span><span class="sxs-lookup"><span data-stu-id="da83b-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="da83b-143">Формат</span><span class="sxs-lookup"><span data-stu-id="da83b-143">Format</span></span></td>
<td><span data-ttu-id="da83b-144">Применяется только для сериализации JSON.</span><span class="sxs-lookup"><span data-stu-id="da83b-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="da83b-145">Построчно указывает, hello выходные данные будут отформатированы, что каждый объект JSON, разделенные на новую строку.</span><span class="sxs-lookup"><span data-stu-id="da83b-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="da83b-146">Массив задает, hello выходные данные будут отформатированы в виде массива объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="da83b-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="da83b-147">Обновление авторизации хранилища озера данных</span><span class="sxs-lookup"><span data-stu-id="da83b-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="da83b-148">В настоящее время имеется ограничение где hello токена проверки подлинности необходимы toobe вручную обновляются каждые 90 дней, для всех заданий с выводом хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="da83b-149">Необходимо также toore-проверка подлинности учетной записи хранилища Озера данных, если пароль были изменены с момента создания задания или раз проходил проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="da83b-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="da83b-150">Признаком этой проблемы является выходные данные задания и ошибки в журналах операций hello, указывающее необходимость в повторной авторизации.</span><span class="sxs-lookup"><span data-stu-id="da83b-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="da83b-151">tooresolve эту проблему, остановите выполнение задания и go вывода tooyour хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="da83b-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="da83b-152">Щелкните ссылку «Обновить авторизации» hello и на короткое время, в течение которых страница появится всплывающее окно, показывающее, «Перенаправление tooauthorization..».</span><span class="sxs-lookup"><span data-stu-id="da83b-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="da83b-153">Страница приветствия автоматически закроется и в случае успешного выполнения указывает «Авторизация успешно возобновлена».</span><span class="sxs-lookup"><span data-stu-id="da83b-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="da83b-154">Затем необходимо tooclick «Сохранить» hello нижней части страницы приветствия и можно продолжить, снова запустите задание из hello потери данных tooavoid время последней остановки.</span><span class="sxs-lookup"><span data-stu-id="da83b-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

