---
title: "aaaAzure AD v2 Windows Desktop начало работы — Настройка | Документы Microsoft"
description: "Здесь описывается, как классические приложения для Windows .NET (XAML) могут вызвать API, требующий маркеры доступа от конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="06a2a-103">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="06a2a-103">Set up your project</span></span>

<span data-ttu-id="06a2a-104">Этот раздел содержит пошаговые инструкции для toocreate нового toodemonstrate проекта как toointegrate .NET рабочего стола Windows приложение (XAML) с *вход с помощью Microsoft* , может обращаться к веб-API, который требует передачи маркера.</span><span class="sxs-lookup"><span data-stu-id="06a2a-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="06a2a-105">приложения Hello, созданным в этом руководстве предоставляет кнопки toograph и отображение результатов на экране и кнопку выхода.</span><span class="sxs-lookup"><span data-stu-id="06a2a-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="06a2a-106">Предпочтение toodownload проекта Visual Studio в этом примере вместо этого?</span><span class="sxs-lookup"><span data-stu-id="06a2a-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="06a2a-107">[Загрузка проекта](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="06a2a-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="06a2a-108">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="06a2a-108">Create your application</span></span>
1. <span data-ttu-id="06a2a-109">В Visual Studio выберите `File` > `New` > `Project`.</span><span class="sxs-lookup"><span data-stu-id="06a2a-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="06a2a-110">В разделе *Шаблоны* выберите `Visual C#`.</span><span class="sxs-lookup"><span data-stu-id="06a2a-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="06a2a-111">Выберите `WPF App` (или *приложение WPF* в зависимости от версии hello в Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="06a2a-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="06a2a-112">Добавление проекта tooyour hello библиотеки проверки подлинности Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="06a2a-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="06a2a-113">В Visual Studio выберите `Tools` > `Nuget Package Manager` > `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="06a2a-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="06a2a-114">Скопируйте и вставьте следующий hello в hello в окне консоли диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="06a2a-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="06a2a-115">пакет Hello выше устанавливает hello библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="06a2a-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="06a2a-116">MSAL обрабатывает получение, кэширование и обновление tooaccess пользователя toskens использовать интерфейсы API, защищенные Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="06a2a-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="06a2a-117">Добавление кода hello tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="06a2a-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="06a2a-118">Этот шаг поможет вам создать взаимодействие toohandle класса с библиотекой MSAL, такие как обработка токенов.</span><span class="sxs-lookup"><span data-stu-id="06a2a-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="06a2a-119">Откройте hello `App.xaml.cs` файл и добавьте ссылку hello для класса toohello MSAL библиотеки:</span><span class="sxs-lookup"><span data-stu-id="06a2a-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="06a2a-120">Обновите следующие toohello класса приложения hello:</span><span class="sxs-lookup"><span data-stu-id="06a2a-120">Update hello App class toohello following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="06a2a-121">Создание пользовательского интерфейса приложения</span><span class="sxs-lookup"><span data-stu-id="06a2a-121">Create your application’s UI</span></span>
<span data-ttu-id="06a2a-122">Hello ниже показано, как приложение может выполнять запросы с защищенным сервером как Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="06a2a-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="06a2a-123">Файл MainWindow.xaml должен создаваться автоматически как часть шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="06a2a-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="06a2a-124">Откройте этот файл, этот файл и следуйте приведенным ниже инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="06a2a-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="06a2a-125">Замена приложения `<Grid>` с быть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="06a2a-125">Replace your application’s `<Grid>` with be hello following:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
