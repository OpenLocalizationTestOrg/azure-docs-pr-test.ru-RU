### <a name="grant-access-to-your-push-certificate-to-mobile-engagement"></a><span data-ttu-id="e28bb-101">Предоставьте доступ к сертификату push-уведомлений для Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e28bb-101">Grant access to your Push Certificate to Mobile Engagement</span></span>
<span data-ttu-id="e28bb-102">Чтобы разрешить Mobile Engagement отправлять push-уведомления от вашего имени, необходимо предоставить доступ к сертификату.</span><span class="sxs-lookup"><span data-stu-id="e28bb-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span></span> <span data-ttu-id="e28bb-103">Это можно сделать путем настройки и ввода сертификата на портале Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e28bb-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span></span> <span data-ttu-id="e28bb-104">Убедитесь, что получили сертификат P12, как описано в [документации Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="e28bb-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="e28bb-105">Перейдите на портал Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e28bb-105">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="e28bb-106">Убедитесь, что все правильно, и нажмите кнопку **Выполнить охват** внизу.</span><span class="sxs-lookup"><span data-stu-id="e28bb-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="e28bb-107">Щелкните станицу **Параметры** на портале Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e28bb-107">Click on the **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="e28bb-108">Выберите здесь раздел **Системное push-уведомление** , чтобы передать ваш сертификат P12:</span><span class="sxs-lookup"><span data-stu-id="e28bb-108">From there click on the **Native Push** section to upload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="e28bb-109">Выберите сертификат P12, отправьте его и введите пароль:</span><span class="sxs-lookup"><span data-stu-id="e28bb-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="e28bb-110"><a id="send"></a>Отправка уведомления в приложение</span><span class="sxs-lookup"><span data-stu-id="e28bb-110"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="e28bb-111">Создадим простую кампанию push-уведомлений, которая отправит push-уведомление в приложение.</span><span class="sxs-lookup"><span data-stu-id="e28bb-111">We will now create a simple Push Notification campaign that will send a push to our app:</span></span>

1. <span data-ttu-id="e28bb-112">Перейдите на вкладку **Рекламная кампания** на портале Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e28bb-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="e28bb-113">Щелкните **Создать объявление** , чтобы создать кампанию push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e28bb-113">Click **New Announcement** to create your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="e28bb-114">Настройте первые поля кампании:</span><span class="sxs-lookup"><span data-stu-id="e28bb-114">Setup the first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="e28bb-115">Задайте **имя** кампании.</span><span class="sxs-lookup"><span data-stu-id="e28bb-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="e28bb-116">Выберите **Время доставки** **Только вне приложения** — это простой тип push-уведомлений Apple с произвольным текстом.</span><span class="sxs-lookup"><span data-stu-id="e28bb-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="e28bb-117">В тексте уведомления введите сначала **заголовок** в первой строке push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="e28bb-117">In the notification text, type first the **Title** which will be the first line in the push.</span></span>
   * <span data-ttu-id="e28bb-118">Затем введите **сообщение** во второй строке.</span><span class="sxs-lookup"><span data-stu-id="e28bb-118">Then type your **Message** which will be the second line</span></span>
4. <span data-ttu-id="e28bb-119">Прокрутите окно вниз и в разделе содержимого выберите пункт **Только уведомления**</span><span class="sxs-lookup"><span data-stu-id="e28bb-119">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="e28bb-120">Вы настроили простейшую кампанию.</span><span class="sxs-lookup"><span data-stu-id="e28bb-120">You're done setting the most basic campaign.</span></span> <span data-ttu-id="e28bb-121">Теперь прокрутите окно вниз и нажмите кнопку **Создать** , чтобы сохранить push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e28bb-121">Now scroll down and click on **Create** button to save your push notification campaign.</span></span> 
6. <span data-ttu-id="e28bb-122">Наконец, щелкните **Активировать** , чтобы отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="e28bb-122">Finally - click on **Activate** to send push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="e28bb-123">Вы сможете получить уведомление на устройстве iOS в центре уведомлений следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e28bb-123">You will be able receive the notification on your iOS device in the notification center like the following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="e28bb-124">Если с вашим устройством iOS связаны часы Apple Watch, уведомление на отображается на Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="e28bb-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

