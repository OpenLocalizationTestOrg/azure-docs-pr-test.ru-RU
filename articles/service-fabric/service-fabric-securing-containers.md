---
title: "aaaAzure безопасности контейнера Service Fabric | Документы Microsoft"
description: "Узнайте, теперь toosecure контейнер служб."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>Безопасность контейнера

Service Fabric предоставляет механизм для служб внутри tooaccess контейнера сертификата, установленного на hello узлов в кластере Windows или Linux (версии 5.7 или более поздней версии). Кроме того, Service Fabric поддерживает групповые управляемые учетные записи службы (gMSA) для контейнеров Windows. 

## <a name="certificate-management-for-containers"></a>Управление сертификатами для контейнеров

Службы контейнеров можно защитить с помощью сертификата. Hello сертификат должен быть установлен на hello узлы кластера hello. Hello сертификат сведения предоставляются в манифесте приложения hello под hello `ContainerHostPolicies` тегу в виде hello в следующем фрагменте кода показан:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

При запуске приложения hello, среда выполнения hello считывает сертификаты hello и приводит к возникновению ошибки PFX-файла и пароль для каждого сертификата. Этот PFX-файл и пароль, доступны в контейнере hello hello следующие переменные среды с помощью: 

* **Certificate_[CodePackageName]_[CertName]_PFX**;
* **Certificate_[CodePackageName]_[CertName]_Password**.

для импорта PFX-файла hello в контейнер hello отвечает Hello контейнера службы или процесса. сертификат tooimport hello, можно использовать `setupentrypoint.sh` выполнения пользовательского кода в рамках процесса контейнера hello или сценариев. Образец кода на языке C# для импорта PFX-файла hello выглядит следующим образом:

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
Этот сертификат PFX-ФАЙЛ можно использовать для проверки подлинности приложения hello или службы или безопасного commmunication с другими службами.


## <a name="set-up-gmsa-for-windows-containers"></a>Настройка gMSA для контейнеров Windows

tooset копирование групповой управляемой учетной записи (группа управляемые учетные записи служб), спецификация файла учетных данных (`credspec`) помещается на всех узлах в кластере hello. Hello файл можно скопировать на всех узлах, используя расширение виртуальной Машины.  Hello `credspec` файл должен содержать сведения об учетной записи gMSA hello. Дополнительные сведения о hello `credspec` файла см. в разделе [учетные записи служб](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Спецификация учетных данных Hello и hello `Hostname` тег указаны в манифесте приложения hello. Hello `Hostname` тега должно соответствовать имя учетной записи gMSA hello, hello выполняется контейнера.  Hello `Hostname` тег позволяет tooauthenticate hello контейнера сам tooother службы в домене hello, с помощью проверки подлинности Kerberos.  Пример для указания hello `Hostname` и hello `credspec` в hello отображается манифест приложения hello, следующий фрагмент кода:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Дальнейшие действия

* [Развертывание tooService контейнера Windows Fabric на Windows Server 2016](service-fabric-get-started-containers.md)
* [Развертывание tooService контейнера Docker структуры в Linux](service-fabric-get-started-containers-linux.md)
