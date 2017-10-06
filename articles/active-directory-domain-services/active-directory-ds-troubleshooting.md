---
title: "Доменные службы Azure Active Directory: руководство по устранению неполадок | Документация Майкрософт"
description: "Руководство по устранению неполадок для доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Доменные службы Azure AD: руководство по устранению неполадок
В этой статье приводятся советы по устранению проблем, с которыми вы можете столкнуться при настройке или администрировании доменных служб Azure Active Directory (AD).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Не удается включить доменные службы Azure AD для каталога Azure AD
Этот раздел поможет Устранение ошибок при попытке tooenable доменные службы Azure AD для каталога и не или получает переключается назад too'Disabled ".

Выберите действия, соответствующие toohello сообщение об ошибке появиться hello.

| **Сообщение об ошибке** | **Способы устранения:** |
| --- |:--- |
| *Hello contoso100.com имя уже используется в этой сети. Введите неиспользуемое имя.* |[Конфликт имен домена в виртуальной сети hello](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Не удалось включить доменных служб в этом клиенте Azure AD. Hello службы не имеет соответствующих разрешений toohello приложение с именем «Домен Azure AD Sync Services». Удалите приложение hello с именем «Домен Azure AD Sync Services», а затем повторите tooenable доменных служб для вашего клиента Azure AD.* |[Доменные службы нет соответствующих разрешений toohello домен Azure AD Sync Services приложения](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Не удалось включить доменных служб в этом клиенте Azure AD. Hello доменных служб приложения в клиенте Azure AD не имеют hello необходимые разрешения tooenable доменных служб. Удаление приложения hello с d87dcbc6-a371-462e-88e3-28ad15ec4e64 идентификатор приложения hello, а затем повторите tooenable доменных служб для вашего клиента Azure AD.* |[неправильно настроен Hello доменных служб приложения в клиенте](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Не удалось включить доменных служб в этом клиенте Azure AD. Hello приложения Microsoft Azure AD отключено в клиенте Azure AD. Включение приложения hello с 00000002-0000-0000-c000-000000000000 идентификатор приложения hello, а затем повторите tooenable доменных служб для вашего клиента Azure AD.* |[приложения Microsoft Graph Hello отключена в клиенте Azure AD](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Конфликт доменных имен
**Сообщение об ошибке:**

*Hello contoso100.com имя уже используется в этой сети. Введите неиспользуемое имя.*

**Исправление:**

Убедитесь, что у вас существующего домена с hello таким же именем домена, виртуальной сети. Например предполагается, что домена с именем «contoso.com» уже есть на выбранной виртуальной сети hello. Позднее, повторите tooenable управляемый домен доменные службы Azure AD с hello таким же именем домена (то есть, «contoso.com») в этой виртуальной сети. Возникновение сбоя при попытке службы домена tooenable Azure AD.

Это происходит из-за конфликтов tooname hello доменное имя виртуальной сети. В этом случае необходимо использовать tooset другое имя копии управляемого домена доменные службы Azure AD. Кроме того можно отменять подготовки hello существующего домена и затем следуют tooenable Azure AD доменных служб.

### <a name="inadequate-permissions"></a>Недостаточно разрешений
**Сообщение об ошибке:**

*Не удалось включить доменных служб в этом клиенте Azure AD. Hello службы не имеет соответствующих разрешений toohello приложение с именем «Домен Azure AD Sync Services». Удалите приложение hello с именем «Домен Azure AD Sync Services», а затем повторите tooenable доменных служб для вашего клиента Azure AD.*

**Исправление:**

Проверьте toosee, если приложение с именем hello «Домен Azure AD Sync Services» в каталоге Azure AD. Если такое приложение есть, удалите его, а затем повторно включите доменные службы Azure AD.

Выполнить hello следующие шаги toocheck hello наличие приложения hello и toodelete его, если существует приложение hello:

1. Перейдите toohello **классический портал Azure** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Выберите hello **Active Directory** узел в левой области hello.
3. Выберите hello Azure AD клиента (каталог), для которого вы хотите tooenable служб домена Azure AD.
4. Перейдите toohello **приложений** вкладки.
5. Выберите hello **приложений, которыми владеет Моя компания** вариант в раскрывающемся списке hello.
6. Проверьте наличие приложения **Azure AD Domain Services Sync**. Если приложение hello существует, переходите toodelete его.
7. После удаления приложения hello еще раз попробуйте tooenable Azure AD доменных служб.

### <a name="invalid-configuration"></a>Недопустимая конфигурация
**Сообщение об ошибке:**

*Не удалось включить доменных служб в этом клиенте Azure AD. Hello доменных служб приложения в клиенте Azure AD не имеют hello необходимые разрешения tooenable доменных служб. Удаление приложения hello с d87dcbc6-a371-462e-88e3-28ad15ec4e64 идентификатор приложения hello, а затем повторите tooenable доменных служб для вашего клиента Azure AD.*

**Исправление:**

Проверьте toosee, если у вас есть приложение с именем hello «AzureActiveDirectoryDomainControllerServices» (с идентификатором приложения из d87dcbc6-a371-462e-88e3-28ad15ec4e64) в каталоге Azure AD. Если это приложение существует, необходимо toodelete его и затем повторно включите Azure доменные службы AD.

Используйте следующие приложения hello toofind сценария PowerShell hello и удалите его.

> [!NOTE]
> В этом скрипте используются командлеты **Azure AD PowerShell версии 2**. Полный список всех доступных командлетов и toodownload hello модуля чтения hello [справочная документация по AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Интерфейс Microsoft Graph отключен
**Сообщение об ошибке:**

Не удалось включить доменные службы в этом клиенте Azure AD. Hello приложения Microsoft Azure AD отключено в клиенте Azure AD. Включение приложения hello с 00000002-0000-0000-c000-000000000000 идентификатор приложения hello, а затем повторите tooenable доменных служб для вашего клиента Azure AD.

**Исправление:**

Проверьте toosee при отключении приложение с идентификатором hello 00000002-0000-0000-c000-000000000000. Это приложение является приложением Microsoft Azure AD hello и предоставляет клиенту tooyour Azure AD Graph API доступа. Доменные службы Azure AD должен toosynchronize toobe включена этого приложения, управляемые вашей tooyour клиента Azure AD домена.

tooresolve эту ошибку, включите это приложение, затем повторите tooenable доменных служб для вашего клиента Azure AD.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Пользователи, не удается toosign в toohello управляемого домена доменные службы Azure AD
Если одного или нескольких пользователей в клиенте Azure AD не удается toosign в только что созданный toohello управляемого домена, выполните следующие действия по устранению неполадок hello:

* **Войдите в систему в формате UPN:** повторите toosign в формате имени участника-пользователя hello (например, "joeuser@contoso.com") вместо формата SAMAccountName hello (CONTOSO\joeuser). Hello SAMAccountName могут создаваться автоматически для пользователей, префикс которого имя участника-пользователя слишком длинное или hello же имени другого пользователя на управляемый домен hello. формат имени участника-пользователя Hello гарантируется toobe уникальным в пределах клиента Azure AD.

> [!NOTE]
> Мы рекомендуем использовать toosign формат имени участника-пользователя hello в управляемый домен toohello доменные службы Azure AD.
>
>

* Убедитесь, что [включена синхронизация паролей](active-directory-ds-getting-started-password-sync.md) в соответствии с hello шаги, описанные в руководстве по началу работы hello.
* **Внешних учетных записей:** убедитесь, что учетная запись пользователя hello влияет внешней учетной записи в клиенте hello Azure AD. К примерам внешних учетных записей относятся учетные записи Майкрософт (например, joe@live.com) или учетные записи из внешнего каталога Azure AD. Так как доменные службы Azure AD не имеет учетных данных для таких учетных записей пользователей, этих пользователей не удается войти toohello управляемый домен.
* **Синхронизированные учетные записи:** Если hello затронутые учетные записи пользователей будут синхронизированы из локального каталога, убедитесь, что:

  * Развертывания или обновления toohello [выпуск Azure AD Connect, рекомендуется использовать последнюю версию](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Вы настроили Azure AD Connect слишком[выполнить полную синхронизацию](active-directory-ds-getting-started-password-sync.md).
  * В зависимости от размера каталога hello он может занять некоторое время для учетных записей пользователей и учетных данных toobe хэши, доступных в доменные службы Azure AD. Убедитесь, что ожидания достаточно долго, прежде чем повторять проверку подлинности (в зависимости от размера каталога - день tooa несколько часов или два больших каталогов hello).
  * Если проблема hello, сохраняется после проверки hello в предыдущих шагах, попробуйте перезагрузить hello службы Microsoft Azure AD Sync. Компьютера синхронизации Запустите командную строку и выполните следующие команды hello:

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **Учетные записи только для облака**: Если hello затронутых учетная запись пользователя является учетной записью пользователя только для облака, убедитесь, hello пользователь изменил пароль, после включения доменные службы Azure AD. В результате этого действия учетных данных hello хэши, необходимые для созданных toobe доменные службы Azure AD.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Пользователи, удаленные из вашего клиента Azure AD, не удаляются из управляемого домена
Azure AD обеспечивает защиту от случайного удаления объектов-пользователей. При удалении учетной записи пользователя с клиентом Azure AD hello соответствующего объекта-пользователя является перемещенный toohello корзины. При этой операции удаления управляемого домена синхронизированные tooyour то hello соответствующий toobe учетной записи пользователя помечен отключено. Эта функция позволяет восстановить или Отмена удаления учетной записи пользователя hello позже.

Здравствуйте, остается в hello в отключенном состоянии в управляемых домена учетной записи пользователя, даже если повторно создать учетную запись пользователя с hello того же имени участника-пользователя в каталоге Azure AD. tooremove hello учетная запись пользователя из управляемого домена, необходимо tooforce удалить его из вашего клиента Azure AD.

Учетная запись пользователя tooremove hello полностью из управляемого домена, окончательно удалить hello пользователей из вашего клиента Azure AD. С помощью командлета PowerShell Remove-MsolUser hello с hello "-RemoveFromRecycleBin" параметра, как описано в этом [статьи MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Свяжитесь с нами
Обратитесь в службу продукта доменных служб Active Directory Azure hello слишком[совместно используют отзывы или поддержку](active-directory-ds-contact-us.md).
