---
title: "aaaAzure Mobile Engagement пользовательский интерфейс - критерий достижения"
description: "Узнайте, как кампаний tooa toouse определения критериев toosend принудительной выделить подмножество пользователей с помощью Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="d1590-103">Как кампаний tooa toouse определения критериев toosend принудительной выделить подмножество пользователей</span><span class="sxs-lookup"><span data-stu-id="d1590-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="d1590-104">Предназначенные для аудитории по указанному условию, с помощью кнопки «Создать условие» hello является одним из hello самых мощных понятий в Azure Mobile Engagement, позволяет отправлять соответствующие push-уведомления, что клиенты hello ответит tooinstead из всех спама.</span><span class="sxs-lookup"><span data-stu-id="d1590-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="d1590-105">Можно ограничить аудитории на основе стандартных критериев и имитировать toodetermine Push-уведомлений как многие пользователи получат уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="d1590-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="d1590-106">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="d1590-106">**See also:**</span></span>

* <span data-ttu-id="d1590-107">[Создание кампаний по рассылке push-уведомлений и управление ими][Link 27]</span><span class="sxs-lookup"><span data-stu-id="d1590-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="d1590-108">Вот некоторые из возможных условий выбора целевой аудитории.</span><span class="sxs-lookup"><span data-stu-id="d1590-108">Audience criteria can include:</span></span>
* <span data-ttu-id="d1590-109">** Technicals: ** вы можете ориентироваться на основе hello же технические сведения, вы увидите на hello аналитика и монитор разделов.</span><span class="sxs-lookup"><span data-stu-id="d1590-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="d1590-110">**Ознакомьтесь со статьями:** [Анализ журналов данных о приложении][Link 15], [Наблюдение за работой приложения в режиме реального времени][Link 16]</span><span class="sxs-lookup"><span data-stu-id="d1590-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="d1590-111">**Расположение:** приложений, использующих «реального времени отчеты о местоположении» с Геозон может служить tootarget критерии аудитории из hello GPS навигатора географического расположения.</span><span class="sxs-lookup"><span data-stu-id="d1590-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="d1590-112">Вызов «Отложенной области расположения отчетов» также быть используется tootarget аудитории из расположения сотовых телефонов hello («реального времени расположение отчетов» и «Отложенной области расположения отчетов» необходимо активировать из hello SDK).</span><span class="sxs-lookup"><span data-stu-id="d1590-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="d1590-113">**Ознакомьтесь со статьями:** [Документация по службам мобильного взаимодействия][Link 5] и [Документация по пакету SDK для интеграции с Android][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d1590-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="d1590-114">**Отзыв на рекламу.** Выбирать аудиторию можно также на основе отзывов клиентов о предыдущей кампании. Эти данные доступны в разделах объявлений, опросов и отправленных данных.</span><span class="sxs-lookup"><span data-stu-id="d1590-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="d1590-115">Это позволяет toobetter целевую аудиторию, по достижении два или три кампаний, чем удалось hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="d1590-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="d1590-116">Он также может использоваться toofilter выход для пользователей, которые уже получил уведомление о аналогичное содержимое, задав tooNOT кампании отправляться toousers, который уже получил предыдущих определенной кампании.</span><span class="sxs-lookup"><span data-stu-id="d1590-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="d1590-117">Вы даже можете исключать из списка получателей новых уведомлений пользователей, которые являются целевой аудиторией другой проводимой кампании.</span><span class="sxs-lookup"><span data-stu-id="d1590-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="d1590-118">**Ознакомьтесь со статьей:** [Управление уникальным контентом для различных типов кампаний push-уведомлений][Link 29]</span><span class="sxs-lookup"><span data-stu-id="d1590-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="d1590-119">**Отслеживание установок.** Вы можете отслеживать информацию, используя данные о месте установки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d1590-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="d1590-120">**Ознакомьтесь со статьей:** [Управление глобальными параметрами приложения][Link 20]</span><span class="sxs-lookup"><span data-stu-id="d1590-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="d1590-121">**Профиль пользователя:** вы можете целевой объект на основании обычного пользователя сведения и вы можете целевой объект на основании сведений пользовательского приложения hello, созданного.</span><span class="sxs-lookup"><span data-stu-id="d1590-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="d1590-122">Сюда входят пользователи, вошедшие в настоящее время и пользователей, которые ответили определенные вопросы вы запросили их tooset в hello самого приложения вместо просто как они ответили tooprevious кампании.</span><span class="sxs-lookup"><span data-stu-id="d1590-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="d1590-123">В этом списке отображаются все сведения, которые вы определили для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="d1590-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="d1590-124">Сегменты. Выбирать целевую аудиторию можно также, исходя из сегментов, которые вы создали на основе определенного поведения пользователей. Такое поведение обычно определяется несколькими условиями.</span><span class="sxs-lookup"><span data-stu-id="d1590-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="d1590-125">В этом списке отображаются все сегменты, которые вы определили для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="d1590-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="d1590-126">**Ознакомьтесь со статьей:** [Создание сегментов пользователей и управление ими для выявления закономерностей][Link 18]</span><span class="sxs-lookup"><span data-stu-id="d1590-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="d1590-127">**Информация приложения:** теги сведений о пользовательских приложений, которые могут быть созданы из поведение пользователя tootrack «Параметры».</span><span class="sxs-lookup"><span data-stu-id="d1590-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="d1590-128">**Ознакомьтесь со статьей:** [Управление глобальными параметрами приложения][Link 20]</span><span class="sxs-lookup"><span data-stu-id="d1590-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="d1590-129">Пример:</span><span class="sxs-lookup"><span data-stu-id="d1590-129">Example:</span></span>
<span data-ttu-id="d1590-130">Toopush объявления toohello только подмножество пользователей, выполнявших в приложении приобрести действия.</span><span class="sxs-lookup"><span data-stu-id="d1590-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="d1590-131">Переход на страницу настройки приложения tooyour, выберите меню «Информация приложения» hello и выберите «Новый info приложения»</span><span class="sxs-lookup"><span data-stu-id="d1590-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="d1590-132">Зарегистрируйте новую информацию с логическими значениями и назовите ее inAppPurchase.</span><span class="sxs-lookup"><span data-stu-id="d1590-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="d1590-133">Сделать приложение задать сведения об этом приложения слишком «true», при hello пользователь успешно выполняет Покупка из приложения (с помощью sendAppInfo hello («inAppPurchase»,...) функция)</span><span class="sxs-lookup"><span data-stu-id="d1590-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="d1590-134">Если вы не хотите toodo это из приложения, можно сделать из серверной части с помощью API hello устройства)</span><span class="sxs-lookup"><span data-stu-id="d1590-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="d1590-135">Затем необходимо просто toocreate объявления, критерием, ограничивая вашей toousers аудитории, имеющих «inAppPurchase» задайте слишком «true»)</span><span class="sxs-lookup"><span data-stu-id="d1590-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="d1590-136">Выбор на основе критериев, отличные от теги сведений о приложении требуется Azure Mobile Engagement toogather информацию из устройств пользователей hello принудительной отправки и таким образом, может привести к задержке.</span><span class="sxs-lookup"><span data-stu-id="d1590-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="d1590-137">Использование расширенных параметров push-уведомлений (например, обновление индикаторов событий) также может привести к задержке рассылки.</span><span class="sxs-lookup"><span data-stu-id="d1590-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="d1590-138">С помощью кампании «один снимок» от hello API принудительной hello абсолютный метод является быстрым push в Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d1590-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="d1590-139">Используя только теги сведений о приложении в качестве условия принудительной кампании Reach (либо hello пользовательского интерфейса из hello Reach API) — hello Далее быстрый способ, поскольку теги сведений о приложении, хранятся на стороне сервера hello.</span><span class="sxs-lookup"><span data-stu-id="d1590-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="d1590-140">С помощью других критериев выбора целевой платформы для кампании push-уведомлений — hello наиболее гибкий, но медленных принудительной, поскольку tooquery hello устройства Azure Mobile Engagement в порядке toosend hello кампании.</span><span class="sxs-lookup"><span data-stu-id="d1590-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![Охват — условие 1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="d1590-142">Подробные сведения об условиях таргетинга</span><span class="sxs-lookup"><span data-stu-id="d1590-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="d1590-143">**Технические данные.**</span><span class="sxs-lookup"><span data-stu-id="d1590-143">**Technicals**</span></span>     
* <span data-ttu-id="d1590-144">Имя встроенного ПО: имя встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="d1590-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="d1590-145">Версия встроенного ПО: версия встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="d1590-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="d1590-146">Модель устройства: модель устройства.</span><span class="sxs-lookup"><span data-stu-id="d1590-146">Device model:    Device model</span></span>
* <span data-ttu-id="d1590-147">Производитель устройства: производитель устройства.</span><span class="sxs-lookup"><span data-stu-id="d1590-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="d1590-148">Версия приложения: версия приложения.</span><span class="sxs-lookup"><span data-stu-id="d1590-148">Application version:    Application version</span></span>
* <span data-ttu-id="d1590-149">Имя оператора: имя оператора, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="d1590-150">Страна оператора: страна оператора, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="d1590-151">Тип сети: тип сети.</span><span class="sxs-lookup"><span data-stu-id="d1590-151">Network type:    Network type</span></span>
* <span data-ttu-id="d1590-152">Языковой стандарт: языковой стандарт.</span><span class="sxs-lookup"><span data-stu-id="d1590-152">Locale:    Locale</span></span>
* <span data-ttu-id="d1590-153">Размер экрана: размер экрана.</span><span class="sxs-lookup"><span data-stu-id="d1590-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="d1590-154">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="d1590-154">**Location**</span></span>      
* <span data-ttu-id="d1590-155">Последнее известное местоположение: страна, регион, населенный пункт.</span><span class="sxs-lookup"><span data-stu-id="d1590-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="d1590-156">Сведения о геозоне в реальном времени: список объектов (название, действия), круговой объект (название, широта, долгота, радиус в метрах).</span><span class="sxs-lookup"><span data-stu-id="d1590-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="d1590-157">**Отзывы о кампании.**</span><span class="sxs-lookup"><span data-stu-id="d1590-157">**Reach feedback**</span></span>     
* <span data-ttu-id="d1590-158">Отзывы об объявлении: объявление, отзывы.</span><span class="sxs-lookup"><span data-stu-id="d1590-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="d1590-159">Отзывы об опросе: опрос, отзывы.</span><span class="sxs-lookup"><span data-stu-id="d1590-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="d1590-160">Отзывы об ответах на вопросы опроса: отзывы об ответах на вопросы опроса, вопрос, варианты ответа.</span><span class="sxs-lookup"><span data-stu-id="d1590-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="d1590-161">Отзывы об отправленных данных: отправленные данные, отзывы.</span><span class="sxs-lookup"><span data-stu-id="d1590-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="d1590-162">**Отслеживание данных об установке.**</span><span class="sxs-lookup"><span data-stu-id="d1590-162">**Install Tracking**</span></span>     
* <span data-ttu-id="d1590-163">Хранилище: хранилище, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="d1590-164">Источник: источник, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="d1590-165">**Профиль пользователя.**</span><span class="sxs-lookup"><span data-stu-id="d1590-165">**User profile**</span></span>     
* <span data-ttu-id="d1590-166">Пол: мужчина или женщина, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="d1590-167">Дата рождения: оператор, дата, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="d1590-168">Участие: true или false, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="d1590-169">**Сведения о приложении.**</span><span class="sxs-lookup"><span data-stu-id="d1590-169">**App Info**</span></span>      
* <span data-ttu-id="d1590-170">Строка: строка, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-170">String:    String, undefined</span></span>
* <span data-ttu-id="d1590-171">Дата: оператор, дата, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="d1590-172">Целое число: оператор, число, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="d1590-173">Логическое значение: true или false, не указано.</span><span class="sxs-lookup"><span data-stu-id="d1590-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="d1590-174">**Сегмент.**</span><span class="sxs-lookup"><span data-stu-id="d1590-174">**Segment**</span></span>    
* <span data-ttu-id="d1590-175">Имя сегмента (из раскрывающегося списка), исключение (пользователи, не входящие в этот сегмент).</span><span class="sxs-lookup"><span data-stu-id="d1590-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

