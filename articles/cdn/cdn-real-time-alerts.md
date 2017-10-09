---
title: "оповещения в режиме реального времени CDN aaaAzure | Документы Microsoft"
description: "Оповещения в режиме реального времени в сети CDN Microsoft Azure. В режиме реального времени оповещения содержат уведомления о производительности hello hello конечных точек в ваш профиль CDN."
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="b59dd-104">Оповещения в режиме реального времени в сети CDN Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b59dd-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="b59dd-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="b59dd-105">Overview</span></span>
<span data-ttu-id="b59dd-106">В этом документе содержатся сведения об оповещениях в режиме реального времени в сети CDN Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b59dd-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="b59dd-107">Эта функция предоставляет в реальном времени уведомления об производительности hello hello конечных точек в ваш профиль CDN.</span><span class="sxs-lookup"><span data-stu-id="b59dd-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="b59dd-108">Вы можете настроить сообщения с оповещением или оповещения HTTP на основе:</span><span class="sxs-lookup"><span data-stu-id="b59dd-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="b59dd-109">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="b59dd-109">Bandwidth</span></span>
* <span data-ttu-id="b59dd-110">Коды состояний</span><span class="sxs-lookup"><span data-stu-id="b59dd-110">Status Codes</span></span>
* <span data-ttu-id="b59dd-111">Состояния кэша</span><span class="sxs-lookup"><span data-stu-id="b59dd-111">Cache Statuses</span></span>
* <span data-ttu-id="b59dd-112">Подключения</span><span class="sxs-lookup"><span data-stu-id="b59dd-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="b59dd-113">Создание оповещения в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="b59dd-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="b59dd-114">В hello [портала Azure](https://portal.azure.com), Обзор профиля CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="b59dd-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Колонка профиля сети CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="b59dd-116">В колонке профиля CDN hello выберите hello **управление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b59dd-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="b59dd-118">Открытие портала управления CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="b59dd-119">Наведите указатель мыши hello **Analytics** , а затем наведите указатель мыши hello **статистики в реальном времени** всплывающим меню.</span><span class="sxs-lookup"><span data-stu-id="b59dd-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="b59dd-120">Щелкните **Real-Time Alerts**(Оповещения в реальном времени).</span><span class="sxs-lookup"><span data-stu-id="b59dd-120">Click on **Real-Time Alerts**.</span></span>
   
    ![Портал управления CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="b59dd-122">отображается список Hello существующей конфигурации оповещений (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="b59dd-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="b59dd-123">Нажмите кнопку hello **Добавление оповещения** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b59dd-123">Click hello **Add Alert** button.</span></span>
   
    ![Кнопка "Добавить оповещение"](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="b59dd-125">Откроется форма для создания оповещения.</span><span class="sxs-lookup"><span data-stu-id="b59dd-125">A form for creating a new alert is displayed.</span></span>
   
    ![Форма нового оповещения](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="b59dd-127">Если требуется этого предупреждения toobe active при нажатии кнопки **Сохранить**, проверьте hello **предупреждение активировано** флажок.</span><span class="sxs-lookup"><span data-stu-id="b59dd-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="b59dd-128">Введите описательное имя для оповещения в hello **имя** поля.</span><span class="sxs-lookup"><span data-stu-id="b59dd-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="b59dd-129">В hello **тип носителя** раскрывающийся список, выберите **HTTP больших объектов**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![Параметр Media Type (Тип носителя) с выбранным значением HTTP Large Object (Большой объект HTTP)](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="b59dd-131">Необходимо выбрать **больших объектов HTTP** как hello **тип носителя**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="b59dd-132">Hello другие параметры не используются **CDN Azure из Verizon**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="b59dd-133">Сбой tooselect **больших объектов HTTP** вызовет предупреждение toonever активироваться.</span><span class="sxs-lookup"><span data-stu-id="b59dd-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="b59dd-134">Создание **выражение** toomonitor, выбрав **метрика**, **оператор**, и **триггера значение**.</span><span class="sxs-lookup"><span data-stu-id="b59dd-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="b59dd-135">Для **метрика**, выберите тип условия, которыми должен наблюдать hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="b59dd-136">**Мбит/с пропускной способности** — hello объем использования пропускной способности в мегабит в секунду.</span><span class="sxs-lookup"><span data-stu-id="b59dd-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="b59dd-137">**Общее число подключений** : hello число одновременных tooour подключений HTTP пограничные серверы.</span><span class="sxs-lookup"><span data-stu-id="b59dd-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="b59dd-138">Определения hello различные состояния кэша и коды состояния, в разделе [коды состояния кэша CDN Azure](https://msdn.microsoft.com/library/mt759237.aspx) и [коды состояния HTTP CDN Azure](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="b59dd-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="b59dd-139">**Оператор** — hello математически оператор, который устанавливает связь hello метрика hello и значение hello триггера.</span><span class="sxs-lookup"><span data-stu-id="b59dd-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="b59dd-140">**Активировать значение** — hello пороговое значение, которое необходимо выполнить, прежде чем будет отправлено уведомление.</span><span class="sxs-lookup"><span data-stu-id="b59dd-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="b59dd-141">В hello ниже примере hello выражения, созданные мной означает, что хотелось бы toobe уведомления, когда число hello кодов состояния 404 больше 25.</span><span class="sxs-lookup"><span data-stu-id="b59dd-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![Пример выражения для оповещения в режиме реального времени](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="b59dd-143">Для **интервал**, введите, как часто требуется выражение hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="b59dd-144">В hello **уведомление на** раскрывающийся список, выберите, если вы хотели бы toobe уведомлять hello выражение имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="b59dd-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="b59dd-145">**Условие запуска** означает, что при указании hello условие первого обнаружения будет отправлено уведомление.</span><span class="sxs-lookup"><span data-stu-id="b59dd-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="b59dd-146">**Условия окончания** означает, что при указании hello больше не обнаруживается будет отправлено уведомление.</span><span class="sxs-lookup"><span data-stu-id="b59dd-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="b59dd-147">Это уведомление можно запустить только после система мониторинга сети обнаружения hello, что указанное условие.</span><span class="sxs-lookup"><span data-stu-id="b59dd-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="b59dd-148">**Непрерывные** означает, что уведомление будет отправлено при каждом hello система мониторинга сети обнаруживает hello указанное условие.</span><span class="sxs-lookup"><span data-stu-id="b59dd-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="b59dd-149">Имейте в виду эту сеть hello мониторинг системы будет только проверка один раз за интервал для hello указанным условиям.</span><span class="sxs-lookup"><span data-stu-id="b59dd-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="b59dd-150">**Условие начала и окончания** означает, что будет отправлено уведомление, hello обнаружена при первом hello указанному условию, и еще раз при hello больше не обнаруживается.</span><span class="sxs-lookup"><span data-stu-id="b59dd-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="b59dd-151">Если вы хотите tooreceive уведомления по электронной почте, проверьте hello **уведомление по электронной почте** флажок.</span><span class="sxs-lookup"><span data-stu-id="b59dd-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![Форма уведомления по электронной почте](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="b59dd-153">В hello **для** введите адрес электронной почты hello место уведомления отправки.</span><span class="sxs-lookup"><span data-stu-id="b59dd-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="b59dd-154">Для **субъекта** и **текст**, можно оставить по умолчанию hello или настраивать приветственное сообщение, с помощью hello **доступные ключевые слова** toodynamically список вставки данных предупреждений при отправляется сообщение Hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b59dd-155">Можно проверить hello уведомление по электронной почте, нажав кнопку hello **тестовое уведомление** кнопку, но только после сохранения конфигурации оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="b59dd-156">Уведомления toobe учтена tooa веб-сервера, установите флажок hello **уведомить с помощью HTTP Post** флажок.</span><span class="sxs-lookup"><span data-stu-id="b59dd-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![Форма уведомления HTTP Post](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="b59dd-158">В hello **URL-адрес** введите URL-адрес hello место сообщение hello HTTP учета.</span><span class="sxs-lookup"><span data-stu-id="b59dd-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="b59dd-159">В hello **заголовки** текстовом поле введите toobe заголовки hello HTTP, отправленные в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="b59dd-160">Для **текст** можно настроить с помощью hello приветственное сообщение **доступные ключевые слова** toodynamically список вставки данных предупреждений при отправке сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="b59dd-161">**Заголовки** и **текст** по умолчанию аналогично toohello полезные данные XML-tooan ниже примере.</span><span class="sxs-lookup"><span data-stu-id="b59dd-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="b59dd-162">Можно проверить hello уведомлений HTTP Post, нажав кнопку hello **тестовое уведомление** кнопку, но только после сохранения конфигурации оповещений hello.</span><span class="sxs-lookup"><span data-stu-id="b59dd-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="b59dd-163">Нажмите кнопку hello **Сохранить** кнопку toosave предупреждения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b59dd-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="b59dd-164">Если вы установили флажок **Alert Enabled** (Оповещение включено) на шаге 5, оповещение активно.</span><span class="sxs-lookup"><span data-stu-id="b59dd-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b59dd-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b59dd-165">Next Steps</span></span>
* <span data-ttu-id="b59dd-166">Ознакомьтесь со статьей [Статистика в реальном времени в сети CDN Microsoft Azure](cdn-real-time-stats.md).</span><span class="sxs-lookup"><span data-stu-id="b59dd-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="b59dd-167">Дополнительные сведения о [расширенных HTTP-отчетах](cdn-advanced-http-reports.md).</span><span class="sxs-lookup"><span data-stu-id="b59dd-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="b59dd-168">[Анализ вариантов использования CDN Azure](cdn-analyze-usage-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="b59dd-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

