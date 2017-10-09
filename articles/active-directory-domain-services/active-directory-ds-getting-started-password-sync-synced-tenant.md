---
title: "Доменные службы Azure AD. Включение синхронизации паролей | Документация Майкрософт"
description: "Приступая к работе с доменными службами Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Включение синхронизации паролей tooAzure доменных служб Active Directory
Выполняя предыдущие задачи, вы включили доменные службы Azure Active Directory для клиента Azure Active Directory (Azure AD). Следующая задача Hello-tooenable синхронизации хэшей учетные данные, необходимые для tooAzure проверки подлинности NT LAN Manager (NTLM) и Kerberos доменные службы AD. После настройки синхронизации учетных данных, пользователи могут входить в управляемый домен toohello со своими корпоративными учетными данными.

этапы Hello отличаются для учетных записей пользователя только для облака учетные записи vs, которые синхронизируются из вашего локального каталога с помощью Azure AD Connect. Если клиент Azure AD имеет сочетание облако только пользователей и пользователей из локальной AD, необходимо tooperform оба шага.

<br>

> [!div class="op_single_selector"]
> * **Учетные записи пользователей только для облака**: [синхронизации паролей для облачных учетных записей пользователей tooyour управляемого домена](active-directory-ds-getting-started-password-sync.md)
> * **Локальные учетные записи пользователей**: [синхронизировать пароли для учетных записей пользователей, синхронизированных из локальной AD tooyour управляемого домена](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Задача 5: Включение пароль tooyour управляемого домена синхронизации учетных записей пользователей, синхронизированные с локальным AD
Объект синхронизации Azure AD клиента задается toosynchronize с локального каталога вашей организации с помощью Azure AD Connect. По умолчанию Azure AD Connect не выполняет синхронизацию, NTLM и Kerberos tooAzure хэши учетных данных AD. toouse доменные службы Azure AD необходимо хэш tooconfigure Azure AD Connect toosynchronize учетные данные, которые требуются для проверки подлинности NTLM и Kerberos. следующие шаги Hello включить синхронизацию хэши hello необходимых учетных данных из клиента Azure AD tooyour локального каталога.

> [!NOTE]
> Если ваша организация использует учетные записи пользователей, которые синхронизируются из вашего локального каталога, необходимо включить синхронизацию хэшей NTLM и Kerberos в порядке toouse hello управляемый домен. Синхронизированные учетная запись расположена синхронизированную учетную запись, которая была создана в ваш локальный каталог и является tooyour клиента Azure AD, используя Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Установка или обновление Azure AD Connect
Установить последние рекомендуется hello выпуска Azure AD Connect на домен присоединен компьютер. Если у вас есть существующий экземпляр программы установки Azure AD Connect, необходимо tooupdate его toouse hello последнюю версию Azure AD Connect. Известные проблемы и ошибки, которые могут уже была исправлена, tooavoid убедитесь, что всегда использовать последнюю версию Azure AD Connect hello.

**[Загрузка Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Рекомендуемая версия: **1.1.553.0** (опубликована 27 июня 2017 г.).

> [!WARNING]
> НЕОБХОДИМО установить hello выпуска Azure AD Connect tooenable hello устаревший пароль учетных данных (требуется для проверки подлинности NTLM и Kerberos) toosynchronize tooyour Azure AD клиента, рекомендуется использовать последнюю версию. Эта функция недоступна в предыдущих версиях Azure AD Connect, или с устаревшего средства DirSync hello
>
>

Инструкции по установке для Azure AD Connect доступны в следующих hello статьи базы знаний - [Приступая к работе с Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Включение синхронизации NTLM и Kerberos tooAzure хэши учетных данных AD
Выполните следующий сценарий PowerShell в каждом лесу, синхронизация паролей полного tooforce hello и включить клиент хэши toosync tooyour Azure AD для всех пользователей в локальной учетных данных. Этот сценарий включает hello хэши учетных данных, необходимых для клиента синхронизированные tooyour Azure AD toobe проверки подлинности NTLM или Kerberos.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

В зависимости от размера каталога hello (число пользователей, групп и т.д.), синхронизации учетных данных хэширует tooAzure AD занимает время. пароли Hello будет использовать на управляемый домен доменные службы Azure AD hello вскоре после синхронизации tooAzure AD hello хэши учетных данных.

<br>

## <a name="related-content"></a>Похожий контент
* [Включение синхронизации паролей tooAAD только для облака Azure в доменных службах AD directory](active-directory-ds-getting-started-password-sync.md)
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Присоединение виртуальной машины tooan доменные службы Azure AD управляемого домена Windows](active-directory-ds-admin-guide-join-windows-vm.md)
* [К домену Red Hat Enterprise Linux виртуальной машины tooan доменные службы Azure AD управляемого](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
