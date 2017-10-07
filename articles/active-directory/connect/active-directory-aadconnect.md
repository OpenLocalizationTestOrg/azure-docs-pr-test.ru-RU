---
title: "Подключение Active Directory к Azure Active Directory | Документация Майкрософт"
description: "Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Это позволяет tooprovide общего удостоверения для приложений Office 365, Azure и SaaS интегрированы с Azure AD."
keywords: "Введение tooAzure AD Connect, общие сведения о Azure AD Connect, что такое Azure AD Connect, установки active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Интеграция локальных каталогов с Azure Active Directory
Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Это позволяет tooprovide общего удостоверения для пользователей для приложений Office 365, Azure и SaaS интегрированы с Azure AD. В этом разделе поможет hello планирования, развертывания и операций. Представляет коллекцию разделов связанных toothis ссылки toohello области.

> [!IMPORTANT]
> [Azure AD Connect hello лучшим способом tooconnect вашего локального каталога с Azure AD и Office 365. Это помешает tooupgrade tooAzure подключение AD из синхронизации Windows Azure Active Directory (DirSync) или Azure AD Sync как эти средства являются теперь рекомендуется к использованию и конец поддержки на 13 апреле 2017 г.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Что такое Azure AD Connect?](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Почему Azure AD Connect?
Интеграция локальных каталогов с Azure AD помогает повысить продуктивность ваших пользователей, предоставляя им единую идентификацию для доступа к облачным и локальным ресурсам. Пользователям и организациям можно воспользоваться преимуществами следующих hello.

* Пользователи могли использовать единое удостоверение tooaccess локальных приложений и облачных служб, таких как Office 365.
* Один tooprovide средство интерфейс удобного развертывания для синхронизации и входе в систему.
* Предоставляет новейшие возможности hello для ваших сценариев. Azure AD Connect заменяет старые версии средств интеграции удостоверений, такие как DirSync и Azure AD Sync. Дополнительные сведения см. в статье [Сравнение инструментов интеграции каталогов гибридной идентификации](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Принципы работы Azure AD Connect
Azure Active Directory Connect состоит из трех основных компонентов: службы синхронизации hello, дополнительный компонент службы федерации Active Directory hello и hello мониторинга компонента с именем [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Стек Azure AD Connect](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Синхронизация. Cлужбы синхронизации отвечают за создание пользователей, групп и других объектов. Он также отвечает за убедиться, что сведения об удостоверении для локальных пользователей и групп них совпадающие hello облака.
* AD FS - федерации является необязательной частью Azure AD Connect и может быть используется tooconfigure гибридной среде с помощью локальной инфраструктуры AD FS. Это позволяет организациям tooaddress сложных развертываний, например присоединения к домену единого входа, принудительного применения политики входа в AD и смарт-карты или третьих сторон многофакторной проверки Подлинности.
* Наблюдение за работоспособностью - Azure AD Connect Health можно обеспечивают надежный мониторинг и предоставление центрального расположения в hello Azure портала tooview это действие. Дополнительные сведения см. в статье [Мониторинг локальной инфраструктуры идентификации и служб синхронизации в облаке](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Установка Azure AD Connect
Hello загрузки для Azure AD Connect можно найти на [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=615771).

| Решение | Сценарий |
| --- | --- |
| Перед началом работы: [оборудование и предварительные требования](active-directory-aadconnect-prerequisites.md) |<li>Toocomplete действия, прежде чем начать tooinstall Azure AD Connect.</li> |
| [Стандартные параметры](active-directory-aadconnect-get-started-express.md) |<li>Если имеется один лес AD затем это hello рекомендуется использовать параметр toouse.</li> <li>Пользователь войти hello же пароль с помощью синхронизации паролей.</li> |
| [Настраиваемые параметры](active-directory-aadconnect-get-started-custom.md) |<li>Используется при наличии нескольких лесов. Поддерживает многие локальные [топологии](active-directory-aadconnect-topologies.md).</li> <li>Настройка режима входа, например AD FS для федерации или использования стороннего поставщика удостоверений.</li> <li>Настройка функций синхронизации, таких как фильтрация и обратная запись.</li> |
| [Обновление из DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Используется при наличии уже работающего сервера DirSync.</li> |
| [Переход с Azure AD Sync на Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Есть несколько разных способов на выбор.</li> |

[После установки](active-directory-aadconnect-whats-next.md) он работает как ожидалось и назначить лицензии пользователям toohello следует проверить.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Дальнейшие действия tooInstall Azure AD Connect
|Раздел |Ссылка|  
| --- | --- |
|Загрузка Azure AD Connect | [Загрузка Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Установка с помощью стандартных параметров | [Экспресс-установка Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Установка с помощью настроенных параметров | [Выборочная установка Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Обновление из DirSync | [Azure AD Connect: обновление DirSync](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|После установки | [Проверка установки hello и назначение лицензий](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Дополнительные сведения об установке Azure AD Connect
Также требуется tooprepare для [рабочей](active-directory-aadconnectsync-operations.md) проблемы. Может потребоваться toohave резервного сервера, можно легко может быть при наличии [аварийного](active-directory-aadconnectsync-operations.md#disaster-recovery). Если планируется часто toomake конфигурацию, необходимо запланировать [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode) сервера.

|Раздел |Ссылка|  
| --- | --- |
|Поддерживаемые топологии | [Топологии Azure AD Connect.](active-directory-aadconnect-topologies.md)|
|Принципы проектирования | [Принципы проектирования Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Учетные записи, используемые для установки | [Azure AD Connect: учетные записи и разрешения](./active-directory-aadconnect-accounts-permissions.md)|
|Операционное планирование | [Службы синхронизации Azure AD Connect: рабочие задачи и рекомендации](active-directory-aadconnectsync-operations.md)|
|Параметры входа пользователя | [Параметры входа в Azure AD Connect](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Настройка функций синхронизации
Azure AD Connect поставляется с несколькими функциями, которые можно при необходимости включить или они включены по умолчанию. В некоторых сценариях и топологиях может потребоваться дополнительная конфигурация некоторых функций.

[Фильтрация](active-directory-aadconnectsync-configure-filtering.md) используется, если toolimit, какие объекты представляют собой синхронизированы tooAzure AD. По умолчанию все пользователи, контакты, группы и компьютеры с ОС Windows 10 синхронизируются. Вы можете изменить hello фильтрации на основе доменов, подразделений или атрибуты.

[Синхронизация паролей](active-directory-aadconnectsync-implement-password-synchronization.md) синхронизирует hello хэш пароля в Active Directory tooAzure AD. Hello конечный пользователь может использовать hello одинаковый пароль локально и в облаке hello, но только управлять ими в одном месте. Поскольку вашей локальной Active Directory используется как центр hello, также можно использовать собственную политику паролей.

[Обратная запись паролей](../active-directory-passwords-getting-started.md) разрешить вашей toochange пользователей и сброса паролей в облаке hello и применяется политика локальных паролей.

[Обратная запись устройств](active-directory-aadconnect-feature-device-writeback.md) позволит устройства, зарегистрированные в Azure AD toobe обратной записи tooon локальный каталог Active Directory, поэтому он может использоваться для условного доступа.

Hello [избежать случайного удаления](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) функция включена по умолчанию и защищает от удаления многочисленные на hello облачного каталога то же время. По умолчанию она позволяет сделать 500 удалений за сеанс. Этот параметр можно изменить в зависимости от размера вашей организации.

[Автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md) включен по умолчанию для установок стандартные параметры и обеспечивает в Azure AD Connect находится в нажатом состоянии toodate с последним выпуском hello.

### <a name="next-steps-tooconfigure-sync-features"></a>Компоненты sync tooconfigure далее действия
|Раздел |Ссылка|  
| --- | --- |
|Настройка фильтрации | [Синхронизация Azure AD Connect: настройка фильтрации](active-directory-aadconnectsync-configure-filtering.md)|
|синхронизации паролей | [Службы синхронизации Azure AD Connect: реализация синхронизации паролей](active-directory-aadconnectsync-implement-password-synchronization.md)|
|Компонент обратной записи паролей | [Приступая к работе с компонентами управления паролями](../active-directory-passwords-getting-started.md)|
|Обратная запись устройств | [Включение обратной записи устройств в службе Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|предотвращения случайного удаления | [Синхронизация Azure AD Connect: предотвращение случайного удаления](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Автоматическое обновление | [Azure AD Connect: автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Настройка синхронизации Azure AD Connect
Синхронизация Azure AD Connect включает конфигурацию по умолчанию, предполагаемого toowork для большинства клиентов и топологии. Однако всегда существуют ситуациях, когда конфигурация по умолчанию hello не работает и должны быть изменены. Это поддерживается toomake изменения документированы в этом разделе и в соответствующих разделах.

Если вы работали не топология синхронизации перед требуется toostart toounderstand hello основы и hello терминов, используемых, как описано в hello [технические концепции](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect является развитием hello MIIS2003, ILM2007 и FIM2010. Даже если некоторые элементы идентичны, многое также изменилось.

Hello [конфигурация по умолчанию](active-directory-aadconnectsync-understanding-default-configuration.md) предполагается в hello конфигурации может быть более чем одном лесе. В таких топологиях объект пользователя может быть представлен как контакт в другом лесу. Hello пользователь также может иметь связанный почтовый ящик в другом лесу ресурсов. Описывается Hello поведение конфигурации по умолчанию hello в [пользователей и контактов,](active-directory-aadconnectsync-understanding-users-and-contacts.md).

модель конфигурации Hello синхронизацию называется [декларативной подготовки](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Hello потоки дополнительных атрибутов используется [функции](active-directory-aadconnectsync-functions-reference.md) tooexpress атрибут преобразования. Можно просматривать и проверить всю конфигурацию hello с помощью средства с Azure AD Connect. При необходимости изменения конфигурации toomake убедитесь, что вы выполните hello [рекомендации](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) это проще tooadopt новых выпусков.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Дальнейшие действия синхронизация toocustomize Azure AD Connect
|Раздел |Ссылка|  
| --- | --- |
|Все статьи о синхронизации Azure AD Connect | [Службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md)|
|технических концепциях | [Синхронизация Azure AD Connect: технические концепции](active-directory-aadconnectsync-technical-concepts.md)|
|Основные сведения о настройке по умолчанию hello | [Синхронизация Azure AD Connect: Общие сведения о конфигурации по умолчанию hello](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Общее представление о пользователях и контактах | [Синхронизация Azure AD Connect: общее представление о пользователях и контактах](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|декларативной подготовкой | [Azure AD Connect Sync: общие сведения о выражениях декларативной подготовки](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Изменение конфигурации по умолчанию hello | [Советы и рекомендации по изменению конфигурации по умолчанию hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Настройка функций федерации
ADFS может быть настроенный toosupport [нескольких доменов](active-directory-aadconnect-multiple-domains.md). Например может иметь несколько основных доменов необходимо toouse для федерации.

Если сервер ADFS не было настроенных tooautomatically обновление сертификатов из Azure AD или при использовании решения не служб федерации Active Directory, затем вы получите уведомление при наличии слишком[обновление сертификатов](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Далее шаги tooconfigure федерации функции
|Раздел |Ссылка|  
| --- | --- |
|Все статьи, посвященные AD FS | [Azure AD Connect и федерация](active-directory-aadconnectfed-whatis.md)|
|Настройка служб AD FS с поддоменами | [Поддержка нескольких доменов для федерации с Azure AD](active-directory-aadconnect-multiple-domains.md)|
|Управление фермой AD FS | [AD FS management and customizaton with Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Обновление сертификатов федерации вручную | [Обновление сертификатов федерации для Office 365 и Azure AD](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Дополнительные сведения и ссылки
|Раздел |Ссылка|  
| --- | --- |
|Журнал версий | [Журнал версий](active-directory-aadconnect-version-history.md)|
|Сравнение DirSync, Azure ADSync и Azure AD Connect | [Сравнение инструментов интеграции каталогов](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Список совместимости решений, отличных от AD FS, для Azure AD | [Список совместимости с федерацией Azure AD](active-directory-aadconnect-federation-compatibility.md)|
|Настройка IdP SAML 2.0|[Использование поставщика удостоверений (IdP) SAML 2.0 для единого входа](active-directory-aadconnect-federation-saml-idp.md)|
|Синхронизированные атрибуты | [Синхронизированные атрибуты](active-directory-aadconnectsync-attributes-synchronized.md)|
|Мониторинг с помощью Azure AD Connect Health | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Часто задаваемые вопросы | [Azure AD Connect: вопросы и ответы](active-directory-aadconnect-faq.md)|

**Дополнительные ресурсы**

Названием «Ignite» 2015 презентации на расширение toohello облачных каталогов в локальной среде.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

