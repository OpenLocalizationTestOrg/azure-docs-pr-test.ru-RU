---
title: "Azure AD B2C: настройка пользовательского интерфейса с помощью настраиваемых политик | Документация Майкрософт"
description: "Сведения о настройке пользовательского интерфейса с помощью настраиваемых политик в Azure AD B2C."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: d5a3c0a323b31696d39e3d2b36317dec3a2337d7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="ba607-103">Azure Active Directory B2C. Настройка пользовательского интерфейса с помощью настраиваемой политики</span><span class="sxs-lookup"><span data-stu-id="ba607-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ba607-104">Выполнив инструкции из этой статьи, вы получите настраиваемую политику регистрации и входа с фирменной символикой и оформлением.</span><span class="sxs-lookup"><span data-stu-id="ba607-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="ba607-105">Благодаря Azure Active Directory B2C (Azure AD B2C) вы получаете практически полный контроль над содержимым HTML и CSS, которое представляется пользователям.</span><span class="sxs-lookup"><span data-stu-id="ba607-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="ba607-106">При использовании настраиваемой политики вы настраиваете пользовательский интерфейс в XML-файле, а не с помощью элементов управления на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ba607-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ba607-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ba607-107">Prerequisites</span></span>

<span data-ttu-id="ba607-108">Прежде чем продолжить, ознакомьтесь со статьей [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ba607-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="ba607-109">Для регистрации и входа с использованием локальных учетных записей необходимо иметь рабочую настраиваемую политику.</span><span class="sxs-lookup"><span data-stu-id="ba607-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="ba607-110">Настройка пользовательского интерфейса страницы</span><span class="sxs-lookup"><span data-stu-id="ba607-110">Page UI customization</span></span>

<span data-ttu-id="ba607-111">С помощью функции настройки пользовательского интерфейса страницы можно настроить оформление любой настраиваемой политики.</span><span class="sxs-lookup"><span data-stu-id="ba607-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="ba607-112">Кроме того, можно обеспечить согласованность фирменной символики и визуализации в приложении и службе Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ba607-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="ba607-113">Вот как это работает. Служба Azure AD B2C выполняет код в браузере пользователя и использует современный метод — [общий доступ к ресурсам независимо от источника (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="ba607-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="ba607-114">Сначала необходимо указать URL-адрес в настраиваемой политике с настраиваемым содержимым HTML.</span><span class="sxs-lookup"><span data-stu-id="ba607-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="ba607-115">Azure AD B2C объединяет элементы пользовательского интерфейса с содержимым HTML, загруженным по указанному URL-адресу, и отображает страницу для пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba607-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="ba607-116">Создание содержимого HTML5</span><span class="sxs-lookup"><span data-stu-id="ba607-116">Create your HTML5 content</span></span>

<span data-ttu-id="ba607-117">Создадим содержимое HTML с названием вашей торговой марки в заголовке.</span><span class="sxs-lookup"><span data-stu-id="ba607-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="ba607-118">Скопируйте следующий фрагмент кода HTML.</span><span class="sxs-lookup"><span data-stu-id="ba607-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="ba607-119">Это код HTML5 с правильным форматом. Он содержит пустой элемент *\<div id="api"\>\</div\>*, заключенный в теги *\<body\>*.</span><span class="sxs-lookup"><span data-stu-id="ba607-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="ba607-120">Этот элемент определяет расположение, в которое будет вставлено содержимое Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ba607-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="ba607-121">По соображениям безопасности использование JavaScript для настройки сейчас заблокировано.</span><span class="sxs-lookup"><span data-stu-id="ba607-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="ba607-122">Вставьте скопированный фрагмент кода в текстовый редактор и сохраните файл как *customize-ui.html*.</span><span class="sxs-lookup"><span data-stu-id="ba607-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="ba607-123">Создание учетной записи хранения BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="ba607-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="ba607-124">В этой статье мы используем хранилище BLOB-объектов Azure для размещения содержимого.</span><span class="sxs-lookup"><span data-stu-id="ba607-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="ba607-125">Можно выбрать для этого веб-сервер, но тогда нужно [включить для веб-сервера поддержку CORS](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="ba607-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="ba607-126">Чтобы разместить HTML-содержимое в хранилище BLOB-объектов, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ba607-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="ba607-127">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba607-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ba607-128">В меню **Концентратор** выберите **Создать** > **Хранилище** > **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="ba607-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="ba607-129">Введите уникальное **имя** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ba607-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="ba607-130">Для параметра **Модель развертывания** можно оставить значение **Диспетчер ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="ba607-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="ba607-131">Измените **тип учетной записи** на **хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="ba607-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="ba607-132">Для параметра **Производительность** можно оставить значение **Стандартная**.</span><span class="sxs-lookup"><span data-stu-id="ba607-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="ba607-133">Для параметра **Репликация** можно оставить значение **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="ba607-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="ba607-134">Для параметра **Уровень доступа** можно оставить значение **Горячий**.</span><span class="sxs-lookup"><span data-stu-id="ba607-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="ba607-135">Для параметра **Шифрование службы хранилища** можно оставить значение **Отключено**.</span><span class="sxs-lookup"><span data-stu-id="ba607-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="ba607-136">Выберите **подписку** для своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ba607-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="ba607-137">Создайте новую **группу ресурсов** или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="ba607-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="ba607-138">Выберите **географический регион** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ba607-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="ba607-139">Щелкните **Создать** , чтобы создать учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="ba607-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="ba607-140">После развертывания колонка **Учетная запись хранения** откроется автоматически.</span><span class="sxs-lookup"><span data-stu-id="ba607-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ba607-141">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="ba607-141">Create a container</span></span>

<span data-ttu-id="ba607-142">Чтобы создать общедоступный контейнер в хранилище BLOB-объектов, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ba607-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="ba607-143">Щелкните вкладку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="ba607-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="ba607-144">Щелкните **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="ba607-144">Click **Container**.</span></span>
3. <span data-ttu-id="ba607-145">В поле **Имя** введите **$root**.</span><span class="sxs-lookup"><span data-stu-id="ba607-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="ba607-146">Задайте для параметра **Тип доступа** значение **BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="ba607-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="ba607-147">Щелкните **$root**, чтобы открыть новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="ba607-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="ba607-148">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="ba607-148">Click **Upload**.</span></span>
7. <span data-ttu-id="ba607-149">Щелкните значок папки рядом с элементом **Выбор файла**.</span><span class="sxs-lookup"><span data-stu-id="ba607-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="ba607-150">Перейдите к файлу **customize-ui.html**, созданному ранее в разделе [Настройка пользовательского интерфейса страницы](#the-page-ui-customization-feature).</span><span class="sxs-lookup"><span data-stu-id="ba607-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="ba607-151">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="ba607-151">Click **Upload**.</span></span>
10. <span data-ttu-id="ba607-152">Выберите BLOB-объект customize-ui.html, который вы загрузили.</span><span class="sxs-lookup"><span data-stu-id="ba607-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="ba607-153">Рядом с полем **URL-адрес** нажмите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="ba607-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="ba607-154">Вставьте скопированный URL-адрес в строку браузера и перейдите на сайт.</span><span class="sxs-lookup"><span data-stu-id="ba607-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="ba607-155">Если он недоступен, убедитесь, что для типа доступа к контейнеру указано значение **BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="ba607-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="ba607-156">Настройка CORS</span><span class="sxs-lookup"><span data-stu-id="ba607-156">Configure CORS</span></span>

<span data-ttu-id="ba607-157">Настройте хранилище BLOB-объектов для общего доступа к ресурсам независимо от источника (CORS), сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="ba607-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="ba607-158">Хотите протестировать функцию настройки пользовательского интерфейса с помощью примера содержимого HTML и CSS?</span><span class="sxs-lookup"><span data-stu-id="ba607-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="ba607-159">Используйте [простое вспомогательное приложение](active-directory-b2c-reference-ui-customization-helper-tool.md), чтобы отправить и настроить пример содержимого в учетной записи хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="ba607-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="ba607-160">Если вы используете такое приложение, перейдите к разделу об [изменении настраиваемой политики регистрации или входа](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="ba607-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="ba607-161">В колонке **Хранилище** в разделе **Параметры** откройте **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ba607-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="ba607-162">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ba607-162">Click **Add**.</span></span>
3. <span data-ttu-id="ba607-163">Для параметра **Разрешенные источники** введите звездочку (\*).</span><span class="sxs-lookup"><span data-stu-id="ba607-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="ba607-164">В раскрывающемся списке **Разрешенные команды** выберите **GET** и **OPTIONS**.</span><span class="sxs-lookup"><span data-stu-id="ba607-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="ba607-165">Для параметра **Разрешенные заголовки** введите звездочку (\*).</span><span class="sxs-lookup"><span data-stu-id="ba607-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="ba607-166">Для параметра **Доступные заголовки** введите звездочку (\*).</span><span class="sxs-lookup"><span data-stu-id="ba607-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="ba607-167">Для параметра **Максимальная длительность (в секундах)** введите **200**.</span><span class="sxs-lookup"><span data-stu-id="ba607-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="ba607-168">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ba607-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="ba607-169">Тестирование CORS</span><span class="sxs-lookup"><span data-stu-id="ba607-169">Test CORS</span></span>

<span data-ttu-id="ba607-170">Проверьте готовность, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="ba607-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="ba607-171">Перейдите на веб-сайт [test-cors.org](http://test-cors.org/) и вставьте URL-адрес в поле **Remote URL** (Удаленный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="ba607-171">Go to the [test-cors.org](http://test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="ba607-172">Щелкните **Send Request** (Отправить запрос).</span><span class="sxs-lookup"><span data-stu-id="ba607-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="ba607-173">Если произошла ошибка, проверьте правильность [параметров CORS](#configure-cors).</span><span class="sxs-lookup"><span data-stu-id="ba607-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="ba607-174">Кроме того, вам может потребоваться очистить кэш браузера или открыть закрытый сеанс, нажав CTRL+SHIFT+P.</span><span class="sxs-lookup"><span data-stu-id="ba607-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="ba607-175">Изменение настраиваемой политики регистрации или входа</span><span class="sxs-lookup"><span data-stu-id="ba607-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="ba607-176">Под тегом *\<TrustFrameworkPolicy\>* верхнего уровня найдите теги *\<BuildingBlocks\>*.</span><span class="sxs-lookup"><span data-stu-id="ba607-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="ba607-177">Между тегами *\<BuildingBlocks\>* добавьте тег *\<ContentDefinitions\>*, скопировав пример ниже.</span><span class="sxs-lookup"><span data-stu-id="ba607-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="ba607-178">Замените свойство *your_storage_account* именем своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ba607-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="ba607-179">Отправка обновленной настраиваемой политики</span><span class="sxs-lookup"><span data-stu-id="ba607-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="ba607-180">На [портале Azure](https://portal.azure.com) [переключитесь в контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) и откройте колонку **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="ba607-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="ba607-181">Щелкните **Все политики**.</span><span class="sxs-lookup"><span data-stu-id="ba607-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="ba607-182">Выберите **Отправить политику**.</span><span class="sxs-lookup"><span data-stu-id="ba607-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="ba607-183">Отправьте `SignUpOrSignin.xml` с добавленным ранее тегом *\<ContentDefinitions\>*.</span><span class="sxs-lookup"><span data-stu-id="ba607-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="ba607-184">Тестирование настраиваемой политики с помощью параметра **Запустить сейчас**</span><span class="sxs-lookup"><span data-stu-id="ba607-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="ba607-185">В колонке **Azure AD B2C** выберите **Все политики**.</span><span class="sxs-lookup"><span data-stu-id="ba607-185">On the **Azure AD B2C** blade, go to **All polices**.</span></span>
2. <span data-ttu-id="ba607-186">Выберите отправленную вами настраиваемую политику и нажмите кнопку **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="ba607-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="ba607-187">Вы сможете зарегистрироваться, используя адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="ba607-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="ba607-188">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="ba607-188">Reference</span></span>

<span data-ttu-id="ba607-189">Здесь можно найти примеры шаблонов для настройки пользовательского интерфейса:</span><span class="sxs-lookup"><span data-stu-id="ba607-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="ba607-190">Папка sample_templates/wingtip содержит следующие файлы HTML:</span><span class="sxs-lookup"><span data-stu-id="ba607-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="ba607-191">Шаблон HTML5</span><span class="sxs-lookup"><span data-stu-id="ba607-191">HTML5 template</span></span> | <span data-ttu-id="ba607-192">Описание</span><span class="sxs-lookup"><span data-stu-id="ba607-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="ba607-193">*phonefactor.html*</span><span class="sxs-lookup"><span data-stu-id="ba607-193">*phonefactor.html*</span></span> | <span data-ttu-id="ba607-194">Этот файл используется как шаблон для страницы многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ba607-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="ba607-195">*ResetPassword.html*</span><span class="sxs-lookup"><span data-stu-id="ba607-195">*resetpassword.html*</span></span> | <span data-ttu-id="ba607-196">Этот файл используется как шаблон для страницы восстановления пароля.</span><span class="sxs-lookup"><span data-stu-id="ba607-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="ba607-197">*selfasserted.html*</span><span class="sxs-lookup"><span data-stu-id="ba607-197">*selfasserted.html*</span></span> | <span data-ttu-id="ba607-198">Этот файл используется как шаблон для страницы регистрации учетных записей социальных сетей, страницы регистрации локальной учетной записи или страницы входа в локальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ba607-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="ba607-199">*unified.html*</span><span class="sxs-lookup"><span data-stu-id="ba607-199">*unified.html*</span></span> | <span data-ttu-id="ba607-200">Этот файл используется как шаблон для единой страницы регистрации или входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ba607-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="ba607-201">*updateprofile.html*</span><span class="sxs-lookup"><span data-stu-id="ba607-201">*updateprofile.html*</span></span> | <span data-ttu-id="ba607-202">Этот файл используется как шаблон для страницы обновления профиля.</span><span class="sxs-lookup"><span data-stu-id="ba607-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="ba607-203">В разделе [Изменение настраиваемой политики регистрации или входа](#modify-your-sign-up-or-sign-in-custom-policy) мы настроили определение содержимого для `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="ba607-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="ba607-204">Полный набор идентификаторов для определения содержимого, распознаваемых в инфраструктуре Identity Experience Framework Azure AD B2C, а также их описания представлены в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="ba607-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="ba607-205">Идентификатор для определения содержимого</span><span class="sxs-lookup"><span data-stu-id="ba607-205">Content definition ID</span></span> | <span data-ttu-id="ba607-206">Описание</span><span class="sxs-lookup"><span data-stu-id="ba607-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="ba607-207">*api.error*</span><span class="sxs-lookup"><span data-stu-id="ba607-207">*api.error*</span></span> | <span data-ttu-id="ba607-208">**Страница ошибки.**</span><span class="sxs-lookup"><span data-stu-id="ba607-208">**Error page**.</span></span> <span data-ttu-id="ba607-209">Эта страница отображается при обнаружении исключения или ошибки.</span><span class="sxs-lookup"><span data-stu-id="ba607-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="ba607-210">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="ba607-210">*api.idpselections*</span></span> | <span data-ttu-id="ba607-211">**Страница выбора поставщика удостоверений.**</span><span class="sxs-lookup"><span data-stu-id="ba607-211">**Identity provider selection page**.</span></span> <span data-ttu-id="ba607-212">На этой странице содержится список поставщиков удостоверений, которых можно выбирать во время входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba607-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="ba607-213">Это поставщики удостоверений организаций, социальных сетей, включая Facebook и Google+, или локальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="ba607-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="ba607-214">*api.idpselections.signup*</span><span class="sxs-lookup"><span data-stu-id="ba607-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="ba607-215">**Выбор поставщика удостоверений для регистрации.**</span><span class="sxs-lookup"><span data-stu-id="ba607-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="ba607-216">На этой странице содержится список поставщиков удостоверений, которых можно выбирать во время регистрации.</span><span class="sxs-lookup"><span data-stu-id="ba607-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="ba607-217">Это поставщики удостоверений организаций, социальных сетей, включая Facebook и Google+, или локальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="ba607-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="ba607-218">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="ba607-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="ba607-219">**Страница восстановления пароля.**</span><span class="sxs-lookup"><span data-stu-id="ba607-219">**Forgot password page**.</span></span> <span data-ttu-id="ba607-220">Эта страница содержит форму, которую нужно заполнить для сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="ba607-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="ba607-221">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="ba607-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="ba607-222">**Страница входа в локальную учетную запись.**</span><span class="sxs-lookup"><span data-stu-id="ba607-222">**Local account sign-in page**.</span></span> <span data-ttu-id="ba607-223">Эта страница содержит форму для входа в локальную учетную запись (на основе адреса электронной почты или имени пользователя).</span><span class="sxs-lookup"><span data-stu-id="ba607-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="ba607-224">Форма может содержать текстовое поле ввода и окно ввода пароля.</span><span class="sxs-lookup"><span data-stu-id="ba607-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="ba607-225">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="ba607-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="ba607-226">**Страница регистрации локальной учетной записи.**</span><span class="sxs-lookup"><span data-stu-id="ba607-226">**Local account sign-up page**.</span></span> <span data-ttu-id="ba607-227">Эта страница содержит форму для регистрации локальной учетной записи (на основе адреса электронной почты или имени пользователя).</span><span class="sxs-lookup"><span data-stu-id="ba607-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="ba607-228">Форма может содержать разные элементы управления для ввода текста, например: текстовое поле, поле ввода пароля, переключатель, раскрывающийся список с единственным выбором или флажки множественного выбора.</span><span class="sxs-lookup"><span data-stu-id="ba607-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="ba607-229">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="ba607-229">*api.phonefactor*</span></span> | <span data-ttu-id="ba607-230">**Страница Многофакторной идентификации.**</span><span class="sxs-lookup"><span data-stu-id="ba607-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="ba607-231">Эта страница позволяет пользователю подтвердить свой номер телефона (с помощью SMS-сообщения или голосового вызова) во время регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="ba607-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="ba607-232">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="ba607-232">*api.selfasserted*</span></span> | <span data-ttu-id="ba607-233">**Страница регистрации учетной записи социальных сетей.**</span><span class="sxs-lookup"><span data-stu-id="ba607-233">**Social account sign-up page**.</span></span> <span data-ttu-id="ba607-234">Эта страница содержит форму регистрации, которую нужно заполнить при регистрации с использованием существующей учетной записи от таких поставщиков удостоверений социальных сетей, как Facebook или Google+.</span><span class="sxs-lookup"><span data-stu-id="ba607-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="ba607-235">Эта страница аналогична странице регистрации локальных учетных записей, за исключением полей для ввода пароля.</span><span class="sxs-lookup"><span data-stu-id="ba607-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="ba607-236">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="ba607-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="ba607-237">**Страница обновления профиля.**</span><span class="sxs-lookup"><span data-stu-id="ba607-237">**Profile update page**.</span></span> <span data-ttu-id="ba607-238">Эта страница содержит форму для обновления профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba607-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="ba607-239">Эта страница аналогична странице регистрации локальных учетных записей, за исключением полей для ввода пароля.</span><span class="sxs-lookup"><span data-stu-id="ba607-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="ba607-240">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="ba607-240">*api.signuporsignin*</span></span> | <span data-ttu-id="ba607-241">**Единая страница регистрации или входа.**</span><span class="sxs-lookup"><span data-stu-id="ba607-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="ba607-242">На этой странице обрабатываются данные для регистрации и входа пользователей, которые могут использовать поставщики удостоверений организаций, поставщики удостоверений социальных сетей, включая Facebook или Google+, или локальные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="ba607-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ba607-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba607-243">Next steps</span></span>

<span data-ttu-id="ba607-244">См. [справочное руководство по настройке пользовательского интерфейса для встроенных политик](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="ba607-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
