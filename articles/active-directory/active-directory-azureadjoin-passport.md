---
title: "aaaAuthenticating удостоверений без паролей в Windows Hello для бизнеса и Azure AD | Документы Microsoft"
description: "Обзор Windows Hello для бизнеса и дополнительные сведения о реализации этого метода."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Проверка подлинности удостоверений без использования паролей с помощью Windows Hello для бизнеса
Hello текущего метода проверки подлинности с помощью паролей сама по себе не являются достаточно tookeep пользователям безопасно. Пользователи имеют тенденцию менять пароли и забывать их. Пароли являются breachable, phishable, подвержен toocracks и угадываемых. Они также могут получить трудно tooremember и tooattacks ошибкам, например «[передачи хэш hello](https://technet.microsoft.com/dn785092.aspx)».

## <a name="about-windows-hello-for-business"></a>Информация о Windows Hello для бизнеса
Windows Hello для бизнеса — это метод проверки подлинности на основе открытых/закрытых ключей и сертификатов для организаций и потребителей, обеспечивающий более надежную защиту, чем пароли. Эта форма проверки подлинности использует учетные данные пары ключей, паролей и устойчивость toobreaches и краж и фишинга.

 Windows Hello для бизнеса позволяет пользователю выполнять проверку подлинности учетной записи Майкрософт tooa, учетной записи Windows Server Active Directory, учетную запись Microsoft Azure Active Directory (Azure AD) или службы сторонних разработчиков, которая поддерживает проверки подлинности быстрого удостоверение Online (FIDO). После первоначальной двухшаговую проверку во время Windows Hello для бизнеса регистрации Windows Hello для бизнеса установлен на устройстве пользователя hello и hello пользователь задает жестов, который может быть Windows Hello или ПИН-код. предоставленные пользователем Hello tooverify жестов hello учетных данных. Затем Windows использует Windows Hello для бизнеса tooauthenticate hello пользователя и помогают им tooaccess защищенных ресурсов и служб.

закрытый ключ Hello доступны только через «жест пользователя» как ПИН-код, биометрические данные или удаленном устройстве как hello пользователя смарт-карты использует toosign в toohello устройства. Эта информация является связанного tooa сертификата или асимметричного пару ключей. закрытый ключ Hello, оборудования, attested при наличии устройства hello микросхема доверенного платформенного модуля (TPM). Hello закрытый ключ никогда не покидает устройство hello.

открытый ключ Hello зарегистрирован в Azure Active Directory и Windows Server Active Directory (для локальной). Поставщики удостоверений (IDPs) проверьте пользователя hello, сопоставление hello открытого ключа hello пользователя toohello закрытого ключа и предоставления сведений о входе через один раз пароля (OTP), PhoneFactor или механизм различных уведомлений.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Преимущества внедрения Windows Hello для бизнеса для предприятий
Используя Windows Hello для бизнеса, предприятия могут обеспечить более надежную защиту своих ресурсов за счет следующего:

* Настройка Windows Hello для бизнеса с использованием предпочитаемого варианта оборудования. (это означает, что ключи будут создаваться на базе TPM 1.2 или TPM 2.0 при наличии. Если он недоступен, программное обеспечение будет создан раздел hello.
* Определение hello сложности и длительности hello ПИН-код и включена ли использование Hello в вашей организации.
* Настройка Windows Hello для бизнес-сценариев, toosupport как смарт-карты с помощью отношения доверия на основе сертификатов.

## <a name="how-windows-hello-for-business-works"></a>Работа с Windows Hello для бизнеса
1. Ключи создаются на оборудовании hello доверенного платформенного МОДУЛЯ или программным путем. Многие устройства имеют встроенные микросхемы TPM, обеспечивающую безопасность hello оборудования благодаря интеграции ключи шифрования устройства. Доверенный платформенный модуль версии 1.2 или 2.0 создает ключи или сертификаты, созданные на основе ключей создается hello.
2. Hello доверенного платформенного МОДУЛЯ подтверждает эти ключи привязкой оборудования.
3. Жест один unlock разблокирует hello устройства. Этот жест позволяет получать доступ к ресурсам toomultiple Если hello устройств, присоединенных к домену или Azure присоединенных к AD.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Как работает hello Windows Hello для бизнеса жизненного цикла
![Жизненный цикл Windows Hello для бизнеса](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Hello предыдущей схеме показаны ключа пары закрытого и открытого hello и проверки hello поставщиком удостоверений hello. Каждое из этих действий подробно рассмотрено ниже.

1. Hello пользователь подтверждает свою подлинность через несколько встроенных проверки методов (жесты, физических смарт-карт, многофакторная проверка подлинности) и отправляет этот tooan сведения поставщика удостоверений (IDP) как Azure Active Directory или локальной Active Directory.
2. устройство Hello затем создает ключ hello, подтверждает ключ hello, принимает hello открытую часть этого раздела, связывает его с помощью инструкций станции, входит в и отправляет его ключ hello tooregister toohello поставщика Удостоверений.
3. Как только hello поставщика Удостоверений регистрирует hello открытую часть ключа hello, проблемы hello поставщика Удостоверений hello toosign устройства с hello закрытую часть ключа hello.
4. затем проверяет Hello поставщика Удостоверений и проблемы hello токена проверки подлинности, позволяющий пользователю hello и hello защищенный доступ к ресурсам для hello устройства. IDPs можно написать кросс платформенные приложения или использовать браузер toocreate поддержки (через API-интерфейсов JavaScript/Webcrypto) и использовать Windows Hello для бизнеса учетные данные для своих пользователей.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Здравствуйте, требования к развертыванию для Windows Hello для бизнеса
### <a name="at-hello-enterprise-level"></a>На уровне предприятия hello
* Hello enterprise имеет подписку Azure.

### <a name="at-hello-user-level"></a>На уровне пользователя hello
* Hello пользователя компьютера Windows 10 Professional или Enterprise.

Подробные указания по развертыванию, в разделе [включить Windows Hello для бизнеса в организации hello](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Дополнительная информация
* [Windows 10 для предприятия hello: способов toouse устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md)
* [Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)

