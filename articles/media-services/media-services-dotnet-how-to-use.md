---
title: "aaaHow tooSet компьютеров для разработки служб мультимедиа с помощью .NET"
description: "Дополнительные сведения о предварительных требованиях hello для служб мультимедиа с помощью hello пакета SDK служб мультимедиа для .NET. Также узнаете, как toocreate приложения Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>Разработка служб мультимедиа с помощью .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

В этом разделе обсуждается, как toostart разработки Media Services приложений с помощью .NET.

Hello **Azure Media Services .NET SDK** библиотека позволяет tooprogram к службам мультимедиа с помощью .NET. Он даже проще toodevelop в .NET Framework, hello toomake **расширения SDK .NET служб мультимедиа Azure** предоставляется библиотеки. Эта библиотека содержит набор методов расширения и вспомогательные функции, упрощающие код .NET. Обе библиотеки доступны в **NuGet** и на **GitHub**.

## <a name="prerequisites"></a>Предварительные требования
* Учетная запись служб мультимедиа в новой или существующей подписке Azure. В разделе hello [как tooCreate учетную запись служб мультимедиа](media-services-portal-create-account.md).
* Операционные системы: Windows 10, Windows 7, Windows 2008 R2 или Windows 8.
* .NET Framework 4.5
* приведенному.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio
В этом разделе показано, как toocreate проекта в Visual Studio и настроить его для разработки служб мультимедиа.  В этом случае hello проект представляет собой консольное приложение C# Windows, но hello показанные здесь шаги установки применения tooother типов проектов, которые можно создать для приложений служб мультимедиа (например, приложение Windows Forms или веб-приложения ASP.NET).

В этом разделе показано, как toouse **NuGet** tooadd Media Services .NET SDK расширений и другие зависимые библиотеки.

Кроме того, можно получить последние Media Services .NET SDK bits hello GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) или [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), построить решение hello и добавить hello ссылки toohello клиентский проект. Все необходимые зависимости hello загружаются и извлекаются автоматически.

1. Создайте в Visual Studio консольное приложение C#. Введите hello **имя**, **расположение**, и **имя решения**, а затем нажмите кнопку ОК.
2. Выполните сборку решения hello.
3. Используйте **NuGet** tooinstall и добавьте **расширения SDK .NET служб мультимедиа Azure** (**windowsazure.mediaservices.extensions**). При установке этого пакета также устанавливается **пакет SDK служб мультимедиа для .NET** и добавляются все остальные необходимые зависимости.
   
    Убедитесь, что hello последняя версия NuGet установлен. Дополнительную информацию и инструкции по установке см. на сайте [NuGet](http://nuget.codeplex.com/).
4. В обозревателе решений щелкните правой кнопкой мыши имя проекта, hello hello и выберите Управление пакетами NuGet.
   
    Откроется диалоговое окно Управление пакетами NuGet Hello.
5. В коллекции hello сети, поиск расширения служб Azure, выберите расширения SDK .NET служб мультимедиа Azure и нажмите кнопку "установить" hello ".
   
    Hello проект будет изменен, ссылается на toohello расширения SDK .NET служб мультимедиа, Media Services .NET SDK и другие зависимые сборки добавляются.
6. toopromote очистки среды разработки, то можно попробовать включить восстановление пакетов NuGet. Дополнительную информацию см. в статье [Восстановление пакета NuGet](http://docs.nuget.org/consume/package-restore).
7. Добавьте ссылку на слишком**System.Configuration** сборки. Эта сборка содержит hello System.Configuration. **ConfigurationManager** класс, являющийся используется tooaccess файлы конфигурации (например, файл App.config).
   
    ссылки на tooadd, с помощью диалогового окна Управление ссылками hello, щелкните правой кнопкой мыши hello имя проекта в обозревателе решений hello. Выберите "Добавить ссылки".
   
    Откроется диалоговое окно Управление ссылками Hello.
8. В списке сборок платформы .NET framework найти выберите сборку System.Configuration hello и нажмите кнопку ОК.
9. Откройте файл App.config hello и добавьте *appSettings* файл toohello раздела.     
   
    Установить значения hello, необходимые tooconnect toohello API служб мультимедиа. Дополнительные сведения см. в разделе [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Если вы используете [проверки подлинности пользователя](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) файл конфигурации, скорее всего, будет иметь значение доменом клиента Azure AD и конечной точкой AMS API hello.
    
    >[!Important]
    >Большинство примеров кода в документации по службам мультимедиа Azure hello набора, используйте тип пользователя (интерактивные) toohello tooconnect проверки подлинности AMS API. Такой метод аутентификации неплохо работает для приложений управления или мониторинга на устройствах: мобильные приложения, приложения Windows и консольные приложения. Но он совершенно не пригоден для аутентификации приложений, работающих на серверах, в веб-службах или API-интерфейсах.  Дополнительные сведения см. в разделе [hello доступа AMS API с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Перезаписать существующую hello **с помощью** операторы в начале hello из файла Program.cs hello hello, следующий код.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

На этом этапе вы являются готов toostart разработки приложений служб мультимедиа.    

## <a name="example"></a>Пример

Ниже приведен небольшой пример, который подключается к toohello AMS API и перечислены все доступные процессоры носителя.
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>Дальнейшие действия

Теперь [подключении toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) и запустить [разработке](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

