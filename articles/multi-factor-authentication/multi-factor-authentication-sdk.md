---
title: "пакет средств разработки программного обеспечения aaaMFA для пользовательских приложений | Документы Microsoft"
description: "В этой статье показано, как toodownload и использование hello Azure SDK многофакторной проверки Подлинности tooenable двухшаговую проверку для пользовательских приложений."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="4d13a-103">Построение Multi-Factor Authentication в пользовательских приложениях (SDK)</span><span class="sxs-lookup"><span data-stu-id="4d13a-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="4d13a-104">Hello Azure многофакторной проверки подлинности Software Development Kit (SDK) предназначена для создания двухшаговую проверку непосредственно в hello входа или транзакции обрабатывает приложений в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d13a-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="4d13a-105">Hello SDK многофакторной проверки подлинности доступна для C#, Visual Basic (.NET), Java, Perl, PHP и Ruby.</span><span class="sxs-lookup"><span data-stu-id="4d13a-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="4d13a-106">Hello SDK предоставляет тонкую оболочку вокруг двухшаговую проверку.</span><span class="sxs-lookup"><span data-stu-id="4d13a-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="4d13a-107">Он включает все необходимые toowrite кода, включая файлы с комментариями исходным кодом, файлы примеров и подробный файл ReadMe.</span><span class="sxs-lookup"><span data-stu-id="4d13a-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="4d13a-108">Каждый пакет SDK также включает сертификат и закрытый ключ для шифрования транзакций, которые являются уникальными tooyour поставщика многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d13a-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="4d13a-109">При условии, что после создания поставщика можно загрузить hello SDK на столько языках и форматах необходимое.</span><span class="sxs-lookup"><span data-stu-id="4d13a-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="4d13a-110">Структура Hello hello API-интерфейсы в hello SDK многофакторной проверки подлинности проста.</span><span class="sxs-lookup"><span data-stu-id="4d13a-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="4d13a-111">Убедитесь в одной функции вызова API tooan с параметрами варианта многофакторной hello (как режим верификации) и пользовательские данные (например hello телефонных номеров toocall или номера toovalidate hello ПИН-код).</span><span class="sxs-lookup"><span data-stu-id="4d13a-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="4d13a-112">Hello API переводят вызов функции hello в web services запросов toohello облачной службы Azure Multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="4d13a-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="4d13a-113">Все вызовы должны включать ссылку toohello закрытый сертификат, который включается в каждый пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="4d13a-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="4d13a-114">Поскольку hello API-интерфейсы не имеют доступа toousers зарегистрировано в Azure Active Directory, необходимо предоставить сведения о пользователе в файл или базу данных.</span><span class="sxs-lookup"><span data-stu-id="4d13a-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="4d13a-115">Кроме того hello API-интерфейсы не предоставляют функции управления регистрации или пользователя, поэтому требуется toobuild эти процессы в приложение.</span><span class="sxs-lookup"><span data-stu-id="4d13a-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d13a-116">toodownload Здравствуйте SDK, необходимо toocreate поставщик многофакторной проверки подлинности Azure, даже если лицензий Azure MFA, Azure Active Directory Premium или EMS.</span><span class="sxs-lookup"><span data-stu-id="4d13a-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="4d13a-117">Если создать поставщик многофакторной проверки подлинности Azure для этой цели с уже лицензий, убедитесь, что toocreate hello поставщика с hello **на включенного пользователя** модели.</span><span class="sxs-lookup"><span data-stu-id="4d13a-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="4d13a-118">Свяжите hello поставщика toohello каталог, содержащий hello лицензий Azure MFA, Azure AD Premium или EMS.</span><span class="sxs-lookup"><span data-stu-id="4d13a-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="4d13a-119">Эта конфигурация гарантирует, что оплата начисляется только при наличии нескольких уникальных пользователей, с помощью пакета SDK, чем hello число лицензий, которыми вы владеете hello.</span><span class="sxs-lookup"><span data-stu-id="4d13a-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="4d13a-120">Загрузите пакет SDK для hello</span><span class="sxs-lookup"><span data-stu-id="4d13a-120">Download hello SDK</span></span>
<span data-ttu-id="4d13a-121">Загрузка hello SDK Azure Multi-factor Authentication требуется [поставщик многофакторной проверки подлинности Azure](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="4d13a-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="4d13a-122">Для этого нужна полная версия подписки Azure, даже если у вас уже есть лицензии Azure MFA, AAD Premium или Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="4d13a-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="4d13a-123">hello toodownload SDK, перейдите toohello портал управления многофакторной.</span><span class="sxs-lookup"><span data-stu-id="4d13a-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="4d13a-124">Можно получить доступ к порталу hello либо управление hello поставщик многофакторной проверки подлинности непосредственно, либо щелкнув hello **«Go toohello портала»** ссылку на странице параметров hello многофакторной проверки Подлинности службы.</span><span class="sxs-lookup"><span data-stu-id="4d13a-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="4d13a-125">Загрузить hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="4d13a-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="4d13a-126">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4d13a-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="4d13a-127">В левой части экрана приветствия выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="4d13a-128">В верхнем выберите hello страницы Active Directory hello **поставщики многофакторной проверки подлинности**</span><span class="sxs-lookup"><span data-stu-id="4d13a-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="4d13a-129">Внизу hello выберите **управление**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="4d13a-130">Откроется новая страница.</span><span class="sxs-lookup"><span data-stu-id="4d13a-130">A new page opens.</span></span>
5. <span data-ttu-id="4d13a-131">Щелкните hello слева, внизу hello **SDK**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="4d13a-132"><center>![Загрузить](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="4d13a-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="4d13a-133">Выберите язык hello и ссылкам один hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="4d13a-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="4d13a-134">Сохраните hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="4d13a-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="4d13a-135">Загрузить параметры службы hello</span><span class="sxs-lookup"><span data-stu-id="4d13a-135">Download from hello service settings</span></span>
1. <span data-ttu-id="4d13a-136">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4d13a-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="4d13a-137">В левой части экрана приветствия выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="4d13a-138">Дважды щелкните свой экземпляр Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d13a-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="4d13a-139">В верхней щелкните hello **Настройка**</span><span class="sxs-lookup"><span data-stu-id="4d13a-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="4d13a-140">В разделе многофакторной идентификации выберите **Управление параметрами службы**
   .![Скачивание](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="4d13a-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="4d13a-141">На странице настройки службы hello hello нижней части экрана приветствия щелкните **портала toohello Go**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="4d13a-142">Откроется новая страница.</span><span class="sxs-lookup"><span data-stu-id="4d13a-142">A new page opens.</span></span>
   <span data-ttu-id="4d13a-143">![Загрузить](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="4d13a-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="4d13a-144">Щелкните hello слева, внизу hello **SDK**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="4d13a-145">Выберите язык hello и ссылкам один hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="4d13a-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="4d13a-146">Сохраните hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="4d13a-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="4d13a-147">Возможности hello SDK</span><span class="sxs-lookup"><span data-stu-id="4d13a-147">What's in hello SDK</span></span>
<span data-ttu-id="4d13a-148">Hello SDK включает hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4d13a-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="4d13a-149">**README**.</span><span class="sxs-lookup"><span data-stu-id="4d13a-149">**README**.</span></span> <span data-ttu-id="4d13a-150">Объясняет, как toouse hello многофакторной проверки подлинности API-интерфейсы в новом или существующем приложении.</span><span class="sxs-lookup"><span data-stu-id="4d13a-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="4d13a-151">**Исходные файлы** для Многофакторной идентификации</span><span class="sxs-lookup"><span data-stu-id="4d13a-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="4d13a-152">**Сертификат клиента** использовать toocommunicate с hello служба многофакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4d13a-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="4d13a-153">**Закрытый ключ** для hello сертификата</span><span class="sxs-lookup"><span data-stu-id="4d13a-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="4d13a-154">**Результаты вызова.**</span><span class="sxs-lookup"><span data-stu-id="4d13a-154">**Call results.**</span></span> <span data-ttu-id="4d13a-155">Список кодов результатов вызова.</span><span class="sxs-lookup"><span data-stu-id="4d13a-155">A list of call result codes.</span></span> <span data-ttu-id="4d13a-156">tooopen этот файл, используйте приложение с форматирования текста, например WordPad.</span><span class="sxs-lookup"><span data-stu-id="4d13a-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="4d13a-157">Используйте hello tootest кодов результатов вызова и устранение неполадок реализации hello многофакторной проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="4d13a-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="4d13a-158">Они отличаются от кодов состояния проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d13a-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="4d13a-159">**Примеры.**</span><span class="sxs-lookup"><span data-stu-id="4d13a-159">**Examples.**</span></span> <span data-ttu-id="4d13a-160">Пример кода для базовой рабочей реализации процесса Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="4d13a-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="4d13a-161">сертификат клиента Hello имеет уникальный закрытый сертификат, созданный специально для вас.</span><span class="sxs-lookup"><span data-stu-id="4d13a-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="4d13a-162">Не показывайте никому и не теряйте этот файл.</span><span class="sxs-lookup"><span data-stu-id="4d13a-162">Do not share or lose this file.</span></span> <span data-ttu-id="4d13a-163">Это вашей безопасности hello ключа tooensuring взаимодействия со службой hello многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d13a-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="4d13a-164">Пример кода</span><span class="sxs-lookup"><span data-stu-id="4d13a-164">Code sample</span></span>
<span data-ttu-id="4d13a-165">Этот пример кода показывает, как hello toouse API-интерфейсы в hello Azure Multi-factor Authentication SDK tooadd стандартный режим голосового вызова приложения tooyour проверки.</span><span class="sxs-lookup"><span data-stu-id="4d13a-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="4d13a-166">Стандартный режим — это телефонный звонок, на который пользователь отвечает tooby нажатие клавиши # hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d13a-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="4d13a-167">В этом примере используется hello C# .NET 2.0 SDK Multi-factor Authentication в простое приложение ASP.NET с серверной логикой на C#, но hello процесс похож на других языках.</span><span class="sxs-lookup"><span data-stu-id="4d13a-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="4d13a-168">Поскольку hello SDK включает исходные файлы, не исполняемые файлы, можно создать файлы hello и ссылаться на них или включить их в самом приложении.</span><span class="sxs-lookup"><span data-stu-id="4d13a-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="4d13a-169">При реализации многофакторной проверки подлинности, следует используйте дополнительные методы hello (телефонный звонок или текстовое сообщение), как вторичная и третичная проверка toosupplement ваш основной способ проверки подлинности (имя пользователя и пароль).</span><span class="sxs-lookup"><span data-stu-id="4d13a-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="4d13a-170">Эти методы не предназначены для использования в качестве основных способов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d13a-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="4d13a-171">Обзор примера кода</span><span class="sxs-lookup"><span data-stu-id="4d13a-171">Code Sample Overview</span></span>
<span data-ttu-id="4d13a-172">Этот пример кода для демонстрации простого веб-приложения использует телефонный звонок с проверкой подлинности # ключа ответа tooverify hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d13a-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="4d13a-173">В рамках Multi-Factor Authentication фактор телефонного вызова называется стандартным режимом.</span><span class="sxs-lookup"><span data-stu-id="4d13a-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="4d13a-174">Hello клиентский код не включает какие-либо элементы зависящие от многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d13a-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="4d13a-175">Поскольку hello дополнительные факторы проверки подлинности не зависят от основной проверки подлинности hello, их можно добавить без изменения hello существующего интерфейса входа.</span><span class="sxs-lookup"><span data-stu-id="4d13a-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="4d13a-176">Hello API-интерфейсы в hello SDK Multi-factor Authentication позволяют настроить взаимодействие с пользователем hello, но может не потребоваться toochange ничего вообще.</span><span class="sxs-lookup"><span data-stu-id="4d13a-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="4d13a-177">Hello серверный код добавляет стандартный режим проверки подлинности на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="4d13a-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="4d13a-178">Он создает объект PfAuthParams с параметрами hello, которые требуются для верификации в стандартном режиме: имя пользователя, телефонные номера, а также режим и hello путь toohello сертификат клиента (CertFilePath), который является обязательным для каждого вызова.</span><span class="sxs-lookup"><span data-stu-id="4d13a-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="4d13a-179">Демонстрацию всех параметров в PfAuthParams см. в разделе файла пример hello в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4d13a-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="4d13a-180">Затем код hello передает функции hello PfAuthParams объекта toohello pf_authenticate().</span><span class="sxs-lookup"><span data-stu-id="4d13a-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="4d13a-181">Возвращаемое значение Hello указывает успешность hello hello проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d13a-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="4d13a-182">Здравствуйте, параметры, callStatus и кода ошибки, содержат сведения о результате дополнительный вызов.</span><span class="sxs-lookup"><span data-stu-id="4d13a-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="4d13a-183">коды результатов звонков Hello описаны в файле результатов вызова hello в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4d13a-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="4d13a-184">Такая минимальная реализация может занимать несколько строк.</span><span class="sxs-lookup"><span data-stu-id="4d13a-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="4d13a-185">Однако в готовый код следует включить более сложную обработку ошибок, дополнительный код базы данных и улучшенный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="4d13a-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="4d13a-186">Код веб-клиента</span><span class="sxs-lookup"><span data-stu-id="4d13a-186">Web Client Code</span></span>
<span data-ttu-id="4d13a-187">Hello ниже приведен код веб-клиента для демонстрационной страницы.</span><span class="sxs-lookup"><span data-stu-id="4d13a-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="4d13a-188">Серверный код</span><span class="sxs-lookup"><span data-stu-id="4d13a-188">Server-Side Code</span></span>
<span data-ttu-id="4d13a-189">В следующий серверный код hello многофакторной проверки подлинности настраивается и запускается на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="4d13a-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="4d13a-190">Стандартный режим (MODE_STANDARD) — отвечает пользователь hello toowhich телефонный звонок, нажав клавишу # hello.</span><span class="sxs-lookup"><span data-stu-id="4d13a-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
