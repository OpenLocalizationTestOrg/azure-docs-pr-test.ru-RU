---
title: "Azure Active Directory B2C: устранение неполадок в пользовательских политиках | Документация Майкрософт"
description: "Узнайте о подходах toosolving ошибок при работе с пользовательской политики в Azure Active Directory."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Устранение неполадок в пользовательских политиках Azure AD B2C и инфраструктуре процедур идентификации

При использовании Azure Active Directory B2C пользовательских политик (Azure AD B2C), могут возникнуть трудности, Настройка hello Identity Framework столкнуться в формате языка XML политики.  Настраиваемые политики toowrite обучения может отображаться как изучение нового языка. В этой статье вы ознакомитесь со средствами и подсказками, которые помогут вам быстро обнаружить и решить проблемы. 

> [!NOTE]
> Мы рассмотрим устранение неполадок, связанных с настройками пользовательских политик Azure AD B2C. Он не удовлетворяет hello проверяющей стороной приложений или библиотек его удостоверения.

## <a name="xml-editing"></a>Редактирование кода XML

Hello наиболее распространенных ошибок при установке пользовательских политик имеет неправильный формат XML. Вам нужен хороший редактор XML. Хороший редактор XML отображает XML в изначальном виде, помечает содержимое цветовыми кодами, предварительно заполняет общие термины, индексирует элементы XML и может проверять их по схеме. Мы предлагаем использовать следующие два редактора XML:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Notepad++](https://notepad-plus-plus.org/)

При проверке по схеме XML определяются ошибки перед отправкой XML-файла. В корневой папке hello пакета начального приветствия получите определения схемы XML hello TrustFrameworkPolicy_0.3.0.0.xsd. Дополнительные сведения содержатся в документации hello редактора XML, искать *XML-инструменты* и *проверки XML*.

Не будет лишним также ознакомиться с правилами XML. Azure AD B2C отклоняет любые обнаруженные ошибки форматирования. Иногда, если используется XML неправильного формата, могут появляться сообщения об ошибках, вводящие в заблуждение.

## <a name="upload-policies-and-policy-validation"></a>Передача политик и их проверка

 Проверка передачи XML-файла выполняется автоматически. Большинство ошибок вызвать toofail передачи hello. Проверка затрагивает файл политики hello, что вы отправляете. Он также включает hello цепочку файлов hello загруженный файл слишком ссылается (hello файл политики проверяющей стороной, hello расширения файла и базовый файл hello). 
 
 Распространенные ошибки проверки включают следующие hello.

Фрагмент кода ошибки: `... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Hello ClaimType значение может быть написано неправильно или не существует в схеме hello.
* ClaimType значения должны быть определены в хотя бы один из файлов hello в политике hello. 
    Например: ` <ClaimType Id="socialIdpUserId">`
* Если ClaimType определяется в файле расширения hello, но оно также используется в значении TechnicalProfile базовом файле hello, передача hello базового файла приводит к ошибке.

Фрагмент кода ошибки: `...makes a reference tooa ClaimsTransformation with id...`
* Здравствуйте причины для hello ошибки может быть hello таким же как и для hello ClaimType ошибки.

Фрагмент кода ошибки: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Проверьте, hello со значением TenantId в hello  **\<TrustFrameworkPolicy\>**  и  **\<BasePolicy\>**  элементов соответствует цели Azure AD B2C клиент.  

## <a name="troubleshoot-hello-runtime"></a>Устранение неполадок выполнения hello

* Используйте `Run Now` и `https://jwt.io` tootest политик независимо от веб-приложения или мобильные приложения. Этот веб-сайт работает как приложение проверяющей стороны. Он отображает содержимое hello hello JSON Web Token (JWT), созданные политикой Azure AD B2C. toocreate тестовое приложение, в удостоверение качества Framework hello используйте следующие значения:
    * Имя: TestApp.
    * Веб-приложение или веб-интерфейс API: нет.
    * Собственный клиент: нет.

* tootrace hello обмен сообщениями между браузера клиента и Azure AD B2C используйте [Fiddler](http://www.telerik.com/fiddler). Это позволит узнать, где в шагах оркестрации случился сбой пути взаимодействия пользователя.

* В **режим разработки**, используйте **Application Insights** tootrace hello действия позволят вам Identity Framework взаимодействие с пользователем. В **режим разработки**, можно наблюдать hello обмен утверждениями между hello Identity Framework качества и hello различные поставщики утверждений, определяемых технические профилей, как поставщики удостоверений, API-служб каталог пользователя Azure AD B2C Hello и другие службы, такие как Azure / Multi-factor-Authentication.  

## <a name="recommended-practices"></a>Рекомендации

**Храните нескольких версий своих сценариев. Группируйте их в проект со своим приложением.** Hello базы, расширения и проверяющей стороной файлы непосредственно зависят друг от друга. Сохраните их как группу. По мере добавления новых возможностей политики tooyour хранить отдельные рабочие версии. Рабочие версии рабочей области в своей собственной файловой системы с их взаимодействия с кодом приложения hello.  Приложения могут вызывать многие различные политики проверяющей стороны в клиенте. Они могут стать зависит hello утверждений, которые ожидают, что на основе политик Azure AD B2C.

**Разрабатывайте и тестируйте технические профили с известными путями взаимодействия пользователя.** Проверить использование начального пакет tooset политики вашей технической профилей. Прежде чем встраивать их в собственные пути взаимодействия пользователя, проверьте их по отдельности.

**Разрабатывайте и тестируйте пути взаимодействия пользователя с проверенными техническими профилями.** Добавочное изменение шагов orchestration hello пути пользователя. Прогрессивно создавайте целевые сценарии.

## <a name="next-steps"></a>Дальнейшие действия

* На портале GitHub Загрузите hello [active-directory-b2c-custom-policy-starterpack] (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) ZIP-файл.
