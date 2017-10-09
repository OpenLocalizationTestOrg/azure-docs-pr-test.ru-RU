---
title: "сертификаты aaaManage в кластере Azure Service Fabric | Документы Microsoft"
description: "Описывает, как tooadd новых сертификатов, сертификат продолжения и удалить сертификат tooor из кластера Service Fabric."
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
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Добавление и удаление сертификатов для кластера Service Fabric в Azure
Рекомендуется ознакомиться с как Service Fabric используются сертификаты X.509 и ознакомьтесь с hello [кластера сценарии безопасности](service-fabric-cluster-security.md). Необходимо понять, что такое сертификат кластера и для чего он используется, прежде чем продолжить.

Служба структуры позволяет указать два кластера сертификатов, первичной и вторичной реплике, при настройке сертификата безопасности во время создания кластера в добавление tooclient сертификаты. См. слишком[создание кластера azure через портал](service-fabric-cluster-creation-via-portal.md) или [создание кластера azure посредством Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) для сведений о настройке их во время создания. Если указать только один сертификат кластера во время создания, затем используется как основной сертификат hello. После создания кластера можно добавить новый сертификат в качестве дополнительного.

> [!NOTE]
> Безопасный кластер всегда необходим сертификат по крайней мере один допустимый (не отозван и не истекшим сроком действия) кластера (основная или вторичная) развернуты (в противном случае hello кластер прекращает работу). 90 дней до истечения срока действия, достичь все действительные сертификаты hello возникнет предупреждение трассировки, а также событие предупреждения работоспособности на узле hello. В настоящее время Service Fabric не отправляет какие-либо электронные сообщения или другие уведомления о данной теме. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Добавление сертификата получателя кластера с помощью портала hello

Невозможно добавить вторичный кластер сертификат через портал Azure hello. У вас есть toouse Azure powershell для этого. Далее в этом документе описывается процесс Hello.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Поменять местами с помощью портала hello сертификаты кластера hello

После того как развернута успешно сертификат получателя кластера, нужно tooswap hello основного и дополнительного, перейдите колонке toohello безопасности и выберите параметр «Переключение с основного» hello из hello контекстного меню tooswap hello вторичного сертификата с основной сертификат Hello.

![Переключение сертификатов][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Удаление сертификата кластера с помощью портала hello

Для безопасного кластера всегда потребуется по крайней мере один допустимый (не отозван и не истекшим сроком действия) сертификат (основная или вторичная) развернуты в противном случае hello кластер прекращает работу.

tooremove дополнительный сертификат не могут использоваться для безопасности кластера, колонке безопасности toohello перейдите и выберите hello «Delete» hello контекстном меню на дополнительный сертификат hello.

Если планируется tooremove hello сертификат, который помечен первичных, вам потребуется tooswap его с сначала hello получателя, а затем удалите hello получателя после завершения обновления hello.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Добавление дополнительного сертификата с помощью PowerShell для Resource Manager

Эти шаги предполагают знакомы с принципами работы диспетчера ресурсов и развернут хотя бы одного Service Fabric кластера с помощью шаблона диспетчера ресурсов, а шаблон hello использования tooset hello кластера под рукой. Предполагается также, что вы уверенно используете JSON.

> [!NOTE]
> Если вы ищете образец шаблона и параметров, которые можно использовать toofollow вдоль или в качестве отправной точки, затем загрузите его из этого [репозитория git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Изменение шаблона Resource Manager

Для удобства ниже вдоль пример 5-VM-1-NodeTypes-Secure_Step2.JSON содержит все изменения hello, уже им. Образец Hello доступен на [репозитория git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Убедитесь, что toofollow все шаги hello**

**Шаг 1.** откройте hello шаблона диспетчера ресурсов, используемые toodeploy кластеризации. (Если вы загрузили пример hello из hello выше репозитория, затем использовать 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy безопасного кластера, а затем откройте копию этого шаблона).

**Шаг 2.** добавить **два новых параметра** «secCertificateThumbprint» и «secCertificateUrlValue» типа «string» toohello раздел параметров шаблона. Можно скопировать следующий фрагмент кода hello и добавить его toohello шаблона. В зависимости от источника hello шаблона могут уже иметь эти определенные, в этом случае переместить toohello следующий шаг. 
 
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
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Шаг 3.** внесение изменений toohello **Microsoft.ServiceFabric/clusters** ресурса, найдите определение ресурсов «Microsoft.ServiceFabric/clusters» hello в шаблон. В разделе Свойства этого определения найдет «Сертификат» JSON тег, который выглядит примерно hello, следующий фрагмент JSON:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Добавьте новый тег thumbprintSecondary и присвойте ему значение [parameters('secCertificateThumbprint')].  

Да, теперь hello определения ресурса должен выглядеть hello следующим образом (в зависимости от источника hello шаблона, он может не быть так же, как в приведенном ниже фрагменте hello). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Если требуется слишком**продолжения hello cert**, укажите в качестве первичного и перемещение hello текущая первичная дополнительный — hello новый сертификат. Это приводит к hello смену текущей основной сертификат toohello новый сертификат в один шаг развертывания.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Шаг 4.** вносить в них изменения слишком**все** hello **Microsoft.Compute/virtualMachineScaleSets** определения ресурсов - обнаружения ресурса Microsoft.Compute/virtualMachineScaleSets hello Определение. Прокрутите toohello «издатель»: «Microsoft.Azure.ServiceFabric» в разделе «virtualMachineProfile».

В настройках издателя структуры службы hello вы увидите примерно следующим образом.

![Json_Pub_Setting1][Json_Pub_Setting1]

Добавить hello нового сертификата записи tooit

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

свойства Hello теперь должна выглядеть следующим образом

![Json_Pub_Setting2][Json_Pub_Setting2]

Если требуется слишком**продолжения hello cert**, укажите в качестве первичного и перемещение hello текущая первичная дополнительный — hello новый сертификат. Это приводит к hello смену текущий сертификат toohello новый сертификат за один шаг развертывания. 


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
свойства Hello теперь должна выглядеть следующим образом

![Json_Pub_Setting3][Json_Pub_Setting3]


**Шаг 5.** вносить изменения слишком**все** hello **Microsoft.Compute/virtualMachineScaleSets** определения ресурсов - обнаружения ресурса Microsoft.Compute/virtualMachineScaleSets hello Определение. Прокрутите toohello «vaultCertificates»:, в разделе «OSProfile». Должно отобразиться примерно следующее.


![Json_Pub_Setting4][Json_Pub_Setting4]

Добавьте hello secCertificateUrlValue tooit. Используйте следующий фрагмент кода hello.

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Hello, возникающие в Json должны выглядеть примерно следующим образом.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Убедитесь, что содержать повторяющиеся шаги 4 и 5 для всех определений ресурсов Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello в шаблон. Если пропустить один из них, hello сертификат будет не устанавливается на этом VMSS и будет привести к непредсказуемым результатам в кластере кластера hello выхода из строя (Если вы получаете действительные сертификаты не могут использовать этот кластер hello для обеспечения безопасности. Поэтому прежде чем продолжать, проверьте все еще раз.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Изменение шаблона файла tooreflect hello новые параметры добавленную выше
При использовании образца hello из hello [репозитория git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow вместе, вы можете запустить toomake изменения в hello пример 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 

Изменение параметра шаблона диспетчера ресурсов файл, добавить два новых параметра hello secCertificateThumbprint и secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Развертывание шаблона tooAzure hello

- Вы являются toodeploy теперь готовы к tooAzure шаблона. Откройте командную строку Azure PowerShell версии не ниже 1.
- Войдите в tooyour учетную запись Azure и выберите конкретную подписку azure hello. Это важный шаг для людей, имеющих доступ toomore более одной подписки azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Тестирование toodeploying предыдущий шаблон hello его. Используйте hello же группе ресурсов кластера в настоящее время развертыванием.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Развертывание группы ресурсов tooyour шаблона hello. Используйте hello же группе ресурсов кластера в настоящее время развертыванием. Выполните команду New-AzureRmResourceGroupDeployment hello. Нет необходимости toospecify hello режиме, так как значение по умолчанию hello **добавочное**.

> [!NOTE]
> При выборе режима tooComplete можно случайно удалить ресурсы, не входящие в шаблон. Поэтому не используйте этот режим данном сценарии.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Вот out пример hello заполненный же powershell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

После завершения развертывания hello подключения tooyour кластера с помощью нового сертификата hello и выполнять некоторые запросы. Если вы не можете toodo. Затем можно удалить старый сертификат hello. 

Если вы используете самозаверяющий сертификат, не забудьте tooimport их в локальное хранилище TrustedPeople сертификат.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Краткий справочник Вот hello команда tooconnect tooa безопасности кластера 

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
Краткий справочник Вот работоспособности кластера tooget команда hello

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Развертывание кластера toohello сертификаты приложений.

Можно использовать hello же шаги, как описано в шаги 5 выше toohave hello сертификаты, развернутых из keyvault toohello узлов. Необходимо только определить и использовать другие параметры.


## <a name="adding-or-removing-client-certificates"></a>Добавление или удаление сертификатов клиента

В дополнение toohello кластера сертификаты можно добавить операции управления tooperform сертификаты клиента на кластере service fabric.

Вы можете добавлять сертификаты клиента двух типов: для администратора или только для чтения. Они затем могут быть операции администрирования toohello доступа используется toocontrol и операций запросов на кластере hello. По умолчанию hello кластера сертификаты добавляются toohello разрешенный список сертификатов администратора.

Количество сертификатов клиента не ограничено. Каждый добавлении или удалении приводит кластера service fabric конфигурации обновления toohello


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Добавление сертификатов клиента для администратора или только для чтения с помощью портала

1. Перейдите в колонку toohello безопасности и выберите hello «+ проверки подлинности» кнопки на колонки безопасности hello.
2. В колонке «Добавление проверки подлинности» hello выберите hello «Тип проверки подлинности» - «Client только для чтения» или «Администратор клиента»
3. Теперь выберите метод авторизации hello. Это означает tooService структуры ли этот сертификат следует искать с помощью hello имени субъекта или отпечатка hello. Как правило он не является методом обеспечения безопасности рекомендуется toouse hello авторизации имени субъекта. 

![Добавление сертификата клиента][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Здравствуйте, удаление сертификатов клиента - администратора или только для чтения с помощью портала

tooremove дополнительный сертификат не могут использоваться для безопасности кластера, колонке безопасности toohello перейдите и выберите hello «Delete» hello контекстном меню на hello конкретного сертификата.



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


