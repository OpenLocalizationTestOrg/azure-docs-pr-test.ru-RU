### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="97a1b-101">Предоставление мобильного охвата доступа tooyour ключ API GCM</span><span class="sxs-lookup"><span data-stu-id="97a1b-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="97a1b-102">tooallow мобильного охвата toosend push-уведомления от вашего имени, необходимо toogrant ему получить доступ к tooyour ключ API.</span><span class="sxs-lookup"><span data-stu-id="97a1b-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="97a1b-103">Это делается путем настройки и ввода ключа на портал мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="97a1b-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="97a1b-104">Классический портал Azure, убедитесь в приложение hello мы используем для этого проекта и нажмите кнопку hello **Владейте** кнопку в нижней части hello:</span><span class="sxs-lookup"><span data-stu-id="97a1b-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="97a1b-105">Нажмите кнопку hello **параметры** -> **системные Push-уведомления** статьи tooenter ключ GCM:</span><span class="sxs-lookup"><span data-stu-id="97a1b-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="97a1b-106">Нажмите кнопку hello **изменить** значок перед **ключ API** в hello **параметры GCM** статьи, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="97a1b-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="97a1b-107">Во всплывающем hello вставьте hello ключ GCM сервера получен до и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97a1b-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="97a1b-108"><a id="send"></a>Отправить уведомление о tooyour приложение</span><span class="sxs-lookup"><span data-stu-id="97a1b-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="97a1b-109">Теперь мы создадим простой принудительной уведомления кампанию, которая отправляет приложении tooour уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="97a1b-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="97a1b-110">Перейдите toohello **ДОСТИЧЬ** вкладка на портале мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="97a1b-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="97a1b-111">Нажмите кнопку **новое извещение** toocreate кампанию push уведомления.</span><span class="sxs-lookup"><span data-stu-id="97a1b-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="97a1b-112">Настройка первого поля hello кампании через hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="97a1b-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="97a1b-113">а.</span><span class="sxs-lookup"><span data-stu-id="97a1b-113">a.</span></span> <span data-ttu-id="97a1b-114">Присвойте имя кампании.</span><span class="sxs-lookup"><span data-stu-id="97a1b-114">Name your campaign.</span></span>
   
    <span data-ttu-id="97a1b-115">b.</span><span class="sxs-lookup"><span data-stu-id="97a1b-115">b.</span></span> <span data-ttu-id="97a1b-116">Выберите hello **тип доставки** как *Системное уведомление -> простой*: это hello простой Android типу push-уведомлений, заголовок и небольших строки текста.</span><span class="sxs-lookup"><span data-stu-id="97a1b-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="97a1b-117">c.</span><span class="sxs-lookup"><span data-stu-id="97a1b-117">c.</span></span> <span data-ttu-id="97a1b-118">Выберите **время доставки** как *любое время* tooallow hello приложения tooreceive уведомление ли запускается приложение hello, или нет.</span><span class="sxs-lookup"><span data-stu-id="97a1b-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="97a1b-119">d.</span><span class="sxs-lookup"><span data-stu-id="97a1b-119">d.</span></span> <span data-ttu-id="97a1b-120">В текст типа hello уведомления hello **заголовок** которой будут находиться в полужирным шрифтом в принудительной hello.</span><span class="sxs-lookup"><span data-stu-id="97a1b-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="97a1b-121">д.</span><span class="sxs-lookup"><span data-stu-id="97a1b-121">e.</span></span> <span data-ttu-id="97a1b-122">Затем введите текст **сообщения**</span><span class="sxs-lookup"><span data-stu-id="97a1b-122">Then type your **Message**</span></span>
4. <span data-ttu-id="97a1b-123">Прокрутите список вниз и в hello **содержимого** выберите **только уведомления**.</span><span class="sxs-lookup"><span data-stu-id="97a1b-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="97a1b-124">Возможные основные кампании параметр hello, процедура завершена.</span><span class="sxs-lookup"><span data-stu-id="97a1b-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="97a1b-125">Теперь прокрутите список вниз и нажмите hello **создать** кнопку toosave кампанию.</span><span class="sxs-lookup"><span data-stu-id="97a1b-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="97a1b-126">Последний шаг: щелкните **активировать** tooactivate вашей кампании toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="97a1b-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

