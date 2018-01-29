---
title: "Управление сертификатами в кластере Azure Service Fabric | Документация Майкрософт"
description: "В этой статье рассказывается о том, как добавить новые, а также сменить или удалить имеющиеся сертификаты в кластере Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Добавление и удаление сертификатов для кластера Service Fabric в Azure
Рекомендуется ознакомиться с тем, как Service Fabric использует сертификаты X.509, и просмотреть раздел [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md). Необходимо понять, что такое сертификат кластера и для чего он используется, прежде чем продолжить.

Service Fabric позволяет указать в дополнение к сертификатам клиента два сертификата кластера, основной и дополнительный. Сделать это можно при настройке сертификата безопасности во время создания кластера. Чтобы узнать больше об их настройке во время создания, ознакомьтесь с процедурой [создания кластера Azure с помощью портала](service-fabric-cluster-creation-via-portal.md) или [создания кластера Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Если во время создания указан только один сертификат кластера, то он используется в качестве основного сертификата. После создания кластера можно добавить новый сертификат в качестве дополнительного.

> [!NOTE]
> Для работы с безопасным кластером всегда требуется хотя бы один действительный (не отозванный и не просроченный) развернутый сертификат кластера (основной или дополнительный). В противном случае кластер не будет функционировать. За 90 дней до истечения срока действия всех действительных сертификатов система создает трассировку "Предупреждение" и событие предупреждения о работоспособности на узле. В настоящее время Service Fabric не отправляет какие-либо электронные сообщения или другие уведомления о данной теме. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a>Добавление дополнительного сертификата кластера с помощью портала

Дополнительный сертификат кластера невозможно добавить с помощью портала Azure. Вместо этого необходимо воспользоваться Azure PowerShell. Данная процедура рассмотрена далее в этом документе.

## <a name="swap-the-cluster-certificates-using-the-portal"></a>Переключение сертификатов кластера с помощью портала

Если после успешного развертывания дополнительного сертификата кластера потребуется поменять основной и дополнительный сертификаты местами, перейдите к колонке "Безопасность" и выберите в контекстном меню параметр Swap with primary (Поменять местами с основным), чтобы дополнительный сертификат стал основным, а основной — дополнительным.

![Переключение сертификатов][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a>Удаление сертификата кластера с помощью портала

Для работы с безопасным кластером всегда требуется хотя бы один действительный (не отозванный и не просроченный) развернутый сертификат (основной или дополнительный). В противном случае кластер не будет функционировать.

Чтобы дополнительный сертификат больше не использовался для обеспечения безопасности кластера, перейдите к колонке "Безопасность" и выберите в контекстном меню дополнительного сертификата параметр "Удалить".

Если вы планируете удалить сертификат, который помечен как основной, необходимо сначала поменять его местами с дополнительным, а затем удалить дополнительный, когда обновление будет завершено.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Добавление дополнительного сертификата с помощью PowerShell для Resource Manager

В этих инструкциях предполагается, что вы ознакомлены с принципами работы Resource Manager, развернули по крайней мере один кластер Service Fabric с помощью шаблона Resource Manager и у вас под рукой имеется шаблон, который использовался для настройки этого кластера. Предполагается также, что вы уверенно используете JSON.

> [!NOTE]
> Если вам нужен пример шаблона и параметров, которые можно использовать в качестве образца или отправной точки, скачайте его из этого репозитория [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Изменение шаблона Resource Manager

Для удобства выполнения инструкций пример 5-VM-1-NodeTypes-Secure_Step2.JSON содержит все изменения, которые мы будем вносить. Этот пример доступен в репозитории [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Обязательные шаги**

**Шаг 1.** Откройте шаблон Resource Manager, который использовался для развертывания кластера. (Если вы загрузили пример из репозитория, указанного выше, воспользуйтесь 5-VM-1-NodeTypes-Secure_Step1.JSON для развертывания кластера, а затем откройте этот шаблон.)

**Шаг 2.** Добавьте **два новых параметра** строчного типа (secCertificateThumbprint и secCertificateUrlValue) в раздел параметров шаблона. Можно скопировать следующий фрагмент кода и добавить его в шаблон. В зависимости от источника шаблона, эти параметры уже могут быть определены. В таком случае перейдите к следующему шагу. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Шаг 3.** Внесите изменения в ресурс **Microsoft.ServiceFabric/clusters**. Для этого найдите определение ресурса Microsoft.ServiceFabric/clusters в шаблоне. В разделе свойств этого определения вы увидите тег Certificate в формате JSON, который должен выглядеть как приведенный ниже фрагмент JSON.

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Добавьте новый тег thumbprintSecondary и присвойте ему значение [parameters('secCertificateThumbprint')].  

Теперь определение ресурса должно выглядеть следующим образом (в зависимости от источника шаблона оно может отличаться от приведенного ниже фрагмента). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Если необходимо **сменить сертификат**, укажите новый сертификат в качестве основного, а текущий основной сертификат обозначьте как дополнительный. В результате текущий основной сертификат заменится новым сертификатом за один шаг развертывания.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Шаг 4.** Внесите изменения во **все** определения ресурсов **Microsoft.Compute/virtualMachineScaleSets**. Для этого найдите определение ресурса Microsoft.Compute/virtualMachineScaleSets. Перейдите к подразделу "publisher": "Microsoft.Azure.ServiceFabric" в разделе "virtualMachineProfile".

В списке параметров издателя Service Fabric должно отображаться примерно следующее.

![Json_Pub_Setting1][Json_Pub_Setting1]

Добавьте к ним новый сертификат.

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

Свойства должны выглядеть следующим образом:

![Json_Pub_Setting2][Json_Pub_Setting2]

Если необходимо **сменить сертификат**, укажите новый сертификат в качестве основного, а текущий основной сертификат обозначьте как дополнительный. В результате текущий сертификат заменяется новым сертификатом за один шаг развертывания. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
Свойства должны выглядеть следующим образом:

![Json_Pub_Setting3][Json_Pub_Setting3]


**Шаг 5.** Внесите изменения во **все** определения ресурсов **Microsoft.Compute/virtualMachineScaleSets**. Для этого найдите определение ресурса Microsoft.Compute/virtualMachineScaleSets. Перейдите к подразделу "vaultCertificates": в разделе "OSProfile". Должно отобразиться примерно следующее.


![Json_Pub_Setting4][Json_Pub_Setting4]

Добавьте к нему secCertificateUrlValue. Воспользуйтесь следующим фрагментом кода:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Теперь окончательная версия кода JSON должна выглядеть следующим образом:
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Обязательно повторите шаги 4 и 5 для всех определений ресурса Nodetypes/Microsoft.Compute/virtualMachineScaleSets в шаблоне. Если пропустить одно из них, сертификат не установится в данный набор VMSS, что приведет к непредсказуемым результатам в кластере, в том числе выходу кластера из строя (если в итоге у вас не будет действительных сертификатов, которые кластер может использовать для обеспечения безопасности). Поэтому прежде чем продолжать, проверьте все еще раз.
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a>Изменение файла шаблона с учетом новых параметров, добавленных выше
Если далее вы будете использовать пример из репозитория [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample), можете начать вносить изменения в пример 5-VM-1-NodeTypes-Secure_Step2.JSON. 

Измените параметр File в шаблоне Resource Manager. Добавьте два новых параметра secCertificateThumbprint и secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a>Развертывание шаблона в Azure

- Теперь все готово к развертыванию шаблона в Azure. Откройте командную строку Azure PowerShell версии не ниже 1.
- Войдите со своей учетной записью Azure и выберите конкретную подписку Azure. Это важный шаг для пользователей, имеющих доступ к нескольким подпискам Azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Проверьте шаблон перед его развертыванием. Используйте группу ресурсов, в которой развернут кластер.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Разверните шаблон в группу ресурсов. Используйте группу ресурсов, в которой развернут кластер. Выполните команду New-AzureRmResourceGroupDeployment. Не нужно указывать режим, так как по умолчанию используется **добавочный**режим.

> [!NOTE]
> Если задан полный режим, то вы можете случайно удалить ресурсы, которые находятся не в шаблоне. Поэтому не используйте этот режим данном сценарии.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Ниже приведен заполненный пример той же команды PowerShell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

После завершения развертывания подключитесь к кластеру с помощью нового сертификата и выполните несколько запросов. Если получится это сделать. Затем можно удалить старый сертификат. 

Если используется самозаверяющий сертификат, то не забудьте импортировать его в локальное хранилище сертификатов TrustedPeople.

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Для краткой справки ознакомьтесь с командой для подключения к безопасному кластеру: 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Для краткой справки ознакомьтесь с командой для получения данных о работоспособности кластера:

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a>Разверните сертификаты приложения в кластере.

Для развертывания сертификатов из хранилища ключей в узлах можно выполнить те же действия, которые описаны выше для шага 5. Необходимо только определить и использовать другие параметры.


## <a name="adding-or-removing-client-certificates"></a>Добавление или удаление сертификатов клиента

В дополнение к сертификатам кластера можно добавить сертификаты клиента, которые позволят выполнять операции управления в кластере Service Fabric.

Вы можете добавлять сертификаты клиента двух типов: для администратора или только для чтения. Затем их можно использовать для управления доступом к операциям, выполняемым администратором, и операциям, связанным с запросами в кластере. По умолчанию сертификаты кластера добавляются в список разрешенных сертификатов администратора.

Количество сертификатов клиента не ограничено. Каждое добавление или удаление приводит к обновлению конфигурации в кластере Service Fabric.


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Добавление сертификатов клиента для администратора или только для чтения с помощью портала

1. Перейдите к колонке "Безопасность" и выберите "+ Проверка подлинности" в ее верхней части.
2. В колонке "Добавление проверки подлинности" выберите "Тип проверки подлинности" — Read-only client (Клиент с доступом только для чтения) или Admin client (Клиент с правами администратора).
3. Теперь выберите метод авторизации. указывает способ поиска сертификата в Service Fabric (по имени субъекта или по отпечатку). Как правило, по соображениям безопасности не рекомендуется использовать метод авторизации по имени субъекта. 

![Добавление сертификата клиента][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a>Удаление сертификатов клиентов для администратора или только для чтения с помощью портала

Чтобы дополнительный сертификат больше не использовался для обеспечения безопасности кластера, перейдите к колонке "Безопасность" и выберите в контекстном меню соответствующего сертификата параметр "Удалить".



## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об управлении кластерами доступны в следующих статьях.

* [Обновление кластера Service Fabric](service-fabric-cluster-upgrade.md)
* [Настройка доступа на основе ролей для клиентов](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


