<span data-ttu-id="83ee1-101">профиль tooenable изменения в приложения, вам потребуется toocreate изменения политики профиля.</span><span class="sxs-lookup"><span data-stu-id="83ee1-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="83ee1-102">Эта политика описывает взаимодействия hello, потребители проходит через во время профиля редактирования и hello содержимое токенов, которые будут получать приложения hello при успешном завершении.</span><span class="sxs-lookup"><span data-stu-id="83ee1-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="83ee1-103">В разделе политик hello параметры, выберите **изменения политики профиля** и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Выберите профиль, изменение политик и нажмите кнопку Добавить hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="83ee1-105">Введите политику **имя** для tooreference вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="83ee1-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="83ee1-106">Например, введите `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="83ee1-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="83ee1-107">Выберите **Поставщики удостоверений** и установите флажок **Локальная учетная запись для входа**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="83ee1-108">При необходимости можно также выбрать поставщиков удостоверений в социальных сетях, если они уже настроены.</span><span class="sxs-lookup"><span data-stu-id="83ee1-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="83ee1-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-109">Click **OK**.</span></span>

![Выберите локальный вход в учетную запись как поставщик удостоверений и нажмите кнопку ОК hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="83ee1-111">Выберите элемент **Атрибуты профиля**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-111">Select **Profile attributes**.</span></span> <span data-ttu-id="83ee1-112">Выберите атрибуты hello потребителя можно просматривать и изменять в своем профиле.</span><span class="sxs-lookup"><span data-stu-id="83ee1-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="83ee1-113">Например, выберите **Страна или регион**, **Отображаемое имя** и **Почтовый индекс**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="83ee1-114">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-114">Click **OK**.</span></span>

![Выберите некоторые атрибуты и нажмите кнопку ОК hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="83ee1-116">Выберите элемент **Утверждения приложения**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-116">Select **Application claims**.</span></span> <span data-ttu-id="83ee1-117">Выберите утверждения, которые должны возвращаться в маркерах авторизации hello отправляются назад tooyour приложения после успешного изменения профилей.</span><span class="sxs-lookup"><span data-stu-id="83ee1-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="83ee1-118">Например, это могут быть **Отображаемое имя** и **Почтовый индекс**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Выбор нескольких утверждений приложения и нажатие кнопки "ОК"](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="83ee1-120">Нажмите кнопку **создать** tooadd hello политики.</span><span class="sxs-lookup"><span data-stu-id="83ee1-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="83ee1-121">политика Hello обозначена как **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="83ee1-122">Hello **B2C_1_** префикс — присоединенных toohello имя.</span><span class="sxs-lookup"><span data-stu-id="83ee1-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="83ee1-123">Откройте политику hello, выбрав **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="83ee1-124">Проверьте параметры hello, указанные в таблице hello, а затем нажмите кнопку **запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="83ee1-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Выбор и запуск политики](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="83ee1-126">Настройка</span><span class="sxs-lookup"><span data-stu-id="83ee1-126">Setting</span></span>      | <span data-ttu-id="83ee1-127">Значение</span><span class="sxs-lookup"><span data-stu-id="83ee1-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="83ee1-128">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="83ee1-128">**Applications**</span></span> | <span data-ttu-id="83ee1-129">Приложение Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="83ee1-129">Contoso B2C app</span></span> |
| <span data-ttu-id="83ee1-130">**Выбор URL-адреса ответа**</span><span class="sxs-lookup"><span data-stu-id="83ee1-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="83ee1-131">Открывает новую вкладку браузера, и можно проверить изменения потребителя согласно настройке профилей hello.</span><span class="sxs-lookup"><span data-stu-id="83ee1-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="83ee1-132">Он может занимать до минуты tooa для создания политики и обновляет tootake эффект.</span><span class="sxs-lookup"><span data-stu-id="83ee1-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>