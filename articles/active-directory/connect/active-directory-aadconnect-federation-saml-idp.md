---
title: "Azure AD Connect: использование поставщика удостоверений SAML 2.0 для единого входа | Документы Майкрософт"
description: "В этом разделе описывается использование поставщика удостоверений, совместимого с SAML 2.0, для единого входа."
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Использование поставщика удостоверений (IdP) SAML 2.0 для единого входа

Этот раздел содержит сведения об использовании SAML 2.0 совместимые профилей SP-Lite поставщиком удостоверений на основе как hello основной службы маркеров безопасности (STS) или поставщика удостоверений. Это полезно при наличии локального каталога пользователей и хранилища паролей, доступ к которым возможен с помощью SAML 2.0. Существующий каталог пользователей может использоваться для входа tooOffice 365 и другим ресурсам Azure AD защищены. Hello SAML 2.0 SP-Lite профиля основан на hello широко используемые Security Assertion Markup Language (SAML) федеративного удостоверения стандартные tooprovide входа и платформы обмена.

>[!NOTE]
>Список сторонних Idps, которые были протестированы для использования с Azure AD см hello [список совместимости федерации Azure AD](active-directory-aadconnect-federation-compatibility.md)

Корпорация Майкрософт поддерживает эти возможности входа как интеграция hello облачной службы Майкрософт, таких как Office 365, с помощью SAML 2.0 правильно настроенного профиля на основе поставщика удостоверений. Поставщики удостоверений SAML 2.0 — это сторонние продукты, и поэтому корпорация Майкрософт не поддерживает hello развертыванию, настройке, устранение неполадок рекомендациям относительно их. После правильной настройке hello интеграция с SAML 2.0 поставщик удостоверений можно проверить на наличие правильной конфигурации с помощью анализатора подключений Майкрософт описанного ниже более подробно hello hello. Дополнительные сведения о поставщика удостоверений на основе SAML 2.0 SP-Lite профиля попросите предоставившую его организацию hello.

>[!IMPORTANT]
>В этом сценарии единого входа с помощью поставщиков удостоверений SAML 2.0 доступен только ограниченный набор клиентов, в число которых входят приведенные далее.

>- Веб-клиенты, такие как Outlook Web Access и SharePoint Online
- Полнофункциональные почтовые клиенты, использующие обычную проверку подлинности и поддерживаемый метод доступа Exchange, таких как IMAP, POP, Active Sync, MAPI, т. д. (hello расширенного клиентского протокола конечной точки является обязательным toobe развертывания), в том числе:
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (различные версии iOS);
    - различные устройства Google Android;
    - Windows Phone 7, Windows Phone 7.8 и Windows Phone 8.0;
    - почтовый клиент Windows 8 и Windows 8.1;
    - почтовый клиент Windows 10.

Все остальные клиенты не поддерживаются в сценарии единого входа с помощью поставщика удостоверений SAML 2.0. Например клиент рабочего стола hello Lync 2010 не может toologin в службу hello с поставщиком удостоверений SAML 2.0, настроенного для единого входа.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Требования Azure AD к протоколу SAML 2.0
Этот раздел содержит подробные требования на протоколе hello и форматирования, что поставщик удостоверений SAML 2.0 должен реализовывать toofederate с Azure AD tooenable входа tooone или несколько облачных служб Майкрософт (например, Office 365) сообщений. Hello SAML 2.0 проверяющей стороны (SP-STS) для облачной службы Майкрософт, используемая в этом сценарии используется Azure AD.

Рекомендуется убедиться, быть выходных сообщений поставщика удостоверений, что аналогично toohello предоставленный образец трассировок можно SAML 2.0. Кроме того используйте значения атрибутов из hello предоставил метаданные Azure AD, где это возможно. После ввода требуемых выходных сообщений можно проверить с помощью анализатора подключений Майкрософт hello как описано ниже.

метаданные Hello Azure AD можно загрузить на этот URL-адрес: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Можно использовать для клиентов в Китае, используя hello Китая экземпляр Office 365, следующая конечная точка федерации hello: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Требования к протоколу SAML
Этот раздел описывает как hello пар сообщений запросов и ответов, объединить в порядке toohelp вы tooformat сообщений правильно.

Azure AD может быть настроенный toowork с поставщиками удостоверений, использующими профиль SAML 2.0 SP Lite hello предъявляется ряд особых требований, указанных ниже. Используя образец SAML запроса и ответного сообщения приветствия вместе с автоматическим и ручным тестированием, вы можете работать tooachieve взаимодействие с Azure AD.

## <a name="signature-block-requirements"></a>Требования к блоку подписи
В пределах hello ответ SAML узел Signature сообщение hello содержит сведения о hello цифровая подпись для само сообщение hello. Hello блоку подписи предъявляются следующие требования к hello:

1. Hello узел утверждения должен быть подписан
2.  как hello DigestMethod необходимо использовать алгоритм RSA-sha1 Hello. Другие алгоритмы цифровой подписи не допускаются.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  Также можно подписать hello XML-документа. 
4.  Hello алгоритм преобразования должна соответствовать значениям hello в следующий образец hello:`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Алгоритм SignatureMethod Hello должны совпадать следующие образец hello:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Поддерживаемые привязки
Привязки-это транспорт hello связанные параметры взаимодействия, которые необходимы. Привет, следующие требования применяются toohello привязки

1. HTTPS-transport необходимые hello.
2.  Службе Azure AD потребуется запрос HTTP POST для отправки токена во время входа.
3.  Azure AD будет использовать HTTP POST для поставщика удостоверений toohello запрос проверки подлинности hello и ПЕРЕНАПРАВЛЕНИЯ для выхода из системы сообщение hello toohello-поставщика удостоверений.

## <a name="required-attributes"></a>Требуемые атрибуты
В этой таблице перечислены требования к для атрибутов в сообщение hello SAML 2.0.
 
|Атрибут|Описание|
| ----- | ----- |
|NameID|значение этого утверждения Hello должен hello совпадает с идентификатором ImmutableID пользователя hello Azure AD. Возможность ее too64 буквенно-цифровые символы. Все небезопасные символы HTML должны кодироваться, например, символ "+" должен быть представлен как ".2B".|
|IDPEmail|Hello имя участника пользователя (UPN) указан в hello SAML ответа как элемент с hello именем IDPEmail это — UserPrincipalName hello пользователя (UPN) в Azure AD и Office 365. Hello имени участника-пользователя находится в формате адреса электронной почты. Значение UPN в Windows Office 365 (Azure Active Directory).|
|Издатель|Это обязательный toobe URI поставщика удостоверений hello. Не следует использовать hello издателя из образцов сообщений hello. При наличии нескольких доменов верхнего уровня в вашей Issuer должно совпадать с приветствия клиентов Azure AD hello указанного URI, настроенным для домена.|

>[!IMPORTANT]
>В настоящее время Azure AD поддерживает следующие URI формат идентификатора имени для SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid hello-формат: постоянно.

## <a name="sample-saml-request-and-response-messages"></a>Примеры сообщений SAML с запросом и ответом
Для обмена сообщениями входа hello показан пару сообщений запросов и ответов.
Это пример сообщения с запросом, полученном от поставщика удостоверений SAML 2.0 образец tooa Azure AD. Службы федерации Active Directory (AD FS) настроен протокол SAML-P toouse является поставщиком удостоверений SAML 2.0 Образец Hello. Тестирование взаимодействия было выполнено и для других поставщиков удостоверений SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Это пример сообщения ответа, полученном от поставщика удостоверений, совместимым tooAzure AD hello образец SAML 2.0 и Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>Настройка поставщика удостоверений, совместимого с SAML 2.0
В этом разделе содержатся рекомендации по как tooconfigure toofederate поставщика удостоверений вашей SAML 2.0, с Azure AD tooenable доступа-tooone или дополнительные Microsoft cloud services (например, Office 365) с помощью протокола hello SAML 2.0. Hello SAML 2.0 проверяющей стороной для облачной службы Майкрософт, используемая в этом сценарии используется Azure AD.

## <a name="add-azure-ad-metadata"></a>Добавление метаданных Azure AD
Поставщик удостоверений SAML 2.0 должен tooinformation tooadhere о доверяющей стороны hello Azure AD. Azure AD публикует метаданные в https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

Рекомендуется всегда импортировать метаданные hello последнюю Azure AD при настройке поставщика удостоверений SAML 2.0. Обратите внимание, что Azure AD не считывает метаданные от поставщика удостоверений hello.

## <a name="add-azure-ad-as-a-relying-party"></a>Добавление Azure AD в качестве проверяющей стороны
У вас есть tooenable обмен данными между поставщиком удостоверений SAML 2.0 и Azure AD. Эта конфигурация будет зависеть от используемого поставщика удостоверений, и вы должны обращаться toodocumentation для него. Hello проверяющей стороной идентификатор toohello обычно задается то же, что entityID hello из метаданных hello Azure AD.

>[!NOTE]
>Проверьте hello часов на сервере поставщика удостоверений SAML 2.0 синхронизированные tooan источника точного времени. Неточное время часов может привести к toofail федеративных входов.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Установка Windows PowerShell для единого входа с помощью поставщика удостоверений SAML 2.0
После настройки поставщика удостоверений SAML 2.0 для использования с входом Azure AD, следующим шагом hello является toodownload и установки hello Azure Active Directory модуля для Windows PowerShell. После установки будет использовать эти командлеты tooconfigure доменов Azure AD в качестве федеративных доменов.

Hello Azure Active Directory модуля для Windows PowerShell можно загрузить для управления данными организации в Azure AD. Этот модуль устанавливает набор командлетов tooWindows PowerShell; выполнить эти командлеты tooset копирование tooAzure единого входа для доступа к AD и в свою очередь tooall из hello облачных служб, которые вы подписаны. Инструкции о hello как toodownload и установка командлетов см. [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Настройка отношения доверия между поставщиком удостоверений SAML и Azure AD
Перед настройкой федерации в домене Azure AD в нем должен быть настроен личный домен. Не удается создать федерацию домен по умолчанию hello, предоставляемой корпорацией Майкрософт. домен по умолчанию Hello корпорации Майкрософт заканчивается на «onmicrosoft.com».
Необходимо выполнить ряд командлетов в tooadd интерфейс командной строки Windows PowerShell hello или преобразовать домены для единого входа.

Каждый домен Azure Active Directory, который вы хотите toofederate с помощью поставщика удостоверений SAML 2.0 необходимо выполнить одно из быть добавлен как домен единого входа или преобразованное toobe домен единого входа из стандартного домена. При добавлении или преобразовании домена между поставщиком удостоверений SAML 2.0 и Azure AD настраивается отношение доверия.

Hello следующая процедура поможет выполнить преобразование существующего стандартного домена tooa федеративного домена с помощью SAML 2.0 SP-Lite. Обратите внимание, что домен может стать сбоя, оказывает влияние на пользователей too2 часов после выполнения этого действия.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Настройка домена в каталоге Azure AD для федерации


1. Tooyour каталог Azure AD администратор клиента подключения: подключение MsolService.
2.  Настройка федерации toouse требуемый домен Office 365 с SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  Вы можете получить сертификат подписи в кодировке base64 из файла метаданных IDP hello. Пример его расположения приведен, но в зависимости от особенностей развертывания оно может быть немного иным.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Дополнительные сведения о командлете Set-MsolDomainAuthentication см. на странице по адресу: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Использовать атрибут "$ecpUrl = "https://WS2012R2-0.contoso.com/PAOS"" следует только в том случае, если для поставщика удостоверений настраивается расширение ECP. Клиенты Exchange Online, исключая Outlook Web Application (OWA), используют активную конечную точку на основе метода POST. Если служба маркеров безопасности SAML 2.0 реализует активную конечную точку как tooShibboleth ECP реализации активной конечной точки может быть возможно, что эти клиенты с расширенными возможностями toointeract с hello службой Exchange Online.

После настройки федерации можно переключиться назад слишком «нефедеративных» (или «managed»), однако это изменение будет занимать toocomplete tootwo часов, а также требуется назначить новый случайный пароль для облака на основе tooeach входа пользователя. Обратное переключение слишком «managed» может быть требуется в некоторых сценариях tooreset ошибка в параметрах настройки. Дополнительные сведения о преобразовании домена см. на странице по адресу: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Подготовить tooAzure участников пользователя AD и Office 365
Прежде чем входить на пользователей tooOffice 365 Azure AD необходимо подготовить для участников, которые соответствуют toohello утверждению в SAML 2.0 hello утверждения пользователя. Если эти субъекты-пользователи не известны заранее tooAzure AD их нельзя использовать для федеративного входа в систему. Azure AD Connect или Windows PowerShell можно использовать tooprovision участников-пользователей.

Azure AD Connect можно используется tooprovision участников tooyour доменах в каталоге Azure AD из hello локальной Active Directory. Дополнительные сведения см. в статье [Интеграция локальных каталогов с Azure Active Directory](active-directory-aadconnect.md).

Windows PowerShell также можно использовать tooautomate, добавление новых пользователей tooAzure AD и toosynchronize меняется с локальным каталогом hello. hello toouse командлеты Windows PowerShell, необходимо загрузить hello [модули Azure Active Directory](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Эта процедура показывает, как tooadd tooAzure одного пользователя AD.


1. Tooyour каталог Azure AD администратор клиента подключения: подключение MsolService.
2.  Создайте субъекта-пользователя: ` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

Дополнительные сведения о командлете New-MsolUser см. на странице по адресу: [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx).

>[!NOTE]
>Здравствуйте, «UserPrinciplName» значение должно соответствовать значение hello, которое будет отправляться для атрибута «IDPEmail» в утверждении SAML 2.0 и hello «ImmutableID» значение должно соответствовать значение hello, отправляемый в утверждение «NameID».

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Проверка единого входа с помощью поставщика удостоверений SAML 2.0
Администратор hello перед проверкой и управления единым входом (также называемого федерацией удостоверений), просмотрите сведения hello и выполните действия hello в hello следующие статьи tooset копирование единого входа с помощью поставщика удостоверений на основе SAML 2.0 SP-Lite.


1.  После знакомства с hello требования к протоколу Azure AD SAML 2.0
2.  Настройки поставщика удостоверений SAML 2.0.
3.  Установка Windows PowerShell для единого входа с помощью поставщика удостоверений SAML 2.0.
4.  Настройка отношения доверия между поставщиком удостоверений SAML 2.0 и Azure AD.
5.  Подготовить основной tooAzure каталога пользователя тестового Active Directory (Office 365) через Windows PowerShell или Azure AD Connect.
6.  Настройка синхронизации каталогов с помощью [Azure AD Connect](active-directory-aadconnect.md).

После настройки единого входа с помощью поставщика удостоверений на основе SAML 2.0 SP-Lite следует проверить, правильно ли он работает.

>[!NOTE]
>Если был преобразован в домен, а не добавлен, может занять tooset часы too24 копирование единого входа.
Перед проверкой единого входа следует завершить настройку синхронизации Active Directory, синхронизировать каталоги и активировать синхронизированных пользователей.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Используйте hello средство tooverify, единый вход настроен неправильно
tooverify, единый вход настроен правильно, можно выполнить следующие tooconfirm процедуры, которые могут toosign в toohello облачной службе с помощью корпоративных учетных данных hello.

Корпорация Майкрософт предоставляет средства, которые можно использовать tootest SAML 2.0 на основе поставщика удостоверений. Перед запуском hello тестирования инструмент, необходимо настроить toofederate клиента Azure AD с поставщиком удостоверений.

>[!NOTE]
>Hello анализатора подключений требуется Internet Explorer 10 или более поздней версии.



1. Загрузка hello анализатор подключений, [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Нажмите кнопку Установить сейчас toobegin Загрузка и установка средства hello.
3.  Выберите пункт "Не удается настроить федерацию с Office 365, Azure или другими службами, использующими Azure Active Directory".
4.  После загрузки и запуска средства hello, вы увидите окно диагностики подключения hello. Hello средство предоставляет пошаговые инструкции по тестированию подключения федерации.
5.  Hello анализатор подключений будет открыть поставщика Удостоверений SAML 2.0 вы toologon, введите учетные данные hello hello тестировании участника-пользователя: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  По hello федерации Проверьте в окне входа следует ввести имя пользователя и пароль для клиента Azure AD hello, настроенных toobe федерации с поставщиком удостоверений SAML 2.0. Средство Hello попытается toosign в с использованием этих учетных данных и подробные результаты тестов, выполненных во время попытки входа hello будут представлены в виде выходных данных.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. В этом окне показано, что тест не пройден. Щелкнув просмотрите подробные результаты можно просмотреть сведения о hello результаты для каждого выполненного теста. Можно также сохранить результаты toodisk hello в порядке tooshare их.
 
>[!NOTE]
>Hello анализатор подключений также тестирует активную федерацию с помощью hello WS *-протоколы на основе и ECP и PAOS. Если вы не используете можно пренебречь hello следующая ошибка: тестирование hello активного потока входа, с помощью конечной точки активной федерации вашего поставщика удостоверений.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Проверка правильной настройки единого входа с помощью средства
Ручная проверка — это дополнительные действия, которые можно предпринять tooensure, поставщик удостоверений SAML 2.0 работает правильно во многих сценариях.
tooverify, единый вход настроен правильно, воспользуйтесь hello следующих шагов:


1. На компьютере, присоединенном к домену вход tooyour облачной службы, с помощью hello же имя, которое используется для корпоративных учетных данных входа в систему.
2.  Щелкните в поле "пароль" hello. Если единый вход настроен, hello пароля будет неактивным и вы увидите следующие сообщение hello: «вы находитесь необходимые toosign в в <your company>.»
3.  Нажмите кнопку hello войдите в систему в <your company> ссылку. Если вы не можете toosign в, затем единый вход настроен.

## <a name="next-steps"></a>Дальнейшие действия


- [Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect](active-directory-aadconnect-federation-management.md)
- [Список совместимости с федерацией Azure AD](active-directory-aadconnect-federation-compatibility.md)
- [Выборочная установка Azure AD Connect](active-directory-aadconnect-get-started-custom.md)
