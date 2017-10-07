---
title: "aaaUse .NET Core в веб-приложения на платформе Linux | Документы Microsoft"
description: "Использование .NET Core в веб-приложении на платформе Linux."
keywords: "служба приложений azure, веб-приложение, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>Использование .NET Core в веб-приложении Azure на платформе Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Веб-приложение](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) в Linux предоставляет высокомасштабируемых, самостоятельно исправления веб-службы размещения, в операционной системе Linux на hello. Этот учебник содержит пошаговые инструкции, которые отображаются как toocreate [.NET Core](https://docs.microsoft.com/aspnet/core/) приложения на веб-приложение Azure в Linux. 

![Веб-приложения на платформе Linux][10]

Выполните действия hello ниже, с помощью компьютером Mac, Windows или Linux.

## <a name="prerequisites"></a>Предварительные требования ##

toocomplete этого учебника: 

* Установка hello [пакета SDK для .NET Core](https://www.microsoft.com/net/download/core).
* Установите [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Создание локального приложения .NET Core ##

Запустите новый сеанс терминала. Создайте каталог с именем `hellodotnetcore`и изменить текущий каталог tooit hello. Затем введите hello следующее: 

```
dotnet new web
``` 

  Эта команда создает три файла (*hellodotnetcore.csproj*, *Program.cs*, и *файла Startup.cs*) и одну пустую папку (*wwwroot /*) в текущем каталоге hello. содержимое Hello `.csproj` файл должен выглядеть hello следующим образом: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Так как это приложение является веб-приложение, tooan ссылку, ASP.NET Core пакет был автоматически добавлен toohello *hellodotnetcore.csproj* файла. номер версии пакета hello Hello задается в соответствии с выбранной framework toohello. В этом примере используется ссылка на ASP.NET Core версии 1.1.2, так как используется .NET Core 1.1.

## <a name="build-and-test-hello-application-locally"></a>Построение и тестирование приложения hello локально ##

Можно построить и запустить приложение .NET Core с hello `dotnet restore` команды следуют hello `dotnet run` команды, как показано ниже:

```
dotnet restore
dotnet run
```


При запуске приложения hello, будет выведено сообщение о том, что приложение hello прослушивает tooincoming запросы по порту. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Протестируйте его путем просмотра слишком`http://localhost:5000/` с браузером. Если все работает правильно, вы увидите сообщение "Hello World!" текст hello результат.

![Тестирование с помощью браузера][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Создать приложение .NET Core на портале Azure hello ##

Во-первых, требуется toocreate пустой веб-приложение. Войдите в toohello [портал Azure](https://portal.azure.com/) и создайте новый [веб-приложения на платформе Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Создание веб-приложения][1]

Здравствуйте, когда **создать** откроется страница, содержат сведения о веб-приложения:

![Выбор стека времени выполнения .NET Core][2]

Используйте следующие hello таблицы как руководство toofill out hello **создать** , а затем выберите **ОК** и **создать** toocreate приложение hello.

| Настройка      | Рекомендуемое значение  | Описание                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| Имя приложения. | hellodotnetcore  | Имя приложения Hello. Это имя должно быть уникальным. |
| Подписки | Выберите существующую подписку. | Здравствуйте, подписки Azure. |
| Группа ресурсов | myResourceGroup |  Hello Azure ресурсов группы toocontain hello веб-приложения. |
| План обслуживания приложения | Имя существующего плана службы приложений. |  Здравствуйте, план служб приложений.  |
| Настроить контейнер | .NET Core 1.1 | Здравствуйте, тип контейнера для этого веб-приложения: встроенные, Docker или частного реестра. |
| Источник образа  | Встроены  |  Источник Hello hello изображения. |
| Стек времени выполнения  | .NET Core 1.1  | стек времени выполнения Hello и версии.  |

## <a name="deploy-your-application-via-git"></a>Развертывание приложения с помощью Git ##

Используйте Git toodeploy hello приложения .NET Core tooAzure приложения службы веб-приложения на платформе Linux.

Hello новый веб-приложение Azure уже настроена развертывания Git. URL-адрес развертывания hello Git можно найти, перейдя по toohello следующий URL-адрес после вставки имя вашего веб-приложения:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Hello URL-адрес Git имеет следующие формы, основанной на имя вашего веб-приложения hello.

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Выполните следующие команды toodeploy hello локальное приложение tooyour веб-приложение Azure hello. 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

Не требуется toopush файлами внутри *bin /* или *obj или* каталоги, так как ваше приложение построено в облаке hello при hello приложения исходные файлы помещаются в стек tooAzure. После завершения процесса построения hello двоичные файлы копируются в каталог приложения hello в */home/сайт/wwwroot/*.

Убедитесь, что операции удаленного развертывания hello сообщать об успехе. Принудительной операции может занять некоторое время с момента разрешения пакет и выполняются в облаке hello процесса построения. Вы увидите несколько сообщений о состоянии, включая сообщения о том, что файлы были скопированы. Hello вывод должен выглядеть примерно toohello следующее:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

После завершения развертывания hello, перезапустите веб-приложения для эффекта tootake hello развертывания. toodo это, перейдите на портал Azure toohello и перейдите toohello **Обзор** страницы веб-приложения. Выберите hello **перезапустите** кнопки странице приветствия. Когда появится всплывающее окно отображается, выберите **Да** tooconfirm. Затем можно будет перейти к своему веб-приложению, как показано ниже.

![Обзор .NET Core развернуто приложение tooAzure службы приложений на платформе Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Дальнейшие действия
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
