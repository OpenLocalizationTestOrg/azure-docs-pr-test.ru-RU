<span data-ttu-id="aca6a-101">вход tooenable на приложение, вам потребуется toocreate входа в политику.</span><span class="sxs-lookup"><span data-stu-id="aca6a-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="aca6a-102">Эта политика описывает взаимодействия hello, потребители проходит через при входе в систему и получит содержимое hello маркеров, которые приложение hello успешного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="aca6a-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="aca6a-103">В разделе политик hello параметры, выберите **политики регистрации или входа в** и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Выберите политики регистрации или входа и нажмите кнопку "Добавить".](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="aca6a-105">Введите политику **имя** для tooreference вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="aca6a-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="aca6a-106">Например, введите `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="aca6a-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="aca6a-107">Щелкните **Поставщики удостоверений** и выберите **Регистрация по электронной почте**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="aca6a-108">При необходимости можно также выбрать поставщиков удостоверений в социальных сетях, если они уже настроены.</span><span class="sxs-lookup"><span data-stu-id="aca6a-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="aca6a-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-109">Click **OK**.</span></span>

![Выберите подписки электронной почты в качестве поставщика удостоверений и нажмите кнопку ОК hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="aca6a-111">Выберите элемент **Атрибуты регистрации**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="aca6a-112">Выберите атрибуты требуется toocollect от потребителя hello во время регистрации.</span><span class="sxs-lookup"><span data-stu-id="aca6a-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="aca6a-113">Например, выберите **Страна или регион**, **Отображаемое имя** и **Почтовый индекс**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="aca6a-114">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-114">Click **OK**.</span></span>

![Выберите некоторые атрибуты и нажмите кнопку ОК hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="aca6a-116">Выберите элемент **Утверждения приложения**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-116">Select **Application claims**.</span></span> <span data-ttu-id="aca6a-117">Выберите утверждения, которые должны возвращаться в маркерах авторизации hello отправляются назад tooyour приложения после успешной регистрации или входа в качества.</span><span class="sxs-lookup"><span data-stu-id="aca6a-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="aca6a-118">Например, выберите **Отображаемое имя**, **Поставщик удостоверений**, **Почтовый индекс**, **User is new** (Новый пользователь) и **ИД объекта пользователя**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Выбор нескольких утверждений приложения и нажатие кнопки "ОК"](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="aca6a-120">Нажмите кнопку **создать** tooadd hello политики.</span><span class="sxs-lookup"><span data-stu-id="aca6a-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="aca6a-121">политика Hello обозначена как **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="aca6a-122">Hello **B2C_1_** префикс — присоединенных toohello имя.</span><span class="sxs-lookup"><span data-stu-id="aca6a-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="aca6a-123">Откройте политику hello, выбрав **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="aca6a-124">Проверьте параметры hello, указанные в таблице hello, а затем нажмите кнопку **запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="aca6a-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Выбор и запуск политики](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="aca6a-126">Настройка</span><span class="sxs-lookup"><span data-stu-id="aca6a-126">Setting</span></span>      | <span data-ttu-id="aca6a-127">Значение</span><span class="sxs-lookup"><span data-stu-id="aca6a-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="aca6a-128">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="aca6a-128">**Applications**</span></span> | <span data-ttu-id="aca6a-129">Приложение Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="aca6a-129">Contoso B2C app</span></span> |
| <span data-ttu-id="aca6a-130">**Выбор URL-адреса ответа**</span><span class="sxs-lookup"><span data-stu-id="aca6a-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="aca6a-131">Открывает новую вкладку браузера и hello регистрации или входа в возможности использования можно проверить, как настроены.</span><span class="sxs-lookup"><span data-stu-id="aca6a-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="aca6a-132">Он может занимать до минуты tooa для создания политики и обновляет tootake эффект.</span><span class="sxs-lookup"><span data-stu-id="aca6a-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>