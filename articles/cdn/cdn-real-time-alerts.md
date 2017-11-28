---
title: "Оповещения в режиме реального времени в Azure CDN | Документация Майкрософт"
description: "Оповещения в режиме реального времени в сети CDN Microsoft Azure. Оповещения в режиме реального времени позволяют получать уведомления о производительности конечных точек в профиле CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="04692-104">Оповещения в режиме реального времени в сети CDN Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="04692-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="04692-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="04692-105">Overview</span></span>
<span data-ttu-id="04692-106">В этом документе содержатся сведения об оповещениях в режиме реального времени в сети CDN Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="04692-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="04692-107">Эта функция предоставляет актуальные уведомления о производительности конечных точек в профиле CDN.</span><span class="sxs-lookup"><span data-stu-id="04692-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="04692-108">Вы можете настроить сообщения с оповещением или оповещения HTTP на основе:</span><span class="sxs-lookup"><span data-stu-id="04692-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="04692-109">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="04692-109">Bandwidth</span></span>
* <span data-ttu-id="04692-110">Коды состояний</span><span class="sxs-lookup"><span data-stu-id="04692-110">Status Codes</span></span>
* <span data-ttu-id="04692-111">Состояния кэша</span><span class="sxs-lookup"><span data-stu-id="04692-111">Cache Statuses</span></span>
* <span data-ttu-id="04692-112">Подключения</span><span class="sxs-lookup"><span data-stu-id="04692-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="04692-113">Создание оповещения в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="04692-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="04692-114">На [портале Azure](https://portal.azure.com)перейдите к профилю CDN.</span><span class="sxs-lookup"><span data-stu-id="04692-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Колонка профиля сети CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="04692-116">В колонке профиля сети CDN нажмите кнопку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="04692-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="04692-118">Откроется портал управления CDN.</span><span class="sxs-lookup"><span data-stu-id="04692-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="04692-119">Наведите указатель на вкладку **Аналитика**, а затем на всплывающее окно **Real-Time Stats** (Статистика в реальном времени).</span><span class="sxs-lookup"><span data-stu-id="04692-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="04692-120">Щелкните **Real-Time Alerts**(Оповещения в реальном времени).</span><span class="sxs-lookup"><span data-stu-id="04692-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Портал управления CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="04692-122">Отобразится список имеющихся конфигураций оповещений (при их наличии).</span><span class="sxs-lookup"><span data-stu-id="04692-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="04692-123">Нажмите кнопку **Добавить оповещение** .</span><span class="sxs-lookup"><span data-stu-id="04692-123">Click the **Add Alert** button.</span></span>
   
    ![Кнопка "Добавить оповещение"](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="04692-125">Откроется форма для создания оповещения.</span><span class="sxs-lookup"><span data-stu-id="04692-125">A form for creating a new alert is displayed.</span></span>
   
    ![Форма нового оповещения](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="04692-127">Если вы хотите, чтобы оповещение становилось активным после нажатия кнопки **Сохранить**, установите флажок **Alert Enabled** (Оповещение включено).</span><span class="sxs-lookup"><span data-stu-id="04692-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="04692-128">В поле **Имя** введите описательное имя для оповещения.</span><span class="sxs-lookup"><span data-stu-id="04692-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="04692-129">В раскрывающемся списке **Media Type** (Тип носителя) выберите **HTTP Large Object** (Большой объект HTTP).</span><span class="sxs-lookup"><span data-stu-id="04692-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Параметр Media Type (Тип носителя) с выбранным значением HTTP Large Object (Большой объект HTTP)](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="04692-131">В качестве **типа носителя** нужно выбрать **HTTP Large Object** (Большой объект HTTP).</span><span class="sxs-lookup"><span data-stu-id="04692-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="04692-132">**Azure CDN от Verizon**не поддерживает другие типы.</span><span class="sxs-lookup"><span data-stu-id="04692-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="04692-133">Если не выбрать тип **HTTP Large Object** (Большой объект HTTP), оповещения не будут активироваться.</span><span class="sxs-lookup"><span data-stu-id="04692-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="04692-134">Создайте **выражение** для мониторинга, выбрав значения параметров **Метрика**, **Оператор** и **Триггер**.</span><span class="sxs-lookup"><span data-stu-id="04692-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="04692-135">Для параметра **Метрика** выберите тип условия, по которому следует осуществлять мониторинг.</span><span class="sxs-lookup"><span data-stu-id="04692-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="04692-136">**Bandwidth Mbps** (Пропускная способность в Мбит/с) — это объем использования пропускной способности в мегабитах в секунду.</span><span class="sxs-lookup"><span data-stu-id="04692-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="04692-137">**Всего подключений** — число одновременных подключений HTTP к нашим пограничным серверам.</span><span class="sxs-lookup"><span data-stu-id="04692-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="04692-138">Определения различных состояний кэша и кодов состояния см. в разделах [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) (Коды состояния кэша в сети Azure CDN) и [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx) (Коды состояний HTTP в сети Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="04692-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="04692-139">**Оператор** — математический оператор, который устанавливает связь между метрикой и значением триггера.</span><span class="sxs-lookup"><span data-stu-id="04692-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="04692-140">**Trigger Value** (Значение триггера) — это пороговое значение, которое должно быть достигнуто для отправления уведомления.</span><span class="sxs-lookup"><span data-stu-id="04692-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="04692-141">В следующем примере используется выражение, которое активирует отправку уведомления, если количество кодов состояния 404 превышает 25.</span><span class="sxs-lookup"><span data-stu-id="04692-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![Пример выражения для оповещения в режиме реального времени](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="04692-143">Для параметра **Интервал**укажите, как часто следует проверять выражение.</span><span class="sxs-lookup"><span data-stu-id="04692-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="04692-144">В раскрывающемся списке **Notify on** (Когда уведомлять) выберите, когда вы хотите получать уведомления, если выражение совпадает.</span><span class="sxs-lookup"><span data-stu-id="04692-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="04692-145">**Condition Start** (Начало условия) означает, что уведомление будет отправлено при обнаружении указанного условия.</span><span class="sxs-lookup"><span data-stu-id="04692-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="04692-146">**Condition End** (Конец условия) означает, что уведомление будет отправлено, когда указанное условие больше не выполняется.</span><span class="sxs-lookup"><span data-stu-id="04692-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="04692-147">Это уведомление будет активировано, только когда система мониторинга сети обнаружит, что заданное условие выполнено.</span><span class="sxs-lookup"><span data-stu-id="04692-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="04692-148">**Непрерывно** означает, что уведомление будет отправляться каждый раз, когда система мониторинга сети обнаружит указанное условие.</span><span class="sxs-lookup"><span data-stu-id="04692-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="04692-149">Обратите внимание, что система мониторинга сети проверяет выполнение заданного условия только один раз в рамках интервала.</span><span class="sxs-lookup"><span data-stu-id="04692-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="04692-150">**Condition Start and End** (Начало и конец условия) указывает, что уведомления будут отправляться сразу после обнаружения заданного условия и еще раз, когда условие больше не будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="04692-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="04692-151">Если вы хотите получать уведомления по электронной почте, установите флажок **Notify by Email** (Уведомлять по электронной почте).</span><span class="sxs-lookup"><span data-stu-id="04692-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![Форма уведомления по электронной почте](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="04692-153">В поле **Кому** введите адрес электронной почты для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="04692-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="04692-154">В полях **Тема** и **Текст** можно оставить значения по умолчанию либо можно настроить сообщение с помощью списка **Available keywords** (Доступные ключевые слова), чтобы динамически вставлять данные оповещения при отправке сообщения.</span><span class="sxs-lookup"><span data-stu-id="04692-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="04692-155">Вы можете проверить уведомление по электронной почте. Для этого после сохранения конфигурации оповещений нажмите кнопку **Test Notification** (Проверить уведомление).</span><span class="sxs-lookup"><span data-stu-id="04692-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="04692-156">Чтобы публиковать уведомления на веб-сервере, установите флажок **Notify by HTTP Post** (Уведомлять с помощью HTTP Post).</span><span class="sxs-lookup"><span data-stu-id="04692-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![Форма уведомления HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="04692-158">В поле **URL-адрес** введите URL-адрес для публикации HTTP-сообщения.</span><span class="sxs-lookup"><span data-stu-id="04692-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="04692-159">В текстовом поле **Заголовки** введите заголовки HTTP, отправляемые в запросе.</span><span class="sxs-lookup"><span data-stu-id="04692-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="04692-160">В поле **Текст** можно настроить сообщение с помощью списка **Available keywords** (Доступные ключевые слова), чтобы динамически вставлять данные оповещения при отправке сообщения.</span><span class="sxs-lookup"><span data-stu-id="04692-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="04692-161">По умолчанию в полях **Заголовки** и **Текст** содержатся полезные данные XML, как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="04692-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="04692-162">Вы можете проверить уведомление HTTP Post. Для этого после сохранения конфигурации оповещений нажмите кнопку **Test Notification** (Проверить уведомление).</span><span class="sxs-lookup"><span data-stu-id="04692-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="04692-163">Нажмите кнопку **Сохранить** , чтобы сохранить конфигурацию оповещений.</span><span class="sxs-lookup"><span data-stu-id="04692-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="04692-164">Если вы установили флажок **Alert Enabled** (Оповещение включено) на шаге 5, оповещение активно.</span><span class="sxs-lookup"><span data-stu-id="04692-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04692-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04692-165">Next Steps</span></span>
* <span data-ttu-id="04692-166">Ознакомьтесь со статьей [Статистика в реальном времени в сети CDN Microsoft Azure](cdn-real-time-stats.md).</span><span class="sxs-lookup"><span data-stu-id="04692-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="04692-167">Дополнительные сведения о [расширенных HTTP-отчетах](cdn-advanced-http-reports.md).</span><span class="sxs-lookup"><span data-stu-id="04692-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="04692-168">[Анализ вариантов использования CDN Azure](cdn-analyze-usage-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="04692-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

