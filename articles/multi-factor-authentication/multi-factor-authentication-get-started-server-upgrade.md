---
title: "tooAzure PhoneFactor aaaUpgrade многофакторной проверки Подлинности сервера | Документы Microsoft"
description: "Начало работы с Azure многофакторной проверки Подлинности сервера, при обновлении от более старых phonefactor agent hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Обновление hello tooAzure PhoneFactor Agent многофакторной проверки подлинности сервера
tooupgrade hello PhoneFactor Agent версии 5.x или более старых tooAzure многофакторной проверки подлинности сервера, удалите агент PhoneFactor hello и сначала связано компонентов. Затем hello многофакторной проверки подлинности сервера и его компоненты могут быть установлены.

## <a name="uninstall-hello-phonefactor-agent"></a>Удалите PhoneFactor Agent hello

1. Во-первых создайте резервную копию файла данных PhoneFactor hello. расположение установки по умолчанию Hello — C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Если установлен пользовательский портал hello:
  1. Перейдите в папку установки toohello и сделайте резервную копию файла web.config hello. расположение установки по умолчанию Hello — C:\inetpub\wwwroot\PhoneFactor.

  2. При добавлении портала toohello пользовательские темы, создайте резервную копию пользовательской папки в каталоге C:\inetpub\wwwroot\PhoneFactor\App_Themes hello.

  3. Удаление hello пользовательский портал, либо с помощью hello PhoneFactor Agent (доступна, только если установлен на hello сервере hello PhoneFactor Agent) или с помощью программы и компоненты Windows.

3. Если устанавливается hello Mobile App Web Service:

  1. Перейдите в папку установки toohello и сделайте резервную копию файла web.config hello. расположение установки по умолчанию Hello — C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService.

  2. Удалите веб-служба мобильного приложения через программы и компоненты Windows hello.

4. Если hello Web Service SDK установлен, удалите его через hello PhoneFactor Agent или с помощью программы и компоненты Windows.

5. Удалите агент PhoneFactor с помощью программы и компоненты Windows hello.

## <a name="install-hello-multi-factor-authentication-server"></a>Установка hello многофакторной проверки подлинности сервера

Hello путь установки берется из реестра hello из предыдущей установки PhoneFactor Agent hello, поэтому его следует устанавливать в hello же расположение (например, C:\Program Files\PhoneFactor). В случае новой установки будет создан другой путь (например, C:\Program Files\Multi-Factor Authentication Server). Здравствуйте, файл данных, оставшийся hello предыдущего PhoneFactor агент должен быть обновлен во время установки, поэтому пользователи и параметры по-прежнему должно быть, что после установки hello новый сервер многофакторной проверки подлинности.

1. При появлении соответствующего запроса, активируйте hello многофакторной проверки подлинности сервера и убедитесь, что он назначен toohello правильной группе репликации.

2. Если ранее была установлена hello Web Service SDK, установка hello новый Web Service SDK через пользовательский интерфейс многофакторной проверки подлинности сервера hello.

  Здравствуйте, теперь имеет имя виртуального каталога по умолчанию **MultiFactorAuthWebServiceSdk** вместо **PhoneFactorWebServiceSdk**. Если требуется toouse hello предыдущее имя, необходимо изменить имя hello hello виртуального каталога во время установки. В противном случае — разрешить hello установки toouse hello новое имя по умолчанию, наличие toochange hello URL-адрес во всех приложениях, ссылка hello toopoint SDK веб-службы (такие как hello пользовательского портала и веб-служба мобильного приложения) hello правильное расположение.

3. Если установить пользовательский портал был ранее установлен на приветствия сервера агента PhoneFactor, приветствия hello новый портал многофакторной проверки подлинности пользователя через пользовательский интерфейс многофакторной проверки подлинности сервера hello.

  Здравствуйте, теперь имеет имя виртуального каталога по умолчанию **MultiFactorAuth** вместо **PhoneFactor**. Если требуется toouse hello предыдущее имя, необходимо изменить имя hello hello виртуального каталога во время установки. В противном случае если разрешить hello установки toouse hello новое имя по умолчанию, следует щелкните значок пользовательского портала hello hello многофакторной проверки подлинности сервера и обновите hello URL-адрес пользовательского портала на вкладке Параметры hello.

4. Если hello пользовательский портал или веб-служба мобильного приложения был ранее установлен на сервере, отличном от PhoneFactor Agent hello:

  1. Перейдите в папку установки toohello (например, C:\Program Files\PhoneFactor) и скопируйте один или несколько установщиков toohello другой сервер. Существуют 32-разрядных и 64-разрядные установщики для hello пользовательского портала и веб-служба мобильного приложения. Файлы имеют имена MultiFactorAuthenticationUserPortalSetupXX.msi и MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. hello tooinstall пользовательский портал на веб-сервере hello, откройте командную строку с правами администратора и запустите MultiFactorAuthenticationUserPortalSetupXX.msi.

    Здравствуйте, теперь имеет имя виртуального каталога по умолчанию **MultiFactorAuth** вместо **PhoneFactor**. Если требуется toouse hello предыдущее имя, необходимо изменить имя hello hello виртуального каталога во время установки. В противном случае если разрешить hello установки toouse hello новое имя по умолчанию, следует щелкните значок пользовательского портала hello hello многофакторной проверки подлинности сервера и обновите hello URL-адрес пользовательского портала на вкладке Параметры hello. Существующие пользователи должны toobe представление о hello новый URL-адрес.

  3. Перейдите в папку установки пользовательского портала toohello (например, C:\inetpub\wwwroot\MultiFactorAuth) и измените файл web.config hello. Скопируйте значения hello в hello разделов AppSetting и applicationSettings из исходного файла web.config, резервная копия перед обновлением hello в новый файл web.config hello. Если новое имя виртуального каталога по умолчанию hello было сохранено при установке hello Web Service SDK, измените hello URL-адрес в правильном расположении hello applicationSettings раздел toopoint toohello. Если все остальные значения по умолчанию были изменены в предыдущем файле web.config hello, применяются те же изменения toohello новый файл web.config.

  4. hello tooinstall веб-служба мобильного приложения на веб-сервере hello, откройте командную строку с правами администратора и запустите hello MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

    Здравствуйте, теперь имеет имя виртуального каталога по умолчанию **MultiFactorAuthMobileAppWebService** вместо **PhoneFactorPhoneAppWebService**. Если требуется toouse hello предыдущее имя, необходимо изменить имя hello hello виртуального каталога во время установки. Вы можете toochoose короткий toomake имя легко tootype конечных пользователей в мобильных устройствах. В противном случае если разрешить hello установки toouse hello новое имя по умолчанию, следует щелкните значок мобильного приложения hello в hello многофакторной проверки подлинности сервера и обновите hello URL веб-службы мобильного приложения.

  5. Перейдите в папку установки toohello веб-служба мобильного приложения (например, C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) и измените файл web.config hello. Скопируйте значения hello в hello разделов AppSetting и applicationSettings из исходного файла web.config, резервная копия перед обновлением hello в новый файл web.config hello. Если новое имя виртуального каталога по умолчанию hello было сохранено при установке hello Web Service SDK, измените hello URL-адрес в правильном расположении hello applicationSettings раздел toopoint toohello. Если все остальные значения по умолчанию были изменены в предыдущем файле web.config hello, применяются те же изменения toohello новый файл web.config.

## <a name="next-steps"></a>Дальнейшие действия

- [Установка портала пользователей hello](multi-factor-authentication-get-started-portal.md) для hello сервера Azure Multi-factor Authentication.

- [Настройте проверку подлинности Windows](multi-factor-authentication-get-started-server-windows.md) для приложений. 
