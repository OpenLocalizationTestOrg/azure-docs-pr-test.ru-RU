---
title: "aaaFix ошибки подключения SQL, временная ошибка | Документы Microsoft"
description: "Узнайте, как tootroubleshoot, диагностика и предотвращение ошибок подключения SQL или временная ошибка в базе данных SQL Azure. "
keywords: "подключение sql,строка подключения,проблемы с подключением, временная ошибка,ошибка подключения"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="27e56-104">Устранение, диагностика и предотвращение ошибок подключения SQL и временных ошибок для базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="27e56-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="27e56-105">В этой статье описывается, как tooprevent, устранение неполадок, диагностики и устранения ошибок подключения и временные ошибки, возникшие клиентского приложения при работе с базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="27e56-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="27e56-106">Узнайте, как tooconfigure логику повторных попыток, создать строку соединения hello и настройка других параметров подключения.</span><span class="sxs-lookup"><span data-stu-id="27e56-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="27e56-107">Временные ошибки (временные сбои)</span><span class="sxs-lookup"><span data-stu-id="27e56-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="27e56-108">Временные ошибки (или временные сбои) возникают из-за причин, которые вскоре устраняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="27e56-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="27e56-109">Случайные причина временных ошибок — когда hello системы Azure быстро перемещается аппаратных ресурсов toobetter балансировать различных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="27e56-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="27e56-110">Большинство этих событий перенастройки часто завершаются менее чем за 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="27e56-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="27e56-111">В течение этого интервала времени перенастройки имеется подключение выдает tooAzure базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="27e56-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="27e56-112">Подключение базы данных SQL должен быть tooAzure построение приложений tooexpect эти временные ошибки дескриптор их, реализовав логику в своем коде, а не отображает их toousers как ошибки приложения повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="27e56-113">Если клиентская программа использует ADO.NET, программа укажет о временная ошибка hello throw hello объекта **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="27e56-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="27e56-114">Hello **номер** свойства можно сравнивать с hello список временных ошибок верхней hello части статьи hello: [коды ошибок SQL для клиентских приложений баз данных SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="27e56-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="27e56-115">Подключения и команды</span><span class="sxs-lookup"><span data-stu-id="27e56-115">Connection versus command</span></span>
<span data-ttu-id="27e56-116">Будет повторять попытки соединения SQL hello или установить ее еще раз, в зависимости от следующих hello:</span><span class="sxs-lookup"><span data-stu-id="27e56-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="27e56-117">**Временная ошибка возникает во время попытки подключения**: hello соединения следует повторить после задержки в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="27e56-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="27e56-118">**Временная ошибка возникает во время команда SQL-запроса**: hello команду следует повторить не сразу.</span><span class="sxs-lookup"><span data-stu-id="27e56-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="27e56-119">Вместо этого после задержки, hello должен быть заново установить соединение.</span><span class="sxs-lookup"><span data-stu-id="27e56-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="27e56-120">Затем можно повторить команду hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="27e56-121">Повтор логики для временных ошибок</span><span class="sxs-lookup"><span data-stu-id="27e56-121">Retry logic for transient errors</span></span>
<span data-ttu-id="27e56-122">Клиентские программы, в которых иногда происходят временные ошибки, являются более надежными, если используют логику повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="27e56-123">Когда программа взаимодействует с базой данных SQL Azure через по промежуточного слоя сторонних производителей, запрос с поставщиком hello ли hello по промежуточного слоя содержит логику повторных попыток для временных ошибок.</span><span class="sxs-lookup"><span data-stu-id="27e56-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="27e56-124">Принципы повторных попыток</span><span class="sxs-lookup"><span data-stu-id="27e56-124">Principles for retry</span></span>
* <span data-ttu-id="27e56-125">Следует повторить tooopen попытки подключения, если ошибка hello является временным.</span><span class="sxs-lookup"><span data-stu-id="27e56-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="27e56-126">Выполнение инструкции SQL SELECT, которая закончилась временным сбоем, не нужно повторять непосредственно.</span><span class="sxs-lookup"><span data-stu-id="27e56-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="27e56-127">Вместо этого установить новое подключение, а затем повторите hello SELECT.</span><span class="sxs-lookup"><span data-stu-id="27e56-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="27e56-128">При неудачном завершении инструкции SQL UPDATE с временной ошибкой перед hello повторная попытка обновления следует установить новое подключение.</span><span class="sxs-lookup"><span data-stu-id="27e56-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="27e56-129">Логика повторных попыток Hello необходимо убедиться, что hello всей базы данных транзакция завершена или что hello всей транзакции выполняется откат.</span><span class="sxs-lookup"><span data-stu-id="27e56-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="27e56-130">Другие соображения по поводу повторных попыток</span><span class="sxs-lookup"><span data-stu-id="27e56-130">Other considerations for retry</span></span>
* <span data-ttu-id="27e56-131">Пакетном, запускается автоматически после окончания рабочего дня и которого будет выполнена до утра, можете toovery пациента с интервалам времени между его повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="27e56-132">Запрос программы должны учитывать возможность toogive человека тенденцию hello копии после слишком много времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="27e56-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="27e56-133">Однако решение hello должен отсутствовать tooretry каждые несколько секунд, так как эта политика может переполнить hello системы вместе с запросами.</span><span class="sxs-lookup"><span data-stu-id="27e56-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="27e56-134">Увеличение интервала между повторными попытками</span><span class="sxs-lookup"><span data-stu-id="27e56-134">Interval increase between retries</span></span>
<span data-ttu-id="27e56-135">Рекомендуется подождать 5 секунд, прежде чем выполнять первую повторную попытку.</span><span class="sxs-lookup"><span data-stu-id="27e56-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="27e56-136">Повторять после задержки, меньше 5 секунд может просто огромным hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="27e56-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="27e56-137">Для каждой последующей повторной попыткой hello задержки должен увеличиваться экспоненциально, копирование tooa максимальное 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="27e56-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="27e56-138">Обсуждение hello *интервала блокирования* для клиентов, использующих ADO.NET доступна в [SQL пулов соединений Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="27e56-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="27e56-139">Можно также tooset максимальное число попыток, прежде чем программа hello самостоятельно завершается.</span><span class="sxs-lookup"><span data-stu-id="27e56-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="27e56-140">Образцы кода с логикой повторных попыток</span><span class="sxs-lookup"><span data-stu-id="27e56-140">Code samples with retry logic</span></span>
<span data-ttu-id="27e56-141">В этой статье доступны образцы кода с логикой повторных попыток на разных языках программирования:</span><span class="sxs-lookup"><span data-stu-id="27e56-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="27e56-142">Библиотеки подключений для Базы данных SQL и SQL Server</span><span class="sxs-lookup"><span data-stu-id="27e56-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="27e56-143">Тестирование логики повторных попыток</span><span class="sxs-lookup"><span data-stu-id="27e56-143">Test your retry logic</span></span>
<span data-ttu-id="27e56-144">tootest логику повторов должен имитировать или приводят к ошибке, не могут быть исправлены, пока выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="27e56-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="27e56-145">Проверьте, отключения от сети hello</span><span class="sxs-lookup"><span data-stu-id="27e56-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="27e56-146">Можно проверить логику повторов можно toodisconnect клиентского компьютера из hello сети во время программы hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="27e56-147">будет возвращена ошибка Hello:</span><span class="sxs-lookup"><span data-stu-id="27e56-147">hello error will be:</span></span>

* <span data-ttu-id="27e56-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="27e56-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="27e56-149">Сообщение: "Данный узел неизвестен."</span><span class="sxs-lookup"><span data-stu-id="27e56-149">Message: "No such host is known"</span></span>

<span data-ttu-id="27e56-150">Как часть hello сначала повторной попытки, программы можно исправить ошибочное hello и повторить попытку tooconnect.</span><span class="sxs-lookup"><span data-stu-id="27e56-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="27e56-151">toomake этом практические отключении компьютера от сети hello перед запуском программы.</span><span class="sxs-lookup"><span data-stu-id="27e56-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="27e56-152">Затем программа распознает параметр время выполнения, который вызывает программу hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="27e56-153">Временно добавьте 11001 список tooits tooconsider ошибок в качестве временной.</span><span class="sxs-lookup"><span data-stu-id="27e56-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="27e56-154">Первый раз пытается подключиться как обычно.</span><span class="sxs-lookup"><span data-stu-id="27e56-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="27e56-155">После ошибки hello перехватывается, удалите 11001 из списка hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="27e56-156">Отображать сообщение о том, tooplug hello hello пользователя компьютера в сети hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="27e56-157">Дополнительно приостановку выполнения с помощью либо hello **Console.ReadLine** метода или диалоговое окно с помощью кнопки "ОК".</span><span class="sxs-lookup"><span data-stu-id="27e56-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="27e56-158">Hello нажатии клавиши ВВОД hello после hello компьютер подключен к сети hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="27e56-159">Повторите попытку tooconnect, ожидается успех.</span><span class="sxs-lookup"><span data-stu-id="27e56-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="27e56-160">Тестирование ошибочное hello баз данных по имени при подключении</span><span class="sxs-lookup"><span data-stu-id="27e56-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="27e56-161">Программу можно специально опечатка hello имя пользователя, прежде чем hello первая попытка соединения.</span><span class="sxs-lookup"><span data-stu-id="27e56-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="27e56-162">будет возвращена ошибка Hello:</span><span class="sxs-lookup"><span data-stu-id="27e56-162">hello error will be:</span></span>

* <span data-ttu-id="27e56-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="27e56-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="27e56-164">Сообщение: "Ошибка входа пользователя WRONG_MyUserName."</span><span class="sxs-lookup"><span data-stu-id="27e56-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="27e56-165">Как часть hello сначала повторной попытки, программы можно исправить ошибочное hello и повторить попытку tooconnect.</span><span class="sxs-lookup"><span data-stu-id="27e56-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="27e56-166">этом практические toomake, программа может распознать параметр время выполнения, который вызывает программу hello:</span><span class="sxs-lookup"><span data-stu-id="27e56-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="27e56-167">Временно добавьте 18456 список tooits tooconsider ошибок в качестве временной.</span><span class="sxs-lookup"><span data-stu-id="27e56-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="27e56-168">Специально добавьте имя пользователя toohello «WRONG_».</span><span class="sxs-lookup"><span data-stu-id="27e56-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="27e56-169">После ошибки hello перехватывается, удалите 18456 из списка hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="27e56-170">Удалите «WRONG_» из имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="27e56-171">Повторите попытку tooconnect, ожидается успех.</span><span class="sxs-lookup"><span data-stu-id="27e56-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="27e56-172">Параметры .NET SqlConnection для повторной попытки подключения</span><span class="sxs-lookup"><span data-stu-id="27e56-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="27e56-173">Если клиентская программа подключается tootooAzure базы данных SQL с помощью класса .NET Framework hello **System.Data.SqlClient.SqlConnection**, следует использовать .NET 4.6.1 или более поздней версии (или .NET Core), можно использовать его компонент повторных попыток подключения.</span><span class="sxs-lookup"><span data-stu-id="27e56-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="27e56-174">Информация о функции hello [здесь](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="27e56-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="27e56-175">При построении hello [строка подключения](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) для вашей **SqlConnection** объекта должен координировать hello значений между hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="27e56-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="27e56-176">ConnectRetryCount — &nbsp;&nbsp;*количество повторных попыток (значение по умолчанию — 1; диапазон — от 0 до 255).*</span><span class="sxs-lookup"><span data-stu-id="27e56-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="27e56-177">ConnectRetryInterval — &nbsp;&nbsp;*интервал между повторными попытками (значение по умолчанию — 1 секунда; диапазон — от 1 до 60).*</span><span class="sxs-lookup"><span data-stu-id="27e56-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="27e56-178">Connection Timeout — &nbsp;&nbsp;*время ожидания подключения (значение по умолчанию — 15 секунд; диапазон — от 0 до 2147483647).*</span><span class="sxs-lookup"><span data-stu-id="27e56-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="27e56-179">В частности выбранных значений необходимо внести следующие true равенства hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="27e56-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="27e56-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="27e56-181">Например, если hello count = 3 и интервала = 10 секунд, время ожидания составляет только 29 секунд не довольно придаст системы hello достаточное время для его третьей и последней попытки подключаться: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="27e56-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="27e56-182">Подключения и команды</span><span class="sxs-lookup"><span data-stu-id="27e56-182">Connection versus command</span></span>
<span data-ttu-id="27e56-183">Hello **ConnectRetryCount** и **ConnectRetryInterval** параметры позволяют вашей **SqlConnection** hello объекта повторить операцию подключения без о том, или беспокоить вашей программу, например возвращение управления программы tooyour.</span><span class="sxs-lookup"><span data-stu-id="27e56-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="27e56-184">повторные попытки Hello может произойти в следующих ситуациях hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="27e56-185">при вызове метода mySqlConnection.Open;</span><span class="sxs-lookup"><span data-stu-id="27e56-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="27e56-186">при вызове метода mySqlConnection.Execute.</span><span class="sxs-lookup"><span data-stu-id="27e56-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="27e56-187">Есть один важный нюанс.</span><span class="sxs-lookup"><span data-stu-id="27e56-187">There is a subtlety.</span></span> <span data-ttu-id="27e56-188">Если возникает временная ошибка во время вашей *запроса* в ходе выполнения вашей **SqlConnection** объекта не hello повторить операцию подключения, и она определенно не повторить запрос.</span><span class="sxs-lookup"><span data-stu-id="27e56-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="27e56-189">Тем не менее **SqlConnection** очень быстро проверок hello подключения перед отправкой запроса на выполнение.</span><span class="sxs-lookup"><span data-stu-id="27e56-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="27e56-190">Если Быстрая проверка hello обнаруживает проблемы с подключением **SqlConnection** попыток hello операцию подключения.</span><span class="sxs-lookup"><span data-stu-id="27e56-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="27e56-191">После успешного "Повторить" hello, то запрос отправляется для выполнения.</span><span class="sxs-lookup"><span data-stu-id="27e56-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="27e56-192">Нужно ли сочетать ConnectRetryCount с логикой повторных попыток в приложении?</span><span class="sxs-lookup"><span data-stu-id="27e56-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="27e56-193">Предположим, что в вашем приложении реализована надежная настраиваемая логика повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="27e56-194">Она может повторить hello 4 раза в операции соединения.</span><span class="sxs-lookup"><span data-stu-id="27e56-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="27e56-195">При добавлении **ConnectRetryInterval** и **ConnectRetryCount** = 3 строки подключения tooyour, увеличит too4 число повторных попыток hello * 3 = 12 повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="27e56-196">Вряд ли вам действительно нужно такое количество повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="27e56-197">TooAzure подключения базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="27e56-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="27e56-198">Подключение: строка подключения</span><span class="sxs-lookup"><span data-stu-id="27e56-198">Connection: Connection string</span></span>
<span data-ttu-id="27e56-199">Строка подключения Hello, необходимые для подключения tooAzure базы данных SQL несколько отличается от строку hello соединения tooMicrosoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27e56-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="27e56-200">Вы можете скопировать hello строку подключения для базы данных из hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="27e56-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="27e56-201">Подключение: IP-адрес</span><span class="sxs-lookup"><span data-stu-id="27e56-201">Connection: IP address</span></span>
<span data-ttu-id="27e56-202">Необходимо настроить hello базы данных SQL server tooaccept соединение с IP-адреса hello hello компьютера, на котором размещается клиентская программа.</span><span class="sxs-lookup"><span data-stu-id="27e56-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="27e56-203">Это делается путем изменения параметров брандмауэра hello через hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="27e56-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="27e56-204">Если вы забыли tooconfigure hello IP-адрес, программа завершится с удобно сообщение hello необходимых IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="27e56-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="27e56-205">Подробнее: [Настройка правила брандмауэра уровня сервера базы данных SQL Azure с помощью портала Azure](sql-database-configure-firewall-settings.md).</span><span class="sxs-lookup"><span data-stu-id="27e56-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="27e56-206">Подключение: порты</span><span class="sxs-lookup"><span data-stu-id="27e56-206">Connection: Ports</span></span>
<span data-ttu-id="27e56-207">Обычно требуется только tooensure, что порт 1433 открыт для исходящей связи, на компьютере hello, на котором размещается клиентская программа.</span><span class="sxs-lookup"><span data-stu-id="27e56-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="27e56-208">Например при размещении клиентскую программу на компьютер с Windows hello брандмауэра Windows на узле hello позволяет tooopen порт 1433:</span><span class="sxs-lookup"><span data-stu-id="27e56-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="27e56-209">Откройте панель управления hello</span><span class="sxs-lookup"><span data-stu-id="27e56-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="27e56-210">&gt; "Все элементы панели управления".</span><span class="sxs-lookup"><span data-stu-id="27e56-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="27e56-211">&gt; "Брандмауэр Windows".</span><span class="sxs-lookup"><span data-stu-id="27e56-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="27e56-212">&gt; "Дополнительные параметры".</span><span class="sxs-lookup"><span data-stu-id="27e56-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="27e56-213">&gt; "Правила для исходящего трафика".</span><span class="sxs-lookup"><span data-stu-id="27e56-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="27e56-214">&gt; "Действия".</span><span class="sxs-lookup"><span data-stu-id="27e56-214">&gt; Actions</span></span>
7. <span data-ttu-id="27e56-215">&gt; "Создать правило".</span><span class="sxs-lookup"><span data-stu-id="27e56-215">&gt; New Rule</span></span>

<span data-ttu-id="27e56-216">Если клиентская программа установлена на виртуальной машине Azure, см. статью</span><span class="sxs-lookup"><span data-stu-id="27e56-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="27e56-217">[Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="27e56-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="27e56-218">Основные сведения о конфигурации портов и IP-адресов собраны в статье [Настройка брандмауэра базы данных SQL Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="27e56-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="27e56-219">Подключение: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="27e56-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="27e56-220">Если программа использует классы ADO.NET как **System.Data.SqlClient.SqlConnection** tooAzure tooconnect базы данных SQL, мы рекомендуем использовать .NET Framework версии 4.6.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="27e56-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="27e56-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="27e56-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="27e56-222">Для базы данных SQL Azure имеется повышения надежности при открытии соединения с помощью hello **SqlConnection.Open** метод.</span><span class="sxs-lookup"><span data-stu-id="27e56-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="27e56-223">Hello **откройте** метод теперь включает лучшие механизмов повтора усилий в ошибках tootransient ответа, для некоторых ошибок в течение периода ожидания соединения hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="27e56-224">Поддерживает работу с пулами подключений.</span><span class="sxs-lookup"><span data-stu-id="27e56-224">Supports connection pooling.</span></span> <span data-ttu-id="27e56-225">Сюда входит проверка эффективный hello соединения объекта, он предоставляет программа работает.</span><span class="sxs-lookup"><span data-stu-id="27e56-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="27e56-226">При использовании объект соединения в пуле соединений, мы рекомендуем, программа временно закрыть соединение hello, при использовании в не сразу.</span><span class="sxs-lookup"><span data-stu-id="27e56-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="27e56-227">Повторное открытие соединения не является ресурсоемким является способом hello, создав новое подключение.</span><span class="sxs-lookup"><span data-stu-id="27e56-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="27e56-228">Если вы используете ADO.NET 4.0 или более ранней версии, рекомендуется обновить toohello последнюю ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="27e56-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="27e56-229">С ноября 2015 года доступна [версия ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="27e56-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="27e56-230">Диагностика</span><span class="sxs-lookup"><span data-stu-id="27e56-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="27e56-231">Диагностика: проверяет, могут ли служебные программы подключаться</span><span class="sxs-lookup"><span data-stu-id="27e56-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="27e56-232">Если программа произошел сбой tooconnect tooAzure базы данных SQL, диагностики уже tooconnect tootry с помощью служебной программы.</span><span class="sxs-lookup"><span data-stu-id="27e56-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="27e56-233">В идеале программа hello могут подключаться с помощью hello же библиотеке, используемого программой.</span><span class="sxs-lookup"><span data-stu-id="27e56-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="27e56-234">На компьютерах под управлением Windows можно использовать следующие служебные программы:</span><span class="sxs-lookup"><span data-stu-id="27e56-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="27e56-235">SQL Server Management Studio (ssms.exe). Подключается с помощью ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="27e56-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="27e56-236">sqlcmd.exe. Подключается с помощью [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="27e56-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="27e56-237">После подключения проверьте, работает ли короткий SQL-запрос SELECT.</span><span class="sxs-lookup"><span data-stu-id="27e56-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="27e56-238">Диагностика: Проверьте Привет открыть порты</span><span class="sxs-lookup"><span data-stu-id="27e56-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="27e56-239">Предположим, что существует подозрение, что попытки подключения завершаются неудачей из-за проблем с tooport.</span><span class="sxs-lookup"><span data-stu-id="27e56-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="27e56-240">На компьютере можно запускать программы, которая сообщает о конфигурации порта hello.</span><span class="sxs-lookup"><span data-stu-id="27e56-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="27e56-241">На Linux hello можно попробовать следующие программы:</span><span class="sxs-lookup"><span data-stu-id="27e56-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="27e56-242">(Изменить значение toobe hello пример IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="27e56-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="27e56-243">В Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) программа может оказаться полезной.</span><span class="sxs-lookup"><span data-stu-id="27e56-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="27e56-244">Ниже приведен пример выполнения, к которым запросы hello ситуации порта на сервере базы данных SQL Azure и которого была запущена на переносном компьютере.</span><span class="sxs-lookup"><span data-stu-id="27e56-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="27e56-245">Диагностика: внесение ошибок в журнал</span><span class="sxs-lookup"><span data-stu-id="27e56-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="27e56-246">Эпизодические неисправности иногда лучше всего диагностировать, выявляя общий шаблон за несколько дней или недель подряд.</span><span class="sxs-lookup"><span data-stu-id="27e56-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="27e56-247">Клиент может помочь в диагностике. Для этого ему следует вносить в журнал все ошибки, с которыми он сталкивается.</span><span class="sxs-lookup"><span data-stu-id="27e56-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="27e56-248">Может быть записи журнала могут toocorrelate hello с ошибочные данные самого внутреннего журналы базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="27e56-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="27e56-249">Enterprise Library 6 (EntLib60) предлагает tooassist .NET управляемые классы с ведением журнала.</span><span class="sxs-lookup"><span data-stu-id="27e56-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="27e56-250">5 — как легко как неполадкой отключение журнала: с помощью hello функциональный блок ведения журнала</span><span class="sxs-lookup"><span data-stu-id="27e56-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="27e56-251">Диагностика: проверка системных журналов на наличие ошибок</span><span class="sxs-lookup"><span data-stu-id="27e56-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="27e56-252">Ниже приведены некоторые Transact-SQL-инструкции SELECT, которые запрашивают в журналах сведения об ошибках и прочую информацию.</span><span class="sxs-lookup"><span data-stu-id="27e56-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="27e56-253">Запрос у журнала</span><span class="sxs-lookup"><span data-stu-id="27e56-253">Query of log</span></span> | <span data-ttu-id="27e56-254">Описание</span><span class="sxs-lookup"><span data-stu-id="27e56-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="27e56-255">Hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) представление предоставляет сведения об отдельных событиях, включая некоторые, которая может вызвать временных ошибок или сбоев подключения к.</span><span class="sxs-lookup"><span data-stu-id="27e56-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="27e56-256">В идеальном случае вы можете соотнести hello **start_time** или **end_time** значения со сведениями о при клиентской программе возникших проблем.</span><span class="sxs-lookup"><span data-stu-id="27e56-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="27e56-257">**Совет:** необходимо подключить toohello **master** базы данных toorun это.</span><span class="sxs-lookup"><span data-stu-id="27e56-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="27e56-258">Hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) , то есть объединенное число типов событий, для дополнительной диагностики.</span><span class="sxs-lookup"><span data-stu-id="27e56-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="27e56-259">**Совет:** необходимо подключить toohello **master** базы данных toorun это.</span><span class="sxs-lookup"><span data-stu-id="27e56-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="27e56-260">Диагностика: Поиск событий проблемы в журнале базы данных SQL hello</span><span class="sxs-lookup"><span data-stu-id="27e56-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="27e56-261">Можно выполнить поиск записей о событиях проблемы в журнале hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="27e56-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="27e56-262">Повторите hello, следующем за инструкцией Transact-SQL SELECT в hello **master** базы данных:</span><span class="sxs-lookup"><span data-stu-id="27e56-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="27e56-263">Несколько возвращенных строк из sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="27e56-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="27e56-264">Ниже показано, как может выглядеть возвращенная строка.</span><span class="sxs-lookup"><span data-stu-id="27e56-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="27e56-265">значения null Hello показано часто не имеют значение null, в других строках.</span><span class="sxs-lookup"><span data-stu-id="27e56-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="27e56-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="27e56-266">Enterprise Library 6</span></span>
<span data-ttu-id="27e56-267">Enterprise Library 6 (EntLib60) — это платформа классов .NET, поможет реализовать надежную клиентов облачных служб, он hello службы базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="27e56-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="27e56-268">Можно найти в котором EntLib60 может помочь, посетив первой области выделенной tooeach разделы:</span><span class="sxs-lookup"><span data-stu-id="27e56-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="27e56-269">Enterprise Library 6. Апрель, 2013 г.</span><span class="sxs-lookup"><span data-stu-id="27e56-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="27e56-270">Одна из областей, в которой может помочь EntLib60, — логика повторных попыток для обработки временных ошибок.</span><span class="sxs-lookup"><span data-stu-id="27e56-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="27e56-271">4 - perseverance, секрет все Triumphs: с помощью hello временных Fault Handling Application Block</span><span class="sxs-lookup"><span data-stu-id="27e56-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="27e56-272">Hello EntLib60 исходный код доступен для роли public [загрузить](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="27e56-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="27e56-273">Корпорация Майкрософт предлагает дополнительные функции toomake нет планов обслуживания или обновления обновляет tooEntLib.</span><span class="sxs-lookup"><span data-stu-id="27e56-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="27e56-274">Классы EntLib60 для временных ошибок и повторов</span><span class="sxs-lookup"><span data-stu-id="27e56-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="27e56-275">следующие классы EntLib60 Hello особенно полезны для логики повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="27e56-276">Здравствуйте, все они находятся в или более, пространство имен **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="27e56-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="27e56-277">*В пространстве имен hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="27e56-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="27e56-278">**RetryPolicy** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="27e56-279">**ExecuteAction** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="27e56-280">**ExponentialBackoff** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="27e56-281">**SqlDatabaseTransientErrorDetectionStrategy** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="27e56-282">**ReliableSqlConnection** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="27e56-283">**ExecuteCommand** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="27e56-284">В пространстве имен hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="27e56-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="27e56-285">**AlwaysTransientErrorDetectionStrategy** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="27e56-286">**NeverTransientErrorDetectionStrategy** ;</span><span class="sxs-lookup"><span data-stu-id="27e56-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="27e56-287">Ниже приведены ссылки tooinformation о EntLib60.</span><span class="sxs-lookup"><span data-stu-id="27e56-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="27e56-288">Бесплатные [загрузки книги: tooMicrosoft руководство разработчика библиотеки Enterprise Library, второй выпуск](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="27e56-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="27e56-289">Рекомендации: в статье [Общие рекомендации по повторным попыткам](../best-practices-retry-general.md) содержится подробное обсуждение логики повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="27e56-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="27e56-290">Загрузка на сайте NuGet компонента [Enterprise Library 6.0: Transient Fault Handling application block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="27e56-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="27e56-291">EntLib60: ведение журнала блока hello</span><span class="sxs-lookup"><span data-stu-id="27e56-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="27e56-292">блок Hello ведения журнала — гибкими и можно настроить решение, которое позволяет:</span><span class="sxs-lookup"><span data-stu-id="27e56-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="27e56-293">создавать и хранить сообщения журнала в разных расположениях;</span><span class="sxs-lookup"><span data-stu-id="27e56-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="27e56-294">классифицировать и фильтровать сообщения;</span><span class="sxs-lookup"><span data-stu-id="27e56-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="27e56-295">собирать контекстную информацию, полезную для отладки, трассировки, аудита и выполнения общих требований к ведению журнала.</span><span class="sxs-lookup"><span data-stu-id="27e56-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="27e56-296">Hello ведения журнала блоков краткие описания hello ведения журнала функции hello место назначения журналов, чтобы код приложения hello согласована, независимо от расположения hello и ведения журнала хранилища hello целевого типа.</span><span class="sxs-lookup"><span data-stu-id="27e56-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="27e56-297">Дополнительные сведения см.: [5 — как легко как неполадкой отключение журнала: с помощью hello функциональный блок ведения журнала](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="27e56-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="27e56-298">Исходный код метода EntLib60 IsTransient</span><span class="sxs-lookup"><span data-stu-id="27e56-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="27e56-299">Далее из hello **SqlDatabaseTransientErrorDetectionStrategy** класса, является исходный код hello C# для hello **IsTransient** метод.</span><span class="sxs-lookup"><span data-stu-id="27e56-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="27e56-300">Hello исходного кода уточняет, какие ошибки рассматривались временной toobe и заслуживает повторных попыток, по состоянию на апрель 2013 г.</span><span class="sxs-lookup"><span data-stu-id="27e56-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="27e56-301">Многочисленные **//comment** строк были удалены из этой копии tooemphasize удобочитаемость.</span><span class="sxs-lookup"><span data-stu-id="27e56-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="27e56-302">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27e56-302">Next steps</span></span>
* <span data-ttu-id="27e56-303">Сведения об устранении неполадок других распространенных проблем с подключением базы данных SQL Azure, посетите [Устранение неполадок подключения выдает tooAzure базы данных SQL](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="27e56-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="27e56-304">Пул подключений SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="27e56-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="27e56-305">*Повторная попытка* — лицензии Apache 2.0 общего назначения, повторная попытка библиотеки, написанные на **Python**, toosimplify задачу hello добавления toojust поведение повторных попыток, о чем-либо.</span><span class="sxs-lookup"><span data-stu-id="27e56-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

