<span data-ttu-id="17687-101">детально регулируемые пароли tooenable сбросить на работу приложения, необходимо будет toocreate политика сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="17687-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="17687-102">Обратите внимание, что hello масштабах клиента сброса пароля указан параметр [здесь](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="17687-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="17687-103">Эта политика описывает взаимодействия hello, потребители hello проходит через во время сброса пароля и получит содержимое hello маркеров, которые приложение hello при успешном завершении.</span><span class="sxs-lookup"><span data-stu-id="17687-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="17687-104">В разделе политик hello параметры, выберите **политики сброса паролей** и нажмите кнопку **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="17687-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Выбор политики регистрации или входа и нажмите кнопку Добавить hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="17687-106">Введите политику **имя** для tooreference вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="17687-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="17687-107">Например, введите `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="17687-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="17687-108">Щелкните **Поставщики удостоверений** и выберите **сброс пароля с помощью электронного адреса**.</span><span class="sxs-lookup"><span data-stu-id="17687-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="17687-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17687-109">Click **OK**.</span></span>

![Выберите пароль сброшен, используя адрес электронной почты в качестве поставщика удостоверений и нажмите кнопку ОК hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="17687-111">Выберите элемент **Утверждения приложения**.</span><span class="sxs-lookup"><span data-stu-id="17687-111">Select **Application claims**.</span></span> <span data-ttu-id="17687-112">Выберите утверждения, которые должны возвращаться в маркерах авторизации hello отправлены назад tooyour приложения после качества для сброса пароля успешно.</span><span class="sxs-lookup"><span data-stu-id="17687-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="17687-113">Например, выберите **ИД объекта пользователя**.</span><span class="sxs-lookup"><span data-stu-id="17687-113">For example, select **User's Object ID**.</span></span>

![Выбор нескольких утверждений приложения и нажатие кнопки "ОК"](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="17687-115">Нажмите кнопку **создать** tooadd hello политики.</span><span class="sxs-lookup"><span data-stu-id="17687-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="17687-116">политика Hello обозначена как **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="17687-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="17687-117">Hello **B2C_1_** префикс — присоединенных toohello имя.</span><span class="sxs-lookup"><span data-stu-id="17687-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="17687-118">Откройте политику hello, выбрав **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="17687-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="17687-119">Проверьте параметры hello, указанные в таблице hello, а затем нажмите кнопку **запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="17687-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Выбор и запуск политики](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="17687-121">Настройка</span><span class="sxs-lookup"><span data-stu-id="17687-121">Setting</span></span>      | <span data-ttu-id="17687-122">Значение</span><span class="sxs-lookup"><span data-stu-id="17687-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="17687-123">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="17687-123">**Applications**</span></span> | <span data-ttu-id="17687-124">Приложение Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="17687-124">Contoso B2C app</span></span> |
| <span data-ttu-id="17687-125">**Выбор URL-адреса ответа**</span><span class="sxs-lookup"><span data-stu-id="17687-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="17687-126">Открывает новую вкладку браузера, и вы можете подтвердить сброс пароля hello возможности использования в приложении.</span><span class="sxs-lookup"><span data-stu-id="17687-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="17687-127">Он может занимать до минуты tooa для создания политики и обновляет tootake эффект.</span><span class="sxs-lookup"><span data-stu-id="17687-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
