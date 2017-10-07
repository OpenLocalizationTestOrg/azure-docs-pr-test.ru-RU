---
title: "секреты aaaManaging Service Fabric приложений | Документы Microsoft"
description: "В этой статье описывается, как значения секрета toosecure в приложении Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>Управление секретами в приложениях Service Fabric
В этом руководстве содержится описание этапов hello управления секретов в приложении Service Fabric. Секретом может считаться любая конфиденциальная информации, например строка подключения к хранилищу, пароль или другое значение, которое не должно обрабатываться в виде обычного текста.

В этом руководстве используется хранилище ключей Azure toomanage ключи и секретные коды. Тем не менее *с помощью* секретов в приложении, размещаемый в облако tooallow платформенно независимые приложения toobe развернутой tooa кластера в любом месте. 

## <a name="overview"></a>Обзор
Hello параметры конфигурации для службы toomanage рекомендуемым способом — с помощью [службы конфигурации пакетов][config-package]. Пакеты конфигурации имеют числовые версии, которые можно обновлять, используя управляемые последовательные обновления с проверкой работоспособности и автоматическим откатом обновления. Это предпочтительный tooglobal конфигурации, поскольку снижает вероятность сбоя глобальной службы hello. Зашифрованные секреты не являются исключением. Служба Service Fabric снабжена встроенными компонентами для шифрования и расшифровки значений в файле Settings.xml пакета конфигурации. При этом используется сертификат шифрования.

Hello следующей схеме показана hello базовой схемы секретный управления в приложении Service Fabric.

![обзор управления секретами][overview]

Этот поток состоит из четырех основных шагов.

1. Получение сертификата шифрования данных.
2. Установите сертификат hello в кластере.
3. Шифрование значения секрета при развертывании приложения с сертификатом hello и вставить их в файл конфигурации службы Settings.xml.
4. Чтение зашифрованные значения из Settings.xml, расшифровывая с hello того же сертификата шифрование. 

[Хранилище ключей Azure] [ key-vault-get-started] используется здесь в безопасном хранилище для сертификатов, а tooget способом сертификатов, установленных в Service Fabric кластеров в Azure. При развертывании не tooAzure, секреты toomanage toouse хранилище ключей в приложениях Service Fabric не обязательно.

## <a name="data-encipherment-certificate"></a>сертификат шифрования данных;
Сертификат шифрования данных используются исключительно для шифрования и расшифровки значений конфигурации в файле Settings.xml службы и не применяется при аутентификации или подписывании зашифрованного текста. Hello сертификат должен удовлетворять hello следующие требования:

* Hello сертификат должен содержать закрытый ключ.
* необходимо создать сертификат Hello для обмена ключами, tooa экспортируемый файл обмена личной информацией (PFX-файл).
* Использование ключа сертификата Hello необходимо включить шифрование данных (10) и не должно включать проверку подлинности сервера или клиента. 
  
  Например, при создании самозаверяющего сертификата с помощью PowerShell, hello `KeyUsage` слишком должен быть установлен флаг`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Установите сертификат hello в кластере
Этот сертификат должен быть установлен на каждом узле в кластере hello. Он будет использоваться во время выполнения toodecrypt значений, хранимых в Settings.xml службы. В разделе [как toocreate имени кластера с помощью диспетчера ресурсов Azure] [ service-fabric-cluster-creation-via-arm] инструкции по установке. 

## <a name="encrypt-application-secrets"></a>Шифрование секретов приложений
пакет Service Fabric SDK Hello имеет встроенные функции секретного шифрования и расшифровки. Значения секретов могут шифроваться в процессе сборки, а затем программно расшифровываться и считываться в коде службы. 

Hello следующую команду PowerShell — используется tooencrypt секрета. Эта команда шифрует только значение hello; Это осуществляется **не** входа hello зашифрованного текста. Необходимо использовать hello же шифрование сертификата, установленного в вашей кластера tooproduce зашифрованного текста для значения секрета:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Hello результирующая строка Base64-содержит секретный зашифрованного текста hello как, так и сведения о сертификате hello, которая была используется tooencrypt его.  Hello строки в кодировке base-64 могут быть вставлены в параметр в файле конфигурации службы Settings.xml с hello `IsEncrypted` атрибут задан слишком`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Включение секретов приложений в экземпляры приложений
В идеальном случае toodifferent сред развертывания должно быть как автоматические максимально. Это можно сделать путем выполнения секретного шифрования в среде построения и предоставление hello зашифрованные секретные данные в качестве параметров при создании экземпляров приложения.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Использование переопределяемых параметров в Settings.xml
файл конфигурации Settings.xml Hello позволяет переопределяемые параметры, которые можно указать во время создания приложения. Используйте hello `MustOverride` вместо указания значения для параметра атрибута:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

toooverride значения в Settings.xml, объявите параметр переопределения для hello службы в файле ApplicationManifest.xml:

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

Теперь можно задать значение hello *параметр приложения* при создании экземпляра приложения hello. Для облегчения интеграции в процессе сборки создание экземпляра приложения можно выполнить с помощью сценария PowerShell или написать на языке C#.

С помощью PowerShell, параметр hello является предоставленного toohello `New-ServiceFabricApplication` как [хэш-таблицу](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

При использовании языка C# параметры приложения указываются в `ApplicationDescription` как `NameValueCollection`:

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>Расшифровка секретов из кода службы
Службы в Service Fabric работают под управлением NETWORK SERVICE по умолчанию в Windows, а не toocertificates доступ установленная на узле hello без дополнительных настроек.

При использовании сертификата шифрование данных, необходимо убедиться, что СЕТЕВОЙ службы или выполняется независимо от служба hello учетная запись пользователя имеет закрытый ключ сертификата toohello доступа toomake. Service Fabric обрабатывающий предоставление доступа для службы автоматически при настройке его toodo таким образом. Такую конфигурацию можно настроить в файле ApplicationManifest.xml, определив пользователей и политики безопасности для сертификатов. В следующем примере hello hello учетной записи СЕТЕВОЙ службы предоставляется определяется его отпечатком сертификата tooa доступ для чтения:

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> При копировании отпечаток сертификата из сертификата hello сохранить оснастку в Windows, невидимые символ находится в начале строки отпечаток hello hello. Этот символ невидимой может вызвать ошибку при попытке toolocate сертификат с отпечатком, поэтому будьте toodelete убедиться, что этот лишний символ.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Использование секретов приложений в коде службы
Hello API для доступа к параметрам конфигурации из Settings.xml в пакет конфигурации позволяет легко расшифровки значений, которые имеют hello `IsEncrypted` атрибут задан слишком`true`. Поскольку текст зашифрован hello содержит информацию о hello сертификат, используемый для шифрования, не обязательно toomanually поиска hello сертификата. сертификат Hello достаточно toobe установлен на узле hello, hello служба работает на. Просто вызвать hello `DecryptValue()` метод tooretrieve hello исходного секретное значение:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о запуске приложений с использованием разных разрешений безопасности см. в [этой статье](service-fabric-application-runas-security.md).

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
