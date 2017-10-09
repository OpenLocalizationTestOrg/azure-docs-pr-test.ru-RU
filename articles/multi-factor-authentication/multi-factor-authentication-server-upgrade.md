---
title: "обновление сервера многофакторной проверки Подлинности aaaAzure | Документы Microsoft"
description: "Шаги и рекомендации tooupgrade hello сервера Azure Multi-factor Authentication tooa новой версии."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Обновление toohello последнего Azure многофакторной проверки подлинности сервера

В этой статье рассматриваются hello процесса обновления сервера Azure Multi-factor Authentication (MFA) версии 6.0 или более поздней версии. Если вам требуется tooupgrade старой версии hello PhoneFactor Agent, см. слишком[обновления hello tooAzure PhoneFactor Agent многофакторной проверки подлинности сервера](multi-factor-authentication-get-started-server-upgrade.md).

Если вы обновления с v6.x или toov7.x старую или более поздней версии, все компоненты измените с .NET 2.0 too.NET 4.5. Для всех компонентов также требуется распространяемый компонент Microsoft Visual C++ 2015, обновление 1 или более поздней версии. Hello многофакторной проверки Подлинности сервера установщик устанавливает обе hello x86- и x64 версии этих компонентов, если они еще не установлены. Если hello пользовательского портала и веб-служба мобильного приложения работают на разных серверах, необходимо tooinstall эти пакеты перед установкой этих компонентов. Можно выполнить поиск последнее обновление Visual C++ 2015 распространяемый компонент Microsoft hello на hello [центра загрузки Майкрософт](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Установить последнюю версию сервера Azure MFA hello

1. Используйте инструкции hello в [hello загрузки сервера Azure Multi-factor Authentication](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello hello Azure многофакторной проверки Подлинности сервера в последнюю версию.
2. Создайте резервную копию файла данных сервера многофакторной проверки Подлинности hello, расположенный в C:\Program Files\Multi-Factor Authentication Server\Data\PhoneFactor.pfdata (если предполагается, что hello каталог установки по умолчанию) на главном сервере многофакторной проверки Подлинности.
3. Если выполняется несколько серверов для обеспечения высокой доступности, измените hello клиентских систем, которые проходят проверку подлинности toohello многофакторной проверки Подлинности сервера, чтобы они останавливали отправки трафика toohello серверов, для обновления. При использовании подсистемы балансировки нагрузки, удалите многофакторной проверки Подлинности сервера из балансировки нагрузки hello, hello обновления и затем добавить сервер hello обратно в ферму hello.
4. Запустите установщик новый hello на каждом сервере многофакторной проверки Подлинности. Сначала обновите подчиненные серверы, так как они смогут прочесть hello реплицируются в главный hello старого файла данных. 

  Необязательно toouninstall к текущему серверу многофакторной проверки Подлинности, прежде чем выполнение установщика hello. Установщик Hello выполняет обновление на месте. Hello путь установки берется из реестра hello из предыдущей установки hello, поэтому устанавливается в hello же расположение (например, C:\Program Files\Multi-Factor Authentication Server). 
  
5. Если вы запрашиваемые tooinstall Microsoft Visual C++ 2015 с обновлением распространяемый пакет пакета напоминание hello. Установлены обе версии x86- и x64 hello hello пакета.
5. Если вы используете hello Web Service SDK, будет предложено tooinstall hello новый Web Service SDK. При установке Здравствуйте новый SDK веб-службы, убедитесь, что имя виртуального каталога, hello соответствует hello ранее установленные виртуальный каталог (например, MultiFactorAuthWebServiceSdk).
6. Повторите шаги hello на все подчиненные серверы. Повысить уровень одного из нового образца hello toobe hello подчиненных объектов, а затем обновления hello старого главного сервера. 

## <a name="upgrade-hello-user-portal"></a>Обновление hello пользовательского портала

1. Создайте резервную копию файла web.config hello в виртуальный каталог hello hello расположение установки пользовательского портала (например, C:\inetpub\wwwroot\MultiFactorAuth). Если тема по умолчанию toohello были сделаны изменения, создайте резервную копию папки App_Themes\Default hello также. Лучше toocreate копию папки по умолчанию hello и создать новую тему, чем toochange тему по умолчанию hello.
2. Если hello пользовательский портал работает на одном сервере как hello другие компоненты многофакторной проверки Подлинности сервера hello hello установки многофакторной проверки Подлинности сервера отобразится tooupdate hello пользовательского портала. Напоминание hello и установите обновление hello пользовательского портала. Убедитесь, что имя виртуального каталога, hello соответствует hello ранее установленные виртуальный каталог (например, MultiFactorAuth).
3. Если hello пользовательского портала на отдельном сервере, копировать файл MultiFactorAuthenticationUserPortalSetup64.msi hello из hello расположение одного hello многофакторной проверки Подлинности серверов установки и сохраните его на веб-сервере пользовательского портала hello. Запустите установщик hello. 

  При возникновении ошибки сообщение о, «Microsoft Visual C++ 2015 распространяемый пакет обновления 1 или более поздней версии требуется,» загрузить и установить последний пакет обновления для hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/). Установка обеих версий x86- и x64 hello.

4. После обновления программного обеспечения установлен пользовательский портал hello Сравните web.config hello резервного копирования, сделанных в шаге 1 со hello новый файл web.config. Если новые атрибуты отсутствуют в файле web.config новый hello, скопируйте файл web.config резервного копирования в hello виртуальный каталог toooverwrite hello новый. Другой вариант — toocopy и вставки hello appSettings значения и hello URL веб-службы SDK из файла резервной копии hello в новый файл web.config hello.

Если у вас есть hello пользовательского портала на нескольких серверах, повторите установку hello на всех из них. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Обновление веб-служба мобильного приложения hello

1. Создайте резервную копию файла web.config hello, который находится в виртуальный каталог hello hello расположение установки веб-служба мобильного приложения (например, C:\inetpub\wwwroot\app или C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Копировать файл MultiFactorAuthenticationMobileAppWebServiceSetup64.msi hello из hello размещение hello многофакторной проверки Подлинности серверов и поместить его в hello мобильное приложение регистрации веб-сервера.
3. Запустите установщик hello. 

  Если возникает ошибка, о том, что требуется Microsoft Visual C++ 2015 распространяемый пакет обновления 1 или более поздней версии, загрузите и установите последний пакет обновления для hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/). Установка обеих версий x86- и x64 hello.

4. После установки программного обеспечения веб-служба мобильного приложения hello обновлены Сравните файл web.config hello архивов, созданных на шаге 1, с новым файлом web.config hello. Если новые атрибуты отсутствуют в файле web.config новый hello, можно скопировать сохраненного файла web.config обратно в виртуальный каталог hello и перезаписать hello новый. Другой вариант — toocopy и вставки hello appSettings значения и hello URL веб-службы SDK из файла резервной копии hello в новый файл web.config hello.

Если у вас есть hello веб-служба мобильного приложения на нескольких серверах, повторите установку hello на всех из них. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Обновление hello адаптера AD FS


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Если MFA и службы AD FS работают на разных серверах

Эти инструкции применяются только в том случае, если сервер Многофакторной идентификации используется отдельно от серверов AD FS. Если обе службы работают hello серверы, пропустите этот раздел и перейти toohello действия по установке. 

1. Сохранить копию hello файл MultiFactorAuthenticationAdfsAdapter.config, который был зарегистрирован в Службах федерации Active Directory или экспортировать конфигурацию hello, используя следующую команду PowerShell hello: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. имя адаптера Hello — «WindowsAzureMultiFactorAuthentication» или «AzureMfaServerAuthentication» в зависимости от ранее установленной версии hello.
2. Скопируйте следующие файлы из серверов hello Server многофакторной проверки Подлинности установки расположение toohello AD FS hello:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Измените скрипт hello Register-MultiFactorAuthenticationAdfsAdapter.ps1, добавив `-ConfigurationFilePath [path]` toohello конец hello `Register-AdfsAuthenticationProvider` команды. Замените *[путь]* с toohello полный путь hello MultiFactorAuthenticationAdfsAdapter.config файл или файл конфигурации hello экспортируются в предыдущем шаге hello. 

  Проверьте атрибуты hello в новый MultiFactorAuthenticationAdfsAdapter.config toosee hello, если они соответствуют hello старый файл конфигурации. Если какие-либо атрибуты были добавлены или удалены в новой версии hello, скопируйте значения атрибутов hello из файла toohello hello старой конфигурации нового или изменения hello старой конфигурации файла toomatch.

### <a name="install-new-ad-fs-adapters"></a>Установка новых AD FS-адаптеров

> [!IMPORTANT] 
> Пользователям не будет обязательным tooperform двухшаговую проверку во время действия 3 – 8 этого раздела. При наличии AD FS, настроенный в несколько кластеров, можно удалить, обновления и восстановления каждого кластера в hello фермы независимо от hello простоя tooavoid других кластеров.

1. Удалите некоторые серверы AD FS из фермы hello. Обновите эти серверы при приветствия другие ВМ продолжают работать.
2. Установите новый адаптер AD FS hello на каждом сервере, удалены из фермы hello AD FS. Hello многофакторной проверки Подлинности сервера установлена на каждом сервере AD FS, можно изменить, если через Здравствуйте, администратор сервера MFA UI. Если нет, то выполните обновление, запустив файл MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  При возникновении ошибки сообщение о, «Microsoft Visual C++ 2015 распространяемый пакет обновления 1 или более поздней версии требуется,» загрузить и установить последний пакет обновления для hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/). Установка обеих версий x86- и x64 hello.

3. Go слишком**AD FS** > **политики проверки подлинности** > **изменение глобальной политики проверки подлинности многофакторный**. Снимите флажок **WindowsAzureMultiFactorAuthentication** или **AzureMFAServerAuthentication** (в зависимости от hello текущей установленной версии). 

  По завершении этого шага двухфакторная проверка подлинности через сервер Mногофакторной идентификации станет доступна в этом кластере AD FS, пока вы не выполните шаг 8.

4. Отменить регистрацию hello старую версию адаптера hello AD FS путем выполнения сценария PowerShell Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 hello. Убедитесь, что hello *-имя* параметр («WindowsAzureMultiFactorAuthentication» или «AzureMFAServerAuthentication») соответствует hello имя, которое отображается на шаге 3. Это относится tooall серверы в кластере hello же AD FS, так как нет центральная база данных конфигурации.
5. Зарегистрируйте новый адаптер AD FS hello путем выполнения сценария PowerShell Register-MultiFactorAuthenticationAdfsAdapter.ps1 hello. Это относится tooall серверы в кластере hello же AD FS, так как нет центральная база данных конфигурации.
6. Hello перезапуск службы AD FS на каждом сервере удалены из hello фермы AD FS.
7. Добавьте серверы hello обновлены резервное фермы toohello AD FS и удалить hello других серверов из фермы hello.
8. Go слишком**AD FS** > **политики проверки подлинности** > **изменение глобальной политики проверки подлинности многофакторный**. Установите флажок **AzureMfaServerAuthentication**.
9. Повторите шаг 2 tooupdate hello серверы удален из фермы hello AD FS и перезапустите службу hello AD FS на этих серверах.
10. Добавьте эти серверы в ферме AD FS hello.

## <a name="next-steps"></a>Дальнейшие действия

- Ознакомьтесь с примерами, приведенными в статье [Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN-решений сторонних поставщиков](multi-factor-authentication-advanced-vpn-configurations.md).

- [Интеграция каталогов между сервером Azure Multi-Factor Authentication и Active Directory](multi-factor-authentication-get-started-server-dirint.md).

- Настройте для своих приложений проверку подлинности Windows, как описано в статье [Проверка подлинности Windows и сервер Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server-windows.md).
