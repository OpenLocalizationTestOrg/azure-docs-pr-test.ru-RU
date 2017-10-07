---
title: "aaaCertificate обновления для пользователей Office 365 и Azure AD | Документы Microsoft"
description: "В этой статье описываются tooOffice 365 пользователей как tooresolve проблемы с сообщения электронной почты, уведомлением об обновлении сертификата."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Обновление сертификатов федерации для Office 365 и Azure AD
## <a name="overview"></a>Обзор
Для успешного федерации между Azure Active Directory (Azure AD) и службы федерации Active Directory (AD FS) hello сертификаты, используемые службой маркеров безопасности tooAzure AD для AD FS toosign должно соответствовать настроенным в Azure AD. Любые различия можно привести toobroken доверия. Azure AD гарантирует, что эта информация синхронизируется при развертывании AD FS и прокси веб-приложения (для доступа к экстрасети).

В этой статье предоставляет дополнительные сведения о toomanage сертификаты подписи токена и синхронизировать их с помощью Azure AD в hello в следующих случаях:

* Hello прокси веб-приложения не развертываются и поэтому метаданные федерации hello недоступен в экстрасети hello.
* Конфигурация по умолчанию hello AD FS не используются для сертификатов для подписи маркеров.
* Вы используете сторонний поставщик удостоверений.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Стандартная конфигурация AD FS для сертификатов для подписи маркеров
для подписи маркера Hello и сертификаты расшифровки маркера, обычно самозаверяющие сертификаты и подходят для одного года. По умолчанию AD FS предусматривает процесс автоматического возобновления действия, который называется **AutoCertificateRollover**. Если вы используете AD FS 2.0 или более поздней версии, службы Office 365 и Azure AD автоматически обновят ваш сертификат до окончания срока его действия.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Уведомление обновления из портала Office 365 hello или сообщение электронной почты
> [!NOTE]
> Если вы получили сообщение электронной почты или портала уведомления, запрашивающее toorenew сертификат для Office, в разделе [управление изменяет сертификаты подписи tootoken](#managecerts) toocheck при необходимости tootake какие-либо действия. Корпорации Майкрософт известно возможная проблема, которая может привести к получению toonotifications для обновления сертификатов, которые были отправлены, даже в том случае, если не требуется никаких действий.
>
>

Azure AD попыток метаданных федерации toomonitor hello и токен hello обновления сертификатов подписи, как указано в метаданных. 30 дней до истечения срока действия hello сертификатов подписи токена hello Azure AD проверяет, если доступны новые сертификаты путем опроса hello метаданных федерации.

* Если он успешно опрашивать метаданных федерации hello и получить новые сертификаты hello, никакого уведомления по электронной почте или предупреждения в портал Office 365 hello выдается toohello пользователя.
* Если не удалось получить новый маркер hello сертификаты подписи, либо потому, что метаданные федерации hello недоступен или не включена операция переключения сертификата автоматическое, Azure AD выдает уведомление по электронной почте и предупреждение портала Office 365 hello.

![Уведомление на портале Office 365](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Если вы используете службы федерации Active Directory, tooensure непрерывность бизнес-процессов, убедитесь, серверы имеют hello, после обновления, чтобы не происходят сбои проверки подлинности для известных проблем. Это позволит устранить известные проблемы с прокси-сервером AD FS при текущем и последующем возобновлении действия сертификатов.
>
> Server 2012 R2 — [Накопительный пакет обновления от мая 2014 г. для Windows RT 8.1, Windows 8.1 и Windows Server 2012 R2](http://support.microsoft.com/kb/2955164).
>
> Server 2008 R2 и 2012 — [Authentication through proxy fails in Windows Server 2012 or Windows Server 2008 R2 SP1](http://support.microsoft.com/kb/3094446)
>
>

## Проверьте, если hello сертификаты должны обновить toobe<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Шаг 1: Проверьте состояние AutoCertificateRollover hello
На сервере AD FS откройте PowerShell. Проверьте, что hello AutoCertificateRollover имеет значение tooTrue.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>При использовании AD FS 2.0 необходимо сначала выполнить команду Add-Pssnapin Microsoft.Adfs.Powershell.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Шаг 2. Убедитесь, что службы AD FS и Azure AD синхронизированы
На сервере AD FS откройте строку hello Azure AD PowerShell и подключитесь tooAzure AD.

> [!NOTE]
> Вы можете скачать Azure AD PowerShell [здесь](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Проверьте сертификаты hello настроены в AD FS и свойства отношений доверия Azure AD для hello указанного домена.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Если отпечатки hello в обоих hello выходы совпадения, ваши сертификаты синхронизированы с Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Шаг 3: Проверьте, является ли сертификат о tooexpire
В выходных данных hello Get-MsolFederationProperty или Get-AdfsCertificate проверьте дату hello в разделе «Не после.» Если дата hello немедленно менее 30 дней, необходимо принять действие.

| AutoCertificateRollover | Сертификаты синхронизированы с Azure AD | Метаданные федерации общедоступны | Срок действия | Действие |
|:---:|:---:|:---:|:---:|:---:|
| Да |Да |Да |- |Никаких действий не требуется. См. раздел [Автоматическое возобновление действия сертификата для подписи маркера](#autorenew). |
| Да |Нет |- |Менее 15 дней |Обновите немедленно. См. раздел [Возобновление действия сертификата для подписи маркера вручную](#manualrenew). |
| Нет |- |- |Менее 30 дней |Обновите немедленно. См. раздел [Возобновление действия сертификата для подписи маркера вручную](#manualrenew). |

\[-] — не имеет значения

## Обновления автоматически сертификат для подписи маркера hello (рекомендуется)<a name="autorenew"></a>
Не требуется tooperform какие-то действия, если выполняются оба указанных ниже hello:

* Развертывания прокси веб-приложения, позволяющие получить доступ к метаданным федерации toohello из экстрасети hello.
* Используется конфигурация по умолчанию hello AD FS (AutoCertificateRollover включен).

Убедитесь, что hello следующие tooconfirm, hello сертификатов могут обновляться автоматически.

**1. hello AD FS свойство AutoCertificateRollover должно быть задано tooTrue.** Это означает, что службы федерации Active Directory автоматически создаст новый подписи маркеров и сертификаты для расшифровки токенов, прежде чем те, срок действия старых hello.

**2. метаданные федерации hello AD FS является общедоступным.** Убедитесь, что метаданные федерации, перейдя по toohello общедоступный следующий URL-адрес с компьютера hello общедоступный Интернет (за пределами корпоративной сети hello):

https://(ваше_имя_FS)/federationmetadata/2007-06/federationmetadata.xml

где `(your_FS_name) `заменяется hello имя службы федерации узел использует вашей организации, например fs.contoso.com.  При наличии возможности tooverify обоих этих параметров успешно, у вас toodo других действий.  

Пример: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Обновить hello сертификат подписи токена вручную<a name="manualrenew"></a>
Вы можете toorenew сертификаты для подписи токенов hello вручную. Например hello следующие сценарии могут лучше подходит для ручного обновления:

* Сертификаты для подписи маркеров не являются самозаверяющими. Hello наиболее распространенной причиной этого является то, что ваша организация управляет AD FS сертификатов, выдаваемых ЦС организации.
* Сетевая безопасность не допускает toobe метаданные федерации hello общедоступным.

В этих сценариях каждый раз при обновлении сертификатов, для подписи маркеров hello необходимо также обновить доменом Office 365 с помощью команды PowerShell hello, Update-MsolFederatedDomain.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Шаг 1. Убедитесь, что в службах AD FS используются новые сертификаты для подписи маркеров
**Нестандартная конфигурация**

При использовании нестандартной конфигурации AD FS, (где **AutoCertificateRollover** задано слишком**False**), возможно, вы используете пользовательские сертификаты (не самозаверяющий). Дополнительные сведения о том, как toorenew hello AD FS сертификатов подписи маркеров см. в разделе [рекомендации для клиентов, не использующих AD FS самозаверяющие сертификаты](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Метаданные федерации не являются общедоступными**

На hello другой стороны, если **AutoCertificateRollover** задано слишком**True**, но метаданные федерации не является общедоступным, сначала убедитесь, что новый сертификат для подписи маркера было создано с AD ФЕДЕРАЦИИ ACTIVE DIRECTORY. Убедитесь, что у вас есть новый маркер подписи сертификатов, выполнив hello следующие шаги:

1. Убедитесь, что вы вошли на сервер toohello первичного AD FS.
2. Проверьте текущие сертификаты подписи hello в AD FS, открыв окно командной строки PowerShell и выполнив hello следующую команду:

    PS C:\>Get-ADFSCertificate –CertificateType token-signing

   > [!NOTE]
   > При использовании AD FS 2.0 необходимо сначала выполнить команду Add-Pssnapin Microsoft.Adfs.Powershell.
   >
   >
3. Посмотрите на выходные данные команды hello во все сертификаты в списке. Если AD FS создан новый сертификат, вы увидите два сертификата в выходных данных hello: один для какой hello **IsPrimary** значение **True** и hello **NotAfter** Дата в течение 5 дней и один для которого **IsPrimary** — **False** и **NotAfter** о год в будущем hello.
4. Если только один сертификат в разделе, а hello **NotAfter** дата находится в пределах 5 дней, вы должны toogenerate новый сертификат.
5. toogenerate новый сертификат, выполните следующую команду в командной строке PowerShell hello: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Проверка обновления hello, выполнив следующую команду еще раз hello: PS C:\>Get-ADFSCertificate — CertificateType подписи токена

Теперь будут указаны два сертификата, один из которых имеет **NotAfter** Дата приблизительно на год в будущем hello и какие hello **IsPrimary** значение **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Шаг 2: Обновление hello новый маркер подписи сертификатов для доверия hello Office 365
Обновление Office 365 с hello новый маркер подписи сертификатов toobe использовать hello отношений доверия, следующим образом.

1. Откройте hello Microsoft Azure Active Directory модуля для Windows PowerShell.
2. Запустите $cred=Get-Credential. Если этот командлет запрашивает учетные данные, введите данные учетной записи администратора облачных служб.
3. Запустите Connect-MsolService –Credential $cred. Этот командлет подключается toohello облачной службы. Перед выполнением дополнительных командлетов hello устанавливается средством hello требуется создание контекста, который используется для подключения toohello облачной службы.
4. Если эти команды выполняются на компьютере, который не является hello AD FS основной сервер федерации, выполните Set-MSOLAdfscontext-компьютере <AD FS primary server>, где <AD FS primary server> является hello внутреннее полное ДОМЕННОЕ имя сервера hello основной AD FS. Этот командлет создает контекст, который подключает вас tooAD федерации Active Directory.
5. Выполните команду Update-MSOLFederatedDomain -DomainName <domain>. Этот командлет обновляет параметры hello от AD FS в облачную службу hello и настраивает hello доверительных отношений между двумя hello.

> [!NOTE]
> Если вам требуется toosupport нескольких доменов верхнего уровня, например contoso.com и fabrikam.com, необходимо использовать hello **SupportMultipleDomain** с любым командлетом. Дополнительные сведения см. в статье [Поддержка нескольких доменов для федерации с Azure AD](active-directory-aadconnect-multiple-domains.md).
>
>

## Восстановление доверия Azure AD с помощью Azure AD Connect <a name="connectrenew"></a>
Если вы настроили вашей фермы AD FS и отношение доверия Azure AD с помощью Azure AD Connect, можно использовать toodetect Azure AD Connect, если требуется tootake какие-либо действия для сертификатов подписи токена. При необходимости toorenew hello сертификаты можно использовать Azure AD Connect toodo таким образом.

Дополнительные сведения см. в разделе [восстановление hello доверия](active-directory-aadconnect-federation-management.md).
