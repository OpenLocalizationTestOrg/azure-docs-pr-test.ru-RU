---
title: "Использование смайликов эмодзи в Службах мобильного взаимодействия Azure"
description: "Как использовать смайлики эмодзи в push-уведомлениях"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="1d4db-103">Использование смайликов эмодзи в push-уведомлениях</span><span class="sxs-lookup"><span data-stu-id="1d4db-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="1d4db-104">Вы легко можете включать смайлики эмодзи в свои push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="1d4db-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="1d4db-105">Сначала вам нужно найти смайлик эмодзи, который будет добавлен в сообщение.</span><span class="sxs-lookup"><span data-stu-id="1d4db-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="1d4db-106">Убедитесь, что выбранный смайлик эмодзи будет отображаться на целевом устройстве, так как производителям устройств обычно требуется некоторое время, чтобы добавить новые смайлики эмодзи на платформы устройств.</span><span class="sxs-lookup"><span data-stu-id="1d4db-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="1d4db-107">В системе **Windows** вы можете перейти по этой [ссылке](http://apps.timwhitlock.info/emoji/tables/unicode) и скопировать значок Native.</span><span class="sxs-lookup"><span data-stu-id="1d4db-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="1d4db-108">В системе **Mac** вы можете найти эмодзи в приложении Dictionary (Словарь), выбрав Edit -> Emoji & Symbols (Правка -> Эмодзи и символы).</span><span class="sxs-lookup"><span data-stu-id="1d4db-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="1d4db-109">На портале Служб мобильного взаимодействия Azure перейдите на вкладку **Reach** (Рекламная кампания).</span><span class="sxs-lookup"><span data-stu-id="1d4db-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="1d4db-110">Выберите тип push-уведомления (объявление, опрос и т. д.).</span><span class="sxs-lookup"><span data-stu-id="1d4db-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="1d4db-111">В данном примере мы выберем объявление.</span><span class="sxs-lookup"><span data-stu-id="1d4db-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="1d4db-112">Заполняйте поля уведомления, пока не дойдете до основного текста.</span><span class="sxs-lookup"><span data-stu-id="1d4db-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="1d4db-113">В это поле можно добавить смайлик эмодзи.</span><span class="sxs-lookup"><span data-stu-id="1d4db-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="1d4db-114">Вы можете вставить его как в заголовок, так и в основной текст.</span><span class="sxs-lookup"><span data-stu-id="1d4db-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="1d4db-115">Вам нужно будет перетащить или скопировать выбранный ранее смайлик эмодзи.</span><span class="sxs-lookup"><span data-stu-id="1d4db-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="1d4db-116">Заполните остальные поля уведомления и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="1d4db-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="1d4db-117">При тестировании или активации объявления появится уведомление с выбранным вами смайликом.</span><span class="sxs-lookup"><span data-stu-id="1d4db-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="1d4db-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="1d4db-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

