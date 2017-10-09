---
title: "Stream Analytics: смена учетных данных для источников входных данных и мест назначения выходных данных | Документация Майкрософт"
description: "Узнайте, как tooupdate hello учетные данные для Stream Analytics входов и выходов."
keywords: "учетные данные для входа в систему"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="2ed18-104">Смена учетных данных для входа в систему</span><span class="sxs-lookup"><span data-stu-id="2ed18-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="2ed18-105">Аннотация</span><span class="sxs-lookup"><span data-stu-id="2ed18-105">Abstract</span></span>
<span data-ttu-id="2ed18-106">Azure Stream Analytics сегодня не допускает замены hello учетные данные при вводе выводе во время выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="2ed18-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="2ed18-107">Хотя Azure Stream Analytics поддерживает возобновление задания из последнего вывода, нам необходимо было tooshare hello весь процесс минимизации hello промежуток между hello остановка и запуск задания hello и поворот hello учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="2ed18-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="2ed18-108">Часть 1 — Подготовка hello новый набор учетных данных:</span><span class="sxs-lookup"><span data-stu-id="2ed18-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="2ed18-109">Эта часть — применимо toohello после ввода вывода:</span><span class="sxs-lookup"><span data-stu-id="2ed18-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="2ed18-110">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="2ed18-110">Blob Storage</span></span>
* <span data-ttu-id="2ed18-111">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="2ed18-111">Event Hubs</span></span>
* <span data-ttu-id="2ed18-112">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="2ed18-112">SQL Database</span></span>
* <span data-ttu-id="2ed18-113">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="2ed18-113">Table Storage</span></span>

<span data-ttu-id="2ed18-114">Сведения, касающиеся других источников входных данных и мест назначения выходных данных см. в части 2.</span><span class="sxs-lookup"><span data-stu-id="2ed18-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="2ed18-115">Хранилище больших двоичных объектов и табличное хранилище</span><span class="sxs-lookup"><span data-stu-id="2ed18-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="2ed18-116">Расширения хранилища toohello перейдите на портал управления Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![рисунок1][graphic1]
2. <span data-ttu-id="2ed18-118">Найдите hello хранилища, используемого в задание, а в его:</span><span class="sxs-lookup"><span data-stu-id="2ed18-118">Locate hello storage used by your job and go into it:</span></span>  
   ![рисунок2][graphic2]
3. <span data-ttu-id="2ed18-120">Выберите команду hello управление ключами доступа:</span><span class="sxs-lookup"><span data-stu-id="2ed18-120">Click hello Manage Access Keys command:</span></span>  
   ![рисунок3][graphic3]
4. <span data-ttu-id="2ed18-122">Между hello первичный ключ доступа и вторичный ключ доступа, hello **выбрать hello не используется в вашей работы**.</span><span class="sxs-lookup"><span data-stu-id="2ed18-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="2ed18-123">Нажмите кнопку повторного создания: </span><span class="sxs-lookup"><span data-stu-id="2ed18-123">Hit regenerate:</span></span>  
   ![рисунок4][graphic4]
6. <span data-ttu-id="2ed18-125">Скопируйте hello вновь созданный ключ:</span><span class="sxs-lookup"><span data-stu-id="2ed18-125">Copy hello newly generated key:</span></span>  
   ![рисунок5][graphic5]
7. <span data-ttu-id="2ed18-127">По-прежнему tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="2ed18-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="2ed18-128">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="2ed18-128">Event hubs</span></span>
1. <span data-ttu-id="2ed18-129">Расширения Service Bus toohello перейдите на портал управления Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![рисунок6][graphic6]
2. <span data-ttu-id="2ed18-131">Найдите hello пространство имен служебной шины, используемые вашей работы и перейдите в него:</span><span class="sxs-lookup"><span data-stu-id="2ed18-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![рисунок7][graphic7]
3. <span data-ttu-id="2ed18-133">Если задание на hello пространства имен шины обслуживания использует политику общего доступа, перейдите к toostep 6</span><span class="sxs-lookup"><span data-stu-id="2ed18-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="2ed18-134">Перейдите вкладку toohello концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="2ed18-134">Go toohello Event Hubs tab:</span></span>  
   ![рисунок8][graphic8]
5. <span data-ttu-id="2ed18-136">Найдите hello концентратора событий, используемых вашей работы и перейдите в него:</span><span class="sxs-lookup"><span data-stu-id="2ed18-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![рисунок9][graphic9]
6. <span data-ttu-id="2ed18-138">Воспользуйтесь toohello вкладке "Настройка".</span><span class="sxs-lookup"><span data-stu-id="2ed18-138">Go toohello Configure Tab:</span></span>  
   ![рисунок10][graphic10]
7. <span data-ttu-id="2ed18-140">На hello раскрывающегося списка имя политики найдите hello общего доступа от политики задания:</span><span class="sxs-lookup"><span data-stu-id="2ed18-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![рисунок11][graphic11]
8. <span data-ttu-id="2ed18-142">Между hello первичный ключ и вторичный ключ hello **выбрать hello не используется в вашей работы**.</span><span class="sxs-lookup"><span data-stu-id="2ed18-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="2ed18-143">Нажмите кнопку повторного создания: </span><span class="sxs-lookup"><span data-stu-id="2ed18-143">Hit regenerate:</span></span>  
   ![рисунок12][graphic12]
10. <span data-ttu-id="2ed18-145">Скопируйте hello вновь созданный ключ:</span><span class="sxs-lookup"><span data-stu-id="2ed18-145">Copy hello newly generated key:</span></span>  
   ![рисунок13][graphic13]
11. <span data-ttu-id="2ed18-147">По-прежнему tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="2ed18-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="2ed18-148">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="2ed18-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="2ed18-149">Примечание: необходимо будет tooconnect toohello службы базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="2ed18-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="2ed18-150">Мы будем tooshow toodo это с помощью hello возможности управления на hello портала управления Azure, но вы можете toouse некоторые клиентские средства, как SQL Server Management Studio также.</span><span class="sxs-lookup"><span data-stu-id="2ed18-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="2ed18-151">Расширение базы данных SQL toohello перейдите на портале управления Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![рисунок14][graphic14]
2. <span data-ttu-id="2ed18-153">Найдите hello базы данных SQL, используемой вашей работы и **щелкните на сервере hello** ссылку hello же строки:</span><span class="sxs-lookup"><span data-stu-id="2ed18-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="2ed18-154">![рисунок15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="2ed18-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="2ed18-155">Выберите команду Управление hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-155">Click hello Manage command:</span></span>  
   ![рисунок16][graphic16]
4. <span data-ttu-id="2ed18-157">Введите главный ключ базы данных: </span><span class="sxs-lookup"><span data-stu-id="2ed18-157">Type Database Master:</span></span>  
   ![рисунок17][graphic17]
5. <span data-ttu-id="2ed18-159">Введите свои имя пользователя и пароль и нажмите кнопку "Вход": </span><span class="sxs-lookup"><span data-stu-id="2ed18-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![рисунок18][graphic18]
6. <span data-ttu-id="2ed18-161">Щелкните "Создать запрос": </span><span class="sxs-lookup"><span data-stu-id="2ed18-161">Click New Query:</span></span>  
   ![рисунок19][graphic19]
7. <span data-ttu-id="2ed18-163">Тип в hello следующий запрос, заменив < login_name > — именем пользователя и замена <enterStrongPasswordHere> с новым паролем:</span><span class="sxs-lookup"><span data-stu-id="2ed18-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="2ed18-164">Щелкните "Выполнить": </span><span class="sxs-lookup"><span data-stu-id="2ed18-164">Click Run:</span></span>  
   ![рисунок20][graphic20]
9. <span data-ttu-id="2ed18-166">Вернитесь обратно toostep 2, и это время щелкните hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="2ed18-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![рисунок21][graphic21]
10. <span data-ttu-id="2ed18-168">Выберите команду Управление hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-168">Click hello Manage command:</span></span>  
   ![рисунок22][graphic22]
11. <span data-ttu-id="2ed18-170">Введите свои имя пользователя и пароль и нажмите кнопку "Вход": </span><span class="sxs-lookup"><span data-stu-id="2ed18-170">type in your User Name, Password, and click Logon:</span></span>  
   ![рисунок23][graphic23]
12. <span data-ttu-id="2ed18-172">Щелкните "Создать запрос": </span><span class="sxs-lookup"><span data-stu-id="2ed18-172">Click New Query:</span></span>  
   ![рисунок24][graphic24]
13. <span data-ttu-id="2ed18-174">Введите следующий запрос, заменив < имя_пользователя > с именем, по которому требуется tooidentify hello это имя входа в контексте hello этой базы данных (вы можете предоставить hello одинаковое значение, заданное для < login_name >, например) и замены < login_name > новое имя пользователя:</span><span class="sxs-lookup"><span data-stu-id="2ed18-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="2ed18-175">Щелкните "Выполнить": </span><span class="sxs-lookup"><span data-stu-id="2ed18-175">Click Run:</span></span>  
   ![рисунок25][graphic25]
15. <span data-ttu-id="2ed18-177">Теперь необходимо предоставить нового пользователя с hello же роли и имели пользовательскими правами.</span><span class="sxs-lookup"><span data-stu-id="2ed18-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="2ed18-178">По-прежнему tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="2ed18-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="2ed18-179">Часть 2: Привет остановка задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ed18-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="2ed18-180">Расширение Stream Analytics toohello перейдите на портал управления Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![рисунок26][graphic26]
2. <span data-ttu-id="2ed18-182">Найдите задание и перейдите к нему: </span><span class="sxs-lookup"><span data-stu-id="2ed18-182">Locate your job and go into it:</span></span>  
   ![рисунок27][graphic27]
3. <span data-ttu-id="2ed18-184">Go toohello входов вкладку или hello выходы зависимости от того, который требуется сменить hello учетные данные на вход или выход.</span><span class="sxs-lookup"><span data-stu-id="2ed18-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![рисунок28][graphic28]
4. <span data-ttu-id="2ed18-186">Выберите команду Stop hello и убедитесь, что задание hello остановлена:</span><span class="sxs-lookup"><span data-stu-id="2ed18-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="2ed18-187">![graphic29][graphic29] ожидания toostop задания hello.</span><span class="sxs-lookup"><span data-stu-id="2ed18-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="2ed18-188">Найдите hello ввода вывода требуется toorotate учетные данные на и вернитесь в него:</span><span class="sxs-lookup"><span data-stu-id="2ed18-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![рисунок30][graphic30]
6. <span data-ttu-id="2ed18-190">Продолжайте tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="2ed18-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="2ed18-191">Часть 3: Изменение hello учетные данные в задание Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="2ed18-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="2ed18-192">Хранилище больших двоичных объектов и табличное хранилище</span><span class="sxs-lookup"><span data-stu-id="2ed18-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="2ed18-193">Найти поле ключа учетной записи хранения hello и вставьте в него к вновь созданному ключу:</span><span class="sxs-lookup"><span data-stu-id="2ed18-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![рисунок31][graphic31]
2. <span data-ttu-id="2ed18-195">Выберите команды "Сохранить" hello и подтвердить сохранение изменений:</span><span class="sxs-lookup"><span data-stu-id="2ed18-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![рисунок32][graphic32]
3. <span data-ttu-id="2ed18-197">При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="2ed18-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="2ed18-198">Продолжайте tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2ed18-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="2ed18-199">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="2ed18-199">Event hubs</span></span>
1. <span data-ttu-id="2ed18-200">Найти поле ключ политики концентратора событий hello и вставьте в него к вновь созданному ключу:</span><span class="sxs-lookup"><span data-stu-id="2ed18-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![рисунок33][graphic33]
2. <span data-ttu-id="2ed18-202">Выберите команды "Сохранить" hello и подтвердить сохранение изменений:</span><span class="sxs-lookup"><span data-stu-id="2ed18-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![рисунок34][graphic34]
3. <span data-ttu-id="2ed18-204">При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="2ed18-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="2ed18-205">Продолжайте tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2ed18-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="2ed18-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="2ed18-206">Power BI</span></span>
1. <span data-ttu-id="2ed18-207">Щелкните hello Renew авторизации:</span><span class="sxs-lookup"><span data-stu-id="2ed18-207">Click hello Renew authorization:</span></span>  

   ![рисунок35][graphic35]
2. <span data-ttu-id="2ed18-209">Вы получите hello, после подтверждения:</span><span class="sxs-lookup"><span data-stu-id="2ed18-209">You will get hello following confirmation:</span></span>  

   ![рисунок36][graphic36]
3. <span data-ttu-id="2ed18-211">Выберите команды "Сохранить" hello и подтвердить сохранение изменений:</span><span class="sxs-lookup"><span data-stu-id="2ed18-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![рисунок37][graphic37]
4. <span data-ttu-id="2ed18-213">При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="2ed18-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="2ed18-214">Продолжайте tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2ed18-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="2ed18-215">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="2ed18-215">SQL Database</span></span>
1. <span data-ttu-id="2ed18-216">Найти hello поля имя пользователя и пароль и вставляется в только что созданный набор учетных данных:</span><span class="sxs-lookup"><span data-stu-id="2ed18-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![рисунок38][graphic38]
2. <span data-ttu-id="2ed18-218">Выберите команды "Сохранить" hello и подтвердить сохранение изменений:</span><span class="sxs-lookup"><span data-stu-id="2ed18-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![рисунок39][graphic39]
3. <span data-ttu-id="2ed18-220">При сохранении изменений автоматически запускается проверка подключения. Убедитесь, что она прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="2ed18-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="2ed18-221">Продолжайте tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2ed18-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="2ed18-222">Часть 4. Запуск задания с момента последней остановки</span><span class="sxs-lookup"><span data-stu-id="2ed18-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="2ed18-223">Покинуть Здравствуй ввода-вывода:</span><span class="sxs-lookup"><span data-stu-id="2ed18-223">Navigate away from hello Input/Output:</span></span>  
   ![рисунок40][graphic40]
2. <span data-ttu-id="2ed18-225">Щелкните команду Start hello:</span><span class="sxs-lookup"><span data-stu-id="2ed18-225">Click hello Start command:</span></span>  
   ![рисунок41][graphic41]
3. <span data-ttu-id="2ed18-227">Выберите время последней остановки hello и нажмите кнопку ОК:</span><span class="sxs-lookup"><span data-stu-id="2ed18-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![рисунок42][graphic42]
4. <span data-ttu-id="2ed18-229">Продолжайте tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="2ed18-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="2ed18-230">Часть 5: Удаление hello старый набор учетных данных</span><span class="sxs-lookup"><span data-stu-id="2ed18-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="2ed18-231">Эта часть — применимо toohello после ввода вывода:</span><span class="sxs-lookup"><span data-stu-id="2ed18-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="2ed18-232">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="2ed18-232">Blob Storage</span></span>
* <span data-ttu-id="2ed18-233">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="2ed18-233">Event Hubs</span></span>
* <span data-ttu-id="2ed18-234">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="2ed18-234">SQL Database</span></span>
* <span data-ttu-id="2ed18-235">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="2ed18-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="2ed18-236">Хранилище больших двоичных объектов и табличное хранилище</span><span class="sxs-lookup"><span data-stu-id="2ed18-236">Blob storage/Table storage</span></span>
<span data-ttu-id="2ed18-237">Повторите часть 1 для hello ключ доступа, который ранее использовался путем задания toorenew hello теперь неиспользуемый ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="2ed18-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="2ed18-238">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="2ed18-238">Event hubs</span></span>
<span data-ttu-id="2ed18-239">Повторите часть 1 для hello ключ, который ранее использовался путем задания toorenew hello теперь неиспользуемый ключ.</span><span class="sxs-lookup"><span data-stu-id="2ed18-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="2ed18-240">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="2ed18-240">SQL Database</span></span>
1. <span data-ttu-id="2ed18-241">Вернитесь к предыдущему окну toohello окна запроса из части 1 шаг 7 и введите hello в следующем запросе, заменив < previous_login_name > hello имя пользователя, который ранее использовался путем задания:</span><span class="sxs-lookup"><span data-stu-id="2ed18-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="2ed18-242">Щелкните "Выполнить": </span><span class="sxs-lookup"><span data-stu-id="2ed18-242">Click Run:</span></span>  
   ![рисунок43][graphic43]  

<span data-ttu-id="2ed18-244">Вы должны получить hello, после подтверждения:</span><span class="sxs-lookup"><span data-stu-id="2ed18-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="2ed18-245">Получение справки</span><span class="sxs-lookup"><span data-stu-id="2ed18-245">Get help</span></span>
<span data-ttu-id="2ed18-246">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="2ed18-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ed18-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ed18-247">Next steps</span></span>
* [<span data-ttu-id="2ed18-248">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ed18-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2ed18-249">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ed18-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2ed18-250">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ed18-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2ed18-251">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ed18-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2ed18-252">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2ed18-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

