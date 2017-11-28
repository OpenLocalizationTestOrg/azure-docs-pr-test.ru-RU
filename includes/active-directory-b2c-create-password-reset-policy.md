<span data-ttu-id="ff8ce-101">Чтобы обеспечить детально настроенный сброс паролей для приложения, необходимо создать политику сброса паролей.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="ff8ce-102">Обратите внимание на возможность сброса паролей в рамках клиента, описанную [здесь](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="ff8ce-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="ff8ce-103">Эта политика описывает действия, которые необходимо выполнить потребителям для сброса пароля, и содержимое маркеров, которые должно получить приложение при успешном изменении.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="ff8ce-104">В разделе параметров политики выберите **Политики сброса пароля** и нажмите кнопку **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Выберите политики регистрации или входа и нажмите кнопку "Добавить".](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="ff8ce-106">Введите **имя** политики, на которое будет ссылаться приложение.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="ff8ce-107">Например, введите `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="ff8ce-108">Щелкните **Поставщики удостоверений** и выберите **сброс пароля с помощью электронного адреса**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="ff8ce-109">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-109">Click **OK**.</span></span>

![В разделе "Поставщики удостоверений" выберите сброс пароля с помощью электронного адреса и нажмите кнопку "ОК".](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="ff8ce-111">Выберите элемент **Утверждения приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-111">Select **Application claims**.</span></span> <span data-ttu-id="ff8ce-112">Выберите утверждения, которые необходимо возвращать в маркерах проверки подлинности, отправляемых приложению после успешного сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="ff8ce-113">Например, выберите **ИД объекта пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-113">For example, select **User's Object ID**.</span></span>

![Выбор нескольких утверждений приложения и нажатие кнопки "ОК"](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="ff8ce-115">Нажмите кнопку **Создать**, чтобы добавить политику.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="ff8ce-116">Отобразится политика с именем **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="ff8ce-117">**B2C_1_** — это префикс, добавленный к имени.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="ff8ce-118">Откройте политику, выбрав **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="ff8ce-119">Просмотрите параметры, указанные в таблице, и щелкните **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-119">Verify the settings specified in the table then click **Run now**.</span></span>

![Выбор и запуск политики](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="ff8ce-121">Настройка</span><span class="sxs-lookup"><span data-stu-id="ff8ce-121">Setting</span></span>      | <span data-ttu-id="ff8ce-122">Значение</span><span class="sxs-lookup"><span data-stu-id="ff8ce-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="ff8ce-123">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="ff8ce-123">**Applications**</span></span> | <span data-ttu-id="ff8ce-124">Приложение Contoso B2C</span><span class="sxs-lookup"><span data-stu-id="ff8ce-124">Contoso B2C app</span></span> |
| <span data-ttu-id="ff8ce-125">**Выбор URL-адреса ответа**</span><span class="sxs-lookup"><span data-stu-id="ff8ce-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="ff8ce-126">Откроется новая вкладка браузера, и вы сможете просмотреть процесс сброса пароля в приложении глазами пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ff8ce-127">Создание, обновление и вступление политики в силу занимает около минуты.</span><span class="sxs-lookup"><span data-stu-id="ff8ce-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
