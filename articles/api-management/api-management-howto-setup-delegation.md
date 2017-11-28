---
title: "Делегирование пользователю регистрации и подписки на продукт"
description: "Узнайте, как делегировать регистрации пользователей и подписки на продукты третьим лицам в службе управления API Azure."
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
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="3d880-103">Делегирование пользователю регистрации и подписки на продукт</span><span class="sxs-lookup"><span data-stu-id="3d880-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="3d880-104">Делегирование позволяет использовать ваш существующий веб-сайт для обработки входа и регистрации разработчика и подписки на продукты вместо применения встроенной функции на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="3d880-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="3d880-105">В результате этого веб-сайт будет владеть пользовательскими данными и проверять эти шаги в соответствии с вашими настройками.</span><span class="sxs-lookup"><span data-stu-id="3d880-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="3d880-106"><a name="delegate-signin-up"> </a>Делегирование входа и регистрации разработчика</span><span class="sxs-lookup"><span data-stu-id="3d880-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="3d880-107">Для делегирования входа и регистрации разработчика на существующем веб-сайте будет нужно создавать специальную конечную точку делегирования на своем сайте, которая действует как точка входа для любого подобного запроса, инициируемого с портала разработчика службы управления API.</span><span class="sxs-lookup"><span data-stu-id="3d880-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="3d880-108">Итоговый рабочий процесс будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="3d880-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="3d880-109">Разработчик щелкает ссылку для входа или регистрации на портале разработчика API Management</span><span class="sxs-lookup"><span data-stu-id="3d880-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="3d880-110">Браузер перенаправляется в конечную точку делегирования</span><span class="sxs-lookup"><span data-stu-id="3d880-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="3d880-111">В свою очередь, конечная точка делегирования перенаправляется или представляет интерфейс пользователя, который предлагает пользователю войти в систему или зарегистрироваться</span><span class="sxs-lookup"><span data-stu-id="3d880-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="3d880-112">При успешном выполнении данной операции пользователь перенаправляется обратно на ту страницу портала разработчика API Management, с которой он начал данный процесс</span><span class="sxs-lookup"><span data-stu-id="3d880-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="3d880-113">Сначала следует настроить службу управления API так, чтобы он направлял запросы через вашу конечную точку делегирования.</span><span class="sxs-lookup"><span data-stu-id="3d880-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="3d880-114">На портале издателя управления API щелкните **Безопасность** и перейдите на вкладку **Делегирование**.</span><span class="sxs-lookup"><span data-stu-id="3d880-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="3d880-115">Для активации параметра "Делегирование входа и регистрации" установите соответствующий флажок.</span><span class="sxs-lookup"><span data-stu-id="3d880-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Страница "Делегирование"][api-management-delegation-signin-up]

* <span data-ttu-id="3d880-117">Выберите для себя нужный URL-адрес своей специальной конечной точки делегирования и введите его в поле **URL-адрес конечной точки делегирования** .</span><span class="sxs-lookup"><span data-stu-id="3d880-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="3d880-118">В поле **Ключ проверки подлинности делегирования** введите секретный ключ, который будет использоваться для вычисления сигнатуры, благодаря которой будет можно убедиться, что запрос действительно поступает из службы управления Azure API.</span><span class="sxs-lookup"><span data-stu-id="3d880-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="3d880-119">Вы можете нажать кнопку **Создать** , и служба управления API сгенерирует для вас случайный ключ.</span><span class="sxs-lookup"><span data-stu-id="3d880-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="3d880-120">Теперь необходимо создать **конечную точку делегирования**.</span><span class="sxs-lookup"><span data-stu-id="3d880-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="3d880-121">Для этого следует выполнить несколько действий:</span><span class="sxs-lookup"><span data-stu-id="3d880-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="3d880-122">Получите запрос в следующей форме:</span><span class="sxs-lookup"><span data-stu-id="3d880-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="3d880-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="3d880-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="3d880-124">Запросите параметры для входа или регистрации:</span><span class="sxs-lookup"><span data-stu-id="3d880-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="3d880-125">**operation**: идентифицирует тип запроса на делегирование (в данном случае может быть только **SignIn**).</span><span class="sxs-lookup"><span data-stu-id="3d880-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="3d880-126">**returnUrl**: URL-адрес страницы, на которой пользователь щелкнул ссылку входа или регистрации.</span><span class="sxs-lookup"><span data-stu-id="3d880-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="3d880-127">**salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.</span><span class="sxs-lookup"><span data-stu-id="3d880-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="3d880-128">**sig**– вычисленный хэш безопасности, который будет сравниваться с вашим вычисленным хэшем.</span><span class="sxs-lookup"><span data-stu-id="3d880-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="3d880-129">Убедитесь, что запрос поступает из службы управления Azure API (это необязательный шаг, но мы настоятельно рекомендуем его выполнять для обеспечения безопасности)</span><span class="sxs-lookup"><span data-stu-id="3d880-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="3d880-130">Вычислите хэш HMAC-SHA512 строки на основе параметров запроса **returnUrl** и **salt** ([на приведенном ниже примере кода]).</span><span class="sxs-lookup"><span data-stu-id="3d880-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="3d880-131">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="3d880-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="3d880-132">Сравните вычисленный выше хэш со значением параметра запроса **sig**.</span><span class="sxs-lookup"><span data-stu-id="3d880-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="3d880-133">Если два хэша совпадают друг с другом, перейдите к следующему шагу. Если нет, отклоните запрос.</span><span class="sxs-lookup"><span data-stu-id="3d880-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="3d880-134">Убедитесь, что вы получаете запрос на вход или регистрацию: параметр запроса **operation** должен иметь значение **SignIn**.</span><span class="sxs-lookup"><span data-stu-id="3d880-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="3d880-135">Предоставление пользователю интерфейса для входа или регистрации</span><span class="sxs-lookup"><span data-stu-id="3d880-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="3d880-136">Если пользователь регистрируется, для него необходимо создать соответствующую учетную запись в API Management.</span><span class="sxs-lookup"><span data-stu-id="3d880-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="3d880-137">[Создание пользователя] с помощью интерфейса API Management REST API.</span><span class="sxs-lookup"><span data-stu-id="3d880-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="3d880-138">После этого убедитесь, что вы ввели тот же идентификатор пользователя, что и идентификатор, который указан в вашем хранилище пользователей, или идентификатор, который можно отслеживать.</span><span class="sxs-lookup"><span data-stu-id="3d880-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="3d880-139">После успешной проверки подлинности пользователя:</span><span class="sxs-lookup"><span data-stu-id="3d880-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="3d880-140">[запросите маркер единого входа (SSO)] через API Management REST API</span><span class="sxs-lookup"><span data-stu-id="3d880-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="3d880-141">добавьте параметр запроса returnUrl в URL-адреса SSO, который вы получили из вызова API, указанного выше:</span><span class="sxs-lookup"><span data-stu-id="3d880-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="3d880-142">например, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="3d880-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="3d880-143">перенаправьте пользователя на вышеупомянутый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="3d880-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="3d880-144">Помимо использования операции **SignIn** , вы можете управлять учетными записями, выполнив указанные выше действия и одну из следующих операций.</span><span class="sxs-lookup"><span data-stu-id="3d880-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="3d880-145">**ChangePassword;**</span><span class="sxs-lookup"><span data-stu-id="3d880-145">**ChangePassword**</span></span>
* <span data-ttu-id="3d880-146">**ChangeProfile;**</span><span class="sxs-lookup"><span data-stu-id="3d880-146">**ChangeProfile**</span></span>
* <span data-ttu-id="3d880-147">**CloseAccount.**</span><span class="sxs-lookup"><span data-stu-id="3d880-147">**CloseAccount**</span></span>

<span data-ttu-id="3d880-148">Для операций управления учетными записями необходимо передать следующие параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="3d880-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="3d880-149">**operation**– определяет тип запроса на делегирование (ChangePassword, ChangeProfile или CloseAccount).</span><span class="sxs-lookup"><span data-stu-id="3d880-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="3d880-150">**userId**– идентификатор пользователя учетной записи для управления.</span><span class="sxs-lookup"><span data-stu-id="3d880-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="3d880-151">**salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.</span><span class="sxs-lookup"><span data-stu-id="3d880-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="3d880-152">**sig**– вычисленный хэш безопасности, который будет сравниваться с вашим вычисленным хэшем.</span><span class="sxs-lookup"><span data-stu-id="3d880-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="3d880-153"><a name="delegate-product-subscription"> </a>Делегирование подписки на продукт</span><span class="sxs-lookup"><span data-stu-id="3d880-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="3d880-154">Процедура делегирования подписки на продукт похожа на процедуру делегирования входа или регистрации пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d880-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="3d880-155">Итоговый рабочий процесс будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="3d880-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="3d880-156">Разработчик выбирает продукт на портале разработчика API Management и щелкает кнопку "Подписка"</span><span class="sxs-lookup"><span data-stu-id="3d880-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="3d880-157">Браузер перенаправляется в конечную точку делегирования</span><span class="sxs-lookup"><span data-stu-id="3d880-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="3d880-158">Конечная точка делегирования выполняет требуемые шаги подписки на продукт. Эту процедуру выполняете вы. В нее могут входить перенаправление на другую страницу для запроса сведений о выставлении счетов, формулирование дополнительных вопросов или просто сохранение информации без выполнения действий пользователя</span><span class="sxs-lookup"><span data-stu-id="3d880-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="3d880-159">Чтобы включить функцию, на странице **Делегирование** щелкните **Делегировать подписку на продукт**.</span><span class="sxs-lookup"><span data-stu-id="3d880-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="3d880-160">Затем убедитесь, что конечная точка делегирования выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3d880-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="3d880-161">Получите запрос в следующей форме:</span><span class="sxs-lookup"><span data-stu-id="3d880-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="3d880-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="3d880-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="3d880-163">Параметры запроса для подписки на продукт:</span><span class="sxs-lookup"><span data-stu-id="3d880-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="3d880-164">**operation**: идентифицирует тип запроса на делегирование.</span><span class="sxs-lookup"><span data-stu-id="3d880-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="3d880-165">Для запросов подписки на продукт допустимыми являются следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="3d880-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="3d880-166">"Subscribe": запрос на подписку пользователя на заданный продукт с предоставленным идентификатором (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="3d880-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="3d880-167">"Unsubscribe": запрос на отказ от подписки пользователя на продукт;</span><span class="sxs-lookup"><span data-stu-id="3d880-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="3d880-168">"Renew": запрос на обновление подписки (например, в случае истечения срока действия).</span><span class="sxs-lookup"><span data-stu-id="3d880-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="3d880-169">**productId**: идентификатор продукта, подписку на который запрашивает пользователь.</span><span class="sxs-lookup"><span data-stu-id="3d880-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="3d880-170">**userId**: идентификатор пользователя, которому отправлен запрос.</span><span class="sxs-lookup"><span data-stu-id="3d880-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="3d880-171">**salt**– специальная строка случайных данных, используемая для вычисления хэша безопасности.</span><span class="sxs-lookup"><span data-stu-id="3d880-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="3d880-172">**sig**– вычисленный хэш безопасности, который будет сравниваться с вашим вычисленным хэшем.</span><span class="sxs-lookup"><span data-stu-id="3d880-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="3d880-173">Убедитесь, что запрос поступает из службы управления Azure API (это необязательный шаг, но мы настоятельно рекомендуем его выполнять для обеспечения безопасности)</span><span class="sxs-lookup"><span data-stu-id="3d880-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="3d880-174">Вычислите хэш HMAC-SHA512 строки на основании параметров запроса **productId**, **userId** и **salt**:</span><span class="sxs-lookup"><span data-stu-id="3d880-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="3d880-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="3d880-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="3d880-176">Сравните вычисленный выше хэш со значением параметра запроса **sig**.</span><span class="sxs-lookup"><span data-stu-id="3d880-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="3d880-177">Если два хэша совпадают друг с другом, перейдите к следующему шагу. Если нет, отклоните запрос.</span><span class="sxs-lookup"><span data-stu-id="3d880-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="3d880-178">Выполните обработку подписки на продукт с учетом типа операции, запрашиваемой в параметре **operation**, например, выставление счета, дополнительные вопросы и т. д.</span><span class="sxs-lookup"><span data-stu-id="3d880-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="3d880-179">В случае успешной подписки пользователя на продукт на вашей стороне подпишите пользователя на продукт службы управления API путем [вызова интерфейса REST API для подписки на продукт].</span><span class="sxs-lookup"><span data-stu-id="3d880-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="3d880-180"><a name="delegate-example-code"> </a> Пример кода</span><span class="sxs-lookup"><span data-stu-id="3d880-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="3d880-181">В этих примерах кода показано, как получить *ключ проверки делегирования*, который задается на странице делегирования портала издателя, и как создать HMAC, который затем используется для проверки подписи, подтверждающей действительность переданного returnUrl.</span><span class="sxs-lookup"><span data-stu-id="3d880-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="3d880-182">Тот же код с незначительными изменениями подходит для productId и userId.</span><span class="sxs-lookup"><span data-stu-id="3d880-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="3d880-183">**Код C# для создания хэша returnUrl**</span><span class="sxs-lookup"><span data-stu-id="3d880-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="3d880-184">**Код NodeJS для создания хэша returnUrl**</span><span class="sxs-lookup"><span data-stu-id="3d880-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="3d880-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d880-185">Next steps</span></span>
<span data-ttu-id="3d880-186">Дополнительную информацию о делегировании см. в следующем видео.</span><span class="sxs-lookup"><span data-stu-id="3d880-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="3d880-187">[запросите маркер единого входа (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="3d880-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="3d880-188">[Создание пользователя]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="3d880-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="3d880-189">[вызова интерфейса REST API для подписки на продукт]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="3d880-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="3d880-190">[на приведенном ниже примере кода]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="3d880-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
