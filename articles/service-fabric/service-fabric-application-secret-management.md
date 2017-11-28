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
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="d7224-103">Управление секретами в приложениях Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7224-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="d7224-104">В этом руководстве содержится описание этапов hello управления секретов в приложении Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d7224-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="d7224-105">Секретом может считаться любая конфиденциальная информации, например строка подключения к хранилищу, пароль или другое значение, которое не должно обрабатываться в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="d7224-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="d7224-106">В этом руководстве используется хранилище ключей Azure toomanage ключи и секретные коды.</span><span class="sxs-lookup"><span data-stu-id="d7224-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="d7224-107">Тем не менее *с помощью* секретов в приложении, размещаемый в облако tooallow платформенно независимые приложения toobe развернутой tooa кластера в любом месте.</span><span class="sxs-lookup"><span data-stu-id="d7224-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="d7224-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="d7224-108">Overview</span></span>
<span data-ttu-id="d7224-109">Hello параметры конфигурации для службы toomanage рекомендуемым способом — с помощью [службы конфигурации пакетов][config-package].</span><span class="sxs-lookup"><span data-stu-id="d7224-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="d7224-110">Пакеты конфигурации имеют числовые версии, которые можно обновлять, используя управляемые последовательные обновления с проверкой работоспособности и автоматическим откатом обновления.</span><span class="sxs-lookup"><span data-stu-id="d7224-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="d7224-111">Это предпочтительный tooglobal конфигурации, поскольку снижает вероятность сбоя глобальной службы hello.</span><span class="sxs-lookup"><span data-stu-id="d7224-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="d7224-112">Зашифрованные секреты не являются исключением.</span><span class="sxs-lookup"><span data-stu-id="d7224-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="d7224-113">Служба Service Fabric снабжена встроенными компонентами для шифрования и расшифровки значений в файле Settings.xml пакета конфигурации. При этом используется сертификат шифрования.</span><span class="sxs-lookup"><span data-stu-id="d7224-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="d7224-114">Hello следующей схеме показана hello базовой схемы секретный управления в приложении Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d7224-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![обзор управления секретами][overview]

<span data-ttu-id="d7224-116">Этот поток состоит из четырех основных шагов.</span><span class="sxs-lookup"><span data-stu-id="d7224-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="d7224-117">Получение сертификата шифрования данных.</span><span class="sxs-lookup"><span data-stu-id="d7224-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="d7224-118">Установите сертификат hello в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7224-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="d7224-119">Шифрование значения секрета при развертывании приложения с сертификатом hello и вставить их в файл конфигурации службы Settings.xml.</span><span class="sxs-lookup"><span data-stu-id="d7224-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="d7224-120">Чтение зашифрованные значения из Settings.xml, расшифровывая с hello того же сертификата шифрование.</span><span class="sxs-lookup"><span data-stu-id="d7224-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="d7224-121">[Хранилище ключей Azure] [ key-vault-get-started] используется здесь в безопасном хранилище для сертификатов, а tooget способом сертификатов, установленных в Service Fabric кластеров в Azure.</span><span class="sxs-lookup"><span data-stu-id="d7224-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="d7224-122">При развертывании не tooAzure, секреты toomanage toouse хранилище ключей в приложениях Service Fabric не обязательно.</span><span class="sxs-lookup"><span data-stu-id="d7224-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="d7224-123">сертификат шифрования данных;</span><span class="sxs-lookup"><span data-stu-id="d7224-123">Data encipherment certificate</span></span>
<span data-ttu-id="d7224-124">Сертификат шифрования данных используются исключительно для шифрования и расшифровки значений конфигурации в файле Settings.xml службы и не применяется при аутентификации или подписывании зашифрованного текста.</span><span class="sxs-lookup"><span data-stu-id="d7224-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="d7224-125">Hello сертификат должен удовлетворять hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="d7224-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="d7224-126">Hello сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="d7224-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="d7224-127">необходимо создать сертификат Hello для обмена ключами, tooa экспортируемый файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="d7224-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d7224-128">Использование ключа сертификата Hello необходимо включить шифрование данных (10) и не должно включать проверку подлинности сервера или клиента.</span><span class="sxs-lookup"><span data-stu-id="d7224-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="d7224-129">Например, при создании самозаверяющего сертификата с помощью PowerShell, hello `KeyUsage` слишком должен быть установлен флаг`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="d7224-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="d7224-130">Установите сертификат hello в кластере</span><span class="sxs-lookup"><span data-stu-id="d7224-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="d7224-131">Этот сертификат должен быть установлен на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="d7224-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="d7224-132">Он будет использоваться во время выполнения toodecrypt значений, хранимых в Settings.xml службы.</span><span class="sxs-lookup"><span data-stu-id="d7224-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="d7224-133">В разделе [как toocreate имени кластера с помощью диспетчера ресурсов Azure] [ service-fabric-cluster-creation-via-arm] инструкции по установке.</span><span class="sxs-lookup"><span data-stu-id="d7224-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="d7224-134">Шифрование секретов приложений</span><span class="sxs-lookup"><span data-stu-id="d7224-134">Encrypt application secrets</span></span>
<span data-ttu-id="d7224-135">пакет Service Fabric SDK Hello имеет встроенные функции секретного шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="d7224-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="d7224-136">Значения секретов могут шифроваться в процессе сборки, а затем программно расшифровываться и считываться в коде службы.</span><span class="sxs-lookup"><span data-stu-id="d7224-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="d7224-137">Hello следующую команду PowerShell — используется tooencrypt секрета.</span><span class="sxs-lookup"><span data-stu-id="d7224-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="d7224-138">Эта команда шифрует только значение hello; Это осуществляется **не** входа hello зашифрованного текста.</span><span class="sxs-lookup"><span data-stu-id="d7224-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="d7224-139">Необходимо использовать hello же шифрование сертификата, установленного в вашей кластера tooproduce зашифрованного текста для значения секрета:</span><span class="sxs-lookup"><span data-stu-id="d7224-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="d7224-140">Hello результирующая строка Base64-содержит секретный зашифрованного текста hello как, так и сведения о сертификате hello, которая была используется tooencrypt его.</span><span class="sxs-lookup"><span data-stu-id="d7224-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="d7224-141">Hello строки в кодировке base-64 могут быть вставлены в параметр в файле конфигурации службы Settings.xml с hello `IsEncrypted` атрибут задан слишком`true`:</span><span class="sxs-lookup"><span data-stu-id="d7224-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="d7224-142">Включение секретов приложений в экземпляры приложений</span><span class="sxs-lookup"><span data-stu-id="d7224-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="d7224-143">В идеальном случае toodifferent сред развертывания должно быть как автоматические максимально.</span><span class="sxs-lookup"><span data-stu-id="d7224-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="d7224-144">Это можно сделать путем выполнения секретного шифрования в среде построения и предоставление hello зашифрованные секретные данные в качестве параметров при создании экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="d7224-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="d7224-145">Использование переопределяемых параметров в Settings.xml</span><span class="sxs-lookup"><span data-stu-id="d7224-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="d7224-146">файл конфигурации Settings.xml Hello позволяет переопределяемые параметры, которые можно указать во время создания приложения.</span><span class="sxs-lookup"><span data-stu-id="d7224-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="d7224-147">Используйте hello `MustOverride` вместо указания значения для параметра атрибута:</span><span class="sxs-lookup"><span data-stu-id="d7224-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="d7224-148">toooverride значения в Settings.xml, объявите параметр переопределения для hello службы в файле ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="d7224-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="d7224-149">Теперь можно задать значение hello *параметр приложения* при создании экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d7224-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="d7224-150">Для облегчения интеграции в процессе сборки создание экземпляра приложения можно выполнить с помощью сценария PowerShell или написать на языке C#.</span><span class="sxs-lookup"><span data-stu-id="d7224-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="d7224-151">С помощью PowerShell, параметр hello является предоставленного toohello `New-ServiceFabricApplication` как [хэш-таблицу](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="d7224-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="d7224-152">При использовании языка C# параметры приложения указываются в `ApplicationDescription` как `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="d7224-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="d7224-153">Расшифровка секретов из кода службы</span><span class="sxs-lookup"><span data-stu-id="d7224-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="d7224-154">Службы в Service Fabric работают под управлением NETWORK SERVICE по умолчанию в Windows, а не toocertificates доступ установленная на узле hello без дополнительных настроек.</span><span class="sxs-lookup"><span data-stu-id="d7224-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="d7224-155">При использовании сертификата шифрование данных, необходимо убедиться, что СЕТЕВОЙ службы или выполняется независимо от служба hello учетная запись пользователя имеет закрытый ключ сертификата toohello доступа toomake.</span><span class="sxs-lookup"><span data-stu-id="d7224-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="d7224-156">Service Fabric обрабатывающий предоставление доступа для службы автоматически при настройке его toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="d7224-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="d7224-157">Такую конфигурацию можно настроить в файле ApplicationManifest.xml, определив пользователей и политики безопасности для сертификатов.</span><span class="sxs-lookup"><span data-stu-id="d7224-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="d7224-158">В следующем примере hello hello учетной записи СЕТЕВОЙ службы предоставляется определяется его отпечатком сертификата tooa доступ для чтения:</span><span class="sxs-lookup"><span data-stu-id="d7224-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="d7224-159">При копировании отпечаток сертификата из сертификата hello сохранить оснастку в Windows, невидимые символ находится в начале строки отпечаток hello hello.</span><span class="sxs-lookup"><span data-stu-id="d7224-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="d7224-160">Этот символ невидимой может вызвать ошибку при попытке toolocate сертификат с отпечатком, поэтому будьте toodelete убедиться, что этот лишний символ.</span><span class="sxs-lookup"><span data-stu-id="d7224-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="d7224-161">Использование секретов приложений в коде службы</span><span class="sxs-lookup"><span data-stu-id="d7224-161">Use application secrets in service code</span></span>
<span data-ttu-id="d7224-162">Hello API для доступа к параметрам конфигурации из Settings.xml в пакет конфигурации позволяет легко расшифровки значений, которые имеют hello `IsEncrypted` атрибут задан слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="d7224-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="d7224-163">Поскольку текст зашифрован hello содержит информацию о hello сертификат, используемый для шифрования, не обязательно toomanually поиска hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="d7224-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="d7224-164">сертификат Hello достаточно toobe установлен на узле hello, hello служба работает на.</span><span class="sxs-lookup"><span data-stu-id="d7224-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="d7224-165">Просто вызвать hello `DecryptValue()` метод tooretrieve hello исходного секретное значение:</span><span class="sxs-lookup"><span data-stu-id="d7224-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="d7224-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7224-166">Next Steps</span></span>
<span data-ttu-id="d7224-167">Дополнительные сведения о запуске приложений с использованием разных разрешений безопасности см. в [этой статье](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="d7224-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
