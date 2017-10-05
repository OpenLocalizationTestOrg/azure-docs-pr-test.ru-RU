---
title: "Подключение к Dynamics 365 (Интернет) из Azure Logic Apps | Документация Майкрософт"
description: "Создайте рабочие процессы приложения логики, управляющие сущностями Dynamics 365 (Интернет) через API, предоставляемые соединителем Dynamics 365"
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
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="6d10f-103">Подключение к Dynamics 365 из рабочих процессов приложения логики</span><span class="sxs-lookup"><span data-stu-id="6d10f-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="6d10f-104">Благодаря приложениям логики можно подключаться к Dynamics 365 (Интернет) и создавать полезные бизнес-процессы для создания записей, обновления элементов или возвращения списка записей.</span><span class="sxs-lookup"><span data-stu-id="6d10f-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="6d10f-105">С помощью соединителя Dynamics 365 можно делать следующее:</span><span class="sxs-lookup"><span data-stu-id="6d10f-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="6d10f-106">формировать бизнес-процессы на основе данных, получаемых из Dynamics 365 (Интернет);</span><span class="sxs-lookup"><span data-stu-id="6d10f-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="6d10f-107">использовать действия, которые получают ответ и делают выходные данные доступными для использования другими действиями.</span><span class="sxs-lookup"><span data-stu-id="6d10f-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="6d10f-108">Например, при обновлении элемента в Dynamics 365 (Интернет) можно отправлять сообщение электронной почты с помощью Office 365.</span><span class="sxs-lookup"><span data-stu-id="6d10f-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="6d10f-109">В этой статье показано, как создать приложение логики, которое создаст задачу в Dynamics 365 после создания нового интереса (потенциального клиента).</span><span class="sxs-lookup"><span data-stu-id="6d10f-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d10f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6d10f-110">Prerequisites</span></span>
* <span data-ttu-id="6d10f-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6d10f-111">An Azure account.</span></span>
* <span data-ttu-id="6d10f-112">Учетная запись Dynamics 365 (Интернет).</span><span class="sxs-lookup"><span data-stu-id="6d10f-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="6d10f-113">Создание задачи при создании интереса в Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="6d10f-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="6d10f-114">[Войдите в Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d10f-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="6d10f-115">В поле поиска Azure введите `Logic apps` и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="6d10f-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Поиск Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="6d10f-117">В разделе **Приложения логики** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-117">Under **Logic apps**, click **Add**.</span></span>

      ![Добавление приложения логики](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="6d10f-119">Чтобы создать приложение логики, заполните поля **Имя**, **Подписка**, **Группа ресурсов** и **Расположение** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="6d10f-120">Выберите новое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="6d10f-120">Select the new logic app.</span></span> <span data-ttu-id="6d10f-121">После получения уведомления **Развертывание прошло успешно** щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="6d10f-122">В разделе **Средства разработки** щелкните **Конструктор приложений логики**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="6d10f-123">В списке шаблонов щелкните **Пустое приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="6d10f-124">В поле поиска введите `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="6d10f-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="6d10f-125">В списке триггеров Dynamics 365 выберите **365 Dynamics — при создании записи**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="6d10f-126">Если будет предложено войти в Dynamics 365, сделайте это.</span><span class="sxs-lookup"><span data-stu-id="6d10f-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="6d10f-127">В разделе описания триггера введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="6d10f-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="6d10f-128">**Название организации**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-128">**Organization Name**.</span></span> <span data-ttu-id="6d10f-129">Выберите экземпляр Dynamics 365 для прослушивания приложением логики.</span><span class="sxs-lookup"><span data-stu-id="6d10f-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="6d10f-130">**Имя сущности**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-130">**Entity Name**.</span></span> <span data-ttu-id="6d10f-131">Выберите сущность для ожидания передачи данных.</span><span class="sxs-lookup"><span data-stu-id="6d10f-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="6d10f-132">Это событие действует как триггер для запуска приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6d10f-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="6d10f-133">В этом пошаговом руководстве выберите **Интересы**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="6d10f-134">**Как часто вам нужно проверять наличие элементов?**</span><span class="sxs-lookup"><span data-stu-id="6d10f-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="6d10f-135">В этом разделе вы задаете, как часто приложение логики будет проверять на наличие обновлений, связанных с триггером.</span><span class="sxs-lookup"><span data-stu-id="6d10f-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="6d10f-136">Значение по умолчанию — проверять на наличие обновлений каждые три минуты.</span><span class="sxs-lookup"><span data-stu-id="6d10f-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="6d10f-137">**Частота**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-137">**Frequency**.</span></span> <span data-ttu-id="6d10f-138">Выберите секунды, минуты, часы или дни.</span><span class="sxs-lookup"><span data-stu-id="6d10f-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="6d10f-139">**Интервал**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-139">**Interval**.</span></span> <span data-ttu-id="6d10f-140">Введите значение секунд, минут, часов или дней, которые должны пройти до следующей проверки.</span><span class="sxs-lookup"><span data-stu-id="6d10f-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Сведения о триггере приложения логики](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="6d10f-142">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="6d10f-143">В поле поиска введите `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="6d10f-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="6d10f-144">В списке действий выберите **Dynamics 365 — создать новую запись**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="6d10f-145">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="6d10f-145">Enter the following information:</span></span>

    * <span data-ttu-id="6d10f-146">**Название организации**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-146">**Organization Name**.</span></span> <span data-ttu-id="6d10f-147">Выберите экземпляр Dynamics 365, в котором последовательность должна создать запись.</span><span class="sxs-lookup"><span data-stu-id="6d10f-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="6d10f-148">Обратите внимание, что это не должен быть экземпляр, который вызывает событие.</span><span class="sxs-lookup"><span data-stu-id="6d10f-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="6d10f-149">**Имя сущности**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-149">**Entity Name**.</span></span> <span data-ttu-id="6d10f-150">Выберите сущность, которая будет создавать запись во время возникновения события.</span><span class="sxs-lookup"><span data-stu-id="6d10f-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="6d10f-151">В этом пошаговом руководстве выберите **Задачи**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="6d10f-152">Щелкните в появившемся поле **Subject** (Субъект).</span><span class="sxs-lookup"><span data-stu-id="6d10f-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="6d10f-153">В появившемся списке динамического содержимого можно выбрать одно из этих полей:</span><span class="sxs-lookup"><span data-stu-id="6d10f-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="6d10f-154">**Фамилия**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-154">**Last Name**.</span></span> <span data-ttu-id="6d10f-155">Выберите это поле, чтобы при создании записи задачи вставить фамилию потенциального клиента в поле Subject (Субъект) задачи.</span><span class="sxs-lookup"><span data-stu-id="6d10f-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="6d10f-156">**Тема**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-156">**Topic**.</span></span> <span data-ttu-id="6d10f-157">Выберите это поле, чтобы при создании записи задачи вставить поле "Тема" для потенциального клиента в поле Subject (Субъект) задачи.</span><span class="sxs-lookup"><span data-stu-id="6d10f-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="6d10f-158">Щелкните поле **Тема**, чтобы добавить его в поле **Subject** (Субъект).</span><span class="sxs-lookup"><span data-stu-id="6d10f-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Сведения о создании новой записи приложения логики](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="6d10f-160">Нажмите кнопку **Сохранить** на панели инструментов конструктора приложений логики.</span><span class="sxs-lookup"><span data-stu-id="6d10f-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Кнопка "Сохранить" на панели инструментов конструктора приложений логики](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="6d10f-162">Чтобы запустить приложение логики, щелкните **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-162">To start the Logic App, click **Run**.</span></span>

    ![Кнопка "Сохранить" на панели инструментов конструктора приложений логики](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="6d10f-164">Теперь создайте запись интереса в Dynamics 365 for Sales, чтобы увидеть поток в действии.</span><span class="sxs-lookup"><span data-stu-id="6d10f-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="6d10f-165">Настройка дополнительных параметров для шага приложения логики</span><span class="sxs-lookup"><span data-stu-id="6d10f-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="6d10f-166">Чтобы указать способ фильтрации данных на шаге приложения логики, щелкните **Показать расширенные параметры** на этом шаге, а затем добавьте фильтр или упорядочивание по запросу.</span><span class="sxs-lookup"><span data-stu-id="6d10f-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="6d10f-167">Например, можно использовать запрос фильтра, чтобы получить только активные учетные записи в поименном порядке.</span><span class="sxs-lookup"><span data-stu-id="6d10f-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="6d10f-168">Чтобы выполнить эту задачу, введите запрос фильтра OData `statuscode eq 1` и в списке динамического содержимого выберите **Имя учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="6d10f-169">См. дополнительные сведения о параметрах строки запроса [$filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) и [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="6d10f-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Расширенные параметры приложения логики](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="6d10f-171">Рекомендации по использованию расширенных параметров</span><span class="sxs-lookup"><span data-stu-id="6d10f-171">Best practices when using advanced options</span></span>

<span data-ttu-id="6d10f-172">При добавлении значения необходимо учитывать тип поля независимо от того, вводите ли вы значение или выбираете из списка динамического содержимого.</span><span class="sxs-lookup"><span data-stu-id="6d10f-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="6d10f-173">Тип поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-173">Field type</span></span>  |<span data-ttu-id="6d10f-174">Использование</span><span class="sxs-lookup"><span data-stu-id="6d10f-174">How to use</span></span>  |<span data-ttu-id="6d10f-175">Место нахождения</span><span class="sxs-lookup"><span data-stu-id="6d10f-175">Where to find</span></span>  |<span data-ttu-id="6d10f-176">Имя</span><span class="sxs-lookup"><span data-stu-id="6d10f-176">Name</span></span>  |<span data-ttu-id="6d10f-177">Тип данных</span><span class="sxs-lookup"><span data-stu-id="6d10f-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="6d10f-178">Текстовые поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-178">Text fields</span></span>|<span data-ttu-id="6d10f-179">В текстовые поля необходимо вводить одну строку текста или динамическое содержимое, представляющее собой поле текстового типа.</span><span class="sxs-lookup"><span data-stu-id="6d10f-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="6d10f-180">Например, поля "Категория" и "Подкатегория".</span><span class="sxs-lookup"><span data-stu-id="6d10f-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="6d10f-181">Параметры > Настройки > Настроить систему > Сущности > Задачи > Поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="6d10f-182">category</span><span class="sxs-lookup"><span data-stu-id="6d10f-182">category</span></span> |<span data-ttu-id="6d10f-183">Одна строка текста</span><span class="sxs-lookup"><span data-stu-id="6d10f-183">Single Line of Text</span></span>        
<span data-ttu-id="6d10f-184">Целочисленные поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-184">Integer fields</span></span> | <span data-ttu-id="6d10f-185">В некоторые поля необходимо ввести целое число или добавить динамическое содержимое, которое является полем целочисленного типа.</span><span class="sxs-lookup"><span data-stu-id="6d10f-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="6d10f-186">Например, поля "Процент выполнения" и "Длительность".</span><span class="sxs-lookup"><span data-stu-id="6d10f-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="6d10f-187">Параметры > Настройки > Настроить систему > Сущности > Задачи > Поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="6d10f-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="6d10f-188">percentcomplete</span></span> |<span data-ttu-id="6d10f-189">Целое число</span><span class="sxs-lookup"><span data-stu-id="6d10f-189">Whole Number</span></span>         
<span data-ttu-id="6d10f-190">Поля даты</span><span class="sxs-lookup"><span data-stu-id="6d10f-190">Date fields</span></span> | <span data-ttu-id="6d10f-191">В некоторые поля необходимо ввести дату в формате "мм/дд/гггг" или добавить динамическое содержимое, которое является полем даты.</span><span class="sxs-lookup"><span data-stu-id="6d10f-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="6d10f-192">Например, такие поля, как "Дата создания", "Дата начала", "Фактическое начало", "Время последней приостановки", "Фактическое окончание" и "Дата выполнения".</span><span class="sxs-lookup"><span data-stu-id="6d10f-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="6d10f-193">Параметры > Настройки > Настроить систему > Сущности > Задачи > Поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="6d10f-194">createdon</span><span class="sxs-lookup"><span data-stu-id="6d10f-194">createdon</span></span> |<span data-ttu-id="6d10f-195">Дата и время</span><span class="sxs-lookup"><span data-stu-id="6d10f-195">Date and Time</span></span>
<span data-ttu-id="6d10f-196">Поля, для которых требуется как идентификатор записи, так и тип поиска</span><span class="sxs-lookup"><span data-stu-id="6d10f-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="6d10f-197">Для некоторых полей, которые ссылаются на другую запись сущности, требуется как идентификатор записи, так и тип поиска.</span><span class="sxs-lookup"><span data-stu-id="6d10f-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="6d10f-198">Параметры > Настройки > Настроить систему > Сущности > Учетная запись > Поля</span><span class="sxs-lookup"><span data-stu-id="6d10f-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="6d10f-199">accountid</span><span class="sxs-lookup"><span data-stu-id="6d10f-199">accountid</span></span>  | <span data-ttu-id="6d10f-200">Первичный ключ</span><span class="sxs-lookup"><span data-stu-id="6d10f-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="6d10f-201">Другие примеры полей, для которых требуется как идентификатор записи, так и тип поиска</span><span class="sxs-lookup"><span data-stu-id="6d10f-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="6d10f-202">В дополнение к предыдущей таблице ниже приведены примеры полей, которые не работают со значениями, выбранными в списке динамического содержимого.</span><span class="sxs-lookup"><span data-stu-id="6d10f-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="6d10f-203">Вместо этого в PowerApps в эти поля необходимо ввести как идентификатор записи, так и тип поиска.</span><span class="sxs-lookup"><span data-stu-id="6d10f-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="6d10f-204">"Владелец" и "Тип владельца".</span><span class="sxs-lookup"><span data-stu-id="6d10f-204">Owner and Owner Type.</span></span> <span data-ttu-id="6d10f-205">Поле "Владелец" должно содержать допустимый идентификатор записи пользователя или рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="6d10f-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="6d10f-206">В поле "Тип владельца" должен быть задан тип **systemusers** (системные пользователи) или **рабочие группы**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="6d10f-207">"Клиент" и "Тип клиента".</span><span class="sxs-lookup"><span data-stu-id="6d10f-207">Customer and Customer Type.</span></span> <span data-ttu-id="6d10f-208">Поле "Клиент" должно содержать допустимый идентификатор учетной записи или записи контакта.</span><span class="sxs-lookup"><span data-stu-id="6d10f-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="6d10f-209">В поле "Тип владельца" должен быть задан тип **учетные записи** или **контакты**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="6d10f-210">"В отношении" и поле типа "В отношении".</span><span class="sxs-lookup"><span data-stu-id="6d10f-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="6d10f-211">Поле "В отношении" должно содержать допустимый идентификатор записи, например идентификатор учетной записи или записи контакта.</span><span class="sxs-lookup"><span data-stu-id="6d10f-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="6d10f-212">В поле типа "В отношении" должен быть задан тип поиска записи, например **учетные записи** или **контакты**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="6d10f-213">В следующем примере действия создания задачи в поле "В отношении" добавляется учетная запись, соответствующая идентификатору записи.</span><span class="sxs-lookup"><span data-stu-id="6d10f-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Идентификатор записи и тип учетной записи](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="6d10f-215">В этом примере задача назначается для конкретного пользователя на основе идентификатора записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="6d10f-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Идентификатор записи и тип учетной записи](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="6d10f-217">Чтобы найти идентификатор записи, ознакомьтесь с разделом *Поиск идентификатора записи*.</span><span class="sxs-lookup"><span data-stu-id="6d10f-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="6d10f-218">Поиск идентификатора записи</span><span class="sxs-lookup"><span data-stu-id="6d10f-218">Find the record ID</span></span>

1. <span data-ttu-id="6d10f-219">Откройте запись, например для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6d10f-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="6d10f-220">На панели инструментов "Действия" щелкните **Всплывающее окно** ![запись всплывающего окна](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="6d10f-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="6d10f-221">Кроме того, на панели инструментов "Действия" щелкните **Отправить ссылку по почте**, чтобы скопировать полный URL-адрес в программу электронной почты по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6d10f-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="6d10f-222">Идентификатор записи отображается между знаками кодирования URL-адреса %7b и %7d.</span><span class="sxs-lookup"><span data-stu-id="6d10f-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Идентификатор записи и тип учетной записи](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="6d10f-224">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="6d10f-224">Troubleshooting</span></span>
<span data-ttu-id="6d10f-225">Чтобы устранить сбой шага в приложении логики, просмотрите сведения о состоянии события.</span><span class="sxs-lookup"><span data-stu-id="6d10f-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="6d10f-226">В разделе **Приложения логики** выберите свое приложение логики и щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="6d10f-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="6d10f-227">Отобразится область "Сводка", где содержатся сведения о состоянии выполнения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="6d10f-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![Состояние выполнения приложения логики](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="6d10f-229">Чтобы получить дополнительные сведения о неудачных циклах выполнения, щелкните событие со сбоем.</span><span class="sxs-lookup"><span data-stu-id="6d10f-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="6d10f-230">Чтобы развернуть шаг с ошибкой, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="6d10f-230">To expand a failed step, click that step.</span></span>

   ![Развертывание шага с ошибкой](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="6d10f-232">Отобразятся сведения о шаге, которые могут помочь устранить причину сбоя.</span><span class="sxs-lookup"><span data-stu-id="6d10f-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Сведения о шаге с ошибкой](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="6d10f-234">Дополнительные сведения об устранении неполадок в приложениях логики см. в статье [Диагностика сбоев приложений логики](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="6d10f-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="6d10f-235">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="6d10f-235">Connector-specific details</span></span>

<span data-ttu-id="6d10f-236">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="6d10f-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6d10f-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d10f-237">Next steps</span></span>
<span data-ttu-id="6d10f-238">Чтобы узнать, какие еще соединители доступны в Logic Apps, просмотрите [список интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6d10f-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
