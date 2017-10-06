---
title: "aaaSet специальную домашнюю страницу для опубликованных приложений с помощью прокси приложения Azure AD | Документы Microsoft"
description: "Описываются основы hello о соединителей прокси приложения Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="bcc38-103">Настройка пользовательской домашней страницы для опубликованных приложений с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc38-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="bcc38-104">В этой статье рассматриваются как tooconfigure приложений toodirect пользователей tooa специальную домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="bcc38-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="bcc38-105">При публикации приложения с помощью прокси приложения задать внутренний URL-адрес, но иногда, не видят пользователи должны сначала страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="bcc38-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="bcc38-106">Задайте специальную домашнюю страницу, чтобы пользователи переход на страницу правой toohello при доступе приложения hello из панели доступа Active Directory Azure hello или средство запуска приложений Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="bcc38-107">Когда пользователь запустит приложение hello, они все руководством по умолчанию toohello корневой домен URL-адрес для опубликованного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="bcc38-108">Целевая страница Hello обычно устанавливается в виде URL-адрес домашней страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="bcc38-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="bcc38-109">Используйте URL-адреса hello Azure AD PowerShell модуль toodefine специальную домашнюю страницу, при необходимости tooland пользователей приложения на конкретной странице в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="bcc38-110">Например:</span><span class="sxs-lookup"><span data-stu-id="bcc38-110">For example:</span></span>
- <span data-ttu-id="bcc38-111">В корпоративной сети, будут переходить пользователи слишком*https://ExpenseApp/login/login.aspx* toosign в и доступ к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="bcc38-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="bcc38-112">Так как у вас есть другие активы, подобно изображениям, прокси-сервер приложений должен tooaccess на верхнем уровне структуры папок hello hello, публикации приложения hello с *https://ExpenseApp* как hello внутренний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bcc38-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="bcc38-113">Здравствуйте, внешний URL-адрес по умолчанию *https://ExpenseApp-contoso.msappproxy.net*, который не принимает toohello входа пользователей на странице.</span><span class="sxs-lookup"><span data-stu-id="bcc38-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="bcc38-114">Задать *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* как hello toogive URL-адрес домашней страницы пользователей эффективной работы.</span><span class="sxs-lookup"><span data-stu-id="bcc38-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="bcc38-115">Когда приложения toopublished предоставить доступ пользователям приложения hello, отображаются в hello [панели доступа Azure AD](active-directory-saas-access-panel-introduction.md) и hello [средство запуска приложений Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="bcc38-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="bcc38-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bcc38-116">Before you start</span></span>

<span data-ttu-id="bcc38-117">Перед установкой URL-адрес домашней страницы приветствия Имейте в виду hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="bcc38-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="bcc38-118">Убедитесь, что этот путь hello представляет собой путь к поддомен hello корневой домен URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bcc38-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="bcc38-119">Если URL-адрес корневого домена hello, например, https://apps.contoso.com/app1/, hello Домашняя страница URL-адреса должно начинаться с https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="bcc38-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="bcc38-120">При внесении изменений toohello публикации приложения, изменение hello может сбросить значение hello URL-адрес домашней страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="bcc38-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="bcc38-121">При обновлении приложения hello в будущем hello, необходимо повторно проверить и, при необходимости измените URL-адрес домашней страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="bcc38-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="bcc38-122">Изменить домашнюю страницу приветствия в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bcc38-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="bcc38-123">Войдите в toohello [портал Azure](https://portal.azure.com) с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bcc38-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="bcc38-124">Перейдите в слишком**Azure Active Directory** > **регистрации приложения** и выберите приложение из списка hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="bcc38-125">Выберите **свойства** из настроек hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="bcc38-126">Обновление hello **URL-адрес домашней страницы** поле ваш новый путь.</span><span class="sxs-lookup"><span data-stu-id="bcc38-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Указание нового URL-адреса домашней страницы](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="bcc38-128">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bcc38-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="bcc38-129">Изменить домашнюю страницу приветствия с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcc38-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="bcc38-130">Установка модуля Azure AD PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="bcc38-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="bcc38-131">Прежде чем определить URL-адрес домашней страницы с помощью PowerShell, установите модуль Azure AD PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="bcc38-132">Можно загрузить пакет hello hello [коллекции PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), который использует hello конечная точка Graph API.</span><span class="sxs-lookup"><span data-stu-id="bcc38-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="bcc38-133">tooinstall hello пакет, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bcc38-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="bcc38-134">Откройте стандартное окно PowerShell и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="bcc38-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="bcc38-135">Если вы используете команду hello как без прав администратора, используйте hello `-scope currentuser` параметр.</span><span class="sxs-lookup"><span data-stu-id="bcc38-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="bcc38-136">Во время установки hello выберите **Y** tooinstall двух пакетов из Nuget.org. Требуются оба пакета.</span><span class="sxs-lookup"><span data-stu-id="bcc38-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="bcc38-137">Найти hello ObjectID приложение hello</span><span class="sxs-lookup"><span data-stu-id="bcc38-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="bcc38-138">Получите hello ObjectID приложение hello и выполните поиск приложения hello, домашняя страница.</span><span class="sxs-lookup"><span data-stu-id="bcc38-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="bcc38-139">Откройте PowerShell и импорт модуля hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcc38-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="bcc38-140">Войдите в toohello модуля Azure AD как администратор клиента hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="bcc38-141">Найти приложение hello в зависимости от его URL-адрес домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="bcc38-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="bcc38-142">Hello URL-адрес можно найти в портале hello, перейдя слишком**Azure Active Directory** > **корпоративных приложений** > **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bcc38-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="bcc38-143">В этом примере используется *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="bcc38-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="bcc38-144">Вы должны получить результат, аналогичный toohello показанной здесь.</span><span class="sxs-lookup"><span data-stu-id="bcc38-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="bcc38-145">Скопируйте hello toouse ObjectID GUID в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="bcc38-146">Обновить URL-адрес домашней страницы приветствия</span><span class="sxs-lookup"><span data-stu-id="bcc38-146">Update hello home page URL</span></span>

<span data-ttu-id="bcc38-147">В hello же модуль PowerShell, который использовался в шаге 1, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="bcc38-148">Убедитесь, что hello исправьте приложения и замените *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* с hello ObjectID, скопированным на предшествующий шаг hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="bcc38-149">Теперь, когда вы убедились, приложение hello, вы готовы tooupdate hello домашней страницы, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bcc38-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="bcc38-150">Создайте пустое приложение объекта toohold hello изменения, которые должны toomake.</span><span class="sxs-lookup"><span data-stu-id="bcc38-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="bcc38-151">Эта переменная содержит hello значения, которые должны tooupdate.</span><span class="sxs-lookup"><span data-stu-id="bcc38-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="bcc38-152">На этом шаге ничто не создается.</span><span class="sxs-lookup"><span data-stu-id="bcc38-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="bcc38-153">Набор hello Домашняя страница URL-адрес toohello нужное значение.</span><span class="sxs-lookup"><span data-stu-id="bcc38-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="bcc38-154">Hello значение должно быть контура поддомен опубликованное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="bcc38-155">Например, если изменить hello URL-адрес домашней страницы из *https://sharepoint-iddemo.msappproxy.net/* слишком*https://sharepoint-iddemo.msappproxy.net/hybrid/*, пользователи приложения перейдите непосредственно настраиваемый toohello Домашняя страница.</span><span class="sxs-lookup"><span data-stu-id="bcc38-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="bcc38-156">Сделать hello обновления с помощью hello GUID (ObjectID), который был скопирован в «шаг 1: hello поиска ObjectID приложение hello.»</span><span class="sxs-lookup"><span data-stu-id="bcc38-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="bcc38-157">tooconfirm, hello изменений успешно выполнена, перезапустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bcc38-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="bcc38-158">URL-адрес домашней страницы приветствия, могут быть сброшены изменения, выполняемые toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="bcc38-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="bcc38-159">Если URL-адрес домашней страницы сбрасывается, то повторите шаг 2.</span><span class="sxs-lookup"><span data-stu-id="bcc38-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcc38-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bcc38-160">Next steps</span></span>

- [<span data-ttu-id="bcc38-161">Включить tooSharePoint удаленного доступа с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcc38-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="bcc38-162">Включите прокси приложения в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bcc38-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
