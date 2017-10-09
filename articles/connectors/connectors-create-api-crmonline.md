---
title: "tooDynamics aaaConnect 365 (в сети) из приложения логики Azure | Документы Microsoft"
description: "Создание логики приложения рабочих процессов, управление сущностями (online) Dynamics 365 через API, предоставляемые соединителя hello Dynamics 365 hello"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="af464-103">Подключение tooDynamics 365 из рабочих процессов приложений логики</span><span class="sxs-lookup"><span data-stu-id="af464-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="af464-104">С приложениями логики можно подключиться tooDynamics 365 (в сети) и создайте потоки полезные бизнеса, создать записи, обновления элементов или вернуть список записей.</span><span class="sxs-lookup"><span data-stu-id="af464-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="af464-105">Соединитель Dynamics 365 hello вы можете:</span><span class="sxs-lookup"><span data-stu-id="af464-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="af464-106">Создать поток вашего бизнеса, на основе hello данных, получаемых из Dynamics 365 (в сети).</span><span class="sxs-lookup"><span data-stu-id="af464-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="af464-107">Используйте действия, которые получить ответ и внесите hello выходные данные для других действий.</span><span class="sxs-lookup"><span data-stu-id="af464-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="af464-108">Например, при обновлении элемента в Dynamics 365 (Интернет) можно отправлять сообщение электронной почты с помощью Office 365.</span><span class="sxs-lookup"><span data-stu-id="af464-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="af464-109">В этом разделе показано, как toocreate приложения логики, создает задачу в Dynamics 365 при создании нового интереса в Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="af464-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af464-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="af464-110">Prerequisites</span></span>
* <span data-ttu-id="af464-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="af464-111">An Azure account.</span></span>
* <span data-ttu-id="af464-112">Учетная запись Dynamics 365 (Интернет).</span><span class="sxs-lookup"><span data-stu-id="af464-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="af464-113">Создание задачи при создании интереса в Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="af464-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="af464-114">[Войдите в tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af464-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="af464-115">Введите в поле поиска Azure hello `Logic apps`, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="af464-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Поиск Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="af464-117">В разделе **Приложения логики** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="af464-117">Under **Logic apps**, click **Add**.</span></span>

      ![Добавление приложения логики](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="af464-119">приложения логики hello toocreate, полный hello **имя**, **подписки**, **группы ресурсов**, и **расположение** полей, а затем нажмите кнопку  **Создание**.</span><span class="sxs-lookup"><span data-stu-id="af464-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="af464-120">Выберите новое приложение логики hello.</span><span class="sxs-lookup"><span data-stu-id="af464-120">Select hello new logic app.</span></span> <span data-ttu-id="af464-121">При получении hello **успешное развертывание** уведомление, нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="af464-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="af464-122">В разделе **Средства разработки** щелкните **Конструктор приложений логики**.</span><span class="sxs-lookup"><span data-stu-id="af464-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="af464-123">Выберите из списка шаблон hello, **пустое приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="af464-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="af464-124">Введите в поле поиска hello `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="af464-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="af464-125">Запускает список с hello Dynamics 365, выберите **Dynamics 365 — при создании записи**.</span><span class="sxs-lookup"><span data-stu-id="af464-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="af464-126">Если запрос toosign в tooDynamics 365, сделайте это сейчас.</span><span class="sxs-lookup"><span data-stu-id="af464-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="af464-127">В сведениях о триггере hello введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="af464-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="af464-128">**Название организации**.</span><span class="sxs-lookup"><span data-stu-id="af464-128">**Organization Name**.</span></span> <span data-ttu-id="af464-129">Выберите экземпляр Dynamics 365 hello, требуется toolisten приложения hello логику для.</span><span class="sxs-lookup"><span data-stu-id="af464-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="af464-130">**Имя сущности**.</span><span class="sxs-lookup"><span data-stu-id="af464-130">**Entity Name**.</span></span> <span data-ttu-id="af464-131">Выберите сущность hello нужного toolisten для.</span><span class="sxs-lookup"><span data-stu-id="af464-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="af464-132">Это событие выступает в качестве триггера toostart hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="af464-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="af464-133">В этом пошаговом руководстве выберите **Интересы**.</span><span class="sxs-lookup"><span data-stu-id="af464-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="af464-134">**Как часто вы хотите toocheck элементов?**</span><span class="sxs-lookup"><span data-stu-id="af464-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="af464-135">Эти значения задают частоту проверяет приложение hello логику для обновления связанных toohello триггера.</span><span class="sxs-lookup"><span data-stu-id="af464-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="af464-136">по умолчанию Hello: toocheck наличие обновлений каждые три минуты.</span><span class="sxs-lookup"><span data-stu-id="af464-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="af464-137">**Частота**.</span><span class="sxs-lookup"><span data-stu-id="af464-137">**Frequency**.</span></span> <span data-ttu-id="af464-138">Выберите секунды, минуты, часы или дни.</span><span class="sxs-lookup"><span data-stu-id="af464-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="af464-139">**Интервал**.</span><span class="sxs-lookup"><span data-stu-id="af464-139">**Interval**.</span></span> <span data-ttu-id="af464-140">Введите число hello секунды, минуты, часы или дни, которые должны toopass перед hello следующей проверки.</span><span class="sxs-lookup"><span data-stu-id="af464-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Сведения о триггере приложения логики](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="af464-142">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="af464-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="af464-143">Введите в поле поиска hello `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="af464-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="af464-144">Выберите из списка действий hello **Dynamics 365 — создать новую запись**.</span><span class="sxs-lookup"><span data-stu-id="af464-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="af464-145">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="af464-145">Enter hello following information:</span></span>

    * <span data-ttu-id="af464-146">**Название организации**.</span><span class="sxs-lookup"><span data-stu-id="af464-146">**Organization Name**.</span></span> <span data-ttu-id="af464-147">Выберите экземпляр Dynamics 365 hello место toocreate hello hello потока записи.</span><span class="sxs-lookup"><span data-stu-id="af464-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="af464-148">Обратите внимание, что этот экземпляр не имеет toobe hello же где hello события из экземпляра.</span><span class="sxs-lookup"><span data-stu-id="af464-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="af464-149">**Имя сущности**.</span><span class="sxs-lookup"><span data-stu-id="af464-149">**Entity Name**.</span></span> <span data-ttu-id="af464-150">Выберите сущность hello требуется toocreate запись при событии hello.</span><span class="sxs-lookup"><span data-stu-id="af464-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="af464-151">В этом пошаговом руководстве выберите **Задачи**.</span><span class="sxs-lookup"><span data-stu-id="af464-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="af464-152">Нажмите кнопку в hello **субъекта** появившемся диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="af464-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="af464-153">Из hello динамического содержимого списка можно выбрать один из этих полей:</span><span class="sxs-lookup"><span data-stu-id="af464-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="af464-154">**Фамилия**.</span><span class="sxs-lookup"><span data-stu-id="af464-154">**Last Name**.</span></span> <span data-ttu-id="af464-155">Этот параметр вставляет hello Фамилия интереса hello в поле темы hello для задачи «hello» при создании записи задачи hello.</span><span class="sxs-lookup"><span data-stu-id="af464-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="af464-156">**Тема**.</span><span class="sxs-lookup"><span data-stu-id="af464-156">**Topic**.</span></span> <span data-ttu-id="af464-157">Установка этого флажка поле вставок hello раздела для hello интерес в поле темы hello для задачи «hello», когда hello задачи создается запись.</span><span class="sxs-lookup"><span data-stu-id="af464-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="af464-158">Нажмите кнопку **разделе** tooadd, toohello **субъекта** поле.</span><span class="sxs-lookup"><span data-stu-id="af464-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Сведения о создании новой записи приложения логики](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="af464-160">На панели инструментов конструктора логики приложения hello, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="af464-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Кнопка "Сохранить" на панели инструментов конструктора приложений логики](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="af464-162">hello toostart приложения логики, щелкните **запуска**.</span><span class="sxs-lookup"><span data-stu-id="af464-162">toostart hello Logic App, click **Run**.</span></span>

    ![Кнопка "Сохранить" на панели инструментов конструктора приложений логики](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="af464-164">Теперь создайте запись интереса в Dynamics 365 for Sales, чтобы увидеть поток в действии.</span><span class="sxs-lookup"><span data-stu-id="af464-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="af464-165">Настройка дополнительных параметров для шага приложения логики</span><span class="sxs-lookup"><span data-stu-id="af464-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="af464-166">как toofilter данных на этапе логики приложения, нажмите кнопку toospecify **Показывать дополнительные параметры** на этом шаге добавьте фильтра или порядка, запрос.</span><span class="sxs-lookup"><span data-stu-id="af464-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="af464-167">Например можно использовать фильтр запроса tooget только учетные записи active и упорядочить по имени учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="af464-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="af464-168">tooperform это задачи, введите запрос фильтра OData hello `statuscode eq 1`и выберите **имя учетной записи** из динамического содержимого списка hello.</span><span class="sxs-lookup"><span data-stu-id="af464-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="af464-169">См. дополнительные сведения о параметрах строки запроса [$filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) и [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="af464-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Расширенные параметры приложения логики](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="af464-171">Рекомендации по использованию расширенных параметров</span><span class="sxs-lookup"><span data-stu-id="af464-171">Best practices when using advanced options</span></span>

<span data-ttu-id="af464-172">При добавлении поля tooa значения, должен соответствовать типу поля hello, введите значение или выберите значение из динамического содержимого списка hello.</span><span class="sxs-lookup"><span data-stu-id="af464-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="af464-173">Тип поля</span><span class="sxs-lookup"><span data-stu-id="af464-173">Field type</span></span>  |<span data-ttu-id="af464-174">Как toouse</span><span class="sxs-lookup"><span data-stu-id="af464-174">How toouse</span></span>  |<span data-ttu-id="af464-175">Где toofind</span><span class="sxs-lookup"><span data-stu-id="af464-175">Where toofind</span></span>  |<span data-ttu-id="af464-176">Имя</span><span class="sxs-lookup"><span data-stu-id="af464-176">Name</span></span>  |<span data-ttu-id="af464-177">Тип данных</span><span class="sxs-lookup"><span data-stu-id="af464-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="af464-178">Текстовые поля</span><span class="sxs-lookup"><span data-stu-id="af464-178">Text fields</span></span>|<span data-ttu-id="af464-179">В текстовые поля необходимо вводить одну строку текста или динамическое содержимое, представляющее собой поле текстового типа.</span><span class="sxs-lookup"><span data-stu-id="af464-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="af464-180">Например, поля категорий и подкатегорий hello.</span><span class="sxs-lookup"><span data-stu-id="af464-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="af464-181">Параметры > настройки > Настройка hello системы > сущностей > задача > поля</span><span class="sxs-lookup"><span data-stu-id="af464-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="af464-182">category</span><span class="sxs-lookup"><span data-stu-id="af464-182">category</span></span> |<span data-ttu-id="af464-183">Одна строка текста</span><span class="sxs-lookup"><span data-stu-id="af464-183">Single Line of Text</span></span>        
<span data-ttu-id="af464-184">Целочисленные поля</span><span class="sxs-lookup"><span data-stu-id="af464-184">Integer fields</span></span> | <span data-ttu-id="af464-185">В некоторые поля необходимо ввести целое число или добавить динамическое содержимое, которое является полем целочисленного типа.</span><span class="sxs-lookup"><span data-stu-id="af464-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="af464-186">Например, поля "Процент выполнения" и "Длительность".</span><span class="sxs-lookup"><span data-stu-id="af464-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="af464-187">Параметры > настройки > Настройка hello системы > сущностей > задача > поля</span><span class="sxs-lookup"><span data-stu-id="af464-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="af464-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="af464-188">percentcomplete</span></span> |<span data-ttu-id="af464-189">Целое число</span><span class="sxs-lookup"><span data-stu-id="af464-189">Whole Number</span></span>         
<span data-ttu-id="af464-190">Поля даты</span><span class="sxs-lookup"><span data-stu-id="af464-190">Date fields</span></span> | <span data-ttu-id="af464-191">В некоторые поля необходимо ввести дату в формате "мм/дд/гггг" или добавить динамическое содержимое, которое является полем даты.</span><span class="sxs-lookup"><span data-stu-id="af464-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="af464-192">Например, такие поля, как "Дата создания", "Дата начала", "Фактическое начало", "Время последней приостановки", "Фактическое окончание" и "Дата выполнения".</span><span class="sxs-lookup"><span data-stu-id="af464-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="af464-193">Параметры > настройки > Настройка hello системы > сущностей > задача > поля</span><span class="sxs-lookup"><span data-stu-id="af464-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="af464-194">createdon</span><span class="sxs-lookup"><span data-stu-id="af464-194">createdon</span></span> |<span data-ttu-id="af464-195">Дата и время</span><span class="sxs-lookup"><span data-stu-id="af464-195">Date and Time</span></span>
<span data-ttu-id="af464-196">Поля, для которых требуется как идентификатор записи, так и тип поиска</span><span class="sxs-lookup"><span data-stu-id="af464-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="af464-197">Некоторые поля, которые ссылаются на другую запись сущности требуют записи с Идентификатором hello и тип поиска hello.</span><span class="sxs-lookup"><span data-stu-id="af464-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="af464-198">Параметры > настройки > Настройка hello системы > сущностей > учетной записи > поля</span><span class="sxs-lookup"><span data-stu-id="af464-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="af464-199">accountid</span><span class="sxs-lookup"><span data-stu-id="af464-199">accountid</span></span>  | <span data-ttu-id="af464-200">Первичный ключ</span><span class="sxs-lookup"><span data-stu-id="af464-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="af464-201">Другие примеры полей, для которых требуется как идентификатор записи, так и тип поиска</span><span class="sxs-lookup"><span data-stu-id="af464-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="af464-202">Расширив hello предыдущей таблице, ниже приведено несколько примеров полей, которые не работают с значения, выбранные из динамического содержимого списка hello.</span><span class="sxs-lookup"><span data-stu-id="af464-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="af464-203">Вместо этого эти поля требуются оба идентификатора и уточняющего запроса тип записи введенных в поля hello в PowerApps.</span><span class="sxs-lookup"><span data-stu-id="af464-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="af464-204">"Владелец" и "Тип владельца".</span><span class="sxs-lookup"><span data-stu-id="af464-204">Owner and Owner Type.</span></span> <span data-ttu-id="af464-205">поле владельца Hello должно быть допустимым идентификатором записи пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="af464-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="af464-206">Тип владельца Hello должен представлять собой **systemusers** или **команды**.</span><span class="sxs-lookup"><span data-stu-id="af464-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="af464-207">"Клиент" и "Тип клиента".</span><span class="sxs-lookup"><span data-stu-id="af464-207">Customer and Customer Type.</span></span> <span data-ttu-id="af464-208">поля Hello клиента должен быть допустимой учетной записи или записи идентификатора контактного лица.</span><span class="sxs-lookup"><span data-stu-id="af464-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="af464-209">Тип владельца Hello должен представлять собой **учетные записи** или **контактов**.</span><span class="sxs-lookup"><span data-stu-id="af464-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="af464-210">"В отношении" и поле типа "В отношении".</span><span class="sxs-lookup"><span data-stu-id="af464-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="af464-211">Hello относительно поля должен быть допустимой записи идентификатор, например учетной записи или записи идентификатора контактного лица.</span><span class="sxs-lookup"><span data-stu-id="af464-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="af464-212">Hello в отношении тип должен быть hello подстановки для записи hello, таких как **учетные записи** или **контактов**.</span><span class="sxs-lookup"><span data-stu-id="af464-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="af464-213">Hello следующий пример действие создания задача добавляет запись об организации, соответствующий идентификатор записи toohello, добавив его toohello относительно поля задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="af464-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![Идентификатор записи и тип учетной записи](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="af464-215">В этом примере также присваивает hello задач tooa конкретного пользователя на основе идентификатора пользователя hello записи.</span><span class="sxs-lookup"><span data-stu-id="af464-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![Идентификатор записи и тип учетной записи](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="af464-217">Идентификатор, toofind запись базы данных см. следующий раздел hello: *найти записи с Идентификатором hello*</span><span class="sxs-lookup"><span data-stu-id="af464-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="af464-218">Найти записи с Идентификатором hello</span><span class="sxs-lookup"><span data-stu-id="af464-218">Find hello record ID</span></span>

1. <span data-ttu-id="af464-219">Откройте запись, например для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="af464-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="af464-220">На панели инструментов действий hello, нажмите кнопку **во всплывающем** ![записи развертывания](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="af464-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="af464-221">Щелкните на панели инструментов действий hello, toocopy hello полный URL-адрес в программу электронной почты по умолчанию, **ССЫЛКУ по электронной ПОЧТЕ**.</span><span class="sxs-lookup"><span data-stu-id="af464-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="af464-222">Идентификатор записи Hello отображается между hello % 7b "и" %7 d кодирования символов hello URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="af464-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![Идентификатор записи и тип учетной записи](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="af464-224">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="af464-224">Troubleshooting</span></span>
<span data-ttu-id="af464-225">tootroubleshoot ошибка в шаге в приложении логики, просмотр сведений о состоянии hello hello события.</span><span class="sxs-lookup"><span data-stu-id="af464-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="af464-226">В разделе **Приложения логики** выберите свое приложение логики и щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="af464-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="af464-227">Hello области со сводкой отображается и предоставляет состояние выполнения hello для hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="af464-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Состояние выполнения приложения логики](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="af464-229">Дополнительные сведения о любой сбой запусков tooview нажмите кнопку hello сбой события.</span><span class="sxs-lookup"><span data-stu-id="af464-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="af464-230">tooexpand ошибка в шаге, щелкните этот шаг.</span><span class="sxs-lookup"><span data-stu-id="af464-230">tooexpand a failed step, click that step.</span></span>

   ![Развертывание шага с ошибкой](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="af464-232">сведения о шаге Hello отображаются и устранения hello причину сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="af464-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Сведения о шаге с ошибкой](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="af464-234">Дополнительные сведения об устранении неполадок в приложениях логики см. в статье [Диагностика сбоев приложений логики](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="af464-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="af464-235">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="af464-235">Connector-specific details</span></span>

<span data-ttu-id="af464-236">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="af464-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af464-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af464-237">Next steps</span></span>
<span data-ttu-id="af464-238">Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="af464-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
