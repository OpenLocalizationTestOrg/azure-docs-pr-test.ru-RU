---
title: "aaaHow toodelegate продукта и регистрации подписки пользователя"
description: "Узнайте, как toodelegate пользователя продукта и регистрации подписки tooa сторонних производителей в службе управления API Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="fc36d-103">Как пользователь toodelegate продукта и регистрации подписки</span><span class="sxs-lookup"><span data-stu-id="fc36d-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="fc36d-104">Делегирование позволяет toouse существующий веб-сайт для обработки разработчика tooproducts входа в-регистрации-повышение и подписки как отличие от toousing hello встроенные функциональные возможности на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="fc36d-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="fc36d-105">Это включает данные пользователей hello tooown веб-сайта и выполняет проверку hello этих шагов любым способом.</span><span class="sxs-lookup"><span data-stu-id="fc36d-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="fc36d-106"><a name="delegate-signin-up"> </a>Делегирование входа и регистрации разработчика</span><span class="sxs-lookup"><span data-stu-id="fc36d-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="fc36d-107">toodelegate разработчика tooyour входа и регистрации существующий веб-сайт на данном узле, который выступает в качестве точки входа для такого запроса, инициированный портал разработчика управления API hello hello потребуется toocreate конечную точку специальные делегирования.</span><span class="sxs-lookup"><span data-stu-id="fc36d-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="fc36d-108">Hello окончательный рабочий процесс будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fc36d-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="fc36d-109">Разработчик щелкает ссылку вход или зарегистрируйте hello в hello портал разработчика управления API</span><span class="sxs-lookup"><span data-stu-id="fc36d-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="fc36d-110">Браузер является конечной точкой перенаправленный toohello делегирования</span><span class="sxs-lookup"><span data-stu-id="fc36d-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="fc36d-111">Конечная точка делегирования взамен перенаправляет представляется tooor пользовательского интерфейса запросом пользователя в toosign или регистрации</span><span class="sxs-lookup"><span data-stu-id="fc36d-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="fc36d-112">В случае успешного выполнения пользователь hello является страница портала разработчика управления API перенаправленный задней toohello их запуска из</span><span class="sxs-lookup"><span data-stu-id="fc36d-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="fc36d-113">toobegin, давайте первый tooroute управления API настройки запросов с помощью делегирования конечной точки.</span><span class="sxs-lookup"><span data-stu-id="fc36d-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="fc36d-114">В портал издателя управления API hello, щелкните **безопасности** и нажмите кнопку hello **делегирования** вкладки. Щелкните флажок hello tooenable «Delegate вход & регистрации».</span><span class="sxs-lookup"><span data-stu-id="fc36d-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Страница "Делегирование"][api-management-delegation-signin-up]

* <span data-ttu-id="fc36d-116">Что hello URL-адрес конечной точки специальные делегирования следует и введите его в hello **URL-адрес конечной точки делегирования** поля.</span><span class="sxs-lookup"><span data-stu-id="fc36d-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="fc36d-117">В рамках hello **ключ проверки подлинности для делегирования** введите секретный код, который будет использоваться toocompute tooyou предоставленный подписи для проверки tooensure, hello запрос на самом деле поступает из API управления Azure.</span><span class="sxs-lookup"><span data-stu-id="fc36d-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="fc36d-118">Можно щелкнуть hello **создания** кнопку toohave API управления случайным образом создать ключ для вас.</span><span class="sxs-lookup"><span data-stu-id="fc36d-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="fc36d-119">Теперь необходимо toocreate hello **делегирования конечной точки**.</span><span class="sxs-lookup"><span data-stu-id="fc36d-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="fc36d-120">Он имеет tooperform ряд действий:</span><span class="sxs-lookup"><span data-stu-id="fc36d-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="fc36d-121">Получает запрос в hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="fc36d-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="fc36d-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="fc36d-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="fc36d-123">Параметры запроса для случая hello вход / регистрации:</span><span class="sxs-lookup"><span data-stu-id="fc36d-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="fc36d-124">**operation**: идентифицирует тип запроса на делегирование (в данном случае может быть только **SignIn**).</span><span class="sxs-lookup"><span data-stu-id="fc36d-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="fc36d-125">**returnUrl**: hello URL-адрес страницы приветствия, где hello нажатия на вход или зарегистрируйте ссылку</span><span class="sxs-lookup"><span data-stu-id="fc36d-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="fc36d-126">**salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.</span><span class="sxs-lookup"><span data-stu-id="fc36d-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="fc36d-127">**SIG**: toobe хэш вычисляемый безопасности, используемый для сравнения tooyour собственные вычисленный хэш</span><span class="sxs-lookup"><span data-stu-id="fc36d-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="fc36d-128">Убедитесь, что этот запрос hello поступает от службы управления API Azure (необязательно, но настоятельно рекомендуется для обеспечения безопасности)</span><span class="sxs-lookup"><span data-stu-id="fc36d-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="fc36d-129">Вычислить хэш-код HMAC-SHA512 из строки с учетом hello **returnUrl** и **соли** параметров запроса ([приведенном ниже примере кода]):</span><span class="sxs-lookup"><span data-stu-id="fc36d-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="fc36d-130">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="fc36d-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="fc36d-131">Сравнить значение toohello выше вычисляемый хэш hello hello **sig** параметр запроса.</span><span class="sxs-lookup"><span data-stu-id="fc36d-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="fc36d-132">Если hello хэши совпадают, переместите на следующем шаге toohello, в противном случае отклонить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="fc36d-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="fc36d-133">Убедитесь, что вы получили запрос для входа в/sign up: hello **операции** параметра запроса устанавливается слишком»**SignIn**».</span><span class="sxs-lookup"><span data-stu-id="fc36d-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="fc36d-134">Текущего пользователя hello с пользовательским Интерфейсом в toosign или регистрации</span><span class="sxs-lookup"><span data-stu-id="fc36d-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="fc36d-135">Если пользователь hello регистрацию вы должны toocreate соответствующая учетная запись для них в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="fc36d-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="fc36d-136">[Создайте учетную запись пользователя] с hello API REST управления API.</span><span class="sxs-lookup"><span data-stu-id="fc36d-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="fc36d-137">При этом убедиться, что toohello идентификатор пользователя hello идентификатор tooan, вы можете хранить список или же она находится в хранилище пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc36d-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="fc36d-138">При успешной аутентификации пользователя hello:</span><span class="sxs-lookup"><span data-stu-id="fc36d-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="fc36d-139">[запрос токена единый вход (SSO)] через API REST управления hello</span><span class="sxs-lookup"><span data-stu-id="fc36d-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="fc36d-140">Добавьте toohello параметр запроса returnUrl URL-адрес единого входа, полученные от hello API вызовов выше:</span><span class="sxs-lookup"><span data-stu-id="fc36d-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="fc36d-141">например, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="fc36d-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="fc36d-142">перенаправление hello пользователя toohello выше создаются URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fc36d-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="fc36d-143">В дополнение toohello **SignIn** операции, может выполнять управление учетными записями, следуя hello предыдущие шаги и с помощью одного из следующих операций hello.</span><span class="sxs-lookup"><span data-stu-id="fc36d-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="fc36d-144">**ChangePassword;**</span><span class="sxs-lookup"><span data-stu-id="fc36d-144">**ChangePassword**</span></span>
* <span data-ttu-id="fc36d-145">**ChangeProfile;**</span><span class="sxs-lookup"><span data-stu-id="fc36d-145">**ChangeProfile**</span></span>
* <span data-ttu-id="fc36d-146">**CloseAccount.**</span><span class="sxs-lookup"><span data-stu-id="fc36d-146">**CloseAccount**</span></span>

<span data-ttu-id="fc36d-147">Необходимо передать hello следующие параметры запроса для операций управления учетными записями.</span><span class="sxs-lookup"><span data-stu-id="fc36d-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="fc36d-148">**operation**– определяет тип запроса на делегирование (ChangePassword, ChangeProfile или CloseAccount).</span><span class="sxs-lookup"><span data-stu-id="fc36d-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="fc36d-149">**userId**: hello идентификатор пользователя для учетной записи toomanage hello</span><span class="sxs-lookup"><span data-stu-id="fc36d-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="fc36d-150">**salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.</span><span class="sxs-lookup"><span data-stu-id="fc36d-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="fc36d-151">**SIG**: toobe хэш вычисляемый безопасности, используемый для сравнения tooyour собственные вычисленный хэш</span><span class="sxs-lookup"><span data-stu-id="fc36d-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="fc36d-152"><a name="delegate-product-subscription"> </a>Делегирование подписки на продукт</span><span class="sxs-lookup"><span data-stu-id="fc36d-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="fc36d-153">Делегирование подписки для продукта работают схожим образом toodelegating пользователя вход и доступ.</span><span class="sxs-lookup"><span data-stu-id="fc36d-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="fc36d-154">Hello окончательный рабочий процесс будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fc36d-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="fc36d-155">Разработчик выбирает продукт в портал разработчика управления API hello и нажимает кнопку Subscribe hello</span><span class="sxs-lookup"><span data-stu-id="fc36d-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="fc36d-156">Браузер является конечной точкой перенаправленный toohello делегирования</span><span class="sxs-lookup"><span data-stu-id="fc36d-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="fc36d-157">Делегирование конечная точка выполняет действия подписки продукта — это копирование tooyou, возможно, придется перенаправление страницы toorequest tooanother информацией о выставлении счетов, задавать дополнительные вопросы или просто хранение сведений о hello и не требует вмешательства пользователя</span><span class="sxs-lookup"><span data-stu-id="fc36d-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="fc36d-158">функциональные возможности hello tooenable на hello **делегирования** щелкните **делегировать подписки для продукта**.</span><span class="sxs-lookup"><span data-stu-id="fc36d-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="fc36d-159">Убедитесь, что конечная точка делегирования hello выполняет hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fc36d-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="fc36d-160">Получает запрос в hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="fc36d-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="fc36d-161">*{операция} HTTP://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe продукта для} & userId = {пользователя, выполняющего запрос} & соли = {строка} & sig = {строка}*</span><span class="sxs-lookup"><span data-stu-id="fc36d-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="fc36d-162">Параметры запроса для случая подписки hello продукта:</span><span class="sxs-lookup"><span data-stu-id="fc36d-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="fc36d-163">**operation**: идентифицирует тип запроса на делегирование.</span><span class="sxs-lookup"><span data-stu-id="fc36d-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="fc36d-164">Для подписки для продукта запросы hello допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="fc36d-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="fc36d-165">«Подписаться»: запрос toosubscribe hello пользователя tooa продукт с учетом предоставленный идентификатор (см. ниже)</span><span class="sxs-lookup"><span data-stu-id="fc36d-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="fc36d-166">«Отменить подписку»: toounsubscribe запрос пользователя из продукта</span><span class="sxs-lookup"><span data-stu-id="fc36d-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="fc36d-167">«Обновить»: которое toorenew подписки (например, может истечение срока действия)</span><span class="sxs-lookup"><span data-stu-id="fc36d-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="fc36d-168">**productId**: hello идентификатор пользователя hello hello запрошенный toosubscribe для</span><span class="sxs-lookup"><span data-stu-id="fc36d-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="fc36d-169">**userId**: hello идентификатор hello пользователя, для которого производится hello</span><span class="sxs-lookup"><span data-stu-id="fc36d-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="fc36d-170">**salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.</span><span class="sxs-lookup"><span data-stu-id="fc36d-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="fc36d-171">**SIG**: toobe хэш вычисляемый безопасности, используемый для сравнения tooyour собственные вычисленный хэш</span><span class="sxs-lookup"><span data-stu-id="fc36d-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="fc36d-172">Убедитесь, что этот запрос hello поступает от службы управления API Azure (необязательно, но настоятельно рекомендуется для обеспечения безопасности)</span><span class="sxs-lookup"><span data-stu-id="fc36d-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="fc36d-173">Вычисления HMAC-SHA512 строки с учетом hello **productId**, **userId** и **соли** параметры запроса:</span><span class="sxs-lookup"><span data-stu-id="fc36d-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="fc36d-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="fc36d-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="fc36d-175">Сравнить значение toohello выше вычисляемый хэш hello hello **sig** параметр запроса.</span><span class="sxs-lookup"><span data-stu-id="fc36d-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="fc36d-176">Если hello хэши совпадают, переместите на следующем шаге toohello, в противном случае отклонить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="fc36d-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="fc36d-177">Выполнить обработку подписки продукта на основе типа hello в запрошенной операции **операции** -например выставление счетов, дополнительные вопросы, и т. д.</span><span class="sxs-lookup"><span data-stu-id="fc36d-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="fc36d-178">На успешно подписка hello пользователя toohello продукта с вашей стороны, подписаться продуктов для управления API toohello hello пользователя по [hello вызовах API-интерфейса REST для подписки для продукта].</span><span class="sxs-lookup"><span data-stu-id="fc36d-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="fc36d-179"><a name="delegate-example-code"> </a> Пример кода</span><span class="sxs-lookup"><span data-stu-id="fc36d-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="fc36d-180">Эти образцы Показать кода как tootake hello *ключ проверки делегирования*, какой набор экране делегирования hello портала издателя hello, toocreate HMAC, которое затем используется toovalidate hello подпись подтверждает действительность hello hello Переданный returnUrl.</span><span class="sxs-lookup"><span data-stu-id="fc36d-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="fc36d-181">Здравствуйте, одинаковый код работает для hello productId и userId с незначительными изменениями.</span><span class="sxs-lookup"><span data-stu-id="fc36d-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="fc36d-182">**C# кода toogenerate хэш returnUrl**</span><span class="sxs-lookup"><span data-stu-id="fc36d-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="fc36d-183">**NodeJS код toogenerate хэш returnUrl**</span><span class="sxs-lookup"><span data-stu-id="fc36d-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="fc36d-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc36d-184">Next steps</span></span>
<span data-ttu-id="fc36d-185">Дополнительные сведения о делегировании см. следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="fc36d-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[запрос токена единый вход (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[Создание пользователя]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello вызовах API-интерфейса REST для подписки для продукта]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[приведенном ниже примере кода]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
