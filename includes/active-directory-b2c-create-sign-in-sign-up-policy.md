<span data-ttu-id="ec0ed-101">Чтобы добавить функцию входа в приложение, необходимо создать политику входа.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-101">To enable sign-in on your application, you will need to create a sign-in policy.</span></span> <span data-ttu-id="ec0ed-102">Эта политика описывает действия, которые пользователь должен выполнить во время входа, и содержимое маркеров, которые должно получить приложение при успешном входе.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-102">This policy describes the experiences that consumers will go through during sign-in and the contents of tokens that the application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="ec0ed-103">В разделе параметров политики выберите **Политики регистрации или входа** и нажмите кнопку **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-103">In the policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Выберите политики регистрации или входа и нажмите кнопку "Добавить".](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="ec0ed-105">Введите **имя** политики, на которое будет ссылаться приложение.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="ec0ed-106">Например, введите `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="ec0ed-107">Щелкните **Поставщики удостоверений** и выберите **Регистрация по электронной почте**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="ec0ed-108">При необходимости можно также выбрать поставщиков удостоверений в социальных сетях, если они уже настроены.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="ec0ed-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-109">Click **OK**.</span></span>

![Выберите регистрацию по электронной почте в разделе "Поставщики удостоверений" и нажмите кнопку "ОК".](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="ec0ed-111">Выберите элемент **Атрибуты регистрации**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="ec0ed-112">Выберите атрибуты, которые пользователь должен предоставить во время регистрации.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-112">Choose attributes you want to collect from the consumer during sign-up.</span></span> <span data-ttu-id="ec0ed-113">Например, выберите **Страна или регион**, **Отображаемое имя** и **Почтовый индекс**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="ec0ed-114">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-114">Click **OK**.</span></span>

![Выбор нескольких атрибутов и нажатие кнопки "ОК"](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="ec0ed-116">Выберите элемент **Утверждения приложения**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-116">Select **Application claims**.</span></span> <span data-ttu-id="ec0ed-117">Выберите утверждения, которые необходимо возвращать в токенах проверки подлинности, отправляемых приложению после успешной регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="ec0ed-118">Например, выберите **Отображаемое имя**, **Поставщик удостоверений**, **Почтовый индекс**, **User is new** (Новый пользователь) и **ИД объекта пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Выбор нескольких утверждений приложения и нажатие кнопки "ОК"](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="ec0ed-120">Нажмите кнопку **Создать**, чтобы добавить политику.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="ec0ed-121">Отобразится политика с именем **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-121">The policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="ec0ed-122">**B2C_1_** — это префикс, добавленный к имени.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="ec0ed-123">Откройте политику, выбрав **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-123">Open the policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="ec0ed-124">Просмотрите параметры, указанные в таблице, и щелкните **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Выбор и запуск политики](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="ec0ed-126">Настройка</span><span class="sxs-lookup"><span data-stu-id="ec0ed-126">Setting</span></span>      | <span data-ttu-id="ec0ed-127">Значение</span><span class="sxs-lookup"><span data-stu-id="ec0ed-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="ec0ed-128">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="ec0ed-128">**Applications**</span></span> | <span data-ttu-id="ec0ed-129">Приложение Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="ec0ed-129">Contoso B2C app</span></span> |
| <span data-ttu-id="ec0ed-130">**Выбор URL-адреса ответа**</span><span class="sxs-lookup"><span data-stu-id="ec0ed-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="ec0ed-131">Откроется новая вкладка браузера, и вы сможете взглянуть на процесс регистрации или входа глазами пользователя.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-131">A new browser tab opens, and you can verify the sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="ec0ed-132">Создание, обновление и вступление политики в силу занимает около минуты.</span><span class="sxs-lookup"><span data-stu-id="ec0ed-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>