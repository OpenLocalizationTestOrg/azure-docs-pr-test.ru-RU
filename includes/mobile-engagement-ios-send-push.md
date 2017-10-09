### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="f2732-101">Предоставление доступа tooyour Push-сертификатов tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f2732-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="f2732-102">tooallow мобильного охвата toosend Push-уведомления от вашего имени, необходимо его доступ к сертификату tooyour toogrant.</span><span class="sxs-lookup"><span data-stu-id="f2732-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="f2732-103">Это делается путем настройки и введя свой сертификат в портал мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="f2732-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="f2732-104">Убедитесь, что получили сертификат P12, как описано в [документации Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="f2732-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="f2732-105">Перейдите tooyour порталу мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="f2732-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="f2732-106">Убедитесь в правильный hello и выберите команду hello **Владейте** кнопку в нижней части hello:</span><span class="sxs-lookup"><span data-stu-id="f2732-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="f2732-107">Щелкните hello **параметры** странице портала обязательств.</span><span class="sxs-lookup"><span data-stu-id="f2732-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="f2732-108">Из отсутствует щелкните hello **системные Push-уведомления** статьи tooupload сертификата p12:</span><span class="sxs-lookup"><span data-stu-id="f2732-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="f2732-109">Выберите сертификат P12, отправьте его и введите пароль:</span><span class="sxs-lookup"><span data-stu-id="f2732-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="f2732-110"><a id="send"></a>Отправить уведомление о tooyour приложение</span><span class="sxs-lookup"><span data-stu-id="f2732-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="f2732-111">Теперь мы создадим простой кампании Push-уведомление, будет отправлять push tooour приложения:</span><span class="sxs-lookup"><span data-stu-id="f2732-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="f2732-112">Перейдите toohello **достичь** вкладка на портале мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="f2732-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="f2732-113">Нажмите кнопку **новое извещение** toocreate кампании push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="f2732-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="f2732-114">Hello первого поля кампании настройки:</span><span class="sxs-lookup"><span data-stu-id="f2732-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="f2732-115">Задайте **имя** кампании.</span><span class="sxs-lookup"><span data-stu-id="f2732-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="f2732-116">Выберите hello **время доставки** как **только вне приложения**: это hello простой Apple типу push-уведомлений, предоставляющем некоторый текст.</span><span class="sxs-lookup"><span data-stu-id="f2732-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="f2732-117">В текст уведомления hello, введите первый hello **заголовок** которого будет первая строка hello в отправке hello.</span><span class="sxs-lookup"><span data-stu-id="f2732-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="f2732-118">Затем введите ваш **сообщение** которого будет вторую строку hello</span><span class="sxs-lookup"><span data-stu-id="f2732-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="f2732-119">Прокрутите вниз и выберите раздел содержимого hello **только уведомления**</span><span class="sxs-lookup"><span data-stu-id="f2732-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="f2732-120">Параметр hello основные кампании, процедура завершена.</span><span class="sxs-lookup"><span data-stu-id="f2732-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="f2732-121">Теперь прокрутите список вниз и выберите команду **создать** кнопку toosave кампанию push уведомления.</span><span class="sxs-lookup"><span data-stu-id="f2732-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="f2732-122">И наконец — щелкнуть **активировать** toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f2732-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="f2732-123">Вы сможете получать уведомления hello на устройства iOS в центре уведомлений hello hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f2732-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="f2732-124">При наличии Apple Watch, связан с этим устройством iOS затем откроется hello уведомление на ваш Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="f2732-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

