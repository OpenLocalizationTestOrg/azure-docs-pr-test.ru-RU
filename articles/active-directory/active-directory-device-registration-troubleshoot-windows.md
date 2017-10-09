---
title: "aaaTroubleshooting hello автоматической регистрации Azure AD домена компьютеров, присоединенных к для Windows 10 и Windows Server 2016 | Документы Microsoft"
description: "Устранение неполадок hello функции автоматической регистрации Azure AD домена компьютеров, присоединенных к для Windows 10 и Windows Server 2016."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016

Этот раздел является применимо toohello следующих клиентов:

-   Windows 10
-   Windows Server 2016

Для других клиентов Windows в разделе [Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD для клиентов нижнего уровня Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

В этом разделе предполагается, что функции автоматической регистрации устройств, присоединенных к домену, перечисленные в описано в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello следующие сценарии:

- [Условный доступ на основе устройств](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Корпоративное перемещение параметров](active-directory-windows-enterprise-state-roaming-overview.md)

- [Настройка Windows Hello для бизнеса](active-directory-azureadjoin-passport-deployment.md)


В этом документе приведены инструкции по устранению как tooresolve потенциальные проблемы. 

Hello регистрация поддерживается в hello Windows обновление 10 ноября 2015 и более поздних версий.  
Рекомендуется использовать для включения выше сценариев hello hello окончания действия обновления.

## <a name="step-1-retrieve-hello-registration-status"></a>Шаг 1: Получить состояние регистрации hello 

**Состояние регистрации hello tooretrieve:**

1. Откройте командную строку hello с правами администратора.

2. Введите **dsregcmd/status**.



    +----------------------------------------------------------------------+
    | Состояние устройства                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Не DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 отпечаток: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected поставщик криптографии Microsoft Platform: Да KeySignTest:: необходимо выполнить с повышенными привилегиями tootest.
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | Состояние пользователя                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>Шаг 2: Оценка hello состояние регистрации 

Просмотрите следующие поля hello и убедитесь в том, что они имеют hello ожидаемые значения:

### <a name="azureadjoined--yes"></a>AzureAdJoined: YES  

В этом поле показан, зарегистрировано ли устройство hello в Azure AD. Если значение hello показывает, как «Нет», регистрации не завершена. 

**Возможные причины:**

- Не удалось выполнить проверку подлинности компьютера hello для регистрации.

- Есть прокси-сервер HTTP hello организации, которые не могут быть обнаружены на компьютере hello

- Hello недоступность Azure AD для проверки подлинности или DRS Azure для регистрации

- Hello компьютер может быть hello внутренней сети организации или VPN с tooan прямая линия видимости локального контроллера домена AD.

- Если компьютер hello доверенного платформенного МОДУЛЯ, возможно, в неверном состоянии.

- Может быть неправильной конфигурации в службах отмечалось в документе hello, которые понадобятся tooverify еще раз. Ниже приведены распространенные примеры.

    - На сервере федерации нет включенных конечных точек WS-Trust.

    - На сервере федерации может быть запрещена входящая аутентификация компьютеров в сети с использованием встроенной проверки подлинности Windows.

    - Нет объекта точки подключения службы, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello

---

### <a name="domainjoined--yes"></a>DomainJoined: YES  

Это поле показывает, является hello устройства присоединены к домену tooan локальной Active Directory, или нет. Если отображается значение hello, что **нет**, hello устройства не может автоматически регистрируются в Azure AD. Сначала проверьте, toohello соединения hello устройства в локальной Active Directory, прежде чем он может зарегистрироваться в Azure AD. Если вы ищете присоединение hello tooAzure компьютера AD напрямую, перейдите в tooLearn о возможности присоединения Azure Active Directory.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: NO  

В этом поле показан, зарегистрировано ли устройство hello в Azure AD, а также как личного устройства (помеченные как «Присоединено к рабочему месту»). Если это значение должно отображаться как «Нет» для присоединенных к домену компьютера, зарегистрированных в Azure AD, однако если показано значение "Да" означает, что рабочей или учебной учетной записи был Завершение регистрации добавлены предыдущих toohello компьютера. В этом случае hello учетной записи будет игнорироваться при использовании версии hello Юбилейного обновления Windows 10 (1607 при выполнении команды WinVer hello hello окна «Выполнить» или окно командной строки).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: YES и AzureADPrt: YES
  
Эти поля видно, что этот пользователь hello еще успешно прошел проверку подлинности tooAzure AD после входа в устройство toohello. Если они показывают «Нет» hello ниже приведены возможные причины ее возникновения.

- Ключ хранилища неправильный (STK) в доверенный платформенный модуль, связанный с hello устройства при регистрации (hello проверка KeySignTest во время работы с повышенными правами).

- Наличие альтернативного имени пользователя.

- Прокси-сервер HTTP не найден.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в разделе hello [автоматической регистрации устройств вопросы и ответы](active-directory-device-registration-faq.md) 
