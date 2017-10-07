---
title: "Установка aaaProblem hello соединитель агента прокси приложения | Документы Microsoft"
description: "Как tootroubleshoot проблемы вы может hello лицевой стороны, при установке соединителя агента прокси-сервера приложений"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Проблемы с установкой hello соединитель агента прокси приложения

Microsoft AAD Application Proxy Connector — это компонент внутреннего домена, который использует подключение hello tooestablish исходящие подключения из внутреннего домена доступную конечную точку облака toohello hello.

## <a name="general-problem-areas-with-connector-installation"></a>Общие проблемные области при установке соединителя

При сбое установки hello соединителя, hello корневой причиной обычно является одним из следующих областей hello:

1.  **Подключение** — toocomplete успешной установке hello tooregister потребностей нового соединителя и устанавливать свойства будущих отношений доверия. Это делается путем подключения toohello облачной службы прокси приложения AAD.

2.  **Установление доверия** — новый соединитель hello создает самозаверяющий сертификат и регистрирует toohello облачной службы.

3.  **Проверка подлинности Здравствуйте, администратор** — во время установки hello пользователь должен предоставить учетные данные администратора установки соединителя toocomplete hello.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Проверка подключения toohello прокси приложения облачной службы и страницы входа Microsoft

**Цель:** проверки возможности подключения этого компьютера соединителя hello toohello конечной точке регистрации прокси-сервер приложения AAD, а также страницы входа Microsoft.

1.  Откройте браузер и перейдите toohello, следующие веб-страницы: <https://aadap-portcheck.connectorporttest.msappproxy.net> и убедитесь, что tooCentral подключения hello США и работа Восток США центрах обработки данных с портами 9090 и 9091.

2.  Если любой из этих портов не обнаруживаются (нет зеленым флажком), убедитесь, что hello брандмауэра или прокси-сервера базы данных имеет \*. msappproxy.net с портами 9090 и 9091 правильно определен.

3.  Откройте браузер (вкладка «отдельный») и перейдите toohello следующие веб-страницы: <https://login.microsoftonline.com>, убедитесь в том, что можно выполнить вход toothat страницы.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Проверка того, поддерживают ли внутренние компоненты и компьютер сертификат доверия прокси приложения

**Цель:** убедитесь, что соединитель машины hello, внутреннего прокси-сервера и брандмауэра поддерживает hello сертификат, созданный соединитель hello для будущих отношений доверия.

>[!NOTE]
>Соединитель Hello предпринимает toocreate cert SHA512, который поддерживается модулем TLS1.2. Если машины hello или hello серверный брандмауэр и прокси-сервера не поддерживает TLS1.2, сбой установки hello.
>
>

**проблема tooresolve hello.**

1.  Проверьте TLS1.2 поддерживает hello компьютер — все версии Windows после 2012 R2 следует поддерживают TLS 1.2. Ли соединитель компьютере версии 2012 R2 или prior, убедитесь в том, что hello статьи базы знаний установлена на машине hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Обратитесь к администратору сети и попросите tooverify что hello внутреннего прокси-сервера и брандмауэра не блокируют SHA512 для исходящего трафика.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Убедитесь, что администратор соединителя используется tooinstall hello

**Цель:** убедитесь hello пользователя, который пытается tooinstall hello соединитель является администратором с правильными учетными данными. В настоящее время hello пользователь должен быть глобальным администратором для установки toosucceed hello.

**используются правильные учетные данные tooverify hello:**

Подключение слишком<https://login.microsoftonline.com> и использование hello одинаковые учетные данные. Убедитесь, что hello вход выполнен успешно. Роль пользователя hello можно проверить, происходит слишком**Azure Active Directory**  - &gt; **пользователей и групп**  - &gt; **всех пользователей**. 

Выберите учетную запись пользователя, а затем «роли каталога» в итоговом меню hello. Убедитесь что hello выбранную роль «Глобальный администратор». Если не удается tooaccess любой hello страницы вместе эти действия, вы не глобального администратора.

## <a name="next-steps"></a>Дальнейшие действия
[Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md)
