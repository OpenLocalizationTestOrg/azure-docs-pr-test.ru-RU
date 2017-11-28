---
title: "Приступая к работе с Azure AD версии 2 для классического приложения для Windows. Настройка | Документация Майкрософт"
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
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="2f453-103">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="2f453-103">Set up your project</span></span>

<span data-ttu-id="2f453-104">В этом разделе содержатся пошаговые инструкции по созданию проекта, чтобы продемонстрировать, как интегрировать классическое приложение для Windows .NET (XAML) с *входом с учетной записью Майкрософт*, что позволит выполнять запрос к веб-API, требующим маркер.</span><span class="sxs-lookup"><span data-stu-id="2f453-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="2f453-105">Приложение, созданное в этом руководстве, предоставляет кнопку для графа, а также отображает результаты на экране и кнопку выхода.</span><span class="sxs-lookup"><span data-stu-id="2f453-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="2f453-106">Предпочитаете скачать этот пример проекта Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="2f453-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="2f453-107">[Скачайте проект](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) и перейдите к [настройке](#create-an-application-express), чтобы настроить пример кода перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="2f453-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="2f453-108">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="2f453-108">Create your application</span></span>
1. <span data-ttu-id="2f453-109">В Visual Studio выберите `File` > `New` > `Project`.</span><span class="sxs-lookup"><span data-stu-id="2f453-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="2f453-110">В разделе *Шаблоны* выберите `Visual C#`.</span><span class="sxs-lookup"><span data-stu-id="2f453-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="2f453-111">Выберите `WPF App` (или *приложение WPF* в зависимости от версии Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="2f453-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="2f453-112">Добавление библиотеки проверки подлинности Майкрософт (MSAL) в проект</span><span class="sxs-lookup"><span data-stu-id="2f453-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="2f453-113">В Visual Studio выберите `Tools` > `Nuget Package Manager` > `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="2f453-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="2f453-114">Скопируйте и вставьте следующий код в окне "Консоль диспетчера пакетов".</span><span class="sxs-lookup"><span data-stu-id="2f453-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="2f453-115">Приведенный выше пакет устанавливает библиотеку проверки подлинности Майкрософт (MSAL).</span><span class="sxs-lookup"><span data-stu-id="2f453-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="2f453-116">MSAL обрабатывает получение, кэширование и обновление маркеров пользователей, которые используются для доступа к API, защищенному конечной точкой Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="2f453-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="2f453-117">Добавление кода для инициализации MSAL</span><span class="sxs-lookup"><span data-stu-id="2f453-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="2f453-118">На этом шаге вы сможете создать класс для обработки взаимодействия с библиотекой MSAL, например обработки маркеров.</span><span class="sxs-lookup"><span data-stu-id="2f453-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="2f453-119">Откройте файл `App.xaml.cs` и добавьте справочник по библиотеке MSAL в класс:</span><span class="sxs-lookup"><span data-stu-id="2f453-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2f453-120">Обновите класс App следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2f453-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="2f453-121">Создание пользовательского интерфейса приложения</span><span class="sxs-lookup"><span data-stu-id="2f453-121">Create your application’s UI</span></span>
<span data-ttu-id="2f453-122">В разделе ниже описывается, как приложение может запрашивать защищенный внутренний сервер, например Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2f453-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="2f453-123">Файл MainWindow.xaml должен создаваться автоматически как часть шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="2f453-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="2f453-124">Откройте этот файл и выполните приведенные далее инструкции.</span><span class="sxs-lookup"><span data-stu-id="2f453-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="2f453-125">Вставьте в раздел `<Grid>` приложения следующий код:</span><span class="sxs-lookup"><span data-stu-id="2f453-125">Replace your application’s `<Grid>` with be the following:</span></span>

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
