---
title: "Приступая к работе aaaAzure проверки подлинности на основе сертификатов Active Directory - | Документы Microsoft"
description: "Узнайте, как tooconfigure на основе сертификатов проверки подлинности в вашей среде"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory

Проверка подлинности на основе сертификатов обеспечивает toobe проверку подлинности Azure Active Directory с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетную Exchange online с: 

- мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;   

- клиентам Exchange ActiveSync (EAS). 

Эта настройка устраняет необходимость hello tooenter имя пользователя и пароль к нему в определенных почты и приложения Microsoft Office на мобильных устройствах. 

В этой статье:

- Предоставляет вам hello tooconfigure шаги, чтобы использовать на основе сертификатов проверки подлинности для пользователей клиентов в Office 365 Enterprise, Business, образовательных учреждений и планы правительства США. В тарифных планах Office 365 China, US Government Defense и US Government Federal доступна предварительная версия этой функции. 

- Предполагается, что у вас уже настроены [инфраструктура открытых ключей (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) и [AD FS](connect/active-directory-aadconnectfed-whatis.md).    


## <a name="requirements"></a>Требования

tooconfigure сертификат проверки подлинности на основе hello должны выполняться следующие условия:  

- Аутентификация на основе сертификата (CBA) поддерживается только для браузерных приложений и собственных клиентов в федеративных средах, использующих современную аутентификацию (ADAL). Hello единственное исключение — Exchange Active Sync (EAS) для EXO, который может использоваться для учетных записей, федеративным и управляемым. 

- в Azure Active Directory необходимо включить Hello корневым центром сертификации и промежуточный центр сертификации.  

- Каждый центр сертификации должен иметь список отзыва сертификатов (CRL), на который можно сослаться с помощью URL-адреса для Интернета.  

- В Azure Active Directory должен быть настроен хотя бы один центр сертификации. Связанные действия можно найти в hello [Настройка центров сертификации hello](#step-2-configure-the-certificate-authorities) раздела.  

- Для клиентов Exchange ActiveSync hello клиентский сертификат должен иметь hello маршрутизируемый адрес электронной почты пользователя адрес в Exchange online в любом hello имени участника-службы или hello имя RFC822 значение hello альтернативное имя субъекта. Azure Active Directory сопоставляет атрибут hello RFC822 значения toohello адрес прокси-сервера в каталоге hello.  

- Устройство клиента должны иметь доступ по крайней мере одно tooat центр сертификации, выдающий сертификаты клиента.  

- Сертификат клиента для проверки подлинности клиента должен быть выдан tooyour клиента.  




## <a name="step-1-select-your-device-platform"></a>Шаг 1. Выбор платформы устройства

В качестве первого шага для hello платформы устройств, которые вас интересуют, необходимы следующие tooreview hello.

- Поддержка мобильных приложений Office Hello 
- требования к реализации Hello  

Привет, связанные с существует сведения для следующих платформ устройств hello:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Шаг 2: Настройка центров сертификации hello 

tooconfigure центров сертификации в Azure Active Directory для каждого центра сертификации передачи hello следующие: 

* Hello открытую часть сертификата hello в *.cer* формат 
* Hello в Интернете URL-адреса, где hello списков отзыва сертификатов (CRL) находятся

Схема Hello для сертификации выглядит следующим образом: 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Для конфигурации hello, можно использовать hello [Azure Active Directory PowerShell версии 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Запустите Windows PowerShell с правами администратора. 
2. Установите модуль hello Azure AD. Требуется версия tooinstall [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) или более поздней версии.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

В конфигурации, сначала должны tooestablish соединение с клиентом. Как только клиент tooyour подключение существует, можно просмотреть, добавить, удалить и изменить hello доверенных центров сертификации, которые определены в каталоге. 

### <a name="connect"></a>Подключение

соединение с клиентом, используйте hello tooestablish [Connect AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) командлета:

    Connect-AzureAD 


### <a name="retrieve"></a>Получение 

tooretrieve hello доверенных центров сертификации, определенные в каталоге, использовать hello [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Добавить

toocreate доверенным центром сертификации, использовать hello [New AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета и набор hello **crlDistributionPoint** tooa правильное значение атрибута: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Удалить

tooremove доверенным центром сертификации, использовать hello [AzureADTrustedCertificateAuthority удаление](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Изменение

toomodify доверенным центром сертификации, использовать hello [AzureADTrustedCertificateAuthority набор](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) командлета:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Шаг 3. Настройка отзыва

toorevoke сертификат клиента Azure Active Directory выбирается сертификат hello список отзыва (CRL) из URL-адресов hello загружены как часть информации о центрах сертификации сертификат и кэширует его. Hello последней публикации отметки времени (**Дата вступления в силу** свойство) в список отзыва Сертификатов используется hello hello tooensure списка отзыва Сертификатов по-прежнему действителен. Hello CRL — toocertificates периодически упоминаемого toorevoke доступа, входящих в состав списка hello.

При необходимости (например, в случае потери устройства) более быстрой отзыва, маркер авторизации hello hello пользователя может стать недействительным. tooinvalidate hello авторизации маркеров, задайте hello **StsRefreshTokenValidFrom** для данного пользователя с помощью Windows PowerShell. Необходимо обновить hello **StsRefreshTokenValidFrom** для каждого пользователя, который вы хотите получить доступ toorevoke для поля.

tooensure отзыва hello сохраняется, необходимо задать hello **Дата вступления в силу** hello CRL tooa даты после hello значение, установленное **StsRefreshTokenValidFrom** и убедитесь в hello сертификата Hello списка отзыва Сертификатов.

Здравствуйте, следуйте процедуре hello структуры шаги для обновления и делает недействительными hello маркер авторизации, установка hello **StsRefreshTokenValidFrom** поля. 

**tooconfigure отзыва:** 

1. Подключение со службой MSOL toohello учетные данные администратора: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Получить текущее значение StsRefreshTokensValidFrom hello для пользователя: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Настройка нового значения StsRefreshTokensValidFrom для пользователя hello равно toohello Текущая отметка времени: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

Дата Hello, задать должна быть в будущем hello. Если дата hello не будущих hello, hello **StsRefreshTokensValidFrom** свойство не задано. Если дата hello в будущем, hello **StsRefreshTokensValidFrom** задано toohello текущее время (не hello даты, указанной командой Set-MsolUser). 


## <a name="step-4-test-your-configuration"></a>Шаг 4. Тестирование конфигурации

### <a name="testing-your-certificate"></a>Тестирование сертификата

В качестве первой конфигурации теста, попробуйте toosign в слишком[Outlook Web Access](https://outlook.office365.com) или [SharePoint Online](https://microsoft.sharepoint.com) с помощью вашей **браузер на устройстве**.

Успешный вход подтверждает, что:

- сертификат пользователя Hello был подготовленных tooyour тестовое устройство
- службы AD FS настроены правильно.  


### <a name="testing-office-mobile-applications"></a>Тестирование мобильных приложений Office

**tootest сертификат проверки подлинности на основе мобильного приложения Office:** 

1. На тестируемом устройстве установите мобильное приложение Office (например, OneDrive).
3. Запуск приложения hello. 
4. Введите имя пользователя и выберите сертификат пользователя hello, требуется toouse. 

Вы должны без проблем войти в систему. 

### <a name="testing-exchange-activesync-client-applications"></a>Тестирование клиентских приложений Exchange ActiveSync

Доступные toohello приложения необходимо tooaccess Exchange ActiveSync (EAS) через сертификат проверки подлинности на основе профиля EAS, содержащий сертификат клиента hello. 

Hello профиля EAS должен содержать hello следующую информацию:

- Здравствуйте, toobe сертификат пользователя, используемый для проверки подлинности 

- Конечная точка EAS Hello (например, outlook.office365.com)

Можно настроить и разместить на устройстве hello путем использования hello управления мобильными устройствами (MDM) как Intune, или установив сертификат hello вручную в hello профиля EAS на устройстве hello профиля EAS.  

### <a name="testing-eas-client-applications-on-android"></a>Тестирование клиентских приложений EAS на Android

**Проверка подлинности сертификата tootest:**  

1. Настройка профиля EAS приложения hello, удовлетворяющее требованиям hello выше.  
2. Откройте приложение hello и убедитесь, что почта синхронизируются. 

