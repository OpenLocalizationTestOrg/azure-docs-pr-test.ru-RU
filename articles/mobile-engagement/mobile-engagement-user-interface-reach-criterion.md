---
title: "Пользовательский интерфейс Служб мобильного взаимодействия Azure — условия охвата"
description: "Узнайте, как в Службах мобильного взаимодействия Azure можно организовать кампанию по рассылке push-уведомлений выбранному подмножеству пользователей."
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
ms.openlocfilehash: 803b44721d0ab1ac7b5a8074e18857fc57adb724
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-targeting-criteria-to-send-push-campaigns-to-a-select-subset-of-your-users"></a><span data-ttu-id="884ee-103">Организация кампаний по рассылке push-уведомлений выбранному подмножеству пользователей с помощью условий таргетинга</span><span class="sxs-lookup"><span data-stu-id="884ee-103">How to use targeting criteria to send push campaigns to a select subset of your users</span></span>
<span data-ttu-id="884ee-104">Выбор целевой аудитории с помощью определенных условий, доступных после нажатия кнопки «Создать условия», — одна из важнейших возможностей, предусмотренных в Службах мобильного взаимодействия Azure. Благодаря этой возможности вы можете отправлять push-уведомления только тем клиентам, для которых эти уведомления представляют ценность — больше никаких рассылок всем без разбора.</span><span class="sxs-lookup"><span data-stu-id="884ee-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span></span> <span data-ttu-id="884ee-105">Определив свою аудиторию с помощью стандартных условий и симитировав рассылку, вы сможете определить, сколько пользователей получит ваше уведомление.</span><span class="sxs-lookup"><span data-stu-id="884ee-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span></span>

<span data-ttu-id="884ee-106">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="884ee-106">**See also:**</span></span>

* <span data-ttu-id="884ee-107">[Создание кампаний по рассылке push-уведомлений и управление ими][Link 27]</span><span class="sxs-lookup"><span data-stu-id="884ee-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="884ee-108">Вот некоторые из возможных условий выбора целевой аудитории.</span><span class="sxs-lookup"><span data-stu-id="884ee-108">Audience criteria can include:</span></span>
* <span data-ttu-id="884ee-109">** Technicals: ** можно выбрать целевую основании же технические сведения, которые можно увидеть в разделах аналитика и монитора.</span><span class="sxs-lookup"><span data-stu-id="884ee-109">**Technicals: ** You can target based on the same technical information you can see in the Analytics and Monitor sections.</span></span> <span data-ttu-id="884ee-110">**Ознакомьтесь со статьями:** [Анализ журналов данных о приложении][Link 15], [Наблюдение за работой приложения в режиме реального времени][Link 16]</span><span class="sxs-lookup"><span data-stu-id="884ee-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="884ee-111">**Местоположение.** Приложения, которые используют данные о геозонах и местоположении в реальном времени, в качестве условия выбора целевой аудитории могут использовать сведения о географическом положении, для определения которого используется GPS-приемник.</span><span class="sxs-lookup"><span data-stu-id="884ee-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span></span> <span data-ttu-id="884ee-112">Сведения о положении мобильного телефона, определяемом только по сотовой или беспроводной сети, тоже можно использовать для таргетинга уведомлений. Использование данных о местоположении, определяемом через GPS-приемник, а также по сотовой или беспроводной сети необходимо активировать из пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="884ee-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span></span> <span data-ttu-id="884ee-113">**Ознакомьтесь со статьями:** [Документация по службам мобильного взаимодействия][Link 5] и [Документация по пакету SDK для интеграции с Android][Link 5]</span><span class="sxs-lookup"><span data-stu-id="884ee-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="884ee-114">**Отзыв на рекламу.** Выбирать аудиторию можно также на основе отзывов клиентов о предыдущей кампании. Эти данные доступны в разделах объявлений, опросов и отправленных данных.</span><span class="sxs-lookup"><span data-stu-id="884ee-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="884ee-115">Отзывы после первых двух или трех рассылок позволяют лучше понять целевую аудиторию и в дальнейшем проводить кампании более эффективно.</span><span class="sxs-lookup"><span data-stu-id="884ee-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span></span> <span data-ttu-id="884ee-116">Это условие может также использоваться для отфильтровывания пользователей, которые уже получили похожее уведомление. Для этого в настройках кампании нужно указать, что уведомления не должны отправляться пользователям, которые уже получили определенное уведомление из предыдущей кампании.</span><span class="sxs-lookup"><span data-stu-id="884ee-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span></span> <span data-ttu-id="884ee-117">Вы даже можете исключать из списка получателей новых уведомлений пользователей, которые являются целевой аудиторией другой проводимой кампании.</span><span class="sxs-lookup"><span data-stu-id="884ee-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="884ee-118">**Ознакомьтесь со статьей:** [Управление уникальным контентом для различных типов кампаний push-уведомлений][Link 29]</span><span class="sxs-lookup"><span data-stu-id="884ee-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="884ee-119">**Отслеживание установок.** Вы можете отслеживать информацию, используя данные о месте установки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="884ee-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="884ee-120">**Ознакомьтесь со статьей:** [Управление глобальными параметрами приложения][Link 20]</span><span class="sxs-lookup"><span data-stu-id="884ee-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="884ee-121">**Профиль пользователя.** Вы можете выбирать целевую аудиторию, исходя из стандартных сведений о пользователях и данных о настраиваемом приложении, которое вы создали.</span><span class="sxs-lookup"><span data-stu-id="884ee-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span></span> <span data-ttu-id="884ee-122">Это подразумевает пользователей, вошедших в данный момент в систему, и пользователей, которые ответили на определенные вопросы в самом приложении. В этом случае не учитывается отклик пользователей на предыдущие кампании.</span><span class="sxs-lookup"><span data-stu-id="884ee-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span></span> <span data-ttu-id="884ee-123">В этом списке отображаются все сведения, которые вы определили для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="884ee-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="884ee-124">Сегменты. Выбирать целевую аудиторию можно также, исходя из сегментов, которые вы создали на основе определенного поведения пользователей. Такое поведение обычно определяется несколькими условиями.</span><span class="sxs-lookup"><span data-stu-id="884ee-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="884ee-125">В этом списке отображаются все сегменты, которые вы определили для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="884ee-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="884ee-126">**Ознакомьтесь со статьей:** [Создание сегментов пользователей и управление ими для выявления закономерностей][Link 18]</span><span class="sxs-lookup"><span data-stu-id="884ee-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="884ee-127">**Сведения о приложении.** В разделе "Параметры" можно создать теги со сведениями о настраиваемом приложении, которые помогут отслеживать поведение пользователей.</span><span class="sxs-lookup"><span data-stu-id="884ee-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span></span> <span data-ttu-id="884ee-128">**Ознакомьтесь со статьей:** [Управление глобальными параметрами приложения][Link 20]</span><span class="sxs-lookup"><span data-stu-id="884ee-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="884ee-129">Пример:</span><span class="sxs-lookup"><span data-stu-id="884ee-129">Example:</span></span>
<span data-ttu-id="884ee-130">Чтобы разослать объявление только пользователям, которые что-то покупали внутри приложения, сделайте вот что.</span><span class="sxs-lookup"><span data-stu-id="884ee-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="884ee-131">Перейдите на страницу параметров приложения, откройте меню App info (Сведения о приложении) и выберите пункт New app info (Создать сведения о приложении).</span><span class="sxs-lookup"><span data-stu-id="884ee-131">Go to your application settings page, select the "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="884ee-132">Зарегистрируйте новую информацию с логическими значениями и назовите ее inAppPurchase.</span><span class="sxs-lookup"><span data-stu-id="884ee-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="884ee-133">Настройте свое приложение таким образом, чтобы оно указывало для этой информации значение true, когда пользователь что-то покупает в приложении (используйте функцию sendAppInfo ("inAppPurchase", ...)).</span><span class="sxs-lookup"><span data-stu-id="884ee-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="884ee-134">Это можно сделать как в самом приложении, так и на сервере через API устройства.</span><span class="sxs-lookup"><span data-stu-id="884ee-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span></span>
5. <span data-ttu-id="884ee-135">Затем создайте объявление и добавьте в него условие, сужающее аудиторию только до тех пользователей, которые сделали покупку в приложении (inAppPurchase = true).</span><span class="sxs-lookup"><span data-stu-id="884ee-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span></span>

> [!NOTE]
> <span data-ttu-id="884ee-136">При отслеживании целевой аудитории на основе критериев, отличных от тегов информации о приложении, перед отправкой push-уведомлений Службам мобильного взаимодействия Azure требуется собирать информацию с пользовательских устройств, что может привести к задержке.</span><span class="sxs-lookup"><span data-stu-id="884ee-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span></span> <span data-ttu-id="884ee-137">Использование расширенных параметров push-уведомлений (например, обновление индикаторов событий) также может привести к задержке рассылки.</span><span class="sxs-lookup"><span data-stu-id="884ee-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="884ee-138">Использование одноразовой кампании через API push-уведомлений — самый быстрый способ отправки push-уведомлений в Службы мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="884ee-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="884ee-139">Второй по скорости способ рассылки рекламы — отправка push-уведомлений с использованием тегов со сведениями о приложении (через API охвата или пользовательский интерфейс), так эти теги хранятся на сервере.</span><span class="sxs-lookup"><span data-stu-id="884ee-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span></span> <span data-ttu-id="884ee-140">Другие условия таргетинга push-уведомлений предлагают наибольшую гибкость настроек, но рассылка происходит медленнее всего. Это связано с тем, что для осуществления рассылки Службы мобильного взаимодействия Azure должны сначала собрать данные с устройств.</span><span class="sxs-lookup"><span data-stu-id="884ee-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span></span>

![Охват — условие 1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="884ee-142">Подробные сведения об условиях таргетинга</span><span class="sxs-lookup"><span data-stu-id="884ee-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="884ee-143">**Технические данные.**</span><span class="sxs-lookup"><span data-stu-id="884ee-143">**Technicals**</span></span>     
* <span data-ttu-id="884ee-144">Имя встроенного ПО: имя встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="884ee-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="884ee-145">Версия встроенного ПО: версия встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="884ee-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="884ee-146">Модель устройства: модель устройства.</span><span class="sxs-lookup"><span data-stu-id="884ee-146">Device model:    Device model</span></span>
* <span data-ttu-id="884ee-147">Производитель устройства: производитель устройства.</span><span class="sxs-lookup"><span data-stu-id="884ee-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="884ee-148">Версия приложения: версия приложения.</span><span class="sxs-lookup"><span data-stu-id="884ee-148">Application version:    Application version</span></span>
* <span data-ttu-id="884ee-149">Имя оператора: имя оператора, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="884ee-150">Страна оператора: страна оператора, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="884ee-151">Тип сети: тип сети.</span><span class="sxs-lookup"><span data-stu-id="884ee-151">Network type:    Network type</span></span>
* <span data-ttu-id="884ee-152">Языковой стандарт: языковой стандарт.</span><span class="sxs-lookup"><span data-stu-id="884ee-152">Locale:    Locale</span></span>
* <span data-ttu-id="884ee-153">Размер экрана: размер экрана.</span><span class="sxs-lookup"><span data-stu-id="884ee-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="884ee-154">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="884ee-154">**Location**</span></span>      
* <span data-ttu-id="884ee-155">Последнее известное местоположение: страна, регион, населенный пункт.</span><span class="sxs-lookup"><span data-stu-id="884ee-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="884ee-156">Сведения о геозоне в реальном времени: список объектов (название, действия), круговой объект (название, широта, долгота, радиус в метрах).</span><span class="sxs-lookup"><span data-stu-id="884ee-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="884ee-157">**Отзывы о кампании.**</span><span class="sxs-lookup"><span data-stu-id="884ee-157">**Reach feedback**</span></span>     
* <span data-ttu-id="884ee-158">Отзывы об объявлении: объявление, отзывы.</span><span class="sxs-lookup"><span data-stu-id="884ee-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="884ee-159">Отзывы об опросе: опрос, отзывы.</span><span class="sxs-lookup"><span data-stu-id="884ee-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="884ee-160">Отзывы об ответах на вопросы опроса: отзывы об ответах на вопросы опроса, вопрос, варианты ответа.</span><span class="sxs-lookup"><span data-stu-id="884ee-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="884ee-161">Отзывы об отправленных данных: отправленные данные, отзывы.</span><span class="sxs-lookup"><span data-stu-id="884ee-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="884ee-162">**Отслеживание данных об установке.**</span><span class="sxs-lookup"><span data-stu-id="884ee-162">**Install Tracking**</span></span>     
* <span data-ttu-id="884ee-163">Хранилище: хранилище, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="884ee-164">Источник: источник, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="884ee-165">**Профиль пользователя.**</span><span class="sxs-lookup"><span data-stu-id="884ee-165">**User profile**</span></span>     
* <span data-ttu-id="884ee-166">Пол: мужчина или женщина, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="884ee-167">Дата рождения: оператор, дата, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="884ee-168">Участие: true или false, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="884ee-169">**Сведения о приложении.**</span><span class="sxs-lookup"><span data-stu-id="884ee-169">**App Info**</span></span>      
* <span data-ttu-id="884ee-170">Строка: строка, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-170">String:    String, undefined</span></span>
* <span data-ttu-id="884ee-171">Дата: оператор, дата, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="884ee-172">Целое число: оператор, число, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="884ee-173">Логическое значение: true или false, не указано.</span><span class="sxs-lookup"><span data-stu-id="884ee-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="884ee-174">**Сегмент.**</span><span class="sxs-lookup"><span data-stu-id="884ee-174">**Segment**</span></span>    
* <span data-ttu-id="884ee-175">Имя сегмента (из раскрывающегося списка), исключение (пользователи, не входящие в этот сегмент).</span><span class="sxs-lookup"><span data-stu-id="884ee-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

