<span data-ttu-id="44cf4-101">Чтобы добавить в приложение возможность изменения профиля, необходимо создать политику изменения профиля.</span><span class="sxs-lookup"><span data-stu-id="44cf4-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="44cf4-102">Эта политика описывает действия, которые необходимо выполнить пользователю для изменения профиля, и содержимое маркеров, которые должно получить приложение при успешном изменении.</span><span class="sxs-lookup"><span data-stu-id="44cf4-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="44cf4-103">В разделе параметров политики выберите **Политики редактирования профиля** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Выбор параметра "Политики редактирования профиля" и нажатие кнопки "Добавить"](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="44cf4-105">Введите **имя** политики, на которое будет ссылаться приложение.</span><span class="sxs-lookup"><span data-stu-id="44cf4-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="44cf4-106">Например, введите `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="44cf4-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="44cf4-107">Выберите **Поставщики удостоверений** и установите флажок **Локальная учетная запись для входа**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="44cf4-108">При необходимости можно также выбрать поставщиков удостоверений в социальных сетях, если они уже настроены.</span><span class="sxs-lookup"><span data-stu-id="44cf4-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="44cf4-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-109">Click **OK**.</span></span>

![Выбор локальной учетной записи для входа в качестве поставщика удостоверений и нажатие кнопки "ОК"](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="44cf4-111">Выберите элемент **Атрибуты профиля**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-111">Select **Profile attributes**.</span></span> <span data-ttu-id="44cf4-112">Выберите атрибуты, которые пользователь сможет просматривать и изменять в своем профиле.</span><span class="sxs-lookup"><span data-stu-id="44cf4-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="44cf4-113">Например, выберите **Страна или регион**, **Отображаемое имя** и **Почтовый индекс**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="44cf4-114">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-114">Click **OK**.</span></span>

![Выбор нескольких атрибутов и нажатие кнопки "ОК"](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="44cf4-116">Выберите элемент **Утверждения приложения**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-116">Select **Application claims**.</span></span> <span data-ttu-id="44cf4-117">Затем выберите утверждения, которые необходимо возвращать в маркерах авторизации, отправляемых приложению после успешного изменения профиля.</span><span class="sxs-lookup"><span data-stu-id="44cf4-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="44cf4-118">Например, это могут быть **Отображаемое имя** и **Почтовый индекс**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Выбор нескольких утверждений приложения и нажатие кнопки "ОК"](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="44cf4-120">Нажмите кнопку **Создать**, чтобы добавить политику.</span><span class="sxs-lookup"><span data-stu-id="44cf4-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="44cf4-121">Отобразится политика с именем **B2C_1_SiPe**, где</span><span class="sxs-lookup"><span data-stu-id="44cf4-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="44cf4-122">**B2C_1_** — это префикс, добавленный к имени.</span><span class="sxs-lookup"><span data-stu-id="44cf4-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="44cf4-123">Откройте политику, выбрав **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="44cf4-124">Просмотрите параметры, указанные в таблице, и щелкните **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="44cf4-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Выбор и запуск политики](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="44cf4-126">Настройка</span><span class="sxs-lookup"><span data-stu-id="44cf4-126">Setting</span></span>      | <span data-ttu-id="44cf4-127">Значение</span><span class="sxs-lookup"><span data-stu-id="44cf4-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="44cf4-128">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="44cf4-128">**Applications**</span></span> | <span data-ttu-id="44cf4-129">Приложение Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="44cf4-129">Contoso B2C app</span></span> |
| <span data-ttu-id="44cf4-130">**Выбор URL-адреса ответа**</span><span class="sxs-lookup"><span data-stu-id="44cf4-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="44cf4-131">Откроется новая вкладка браузера, и вы сможете взглянуть на процесс изменения профиля глазами пользователя согласно заданным параметрам.</span><span class="sxs-lookup"><span data-stu-id="44cf4-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="44cf4-132">Создание, обновление и вступление политики в силу занимает около минуты.</span><span class="sxs-lookup"><span data-stu-id="44cf4-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>