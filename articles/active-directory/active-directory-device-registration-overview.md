---
title: "Общие сведения о регистрации устройств Active Directory aaaAzure | Документы Microsoft"
description: "Регистрация устройств Azure Active Directory — hello основа для сценариев условного доступа на основе устройств. При регистрации устройства, устройства hello подготавливает регистрации устройств Azure Active Directory удостоверение, которое является используется tooauthenticate hello устройства при входе пользователя hello."
services: active-directory
keywords: "регистрация устройств, включить регистрацию устройств, регистрация устройств и MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Знакомство с регистрацией устройств в Azure Active Directory
Регистрация устройств Azure Active Directory — hello основа для сценариев условного доступа на основе устройств. При регистрации устройства регистрации устройств Azure Active Directory предоставляет устройства hello удостоверение, которое является используется tooauthenticate hello устройства при входе пользователя hello. Hello проверку подлинности устройства и атрибуты hello hello устройства, затем можно используется tooenforce политик условного доступа для приложений, размещенных в облаке hello и в локальной среде.

В сочетании с мобильными устройствами management(MDM) например Microsoft Intune, атрибуты устройства hello в Azure Active Directory обновляются с дополнительными сведениями об устройстве hello. Это позволяет вам toocreate правила условного доступа, которые осуществляют доступ к устройствам toomeet стандартов безопасности и соответствия требованиям. Дополнительные сведения о регистрации устройств в Microsoft Intune см. в статье [Регистрация устройств для управления в Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Сценарии, обеспечиваемые службой регистрации устройств в Azure Active Directory
Регистрация устройств в Azure Active Directory предусматривает поддержку устройств iOS, Android и Windows. Hello отдельных сценариях использования службы регистрации устройств в Azure AD может иметь особые требования и поддерживаться другие платформы. Эти сценарии выглядят так.

* **Tooapplications условного доступа, которые размещается локально**: зарегистрированные устройства можно использовать с политиками доступа для приложений, которые будут настроены toouse AD FS Windows Server 2012 R2. Узнать больше о настройке условного доступа для локальной среды можно в разделе [Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory](active-directory-device-registration-on-premises-setup.md).
* **Условный доступ для приложений Office 365 с помощью Microsoft Intune** : ИТ-администраторы могут создавать условного доступа устройств политики toosecure корпоративным ресурсам, пока в hello же время позволяя информационных работников на совместимых устройствах службы tooaccess hello. Дополнительные сведения см. в разделе [Политики условного доступа к службам Office 365 с устройств](active-directory-conditional-access-device-policies.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Настройка регистрации устройств в Azure Active Directory
Необходимо tooenable регистрации устройств Azure AD в портале Azure hello мобильных устройств можно обнаруживать службу hello, просматривая хорошо известные записи DNS. Необходимо настроить DNS вашей компании, чтобы устройства Windows 10, Windows 8.1, Windows 7, Android и iOS можно обнаруживать и использовать службы hello.
Можно просмотреть и включить или выключить зарегистрированные устройства с помощью портала администрирования hello в Azure Active Directory.

> [!NOTE]
> Tooset копирование автоматической регистрации устройств. в статье, последней инструкции [как устройств с Azure Active Directory присоединенных к toosetup Автоматическая регистрация домена Windows](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Включение службы регистрации устройств Azure Active Directory
1. Войдите в toohello портал Microsoft Azure от имени администратора.
2. Выберите на левой панели hello **Active Directory**.
3. На hello **каталога** вкладке, выберите свой каталог.
4. Выберите hello **Настройка** вкладки.
5. Прокрутите раздел с именем toohello **устройств**.
6. Выберите значение **ВСЕ** для пункта **ПОЛЬЗОВАТЕЛИ МОГУТ ПРИСОЕДИНЯТЬ УСТРОЙСТВА К РАБОЧЕЙ ОБЛАСТИ**.
7. Выберите максимальное число hello устройств требуется tooauthorize на пользователя.

> [!NOTE]
> Для регистрации в Microsoft Intune или службе управления мобильными устройствами для Office 365 требуется присоединение к рабочей области. Если настроены обе эти службы, все выбранные и hello NONE кнопка отключена.
> 
> 

По умолчанию двухфакторная проверка подлинности не включена для службы hello. Однако ее рекомендуется использовать при регистрации устройства.

* Прежде чем делать обязательной двухфакторную проверку подлинности для этой службы, необходимо настроить поставщик двухфакторной проверки подлинности в Azure Active Directory и настроить учетные записи пользователей для многофакторной проверки подлинности, в разделе [Добавление многофакторной TooAzure проверки подлинности Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Если вы используете службы федерации Active Directory с Windows Server 2012 R2, для них необходимо настроить модуль двухфакторной проверки подлинности. См. статью [Приступая к работе с сервером Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Настройка обнаружения службы регистрации устройств Azure Active Directory
Windows 7 и Windows 8.1 устройства будут обнаруживать hello службы регистрации устройств, объединяя hello учетную запись пользователя с именем сервера регистрации известных устройств.

Необходимо создать запись DNS CNAME, которая указывает toohello A-запись, связанную с вашей службой регистрации устройств Azure Active Directory. Hello записи CNAME необходимо использовать хорошо известный префикс enterpriseregistration hello, за которым следует суффикс UPN hello hello учетными записями пользователей в вашей организации. Если ваша организация использует несколько суффиксов имени участника-пользователя, следует создать несколько записей CNAME в DNS.

Например, если используется два суффикса имени участника-пользователя в вашей организации с именем @contoso.com и @region.contoso.com, вы создадите следующие записи DNS hello.

| Запись | Тип | Адрес |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Просмотр объектов устройств в Azure Active Directory и управление ими
1. Из портала администратора Azure hello можно просматривать, блокировать и разблокировать устройства. Заблокированное устройство больше не будут иметь доступ tooapplications, которые настроенное tooallow только зарегистрированные устройства.
2. Войдите на портал Microsoft Azure toohello от имени администратора.
3. Выберите на левой панели hello **Active Directory**.
4. Выберите свой каталог.
5. Выберите hello **пользователей** вкладки. Выберите свои устройства tooview пользователя
6. Выберите hello **устройств** вкладки.
7. Выберите **зарегистрированные устройства** из hello раскрывающемся меню.
8. Здесь можно просмотреть, заблокировать или разблокировать зарегистрированные устройства пользователя hello.

## <a name="additional-topics"></a>Дополнительные разделы
Регистрировать присоединенные к домену устройства Windows 7 и Windows 8.1 можно с помощью службы регистрации устройств Azure AD. следующие вопросы Hello предоставляет дополнительные сведения о необходимых условиях hello и регистрацию устройств tooconfigure необходимые шаги hello на устройствах Windows 7 и Windows 8.1.

* [Автоматическая регистрация в Azure Active Directory присоединенных к домену устройств Windows](active-directory-conditional-access-automatic-device-registration.md)
* [Автоматическая регистрация в Azure Active Directory присоединенных к домену устройств Windows 10](active-directory-azureadjoin-devices-group-policy.md)

