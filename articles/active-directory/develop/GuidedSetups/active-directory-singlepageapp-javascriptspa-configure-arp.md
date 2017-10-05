---
title: "Интерактивная настройка Azure AD версии 2 для приложений JS SPA — настройка (ARP) | Документация Майкрософт"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2 (ARP)."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="4a863-103">Добавление в приложение сведений о его регистрации</span><span class="sxs-lookup"><span data-stu-id="4a863-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="4a863-104">На этом шаге необходимо настроить URL-адрес перенаправления сведений о регистрации приложения, а затем добавить идентификатор приложения в одностраничное приложение JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4a863-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="4a863-105">Настройка URL-адреса перенаправления</span><span class="sxs-lookup"><span data-stu-id="4a863-105">Configure redirect URL</span></span>

<span data-ttu-id="4a863-106">Настройте указанное выше поле `Redirect URL`, используя URL-адрес страницы index.html на основе веб-сервера, а затем нажмите кнопку *Обновить*.</span><span class="sxs-lookup"><span data-stu-id="4a863-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="4a863-107">Инструкции Visual Studio для получения URL-адреса перенаправления</span><span class="sxs-lookup"><span data-stu-id="4a863-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="4a863-108">Чтобы получить URL-адрес перенаправления, следуйте инструкциям ниже.</span><span class="sxs-lookup"><span data-stu-id="4a863-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="4a863-109">В *обозревателе решений* выберите проект и просмотрите окно `Properties` (если окно свойств не отображается, нажмите клавишу `F4`).</span><span class="sxs-lookup"><span data-stu-id="4a863-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="4a863-110">Скопируйте значение `URL` в буфер обмена:</span><span class="sxs-lookup"><span data-stu-id="4a863-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="4a863-111">![Свойства проекта](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="4a863-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="4a863-112">Вставьте это значение в поле `Redirect URL` в верхней части этой страницы, а затем нажмите кнопку `Update`.</span><span class="sxs-lookup"><span data-stu-id="4a863-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="4a863-113">Настройка URL-адреса перенаправления для Python</span><span class="sxs-lookup"><span data-stu-id="4a863-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="4a863-114">Для Python можно задать порт веб-сервера через командную строку.</span><span class="sxs-lookup"><span data-stu-id="4a863-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="4a863-115">В этой интерактивной настройке в качестве примера используется порт 8080, но можно использовать любой другой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="4a863-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="4a863-116">Как бы то ни было, выполните инструкции ниже, чтобы настроить URL-адрес перенаправления в сведениях о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="4a863-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="4a863-117">В верхней части этой страницы выберите `http://localhost:8080/` в качестве `Redirect URL` или воспользуйтесь `http://localhost:[port]/`, если используете настраиваемый TCP-порт (где *[port]* — это номер настраиваемого TCP-порта), а затем нажмите кнопку "Обновить".</span><span class="sxs-lookup"><span data-stu-id="4a863-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="4a863-118">Настройка одностраничного приложения JavaScript</span><span class="sxs-lookup"><span data-stu-id="4a863-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="4a863-119">Создайте файл с именем `msalconfig.js`, в котором будут содержаться сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="4a863-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="4a863-120">Если вы работаете с Visual Studio, выберите проект (корневую папку проекта), щелкните правой кнопкой мыши и выберите `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="4a863-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="4a863-121">Назовите класс `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="4a863-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="4a863-122">Добавьте в файл `msalconfig.js` следующий код:</span><span class="sxs-lookup"><span data-stu-id="4a863-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
