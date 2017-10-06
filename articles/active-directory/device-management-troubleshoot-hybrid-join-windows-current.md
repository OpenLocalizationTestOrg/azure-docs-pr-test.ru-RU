---
title: "Windows 10 и Windows Server 2016 устройств, присоединенных к aaaTroubleshooting гибридной Azure Active Directory | Документы Microsoft"
description: "Устранение неполадок на устройствах под управлением Windows 10 и Windows Server 2016 с гибридным присоединением к Azure Active Directory ."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Устранение неполадок на устройствах под управлением Windows 10 и Windows Server 2016 с гибридным присоединением к Azure Active Directory 

Этот раздел является применимо toohello следующих клиентов:

-   Windows 10
-   Windows Server 2016

Сведения о других клиентах Windows см. в статье [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md) (Устранение неполадок на устройствах нижнего уровня с гибридным присоединением к Azure Active Directory).

В этом разделе предполагается, что [устройств, присоединенных к настроенным гибридной Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello следующие сценарии:

- Условный доступ на основе устройств

- [Корпоративное перемещение параметров](active-directory-windows-enterprise-state-roaming-overview.md)

- [Настройка Windows Hello для бизнеса](active-directory-azureadjoin-passport-deployment.md)


В этом документе приведены инструкции по устранению как tooresolve потенциальные проблемы. 


Для Windows 10 и Windows Server 2016, с помощью гибридного hello поддерживает соединения Azure Active Directory Windows 10 ноября 2015 г. обновление и более поздних версий. Мы рекомендуем использовать hello окончания действия обновления.

## <a name="step-1-retrieve-hello-join-status"></a>Шаг 1: Получить состояние соединения hello 

**состояние соединения hello tooretrieve:**

1. Привет открыть командную строку с правами администратора

2. Введите **dsregcmd/status**.



    +----------------------------------------------------------------------+
    | Состояние устройства                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Не DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 отпечаток: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected поставщик криптографии Microsoft Platform: Да KeySignTest:: необходимо выполнить с повышенными привилегиями tootest.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | Состояние пользователя                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>Шаг 2: Оценка hello состояние соединения 

Просмотрите следующие поля hello и убедитесь в том, что они имеют hello ожидаемые значения:

### <a name="azureadjoined--yes"></a>AzureAdJoined: YES  

Это поле указывает, присоединен ли hello устройства в Azure AD. Если значение hello **нет**, hello tooAzure соединения AD еще не завершен. 

**Возможные причины:**

- Ошибка проверки подлинности компьютера hello для соединения.

- Есть прокси-сервер HTTP hello организации, которые не могут быть обнаружены на компьютере hello

- для регистрации компьютера Hello не могут достичь tooauthenticate Azure AD или Azure DRS

- Hello компьютер может быть hello внутренней сети организации или VPN с tooan прямая линия видимости локального контроллера домена AD.

- Если hello компьютера доверенным платформенным Модулем, он может быть в неверном состоянии.

- Может быть неправильной конфигурации в службах hello отмечалось в документе hello, которые понадобятся tooverify еще раз. Ниже приведены распространенные примеры.

    - На сервере федерации нет включенных конечных точек WS-Trust.

    - На сервере федерации может быть запрещена входящая аутентификация компьютеров в сети с использованием встроенной проверки подлинности Windows.

    - Нет объекта точки подключения службы, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello

---

### <a name="domainjoined--yes"></a>DomainJoined: YES  

Это поле указывает ли hello устройство присоединено tooan локальной Active Directory или нет. Если значение hello **нет**, hello устройства не может выполнить соединение гибридной Azure AD.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: NO  

Это поле указывает, зарегистрировано ли устройство hello в Azure AD в качестве персонального устройства (помечен как *присоединено к рабочему месту*). Этот параметр должен иметь значение **NO** для присоединенных к домену компьютеров, на которых также настроено гибридное присоединение к Azure AD. Если значение hello **Да**, рабочей или учебной учетной записи был добавлен завершения предыдущего toohello соединения hello гибридной Azure AD. В этом случае hello учетной записи учитывается при использовании версии hello Юбилейного обновления Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: YES и AzureADPrt: YES
  
Эти поля указывают, является ли пользователь hello успешно проверку подлинности tooAzure AD при входе в toohello устройства. Если значения hello **нет**, может быть вызвано:

- Ключ хранилища неправильный (STK) в доверенный платформенный модуль, связанный с hello устройства при регистрации (hello проверка KeySignTest во время работы с повышенными правами).

- Наличие альтернативного имени пользователя.

- Прокси-сервер HTTP не найден.

## <a name="next-steps"></a>Дальнейшие действия

Ответы на вопросы см hello [управление устройствами вопросы и ответы](device-management-faq.md) 
