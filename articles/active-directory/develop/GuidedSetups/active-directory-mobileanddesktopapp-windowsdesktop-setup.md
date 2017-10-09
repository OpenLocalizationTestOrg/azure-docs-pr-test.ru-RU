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
## <a name="set-up-your-project"></a>Настройка проекта

Этот раздел содержит пошаговые инструкции для toocreate нового toodemonstrate проекта как toointegrate .NET рабочего стола Windows приложение (XAML) с *вход с помощью Microsoft* , может обращаться к веб-API, который требует передачи маркера.

приложения Hello, созданным в этом руководстве предоставляет кнопки toograph и отображение результатов на экране и кнопку выхода.

> Предпочтение toodownload проекта Visual Studio в этом примере вместо этого? [Загрузка проекта](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.


### <a name="create-your-application"></a>Создание приложения
1. В Visual Studio выберите `File` > `New` > `Project`.<br/>
2. В разделе *Шаблоны* выберите `Visual C#`.
3. Выберите `WPF App` (или *приложение WPF* в зависимости от версии hello в Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Добавление проекта tooyour hello библиотеки проверки подлинности Microsoft (MSAL)
1. В Visual Studio выберите `Tools` > `Nuget Package Manager` > `Package Manager Console`.
2. Скопируйте и вставьте следующий hello в hello в окне консоли диспетчера пакетов:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> пакет Hello выше устанавливает hello библиотеки проверки подлинности Microsoft (MSAL). MSAL обрабатывает получение, кэширование и обновление tooaccess пользователя toskens использовать интерфейсы API, защищенные Azure Active Directory v2.

## <a name="add-hello-code-tooinitialize-msal"></a>Добавление кода hello tooinitialize MSAL
Этот шаг поможет вам создать взаимодействие toohandle класса с библиотекой MSAL, такие как обработка токенов.

1. Откройте hello `App.xaml.cs` файл и добавьте ссылку hello для класса toohello MSAL библиотеки:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Обновите следующие toohello класса приложения hello:
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

## <a name="create-your-applications-ui"></a>Создание пользовательского интерфейса приложения
Hello ниже показано, как приложение может выполнять запросы с защищенным сервером как Microsoft Graph. Файл MainWindow.xaml должен создаваться автоматически как часть шаблона проекта. Откройте этот файл, этот файл и следуйте приведенным ниже инструкциям hello:

Замена приложения `<Grid>` с быть hello следующее:

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
