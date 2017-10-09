---
title: "Azure AD Connect. История выпусков версий | Документация Майкрософт"
description: "В этой статье перечислены все выпуски Azure AD Connect и Azure AD Sync"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect. История выпусков версий
группы Azure Active Directory (Azure AD) Hello регулярно обновляет Azure AD Connect с новыми функциями и возможностями. Не все дополнения доступны применимо tooall аудитории.

Эта статья является спроектированный toohelp хранить список версий hello, которые были выпущены и toounderstand необходимости tooupdate toohello последнюю версию или нет.

Ниже приведен список связанных статей.


Раздел |  Сведения
--------- | --------- |
Tooupgrade действия из Azure AD Connect | Различные методы слишком[обновление с предыдущей версии toohello последней](active-directory-aadconnect-upgrade-previous-version.md) выпуска Azure AD Connect.
Необходимые разрешения | Разрешения, необходимые tooapply обновления, см. в разделе [учетных записей и разрешений](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Загрузить| [Скачать Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

## <a name="115610"></a>1.1.561.0
Состояние: 23 июля 2017 г.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Исправленные проблемы

* Устранена проблема, вызвавшего правило синхронизации out-of-box hello toobe «ожидания tooAD - ImmutableId пользователя» удалены:

  * Hello проблема возникает при обновлении Azure AD Connect, или когда hello параметр задачи *обновление конфигурации синхронизации* в Azure AD Connect hello мастер является конфигурация синхронизации используется tooupdate Azure AD Connect.
  
  * Это правило синхронизации не применимо toocustomers, который включен hello [msDS-ConsistencyGuid как источник привязки функция](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Эта функция доступна начиная с версии 1.1.524.0. При удалении правила синхронизации hello Azure AD Connect можно заполнить больше не в локальной среде AD DS-ms-ConsistencyGuid атрибута с hello ObjectGuid значение атрибута. Он не предотвращает подготовку новых пользователей в Azure AD.
  
  * исправление Hello гарантирует, что больше не будут удалены hello правила синхронизации, при обновлении или во время изменения конфигурации, при условии, что включена функция hello. Для существующих клиентов, затронутые этой проблемой исправление hello также гарантирует, что это правило синхронизации hello добавляется обратно после обновления версии toothis Azure AD Connect.

* Устранена проблема, вызывает правила синхронизации out-of-box toohave значение приоритета, меньше 100:

  * Как правило, более высокие значения приоритета (от 0 до 99) зарезервированы для пользовательских правил синхронизации. Во время обновления значения hello приоритет правила синхронизации out-of-box: обновленные tooaccommodate изменения правила синхронизации. Из-за проблемы toothis правила синхронизации out-of-box можно назначить значение приоритета, меньше 100.
  
  * исправление Hello предотвращает проблемы hello во время обновления. Однако он не восстанавливает hello приоритет значения для существующих клиентов, затронутые проблемой hello. В будущих toohelp hello с hello восстановления будет отображено отдельные исправления.

* Устранена проблема, где hello [домен и Подразделение фильтрации экрана](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) в Azure AD Connect hello отображается мастер *синхронизировать все домены и подразделения* параметр как выбранные, даже если включена фильтрация на основе Подразделения.

*   Устранена проблема, что вызвало hello [экрана Настройка разделов каталога](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) в hello tooreturn диспетчер службы синхронизации выдается ошибка, если hello *обновление* кнопки. сообщение об ошибке Hello *«произошла ошибка при обновлении доменов: не удается toocast объекта типа «System.Collections.ArrayList» tootype " Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject.»* Hello ошибка возникает, когда новый домен AD был добавлен tooan существующего леса AD, вы пытаетесь tooupdate Azure AD Connect с помощью hello кнопку "Обновить".

#### <a name="new-features-and-improvements"></a>Новые функции и внесенные улучшения

* [Функцию автоматического обновления](active-directory-aadconnect-feature-automatic-upgrade.md) было развернутой toosupport клиентов с hello конфигурации:
  * Вы включили hello функции обратной записи устройства.
  * Вы включили hello функции обратной записи группы.
  * Установка Hello не является экспресс-параметры или обновление DirSync.
  * У вас есть более чем 100 000 объектов в метавселенной hello.
  * При подключении toomore чем одном лесе. Экспресс-установку только подключается tooone леса.
  * Hello соединителя AD учетная запись уже не учетная запись MSOL_ по умолчанию hello.
  * Hello сервера задан toobe в промежуточный режим.
  * Вы включили hello функции обратной записи пользователя.
  
  >[!NOTE]
  >расширение области Hello функции автоматического обновления hello затрагивает клиентов с Azure AD Connect построения 1.1.105.0 и после. Если не хотите, чтобы автоматически обновить сервер toobe к Azure AD Connect система, необходимо выполнить следующий командлет на сервере Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Дополнительные сведения о Включение и отключение автоматического обновления, см. в разделе tooarticle [Azure AD Connect: автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Состояние: не будет выпущено. Изменения в этой сборке добавлены в версию 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Исправленные проблемы

* Устранена проблема, вызвавшего hello синхронизации out-of-box правило «Out tooAD - ImmutableId пользователя» toobe удаляется, когда обновляется настройки фильтрации на основе Подразделения. Это правило синхронизации не требуется для hello [msDS-ConsistencyGuid как источник привязки функция](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Устранена проблема, где hello [домен и Подразделение фильтрации экрана](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) в Azure AD Connect hello отображается мастер *синхронизировать все домены и подразделения* параметр как выбранные, даже если включена фильтрация на основе Подразделения.

*   Устранена проблема, что вызвало hello [экрана Настройка разделов каталога](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) в hello tooreturn диспетчер службы синхронизации выдается ошибка, если hello *обновление* кнопки. сообщение об ошибке Hello *«произошла ошибка при обновлении доменов: не удается toocast объекта типа «System.Collections.ArrayList» tootype " Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject.»* Hello ошибка возникает, когда новый домен AD был добавлен tooan существующего леса AD, вы пытаетесь tooupdate Azure AD Connect с помощью hello кнопку "Обновить".

#### <a name="new-features-and-improvements"></a>Новые функции и внесенные улучшения

* [Функцию автоматического обновления](active-directory-aadconnect-feature-automatic-upgrade.md) было развернутой toosupport клиентов с hello конфигурации:
  * Вы включили hello функции обратной записи устройства.
  * Вы включили hello функции обратной записи группы.
  * Установка Hello не является экспресс-параметры или обновление DirSync.
  * У вас есть более чем 100 000 объектов в метавселенной hello.
  * При подключении toomore чем одном лесе. Экспресс-установку только подключается tooone леса.
  * Hello соединителя AD учетная запись уже не учетная запись MSOL_ по умолчанию hello.
  * Hello сервера задан toobe в промежуточный режим.
  * Вы включили hello функции обратной записи пользователя.
  
  >[!NOTE]
  >расширение области Hello функции автоматического обновления hello затрагивает клиентов с Azure AD Connect построения 1.1.105.0 и после. Если не хотите, чтобы автоматически обновить сервер toobe к Azure AD Connect система, необходимо выполнить следующий командлет на сервере Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Дополнительные сведения о Включение и отключение автоматического обновления, см. в разделе tooarticle [Azure AD Connect: автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Состояние: июль 2017 г.

>[!NOTE]
>Эта сборка не toocustomers доступны через компонент подключения автоматическое обновление hello Azure AD.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Исправленные проблемы
* Устранена проблема с командлетом hello Initialize-ADSyncDomainJoinedComputerSync, вызвавшего hello проверенного домена, настроенного для hello существующей службы подключения точки объекта toobe изменения, даже если она по-прежнему допустимый домен. Эта проблема возникает, когда клиент Azure AD имеется несколько проверенных доменов, которые могут использоваться для настройки точки подключения службы hello.

#### <a name="new-features-and-improvements"></a>Новые функции и внесенные улучшения
* Обратная запись паролей доступна в виде предварительной версии в облаке Microsoft Azure для государственных организаций и Microsoft Cloud для Германии. Дополнительные сведения о поддержке Azure AD Connect hello различным экземплярам службы см. в разделе tooarticle [Azure AD Connect: особенности экземпляры](active-directory-aadconnect-instances.md).

* командлет Initialize-ADSyncDomainJoinedComputerSync Hello появился новый дополнительный параметр с именем AzureADDomain. Этот параметр позволяет указать, которые проверить toobe домена, используемым для настройки точки подключения службы hello.

### <a name="pass-through-authentication"></a>Сквозная проверка подлинности

#### <a name="new-features-and-improvements"></a>Новые функции и внесенные улучшения
* Имя Hello hello агента, необходимые для проверки подлинности было изменено с *соединитель прокси приложения Microsoft Azure AD* слишком*агент Microsoft Azure AD Connect проверки подлинности*.

* Включение сквозной проверки подлинности больше не включает синхронизацию хэша паролей по умолчанию.


## <a name="115530"></a>1.1.553.0
Состояние: июнь 2017 г.

> [!IMPORTANT]
> В этой сборке представлены изменения схем и правил синхронизации. После обновления служба синхронизации Azure AD Connect синхронизации запустит действия полного импорта и полной синхронизации. Сведения об изменениях hello описаны ниже. tootemporarily отложить полный импорт и полную синхронизацию действия после обновления см. в tooarticle [как toodefer полная синхронизация после обновления](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Синхронизация Azure AD Connect

#### <a name="known-issue"></a>Известная проблема
* Существует проблема, которая затрагивает клиентов, использующих [фильтрацию по подразделениям](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) при синхронизации Azure AD Connect. При переходе toohello [домен и Подразделение фильтрацию страницы](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) в мастер hello Azure AD Connect, ожидается hello, следуя поведение:
  * Если включена фильтрация на основе Подразделения hello **синхронизировать выбранные домены и подразделения** выбран параметр.
  * В противном случае hello **синхронизировать все домены и подразделения** выбран параметр.

Hello проблем является, hello **синхронизировать все домены и подразделения параметр** всегда выбран при запуске мастера hello.  Это происходит, даже если уже настроена фильтрация по подразделениям. Прежде чем сохранять изменения конфигурации AAD Connect, убедитесь, что hello **синхронизировать выбранные домены и подразделения параметр** и подтвердите повторного включения всех подразделений, которые должны toosynchronize. В противном случае фильтрация по подразделениям будет отключена.

#### <a name="fixed-issues"></a>Исправленные проблемы

* Устранена проблема с обратной записью паролей и позволяющая Azure AD администратор tooreset hello пароль локальной AD Привилегированная учетная запись пользователя. Hello проблема возникает, когда Azure AD Connect, предоставляется разрешение hello сброс пароля через hello Привилегированная учетная запись. Hello проблемы в данной версии Azure AD Connect, не позволяя Azure AD администратор tooreset пароль hello произвольный локальной AD Привилегированная учетная запись пользователя, Здравствуйте, администратор выполняется не владельцем hello этой учетной записи. Дополнительные сведения см. в разделе слишком[4033453 советы по безопасности](https://technet.microsoft.com/library/security/4033453).

* Устранена проблема связанные toohello [msDS-ConsistencyGuid как источник привязки](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) компонентов, где Azure AD Connect не обратной записи tooon локальные не атрибут msDS-ConsistencyGuid AD. Hello проблема возникает при наличии нескольких локальных лесов AD добавлены tooAzure AD Connect и hello *удостоверения пользователей существуют в нескольких каталогах параметр* выбран. При использовании такой конфигурации правила итоговые синхронизации hello не заполняют атрибута sourceAnchorBinary hello в метавселенной hello. атрибут sourceAnchorBinary Hello используется как атрибут источника hello для атрибута msDS-ConsistencyGuid. В результате атрибут ms DSConsistencyGuid toohello обратной записи не возникает. проблема toofix hello, следующие правила синхронизации были обновленные tooensure, hello sourceAnchorBinary атрибута в метавселенной заполняется всегда приветствия:
  * In from AD - InetOrgPerson AccountEnabled.xml;
  * In from AD - InetOrgPerson Common.xml;
  * In from AD - User AccountEnabled.xml;
  * In from AD - User Common.xml;
  * In from AD - User Join SOAInAAD.xml.

* Ранее, даже если hello [msDS-ConsistencyGuid как источник привязки](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) функция не включена, hello «ожидания tooAD — ImmutableId пользователя» правила синхронизации по-прежнему добавляется tooAzure AD Connect. эффект Hello носит информационный характер и не вызывает toooccur атрибут msDS-ConsistencyGuid обратная запись. путаницы tooavoid был добавлен код, hello правило синхронизации tooensure добавляется только в том случае, если включена функция hello.

* Устранена проблема, вызвавшего с событием ошибки 611 toofail синхронизации хэша пароля. Эта проблема возникает после удаления одного или нескольких контроллеров домена из локальной службы AD. В конце каждого цикла синхронизации пароля hello hello выдан файла cookie синхронизации с локальным AD идентификаторами вызова hello удалены контроллеров домена с USN (номеров последовательного обновления) значение 0. не удается toopersist синхронизации cookie содержащего USN значение 0 и выходит из строя с событием ошибки 611 Hello диспетчер синхронизации паролей. Во время следующей синхронизации hello цикла, hello диспетчер синхронизации паролей использует hello последнего сохраненного файла cookie синхронизации, не содержащий USN значение 0. В результате hello так же toobe повторную синхронизацию. Благодаря этому исправлению hello диспетчер синхронизации паролей сохраняет файл cookie синхронизации hello правильно.

* Ранее даже если автоматическое обновление отключено с помощью командлета Set ADSyncAutoUpgrade hello, hello процесса автоматического обновления периодически продолжает toocheck для обновления и зависит от hello загрузить установщик toohonor отключения. Благодаря этому исправлению hello процесса автоматического обновления больше не проверяет наличие обновления периодически. исправление Hello применяется автоматически, если установщик обновления для этой версии Azure AD Connect выполняется один раз.

#### <a name="new-features-and-improvements"></a>Новые функции и внесенные улучшения

* Здравствуйте, ранее [msDS-ConsistencyGuid как источник привязки](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) функция была доступной toonew развертываний только. Теперь оно имеет доступные tooexisting развертываний. В частности:
  * tooaccess hello компонент, запустите мастер hello Azure AD Connect и выберите hello *обновление источника привязки* параметр.
  * Этот параметр является только видимым tooexisting развертываний, использующих objectGuid в качестве атрибута sourceAnchor.
  * При настройке параметра hello hello мастер проверяет состояние hello атрибута msDS-ConsistencyGuid hello в локальной службе Active Directory. Если атрибут hello не настроен для любого объекта пользователя в каталоге hello, hello мастер использует hello msDS-ConsistencyGuid как атрибут sourceAnchor hello. Если атрибут hello настроен один или несколько объектов-пользователей в каталоге hello, приветствия мастера завершается hello атрибута используется другими приложениями и не может использоваться как атрибут sourceAnchor и не разрешает изменение tooproceed hello источника привязки. Если вы уверены, что этот атрибут hello не используется средством существующих приложений, сведения о как toosuppress hello ошибки необходимо toocontact поддержки.

* Определенные слишком**userCertificate** атрибут на объектах устройств, Azure AD Connect, теперь выглядит значения сертификатов, необходимых для [подключение устройств, присоединенных к домену tooAzure AD для работы с Windows 10](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) и отфильтровывает rest hello перед синхронизацией tooAzure AD. tooenable такое поведение, правило синхронизации out-of-box hello, «Out tooAAD - устройства присоединение SOAInAD» были обновлены.

* Azure AD Connect теперь поддерживает обратная запись Exchange Online **cloudPublicDelegates** атрибута tooon локальной AD **publicDelegates** атрибута. Это позволяет hello сценарии, где почтовый ящик Exchange Online могут быть предоставлены toousers права SendOnBehalfTo с почтовых ящиков Exchange в локальной среде. toosupport эту функцию, новое правило синхронизации out-of-box «ожидания tooAD — обратная запись пользователя Exchange гибридного PublicDelegates» был добавлен. Это правило синхронизации добавляется только tooAzure AD подключения, если включена функция гибридный Exchange.

*   Теперь поддерживает Azure AD Connect, синхронизация hello **altRecipient** атрибутов из Azure AD. Это изменение правил синхронизации out-of-box были toosupport обновление tooinclude hello требуется атрибут потока:
  * Поступление из AD — пользователь Exchange
  * Out tooAAD — ExchangeOnline пользователя
  
* Hello **cloudSOAExchMailbox** атрибут в метавселенной hello указывает, имеет ли заданный пользователь почтовый ящик Exchange Online. Его определение было обновленные tooinclude дополнительных Exchange Online RecipientDisplayTypes от такого оборудования и конференц-зале почтовые ящики. tooenable это изменение определения hello hello cloudSOAExchMailbox атрибута, который находится в папке правило синхронизации out-of-box «В из AAD — пользователь гибридный Exchange», была обновлена с:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello следующее:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* X509Certificate2-совместимой функции для создания значения сертификата toohandle выражения правила синхронизации в атрибуте userCertificate hello набора hello добавлено следующее:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Выберите пункт|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* После изменения схемы выполнены введено tooallow клиентов toocreate синхронизации пользовательские правила tooflow sAMAccountName, domainNetBios и domainFQDN объектов групп, а также distinguishedName для пользовательских объектов:

  * Следующие атрибуты были добавлены tooMV схемы:
    * Группа: AccountName.
    * Группа: domainNetBios.
    * Группа: domainFQDN.
    * Пользователь: distinguishedName.

  * Следующие атрибуты были добавлены tooAzure схемы соединителя AD:
    * Группа: OnPremisesSamAccountName.
    * Группа: NetBiosName.
    * Группа: DnsDomainName.
    * Пользователь: OnPremisesDistinguishedName.

* Hello скрипт командлетов ADSyncDomainJoinedComputerSync теперь содержит новый дополнительный параметр с именем AzureEnvironment. параметр Hello является используется toospecify, какие области hello соответствующего клиента Azure Active Directory размещается в. Допустимые значения:
  * AzureCloud (по умолчанию).
  * AzureChinaCloud;
  * AzureGermanyCloud.
  * USGovernment.
 
* Обновленный toouse редактор правил синхронизации соединить (вместо подготовки) как значение по умолчанию hello типа ссылки во время создания правила синхронизации.

### <a name="ad-fs-management"></a>Управление AD FS

#### <a name="issues-fixed"></a>Исправленные проблемы

* Следующие URL-адреса, новые конечные точки WS-Federation, представленный устойчивости tooimprove Azure AD для простой проверки подлинности и будет добавлен локальный tooon ответе конфигурация стороны отношения доверия AD FS:
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* Устранена проблема, вызвавшего AD FS toogenerate неправильное значение для IssuerID. Hello проблема возникает, если имеется несколько проверенных доменов в клиенте Azure AD hello и суффикс домена hello toogenerate используется атрибут userPrincipalName hello hello утверждения имеет по крайней мере IssuerID уровни 3 глубокой (например, johndoe@us.contoso.com). Hello неполадки, обновив hello регулярное выражение используется с правилами утверждений hello.

#### <a name="new-features-and-improvements"></a>Новые функции и внесенные улучшения
* Ранее hello функциональности управления сертификатами служб федерации Active Directory с Azure AD Connect может использоваться только с помощью служб федерации Active Directory ферм, управляемых с помощью Azure AD Connect. Теперь можно использовать функции hello с фермы служб федерации Active Directory, которые не управляются с помощью Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Дата выпуска: май 2017 г.

> [!IMPORTANT]
> В этой сборке представлены изменения схем и правил синхронизации. После обновления служба синхронизации Azure AD Connect синхронизации запустит действия полного импорта и полной синхронизации. Сведения об изменениях hello описаны ниже.
>
>

**Исправленные проблемы:**

Службы синхронизации Azure AD Connect

* Устранена проблема, вызывающая toooccur автоматическое обновление на сервере hello Azure AD Connect, даже если клиент отключил компонент hello, с помощью командлета Set-ADSyncAutoUpgrade hello. Благодаря этому исправлению hello процесс автоматического обновления на сервере hello по-прежнему проверяет наличие обновления периодически, но hello установщик учитывает hello автоматическое обновление конфигурации.
* Во время обновления на месте DirSync Azure AD Connect создает toobe учетной записи службы Azure AD, используемые соединителем hello Azure AD для синхронизации с Azure AD. После создания учетной записи hello Azure AD Connect использует для проверки подлинности Azure AD, используя учетную запись hello. В некоторых случаях не пройдет проверку подлинности из-за временных проблем, который в свою очередь приводит toofail обновления на месте DirSync с ошибкой *«Ошибка выполнения задачи настройки AAD Sync: AADSTS50034: toosign в это приложение hello учетной записи необходимо добавить каталог xxx.onmicrosoft.com toohello.»* Устойчивость hello tooimprove обновления DirSync, Azure AD Connect теперь повторяет шаг проверки подлинности hello.
* Возникла проблема с построением 443, вызывающая toosucceed обновления на месте DirSync, но профилей выполнения, необходимые для синхронизации службы каталогов не создаются. В эту сборку Azure AD Connect включена логика восстановления. Когда клиент обновляет toothis сборки, Azure AD Connect обнаруживает отсутствие профилей выполнения и создает их.
* Устранена проблема, вызывающая toostart toofail процесс синхронизации паролей 6900 идентификатор события и ошибки *«Элемент с таким ключом уже был добавлен hello»*. Эта проблема возникает при обновлении фильтрации раздел конфигурации для конфигурации tooinclude AD Подразделение. эту проблему, синхронизация паролей обработать сейчас toofix синхронизирует изменения паролей от только разделы домена AD. Разделы, не относящиеся к домену (такие как раздел конфигурации), пропускаются.
* Во время установки экспресс-выпуск Azure AD Connect создает локальной среды AD DS учетной записи toobe, используемые toocommunicate соединитель hello AD с локальным AD. Ранее при создании учетной записи hello флаг PASSWD_NOTREQD hello атрибуту hello контроль учетных записей пользователей и имеет значение случайный пароль для учетной записи hello. Теперь Azure AD Connect явно удаляет флаг PASSWD_NOTREQD hello после установки пароля hello hello учетной записи.
* Устранена проблема, вызывающая toofail обновления DirSync ошибка *«Произошла взаимоблокировка в sql server какие идет tooacquire блокировку приложения»* когда hello mailNickname атрибут находится в hello в локальной среде AD схемы, но не связывает toohello класс объекта пользователя AD.
* Фиксированный проблему, которая вызывает tooautomatically функция обратной записи устройства быть отключены, когда администратор обновляет конфигурацию синхронизации Azure AD Connect, с помощью мастера Azure AD Connect. Это связано с проверьте выполнение необходимых компонентов мастер hello существующей конфигурации обратной записи устройства hello в локальном AD и hello проверка завершается неудачно. исправление Hello tooskip hello проверка выполняется, если устройство включена обратная запись уже ранее.
* tooconfigure Подразделение фильтрации, можно использовать мастер Azure AD Connect hello или hello диспетчер службы синхронизации. Ранее при использовании мастера tooconfigure hello Azure AD Connect Подразделение фильтрации, создания новых подразделениях впоследствии включаются для синхронизации каталогов. Если не требуется новый toobe подразделений включены, необходимо настроить Подразделения фильтрации с помощью Synchronization Service Manager "hello". Теперь можно добиться hello такое же поведение, с помощью мастера Azure AD Connect.
* Устранена проблема, хранимые процедуры, которые требуется создать в схеме hello hello Установка admin, а не в схеме dbo hello toobe Azure AD Connect.
* Устранена проблема, вызывающая атрибут TrackingId hello, возвращенный Azure AD toobe опущен в hello журналы событий сервера подключения AAD. Hello проблема возникает, если Azure AD Connect получает сообщение о перенаправлении от Azure AD и Azure AD Connect toohello невозможно tooconnect конечных точек, предоставляемых. Hello TrackingId используется toocorrelate инженеры службы поддержки со стороны журналы службы во время устранения неполадок.
* Когда Azure AD Connect получает сообщение об ошибке LargeObject из Azure AD, Azure AD Connect создается событие с идентификатором EventID 6941 и сообщений *«hello подготовленный объект слишком велик. Trim hello число значений атрибутов для этого объекта».* В hello же время, Azure AD Connect также приводит к возникновению события с EventID 6900 и сообщений пользователя в заблуждение *«Microsoft.Online.Coexistence.ProvisionRetryException: не удается toocommunicate с hello Windows службы Azure Active Directory.»* toominimize путаницы, Azure AD Connect, больше не приводит к возникновению ошибки hello последнее событие, когда сообщение об ошибке LargeObject.
* Устранена проблема, вызывающая hello toobecome Synchronization Service Manager не отвечает при попытке настройки hello tooupdate для универсальный соединитель LDAP.

**Новые функции и улучшения:**

Службы синхронизации Azure AD Connect
* Изменения правила синхронизации — hello после изменения правила синхронизации были реализованы.
  * Правило синхронизации по умолчанию обновлена задать toonot атрибуты экспорта **userCertificate** и **userSMIMECertificate** у более чем на 15 значения атрибутов hello.
  * Атрибуты AD **employeeID** и **msExchBypassModerationLink** теперь включены в набор правил синхронизации по умолчанию hello.
  * Атрибут AD **photo** удален из набора правил синхронизации по умолчанию.
  * Добавлен **preferredDataLocation** toohello метавселенной и соединитель AAD схему. Пользователи будут tooupdate, которые либо атрибутов в Azure AD, можно реализовать пользовательский синхронизации toodo правила таким образом. toofind Дополнительные сведения об атрибуте hello, см. раздел tooarticle [синхронизации Azure AD Connect: как toomake toohello изменение по умолчанию конфигурация - включить синхронизацию PreferredDataLocation](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Добавлен **userType** toohello метавселенной и соединитель AAD схему. Пользователи будут tooupdate, которые либо атрибутов в Azure AD, можно реализовать пользовательский синхронизации toodo правила таким образом.

* Azure AD Connect теперь автоматически обеспечивает использование атрибута ConsistencyGuid hello как атрибут источника привязки hello для локальных объектов AD. Более того, Azure AD Connect заполняет hello ConsistencyGuid атрибут со значением атрибута objectGuid hello, если она пуста. Этот компонент является toonew применимо только для развертывания. toofind дополнительных сведений об этой функции см. раздел tooarticle [Azure AD Connect: Разработка концепции — с помощью msDS-ConsistencyGuid как sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Новое разрешение командлет Invoke-ADSyncDiagnostics было добавлено toohelp диагностики синхронизация хэшей паролей проблем, связанных с. Дополнительную информацию об использовании командлета hello tooarticle [неполадок с синхронизацией паролей с Azure AD Connect sync](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect теперь поддерживает синхронизации общих папок Mail-Enabled объекты из локальной AD tooAzure AD. Для включения функции hello, с помощью мастера Azure AD Connect в списке дополнительных компонентов. toofind дополнительных сведений об этой функции см. tooarticle [Office 365 Directory на основе Edge блокирует поддержку локальных почты включены общие папки](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect требуется toosynchronize учетной записи службы AD DS из локальной AD. Ранее Если вы установили Azure AD Connect с помощью режима Express hello, можно предоставить учетные данные учетной записи администратора предприятия hello и создать hello AD DS требуется учетная запись Azure AD Connect. Однако для выборочной установки и добавления существующего развертывания tooan лесов, можно было hello tooprovide требуется учетная запись службы AD DS вместо. Вы также получили tooprovide параметр hello hello учетные данные учетной записи администратора предприятия во время выборочной установки, чтобы создать hello AD DS требуется учетная запись Azure AD Connect.
* Azure AD Connect теперь поддерживает функцию SQL AOA. Перед установкой Azure AD Connect включите функцию SQL AOA. Во время установки Azure AD Connect определяет, включен ли указанный экземпляр SQL hello для SQL AOA. При включении SQL AOA дальнейшей Azure AD Connect определяет, является ли SQL AOA настроенных toouse Синхронная репликация или асинхронная репликация. При настройке прослушивателя группы доступности hello, рекомендуется установить свойство too0 hello RegisterAllProvidersIP. Это так, как Azure AD Connect в настоящее время использует собственный клиент SQL tooconnect tooSQL и собственный клиент SQL не поддерживает использование hello MultiSubNetFailover свойства.
* Если используется LocalDB как hello базы данных для сервера Azure AD Connect и был достигнут предельный размер 10 ГБ, hello служба синхронизации не запускается. Ранее вы должны tooperform ShrinkDatabase операцию hello LocalDB tooreclaim недостаточно места для базы данных для службы синхронизации toostart hello. После которого, вы hello используйте Synchronization Service Manager toodelete выполнять tooreclaim журнал больше места для базы данных. Теперь можно использовать toopurge командлет Start-ADSyncPurgeRunHistory запуска данных журнала из места базы данных LocalDB tooreclaim. Кроме того, этот командлет поддерживает автономный режим (путем указания hello - параметр offline) может принимать Здравствуйте, когда служба синхронизации не запущена. Примечание: hello автономный режим может использоваться только в том случае, если hello синхронизации служба не запущена и hello базы данных, используемой LocalDB.
* требуется tooreduce hello объем хранилища, в Azure AD Connect теперь сжимает сведения об ошибке синхронизации перед их сохранением в базе данных LocalDB или SQL. При обновлении с более старой версии Azure AD Connect toothis версии Azure AD Connect выполняет однократную сжатия существующие сведения об ошибке синхронизации.
* Ранее после обновления конфигурацией фильтрации Подразделение, вам необходимо вручную выполнить полный импорт tooensure существующие объекты должным образом включены или исключены из синхронизации службы каталогов. Теперь Azure AD Connect автоматически запускает полный импорт во время следующей синхронизации hello цикла. Кроме того, полный импорт только быть применен toohello AD соединители с hello update. Примечание: это улучшение является применимо tooOU фильтрации обновлений, выполняемых с помощью мастера только по hello Azure AD Connect. Это не применимо tooOU фильтрации обновления, выполненные с помощью hello диспетчер службы синхронизации.
* Раньше при фильтрации на основе группы поддерживались только объекты User, Group и Contact. Теперь фильтрация на основе группы также поддерживает объекты-компьютеры.
* Раньше данные из пространства соединителя можно было удалить без отключения планировщика синхронизации Azure AD Connect. Теперь hello диспетчер службы синхронизации блокирует удаление hello пространство соединителя данных при обнаружении этого планировщика hello включен. Кроме того возвращается предупреждение, tooinform клиентов о возможной потере данных при удалении hello данные пространства соединителя.
* Ранее необходимо отключить транскрипции PowerShell для Azure AD Connect мастер toorun правильно. Эта проблема частично решена. Если вы используете конфигурацию синхронизации Azure AD Connect мастера toomanage можно включить транскрипции PowerShell. Если вы используете конфигурацию служб федерации Active Directory toomanage мастера Azure AD Connect, необходимо отключить транскрипции PowerShell.



## <a name="114860"></a>1.1.486.0
Дата выпуска: апрель 2017 г.

**Исправленные проблемы:**
* Исправлена проблема hello, где Azure AD Connect не удастся успешно установить локализованной версии Windows Server.

## <a name="114840"></a>1.1.484.0
Дата выпуска: апрель 2017 г.

**Известные проблемы:**

* Эта версия Azure AD Connect не удастся успешно установить Если hello следующие условия:
   1. При выполнении обновления "на месте" службы DirSync или новой установки Azure AD Connect.
   2. Вы используете локализованную версию Windows Server, где имя встроенной группы администраторов на сервере hello hello не «Администраторы».
   3. Используется по умолчанию hello SQL Server 2012 Express LocalDB устанавливается вместе с Azure AD Connect, а не полный SQL.

**Исправленные проблемы:**

Службы синхронизации Azure AD Connect
* Устранена проблема, где планировщика синхронизации hello пропускает шаг hello всей синхронизации, если отсутствует один или несколько соединителей профилей выполнения для этого этапа синхронизации. Например добавленные вручную соединитель с помощью hello диспетчер службы синхронизации без создания разностный Импорт профиля запуска для нее. Это исправление гарантирует, что этот планировщик синхронизации hello продолжается toorun разностный Импорт для других соединителей.
* Устранена проблема, где hello служба синхронизации немедленно прекращает обработку профиля запуска, когда это возникает ошибка с одним из шагов выполнения hello. Это исправление гарантирует, что hello пропускает служба синхронизации, выполните шаг и tooprocess hello rest. Например, у вас есть профиль выполнения импорта изменений для соединителя AD с несколькими этапами выполнения (по одному этапу на каждый локальный домен AD). Служба синхронизации Hello запускаются разностный импорт с hello другие домены AD даже если один из них имеет проблемы с сетевым соединением.
* Исправлена проблема, которое вызывает обновление toobe hello соединителя Azure AD, пропущенных во время автоматического обновления.
* Устранена проблема, tooincorrectly причины Azure AD Connect определить, является ли hello сервера контроллера домена во время установки, который в свою очередь приводит к возникновению DirSync обновление toofail.
* Фиксированный проблему, которая вызывает DirSync toonot обновления на месте создать любое запустить профиль для hello соединителя Azure AD.
* Устранена проблема, где hello диспетчер службы синхронизации пользовательского интерфейса отвечает при попытке tooconfigure универсальный соединитель LDAP.

Управление AD FS
* Устранена проблема, где приветствия мастера Azure AD Connect не выполняется, если основной узел hello AD FS был перемещенный tooanother сервера.

Desktop SSO
* Устранена проблема мастер Azure AD Connect hello где hello экрана входа не позволяет включить возможность единого входа рабочего стола при выборе синхронизации паролей в качестве дополнения вход во время новой установки.

**Новые функции и улучшения:**

Службы синхронизации Azure AD Connect
* Подключения синхронизации Azure AD теперь поддерживает hello использования виртуальной учетной записи службы, управляемой учетной записи службы и групповой управляемой учетной записи службы в качестве учетной записи службы. Это относится toonew установку только Azure AD Connect. При установке Azure AD Connect происходит следующее:
    * По умолчанию мастер Azure AD Connect создаст учетную запись виртуальной службы и будет использовать ее в качестве учетной записи службы.
    * При установке контроллера домена Azure AD Connect будет использоваться поведение tooprevious, где он создаст учетную запись пользователя домена и использует его в качестве учетной записи службы.
    * Можно переопределить поведение по умолчанию hello, указав одно из следующих hello:
      * групповую управляемую учетную запись службы;
      * управляемую учетную запись службы;
      * учетную запись пользователя домена;
      * локальную учетную запись пользователя.
* Ранее при обновлении tooa новой сборки Azure AD Connect, содержащего соединители обновления или изменения правил синхронизации, Azure AD Connect будет активировать цикла полной синхронизации. Теперь Azure AD Connect выборочно запустит этап полного импорта только для соединителей с обновлениями и этап полной синхронизации только для соединителей с измененными правилами синхронизации.
* Ранее hello пороговое значение удаления экспорта применяется только tooexports активировавшего через планировщика синхронизации hello. Теперь функция hello расширяется экспортов tooinclude вручную вызвано hello клиента с помощью hello диспетчер службы синхронизации.
* В вашем клиенте Azure AD есть конфигурация службы, которая указывает, включена ли для этого клиента функция синхронизации паролей. Ранее будет легко toobe конфигурации службы hello, неправильно настроен для Azure AD Connect, при наличии активной и промежуточного сервера. Теперь Azure AD Connect попытается согласуется с текущей конфигурации службы hello tookeep только сервер Azure AD Connect.
* Теперь мастер Azure AD Connect обнаруживает и возвращает предупреждение, если в локальном AD не включена корзина AD.
* Ранее tooAzure экспорта AD времени ожидания и завершается неудачей, если hello совокупный размер hello объектов в пакете hello превышает определенный порог. Теперь hello служба синхронизации будет предпринята повторная tooresend hello объекты в пакетах меньшего размера, если была обнаружена проблема hello.
* Управление ключами службы синхронизации приложения Hello был удален из меню "Пуск" Windows. Управление ключами по-прежнему поддерживается через интерфейс командной строки, с помощью miiskmu.exe toobe. Дополнительную информацию об управлении ключами шифрования tooarticle [ключ шифрования Abandoning hello Azure AD Sync подключения](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Ранее при изменении пароля учетной записи службы синхронизации Azure AD Connect hello hello службы синхронизации будут начала может неверно до прервана hello ключ шифрования и пароль учетной записи службы синхронизации Azure AD Connect hello повторной инициализации. Теперь эти действия не требуются.

Desktop SSO

* Мастер Azure AD Connect больше не требуется toobe 9090 порт открыт hello сети при настройке сквозной проверки подлинности и единого входа рабочего стола. Требуется только порт 443. 

## <a name="114430"></a>1.1.443.0
Дата выпуска: март 2017 г.

**Исправленные проблемы:**

Службы синхронизации Azure AD Connect
* Устранена проблема, из-за чего toofail мастер Azure AD Connect, если отображаемое имя hello hello соединителя Azure AD не содержит клиента Azure AD toohello домена, назначенное начальной onmicrosoft.com hello.
* Исправлена проблема, вследствие чего toofail мастер Azure AD Connect при проведении tooSQL подключение к базе данных, если пароль учетной записи службы синхронизации hello hello содержит специальные символы, такие как апостроф, двоеточия и пространства.
* Устранена проблема, который вызывает ошибку hello toooccur «hello dimage содержит привязку, которая отличается от образа hello» на сервере служб Azure AD Connect в промежуточный режим, после был временно исключен из локальной AD из синхронизации объекта и его снова, затем включаются Идет синхронизация.
* Устранена проблема, который вызывает ошибку hello toooccur «hello объекта, который DN is фантомных» на сервере служб Azure AD Connect в промежуточный режим, после был временно исключен из локальной AD из синхронизации объекта и затем включили его для синхронизации.

Управление AD FS
* Устранена проблема, при котором мастер Azure AD Connect не обновить конфигурацию AD FS, а hello право собственности на hello проверяющей стороной, после настройки альтернативного идентификатора входа.
* Устранена проблема, где невозможно toocorrectly дескриптор AD FS серверы, учетные записи службы настроены с использованием формата userPrincipalName вместо формата sAMAccountName мастер Azure AD Connect.

Сквозная проверка подлинности
* Устранена проблема, из-за чего toofail мастер Azure AD Connect, если выбран передать через проверку подлинности, но регистрация его соединителя завершится ошибкой.
* Исправлена проблема, вследствие чего Azure AD Connect, мастер toobypass проверки входа в выбранный метод при включенной функции единого входа рабочего стола.

Сброс паролей
* Исправлена проблема, что может стать причиной toonot Azure AAD Connect сервера hello попытки toore-подключаться, если подключение hello был уничтожен брандмауэра или прокси-сервера.

**Новые функции и улучшения:**

Службы синхронизации Azure AD Connect
* Теперь командлет Get-ADSyncScheduler возвращает новое логическое свойство SyncCycleInProgress. Если hello вернул значение true, оно означает, что цикл запланированной синхронизации выполняется.
* Папка назначения для хранения установки Azure AD Connect и журналы программы установки была перенесена в toohello %localappdata%\AADConnect too%programdata%\AADConnect tooimprove специальные файлы журналов.

Управление AD FS
* Добавлена поддержка обновления SSL-сертификата фермы AD FS.
* Добавлена поддержка управления AD FS 2016.
* Теперь во время установки AD FS можно указать существующую групповую управляемую учетную запись службы (GMSA).
* Теперь можно настроить SHA-256, как хэш-алгоритм подписей hello для доверия с проверяющей стороной Azure AD.

Сброс паролей
* Усовершенствования, появившиеся с выходом tooallow hello toofunction продукта в средах с более строгими правилами брандмауэра.
* TooAzure надежности подключений служебной шины.

## <a name="113800"></a>1.1.380.0
Дата выпуска: декабрь 2016 г.

**Исправлена проблема:**

* Проблема основных hello, где hello issuerid правил утверждений для служб федерации Active Directory (AD FS) отсутствует в этой сборке.

>[!NOTE]
>Эта сборка не toocustomers доступны через компонент подключения автоматическое обновление hello Azure AD.

## <a name="113710"></a>1.1.371.0
Дата выпуска: декабрь 2016 г.

**Известная проблема:**

* правило для утверждений Hello issuerid для AD FS отсутствует в этой сборке. правило для утверждений issuerid Hello является обязательным, если федерацию нескольких доменов в Azure Active Directory (Azure AD). Если вы используете Azure AD Connect toomanage локальной развертывания AD FS, обновление сборки toothis удаляет hello существующее правило утверждения issuerid из конфигурации AD FS. Hello проблему можно обойти путем добавления правил утверждений issuerid hello после обновления установки hello. Сведения о добавлении hello issuerid правил утверждений, описаны в статье toothis на [поддержку нескольких доменов для создания федерации с Azure AD](active-directory-aadconnect-multiple-domains.md).

**Исправлена проблема:**

* Если 9090 порт не открыт для исходящего подключения hello, hello Azure AD Connect установку или обновление завершается ошибкой.

>[!NOTE]
>Эта сборка не toocustomers доступны через компонент подключения автоматическое обновление hello Azure AD.

## <a name="113700"></a>1.1.370.0
Дата выпуска: декабрь 2016 г.

**Известные проблемы:**

* правило для утверждений Hello issuerid для AD FS отсутствует в этой сборке. правило для утверждений issuerid Hello является обязательным, если федерацию нескольких доменов в Azure AD. Если вы используете Azure AD Connect toomanage локальной развертывания AD FS, обновление сборки toothis удаляет hello существующее правило утверждения issuerid из конфигурации AD FS. Hello проблему можно обойти путем добавления правил утверждений issuerid hello после установки или обновления. Сведения о добавлении issuerid правил утверждений, описаны в статье toothis на [поддержку нескольких доменов для создания федерации с Azure AD](active-directory-aadconnect-multiple-domains.md).
* Открыть исходящий toocomplete установки должен быть порт 9090.

**Новые функции:**

* Сквозная проверка подлинности (предварительная версия).

>[!NOTE]
>Эта сборка не toocustomers доступны через компонент подключения автоматическое обновление hello Azure AD.

## <a name="113430"></a>1.1.343.0
Дата выпуска: ноябрь 2016 г.

**Известная проблема:**

* правило для утверждений Hello issuerid для AD FS отсутствует в этой сборке. правило для утверждений issuerid Hello является обязательным, если федерацию нескольких доменов в Azure AD. Если вы используете Azure AD Connect toomanage локальной развертывания AD FS, обновление сборки toothis удаляет hello существующее правило утверждения issuerid из конфигурации AD FS. Hello проблему можно обойти путем добавления правил утверждений issuerid hello после установки или обновления. Сведения о добавлении issuerid правил утверждений, описаны в статье toothis на [поддержку нескольких доменов для создания федерации с Azure AD](active-directory-aadconnect-multiple-domains.md).

**Исправленные проблемы:**

* В некоторых случаях установка Azure AD Connect завершается неудачно, так как это не удается toocreate учетная запись локальной службы, пароль которого соответствует hello уровень сложности, заданные политики паролей организации hello.
* Устранена проблема, где правила присоединения не перестраиваются, когда объект в пространство соединителя hello одновременно становится вне области для одного соединения правило и становятся в области для другого. Это может произойти при наличии нескольких правил объединения, условия которых являются взаимоисключающими.
* Исправлена проблема, при которой входящие правила синхронизации (из Azure AD), не содержащие правил объединения, не обрабатываются при более низких значениях приоритета, в отличие от правил, содержащих правила объединения.

**Улучшения:**

* Добавлена поддержка установки Azure AD Connect на Windows Server 2016 Standard или более поздней версии.
* Добавлена поддержка использования SQL Server 2016 hello удаленной базы данных для Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Дата выпуска: август 2016 г.

**Исправленные проблемы:**

* Интервал toosync изменения вступают в месте после hello выполнена следующего цикла синхронизации.
* Мастер Azure AD Connect не принимает учетную запись Azure AD, если ее имя пользователя начинается с подчеркивания (\_).
* Мастер Azure AD Connect сбой учетной записи Azure AD tooauthenticate hello, если пароль учетной записи hello содержит слишком много специальные символы. Сообщение об ошибке «не удается toovalidate учетные данные. Произошла непредвиденная ошибка". .
* При удалении тестового сервера отключает синхронизации паролей в клиенте Azure AD и вызывает toofail синхронизации паролей с активного сервера.
* Синхронизация паролей к сбою в редких случаях не хранятся на пользователя hello хэш пароля.
* Если на сервере Azure AD Connect разрешен промежуточный режим, компонент обратной записи паролей временно не отключается.
* Мастер Azure AD Connect не показывает hello фактический пароль синхронизации и настройки обратной записи паролей, когда сервер находится в промежуточном режиме. Он всегда отображает их как отключенные.
* Синхронизации toopassword изменения конфигурации и обратная запись паролей, не сохраняются с помощью мастера Azure AD Connect, когда сервер находится в промежуточном режиме.

**Улучшения:**

* Обновить tooindicate командлет hello начала ADSyncSyncCycle как начало может toosuccessfully новый цикл синхронизации, так и не.
* Цикла синхронизации tooterminate добавлены hello Stop ADSyncSyncCycle командлета и операции, которые в настоящее время выполняется.
* Цикла синхронизации обновленной hello Stop ADSyncScheduler командлет tooterminate и операции, которые в настоящее время выполняется.
* При настройке [расширения каталогов](active-directory-aadconnectsync-feature-directory-extensions.md) в мастере Azure AD Connect, теперь можно выбрать атрибут типа «Телетекса строка» hello Azure AD.

## <a name="111890"></a>1.1.189.0
Дата выпуска: июнь 2016 г.

**Исправленные проблемы и внесенные улучшения:**

* Службу Azure AD Connect теперь можно устанавливать на FIPS-совместимом сервере.
  * Дополнительные сведения о синхронизации паролей см. в разделе [Синхронизация паролей и FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Устранена проблема, где NetBIOS-имя не удалось разрешить toohello полное доменное имя в hello Соединитель Active Directory.

## <a name="111800"></a>1.1.180.0
Дата выпуска: май 2016 г.

**Новые функции:**

* Предупреждает и помогает выполнить проверку доменов, если это не сделано перед запуском Azure AD Connect.
* Добавлена поддержка облака [Microsoft Cloud Germany](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Добавлена поддержка последнего hello [облако Microsoft Azure для государственных](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) инфраструктуру с новыми требованиями URL-адрес.

**Исправленные проблемы и внесенные улучшения:**

* Добавлены фильтрации toohello toomake редактор правил синхронизации его легко toofind правила синхронизации.
* Повышена производительность при удалении пространства соединителя.
* Устранена проблема, когда hello один объект был удален и добавлен в hello же запуска (вызываемой удаления или добавления).
* Отключенное правило синхронизации больше не будет повторно включать включенные объекты и атрибуты при обновлении версии или схемы.

## <a name="111300"></a>1.1.130.0
Дата выпуска: апрель 2016 г.

**Новые функции:**

* Добавлена поддержка для многозначных атрибутов слишком[расширения каталогов](active-directory-aadconnectsync-feature-directory-extensions.md).
* Добавлена поддержка Дополнительные варианты конфигурации для [автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md) toobe считается могут быть обновлены.
* Добавлены некоторые командлеты для [настраиваемого планировщика](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Дата выпуска: март 2016 г.

**Исправленные проблемы:**

* Отключена возможность быстрой установки в Windows Server 2008 (до выпуска R2), так как в этой операционной системе не поддерживается синхронизация паролей.
* Обновление из DirSync с конфигурацией пользовательского фильтра не работало как ожидалось.
* После обновления до более новой версии tooa существуют toohello без изменения конфигурации, не должна планироваться полного импорта или синхронизации.

## <a name="111100"></a>1.1.110.0
Дата выпуска: февраль 2016 г.

**Исправленные проблемы:**

* Обновление с более ранних версий не работает, если установка hello не в папку C:\Program Files по умолчанию hello.
* Если вы установите и снимите **запуска процесса синхронизации hello** конце hello приветствия мастера установки, выполнение мастера установки hello повторно не включит hello планировщика.
* Hello планировщика не работает должным образом на серверах, где hello формат даты и времени для английского языка США не используется. Он также будет блокировать `Get-ADSyncScheduler` tooreturn правильного времени.
* Если вы установили более раннего выпуска Azure AD Connect с AD FS как hello вариант входа и обновления, не может снова запустите мастер установки hello.

## <a name="111050"></a>1.1.105.0
Дата выпуска: февраль 2016 г.

**Новые функции:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) для тех, кто использует стандартные параметры.
* Поддержка hello глобального администратора с помощью многофакторной проверки подлинности Azure и управления привилегированными пользователями в мастере установки hello.
  * Требуется tooallow вашей tooalso прокси-сервер разрешает toohttps://secure.aadcdn.microsoftonline-p.com трафика при использовании многофакторной проверки подлинности.
  * Список доверенных узлов tooyour https://secure.aadcdn.microsoftonline-p.com tooadd требуется для работы tooproperly многофакторной проверки подлинности.
* Разрешить изменение способ входа пользователей hello после первоначальной установки.
* Разрешить [домен и Подразделение фильтрации](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) приветствия мастера установки. Это также позволяет подключение tooforests, где доступны не все домены.
* [Планировщик](active-directory-aadconnectsync-feature-scheduler.md) создается в модуле toohello синхронизации.

**Функции, перенесенных из tooGA предварительного просмотра:**

* [Обратная запись устройства](active-directory-aadconnect-feature-device-writeback.md).
* [Расширения каталога](active-directory-aadconnectsync-feature-directory-extensions.md).

**Новые функции предварительной версии:**

* Hello новый по умолчанию синхронизации цикл интервал составляет 30 минут. Использовать toobe трех часов для всех более ранних выпусков. Добавляет поддержку hello toochange [планировщика](active-directory-aadconnectsync-feature-scheduler.md) поведение.

**Исправленные проблемы:**

* Hello убедитесь, что страницу доменов DNS не удалось опознать всегда hello доменов.
* Запрос на ввод учетных данных администратора домена при настройке служб AD FS.
* Hello в локальном учетные записи AD не распознаются мастером установки hello, если находится в домене, в другом дереве DNS, чем hello корневого домена.

## <a name="1091310"></a>1.0.9131.0
Дата выпуска: декабрь 2015 г.

**Исправленные проблемы:**

* Синхронизация паролей при их изменении в Active Directory Domain Services (AD DS) может не работать, но работает при установке паролей.
* При наличии прокси-сервера, tooAzure проверки подлинности, который AD может завершиться ошибкой во время установки или при отмене обновления на странице конфигурации hello.
* Обновление предыдущего выпуска Azure AD Connect с полной версией сервера SQL Server завершается ошибкой при отсутствии прав системного администратора (SA) в среде SQL.
* Обновление с предыдущей версии Azure AD Connect с удаленным сервером SQL показана ошибка «не удается tooaccess hello база данных ADSync SQL» hello.

## <a name="1091250"></a>1.0.9125.0
Дата выпуска: ноябрь 2015 г.

**Новые функции:**

* Можно перенастроить tooAzure AD доверия AD FS.
* Можно обновить схему Active Directory hello и повторное создание правила синхронизации.
* Отключение правила синхронизации.
* Определение AuthoritativeNull как нового литерала в правиле синхронизации.

**Новые функции предварительной версии:**

* [Azure AD Connect Health для синхронизации](../connect-health/active-directory-aadconnect-health-sync.md).
* Поддержка синхронизации паролей [доменных служб Azure AD](../active-directory-passwords-update-your-own-password.md).

**Новый поддерживаемый сценарий:**

* Поддерживает несколько локальных организаций Exchange. Дополнительные сведения см. в статье [Гибридные развертывания в нескольких лесах Active Directory](https://technet.microsoft.com/library/jj873754.aspx).

**Исправленные проблемы:**

* Проблемы синхронизации паролей
  * Объект перемещен из области видимости вне области tooin не будет синхронизировать пароль. Это относится к фильтрации как подразделений, так и атрибутов.
  * При выборе нового Подразделения tooinclude синхронизации не требует полной синхронизации паролей.
  * При включении отключенного пользователя пароль hello не выполняется синхронизация.
  * очереди повторных попыток Hello пароль является бесконечным и 5000 toobe объектов удалено ограничение в предыдущих hello был удален.
* Не удается tooconnect tooActive каталога с уровнем режим работы леса Windows Server 2016.
* Не удается toochange hello группа используется для фильтрации группы после первоначальной установки hello.
* Больше не создает новый профиль пользователя на сервере hello Azure AD Connect для каждого пользователя, выполняющего изменения пароля с включенной функцией обратной записи паролей.
* Не удается toouse длинных целых значений области правила синхронизации.
* Если имеются контроллеры домена недоступен, Hello флажок «обратной записи устройства» останется отключенным.

## <a name="1086670"></a>1.0.8667.0
Дата выпуска: август 2015 г.

**Новые функции:**

* Hello Azure AD Connect, мастер установки сейчас локализованные языки tooall Windows Server.
* При использовании управления паролями Azure AD добавлена поддержка разблокирования учетной записи.

**Исправленные проблемы:**

* Мастер установки Azure AD Connect аварийно завершает работу, если другой пользователь по-прежнему установки, а не hello запустившего сначала hello установки.
* В случае предыдущего удаления из Azure AD Connect синхронизации Azure AD Connect toouninstall аккуратно, не возможных tooreinstall.
* Не удается установить Azure AD Connect, с помощью экспресс-установки, если пользователь hello не в корневом домене леса hello hello или если используется локализованная версия службы каталогов Active Directory.
* Если не удается разрешить полное доменное имя учетной записи пользователя Active Directory hello hello, отображается в заблуждение сообщение об ошибке Сбой toocommit hello «схема».
* Изменении hello учетная запись, используемая на hello Соединитель Active Directory за пределами мастере приветствия мастера hello завершится ошибкой при последующих запусках.
* Azure AD Connect иногда не удается выполнить tooinstall на контроллере домена.
* Невозможно включить и отключить промежуточный режим, если были добавлены атрибуты расширения.
* Обратная запись паролей происходит сбой из-за неправильного пароля на hello Соединитель Active Directory в некоторых конфигурациях.
* DirSync невозможно обновить, если при фильтрации атрибутов используется различающееся имя (DN).
* Чрезмерное использование ресурсов ЦП при использовании сброса пароля.

**Удаленные функции предварительной версии:**

* Предварительная версия функции Hello [обратной записи пользователей](active-directory-aadconnect-feature-preview.md#user-writeback) временно был удален на основе отзывов клиентов предварительной версии корпорации Майкрософт. Он добавляется позже после обсуждалась hello, предоставленный отзыв.

## <a name="1086410"></a>1.0.8641.0
Дата выпуска: июнь 2015 г.

**Первоначальный выпуск Azure AD Connect.**

Измененные имена из Azure AD Sync tooAzure AD Connect.

**Новые функции:**

* установка [со стандартными параметрами](active-directory-aadconnect-get-started-express.md);
* возможность [настройки AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs);
* возможность [обновления из DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md);
* [Предотвращение случайного удаления](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Добавлен [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode)

**Новые функции предварительной версии:**

* [Обратная запись пользователей](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Обратная запись групп](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Обратная запись устройств](active-directory-aadconnect-feature-device-writeback.md)
* [Расширения каталогов](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Дата выпуска: май 2015 г.

**Новое требование:**

* Azure AD Sync теперь требуется hello .NET Framework версии 4.5.1 toobe установлен.

**Исправленные проблемы:**

* Компонент обратной записи паролей из Azure AD завершается ошибкой подключения к служебной шине.

## <a name="104910413"></a>1.0.491.0413
Дата выпуска: апрель 2015 г.

**Исправленные проблемы и внесенные улучшения:**

* Соединитель Active Directory Hello неправильно обрабатывает удаления, если включена Корзина hello и имеется несколько доменов в лесу hello.
* Улучшена производительность Hello операций импорта для hello соединителя Azure Active Directory.
* При группа превышала лимит членства hello (по умолчанию hello ограничение установлено равным too50 000 объектов), hello группа была удалена в Azure Active Directory. С помощью нового поведения hello hello группа не удаляется, возникает ошибка и новые изменения членства не экспортируются.
* Новый объект не может быть подготовлен, если промежуточное удаление с hello таким же доменным Именем уже существует в пространство соединителя hello.
* Некоторые объекты помечаются для синхронизации при синхронизации изменений, несмотря на то, что нет изменений для промежуточного хранения на hello объекта.
* Принудительная синхронизация паролей также удаляет список hello основной контроллер домена.
* В CSExportAnalyzer возникают проблемы с некоторыми состояниями объектов.

**Новые функции:**

* Соединение теперь может подключать слишком «любой» тип объекта в hello MV.

## <a name="104850222"></a>1.0.485.0222
Дата выпуска: февраль 2015 г.

**Улучшения:**

* Улучшена производительность импорта.

**Исправленные проблемы:**

* Синхронизация паролей учитывает атрибут cloudFiltered hello, используемый при фильтрации атрибутов. Отфильтрованные объекты больше не будут находиться в области видимости для синхронизации паролей.
* В редких случаях, где hello топологии имелось много контроллеров домена не работает синхронизация паролей.
* «Stopped-server» при импорте из соединителя Azure AD hello после управления устройствами работает в Azure AD или Intune.
* Присоединение внешних участников безопасности из нескольких доменов в одном и том же лесу приводит к ошибке неоднозначного соединения.

## <a name="104751202"></a>1.0.475.1202
Дата выпуска: декабрь 2014 г.

**Новые функции:**

* Теперь поддерживается синхронизация паролей с фильтрацией на основе атрибутов. Дополнительные сведения см. в статье [Службы синхронизации Azure AD Connect: настройка фильтрации](active-directory-aadconnectsync-configure-filtering.md).
* Атрибут msDS-ExternalDirectoryObjectID Hello записываются обратно tooActive каталога. Эта функция добавляет поддержку приложений Office 365. Она использует OAuth2 tooaccess Online и локальным почтовым ящикам в гибридном развертывании Exchange.

**Исправленные проблемы обновления:**

* На сервере hello доступна более новая версия помощника по входу hello.
* Пользовательский путь установки был tooinstall используется Azure AD Sync.
* Обновление hello блоки критерий недопустимый пользовательские соединения.

**Другие исправления:**

* Фиксированный hello шаблоны для Office Pro Plus.
* Исправлены проблемы с установкой, связанные с именами пользователей, которые начинаются с дефиса.
* Фиксированный проигравшей hello параметра sourceAnchor при запуске мастера установки hello еще раз.
* Исправлена трассировка ETW для синхронизации паролей.

## <a name="104701023"></a>1.0.470.1023
Дата выпуска: октябрь 2014 г.

**Новые функции:**

* Синхронизация паролей нескольких локальных tooAzure Active Directory AD.
* Локализованные языки интерфейса tooall Windows Server для установки.

**Обновление с версии AADSync 1.0 GA**

Если уже установлен в Azure AD Sync, есть один дополнительный шаг, имеют tootake, если вы изменили ни одному из правил синхронизации out-of-box hello. После обновления выпуска toohello 1.0.470.1023 hello правила синхронизации с измененной дублируются. Для каждого правила синхронизации измененные hello следующие:

1.  Найдите правило синхронизации hello изменены и запишите изменения hello.
* Удалите правило синхронизации hello.
* Найдите hello новое правило синхронизации, создаваемый службой Azure AD Sync и затем повторно примените изменения hello.

**Разрешения для учетной записи Active Directory hello**

Hello учетной записи Active Directory должны быть предоставлены хэши паролей hello может tooread toobe дополнительные разрешения из Active Directory. toogrant разрешения Hello именуются «Репликация изменений каталога» и «Репликация всех изменений каталога.» Оба эти разрешения являются хэши паролей требуется toobe может tooread hello.

## <a name="104190911"></a>1.0.419.0911
Дата выпуска: сентябрь 2014 г.

**Первоначальный выпуск Azure AD Sync.**

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
