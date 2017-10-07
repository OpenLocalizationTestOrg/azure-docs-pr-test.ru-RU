---
title: "aaaGet данных с помощью hello Azure Reporting API AD с сертификатами | Документы Microsoft"
description: "Объясняет, как toouse hello Azure AD API Reporting с данными tooget учетные данные сертификата из каталогов без вмешательства пользователя."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="aa0c9-103">Получение данных с помощью API отчетов hello Azure AD с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="aa0c9-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="aa0c9-104">В этой статье рассматриваются как toouse hello Azure AD API Reporting с данными tooget учетные данные сертификата из каталогов без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="aa0c9-105">Здравствуйте, используйте API отчетов Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa0c9-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="aa0c9-106">API отчетов Azure AD требует выполнения hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="aa0c9-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="aa0c9-107">установить необходимые компоненты;</span><span class="sxs-lookup"><span data-stu-id="aa0c9-107">Install prerequisites</span></span>
 *  <span data-ttu-id="aa0c9-108">Задать сертификат hello в приложении</span><span class="sxs-lookup"><span data-stu-id="aa0c9-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="aa0c9-109">Получение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="aa0c9-109">Get an access token</span></span>
 *  <span data-ttu-id="aa0c9-110">Использовать hello toocall токена доступа hello Graph API</span><span class="sxs-lookup"><span data-stu-id="aa0c9-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="aa0c9-111">Сведения об исходном коде см. в [практическом руководстве по использованию модуля API отчетов](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="aa0c9-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="aa0c9-112">установить необходимые компоненты;</span><span class="sxs-lookup"><span data-stu-id="aa0c9-112">Install prerequisites</span></span>
<span data-ttu-id="aa0c9-113">Необходимо будет toohave Azure AD PowerShell V2 и AzureADUtils модуль установлен.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="aa0c9-114">Загрузите и установите Azure AD Powershell V2, следуя инструкциям hello в [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="aa0c9-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="aa0c9-115">Загрузите модуль Azure AD Odatautils hello из [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="aa0c9-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="aa0c9-116">Этот модуль предоставляет несколько служебных командлетов, позволяющих получить:</span><span class="sxs-lookup"><span data-stu-id="aa0c9-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="aa0c9-117">Hello последнюю версию ADAL с помощью Nuget</span><span class="sxs-lookup"><span data-stu-id="aa0c9-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="aa0c9-118">маркеры доступа пользователя, ключи приложений и сертификаты с использованием ADAL;</span><span class="sxs-lookup"><span data-stu-id="aa0c9-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="aa0c9-119">обработку результатов с разбивкой на страницы с помощью API Graph.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-119">Graph API handling paged results</span></span>

<span data-ttu-id="aa0c9-120">**модуль Odatautils AD Azure hello tooinstall:**</span><span class="sxs-lookup"><span data-stu-id="aa0c9-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="aa0c9-121">Создать модуль программы hello toosave каталог (например, c:\azureAD) и загрузите hello модуля из GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="aa0c9-122">Откройте сеанс PowerShell и перейдите в каталог toohello, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="aa0c9-123">Импорт модуля hello и установите его в путь к модулю hello PowerShell с помощью командлета Install AzureADUtilsModule hello.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="aa0c9-124">Hello сеанса должен выглядеть примерно toothis экрана.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-124">hello session should look similar toothis screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="aa0c9-126">Задать сертификат hello в приложении</span><span class="sxs-lookup"><span data-stu-id="aa0c9-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="aa0c9-127">Если уже имеется приложение, получите его идентификатор объекта из hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Портал Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="aa0c9-129">Откройте сеанс PowerShell и подключитесь tooAzure AD с помощью командлета Connect AzureAD hello.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Портал Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="aa0c9-131">С помощью командлета New-AzureADApplicationCertificateCredential hello из AzureADUtils tooadd tooit учетные данные сертификата.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="aa0c9-132">Вам необходимы приложения hello tooprovide идентификатор объекта, которые собраны в более ранних версий, а также hello объекта сертификата (получить это с помощью hello Cert: диск).</span><span class="sxs-lookup"><span data-stu-id="aa0c9-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Портал Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="aa0c9-134">Получение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="aa0c9-134">Get an access token</span></span>

<span data-ttu-id="aa0c9-135">tooget маркер доступа с помощью командлета Get-AzureADGraphAPIAccessTokenFromCert hello из AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="aa0c9-136">Необходимо toouse hello идентификатор приложения, вместо hello идентификатор объекта, который использовался в последний раздел hello.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Портал Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="aa0c9-138">Использовать hello toocall токена доступа hello Graph API</span><span class="sxs-lookup"><span data-stu-id="aa0c9-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="aa0c9-139">Теперь можно создать сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-139">Now you can create hello script.</span></span> <span data-ttu-id="aa0c9-140">Ниже приведен пример использования командлета Invoke-AzureADGraphAPIQuery hello из hello AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="aa0c9-141">Этот командлет обрабатывает результаты нескольких страниц, а затем отправляет эти конвейер PowerShell toohello результаты.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Портал Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="aa0c9-143">Теперь вы готовы tooexport tooa CSV и сохранить tooa системы SIEM.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="aa0c9-144">Также можно включить сценарий в назначенное задание tooget данных Azure AD из вашего клиента периодически без необходимости toostore приложения ключей в исходном коде hello.</span><span class="sxs-lookup"><span data-stu-id="aa0c9-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aa0c9-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa0c9-145">Next steps</span></span>
[<span data-ttu-id="aa0c9-146">Основные принципы управления удостоверениями Azure Hello</span><span class="sxs-lookup"><span data-stu-id="aa0c9-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



