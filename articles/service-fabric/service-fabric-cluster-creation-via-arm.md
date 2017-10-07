---
title: "aaaCreate Azure Service Fabric кластера из шаблона | Документы Microsoft"
description: "В этой статье описывается, как tooset копирование безопасного Service Fabric кластер в Azure с помощью диспетчера ресурсов Azure, хранилище ключей Azure и Azure Active Directory (Azure AD) для проверки подлинности клиента."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Создание кластера Service Fabric в Azure с помощью Azure Resource Manager
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов Azure](service-fabric-cluster-creation-via-arm.md)
> * [Портал Azure](service-fabric-cluster-creation-via-portal.md)
>
>

Это пошаговое руководство поможет выполнить настройку защищенного кластера Azure Service Fabric в Azure с помощью Azure Resource Manager. Мы подтверждаю, что эту статью hello велика. Тем не менее если вы уже знакомы тщательно с содержимым hello, быть toofollow убедиться, что каждый шаг внимательно.

Hello руководстве описываются hello следующих процедур:

* Настройка сертификатов tooupload хранилища ключей Azure для обеспечения безопасности кластера и приложения
* Создание защищенного кластера в Azure с помощью Azure Resource Manager
* Аутентификация пользователей с помощью Azure Active Directory для управления кластером

Безопасный кластер — это кластер, предотвращает несанкционированный доступ toomanagement операции. Это включает в себя развертывание, обновление и удаление приложений, служб и данных hello, содержащихся в них. Небезопасные кластер — это кластер, что любой пользователь может подключиться tooat в любое время и выполнять операции управления. Несмотря на возможные toocreate кластер небезопасным, настоятельно рекомендуется создать безопасный кластер с самого начала hello. Поскольку незащищенный кластер невозможно будет защитить позднее, нужно создать новый кластер.

Понятие Hello создания защищенных кластеров является hello одинаковым, являются ли они кластеров Windows или Linux. Дополнительные сведения о создании безопасных кластеров Linux, а также вспомогательные скрипты см. в разделе [Создание безопасных кластеров в Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Войдите в tooyour учетная запись Azure
В этом руководстве используется [Azure PowerShell][azure-powershell]. При запуске нового сеанса PowerShell, войдите в tooyour учетная запись Azure и выберите подписку, перед выполнением команды Azure.

Войдите в tooyour учетная запись Azure.

```powershell
Login-AzureRmAccount
```

Выберите свою подписку.

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Настройка хранилища ключей
В этом разделе описывается, как создать хранилище ключей для кластера Service Fabric в Azure и приложений Service Fabric. Полное руководство по tooAzure хранилище ключей см. в разделе toohello [хранилище ключей Знакомство с][key-vault-get-started].

Service Fabric использует сертификаты X.509 toosecure кластера и обеспечивает функции безопасности приложения. Использовать хранилище ключей toomanage сертификаты для кластеров Service Fabric в Azure. При развертывании в Azure, hello поставщика ресурсов Azure, который отвечает за создание кластеров Service Fabric извлекает сертификаты из хранилища ключей и устанавливает их на кластере hello виртуальных машин.

Hello следующей схеме показана связь hello хранилище ключей Azure, кластер Service Fabric и hello поставщика ресурсов Azure, которая использует сертификаты, хранящиеся в хранилище ключей при создании кластера.

![Схема установки сертификата][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Создание группы ресурсов
Hello первым шагом является toocreate группы ресурсов, в частности для хранилища ключей. Рекомендуется поместить hello хранилища ключей в отдельной группе ресурсов. Это действие позволяет удалить hello вычислений и хранения групп ресурсов, включая hello группы ресурсов, содержащем кластер Service Fabric, без потери ключи и секретные коды. группы ресурсов Hello, содержащий ваше хранилище ключа _должен находиться в hello одного региона_ как кластер hello, он используется.

Если планируется toodeploy кластеров в нескольких регионах, мы советуем использовать имя группы ресурсов hello и hello хранилища ключей, в результате которого указывает область, которая принадлежит.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
Hello вывод должен выглядеть следующим образом:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Создание хранилища ключей в новую группу ресурсов hello
хранилище ключей Hello _должна быть включена для развертывания_ tooallow hello сертификаты tooget поставщика вычислительных ресурсов от него и установите его на экземпляры виртуальной машины:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

Hello вывод должен выглядеть следующим образом:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Использование существующего хранилища ключей

toouse существующего хранилища ключей, вы _необходимо включить его для развертывания_ tooallow hello сертификаты tooget поставщика вычислительных ресурсов от него и установите его на узлах кластера:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Добавление хранилища ключей tooyour сертификатов

Сертификаты используются в Service Fabric tooprovide проверки подлинности и шифрования toosecure различные аспекты кластера и его применения. Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Сертификат кластера и сервера (обязательно)
Этот сертификат является обязательным toosecure кластером и предотвратить несанкционированный доступ tooit. Он обеспечивает безопасность кластера двумя способами.

* Аутентификация в кластере позволяет аутентифицировать обмен данными между узлами для федерации кластера. Только узлы, которые можно подтвердить свою личность с помощью этого сертификата можно соединить hello кластера.
* Проверка подлинности сервера: проверяет подлинность hello кластера управления конечными точками tooa клиента управления, чтобы hello управления клиент узнает, осуществляет обмен данными toohello реальные кластера. Этот сертификат также предоставляет SSL для hello API управления HTTPS и обозреватель Service Fabric по протоколу HTTPS.

tooserve этих целей, hello сертификат должен удовлетворять hello следующие требования:

* Hello сертификат должен содержать закрытый ключ.
* необходимо создать сертификат Hello для обмена ключами, который является tooa экспортируемый файл обмена личной информацией (PFX-файл).
* Имя субъекта сертификата Hello должен соответствовать домену hello, использовать кластер Service Fabric tooaccess hello. Это сопоставление является обязательным tooprovide SSL для конечных точек управления HTTPS hello кластера и обозреватель Service Fabric. Не удается получить SSL-сертификат центра сертификации (ЦС), для hello. cloudapp.azure.com домена. Необходимо получить имя личного домена для кластера. При запросить сертификат от центра сертификации, hello имя субъекта сертификата должно соответствовать hello собственное доменное имя для вашего кластера.

### <a name="application-certificates-optional"></a>Сертификаты приложения (необязательно)
В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений. Перед созданием кластера, рассмотрим hello безопасности приложений, требующих toobe сертификатов, установленных на узлах hello, такие как:

* шифрование и расшифровка значений конфигурации приложений;
* шифрование данных между узлами во время репликации.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>форматирование сертификатов для использования поставщиком ресурсов Azure.
Файлы закрытых ключей (PFX) можно добавить и использовать непосредственно в своем хранилище ключей. Однако поставщик ресурсов hello вычислений Azure требует toobe ключи, хранящиеся в специальном формате JavaScript Object Notation (JSON). Формат Hello включает hello PFX-файл как базовый строка в кодировке Base64 и hello пароль закрытого ключа. tooaccommodate эти требования hello ключей необходимо поместить в строку JSON и затем сохраняются в виде «секреты» hello ключа хранилища.

Эта процедура, toomake [модуль PowerShell можно найти в GitHub][service-fabric-rp-helpers]. модуль toouse hello, hello следующие:

1. Загрузите все содержимое репозитория hello hello в локальный каталог.
2. Последовательно выберите toohello локальный каталог.
2. Импорт модуля ServiceFabricRPHelpers hello в окне PowerShell:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Hello `Invoke-AddCertToKeyVault` команды в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строке JSON и отправляет его toohello хранилища ключей. Используйте hello команда tooadd hello кластера сертификат и все сертификаты дополнительное приложение toohello ключа хранилища. Повторите это действие другие сертификаты, требуется tooinstall в кластере.

#### <a name="uploading-an-existing-certificate"></a>Загрузка существующего сертификата

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Если возникает ошибка, например hello показанной здесь, это обычно означает, что имеется конфликт ресурсов URL-адрес. конфликт tooresolve hello, изменить имя хранилища ключей hello.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

После устранения конфликта hello hello вывод должен выглядеть следующим образом:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>Необходимо hello три предыдущей строки, CertificateThumbprint, SourceVault и CertificateURL tooset безопасности кластера Service Fabric и tooobtain все сертификаты приложения, которые можно использовать для обеспечения безопасности приложения. Если не сохранить строки hello, может быть трудно tooretrieve их с помощью запроса hello ключ в хранилище позже.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Создание самозаверяющего сертификата и передачи их в хранилище ключей toohello

Если вы уже отправили хранилища ключей toohello сертификаты, пропустите этот шаг. Этот шаг является создание нового самозаверяющего сертификата, и передачи их в хранилище ключей tooyour. После изменения параметров hello в hello, выполнив сценарий и запустите его, должен быть запрос пароль сертификата.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Если возникает ошибка, например hello показанной здесь, это обычно означает, что имеется конфликт ресурсов URL-адрес. конфликт tooresolve hello, изменить имя хранилища ключей hello, RG имя и т. д.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

После устранения конфликта hello hello вывод должен выглядеть следующим образом:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>Необходимо hello три предыдущей строки, CertificateThumbprint, SourceVault и CertificateURL tooset безопасности кластера Service Fabric и tooobtain все сертификаты приложения, которые можно использовать для обеспечения безопасности приложения. Если не сохранить строки hello, может быть трудно tooretrieve их с помощью запроса hello ключ в хранилище позже.

 На этом этапе должно быть hello следующие элементы на месте:

* Группа ресурсов хранилища ключей Hello.
* Здравствуйте, хранилище ключей и его URL-адреса (называемая SourceVault в hello, предшествующие выходные данные PowerShell).
* сертификат проверки подлинности сервера Hello кластера и его URL-адреса в хранилище ключей hello.
* Hello приложения сертификаты и их URL-адреса в хранилище ключей hello.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Настройка Azure Active Directory для проверки подлинности клиента

Azure AD обеспечивает tooapplications доступ пользователя toomanage организаций (это называется клиентов). Приложения можно разделить на две группы: те, в которых есть пользовательский веб-интерфейс входа в систему, и те, в которых вход выполняется с помощью собственного клиентского приложения. В этой статье предполагается, что клиент уже создан. Если нет, начните с просмотра [как для клиента Azure Active Directory tooget][active-directory-howto-tenant].

Кластер Service Fabric предлагает несколько tooits точки входа функции управления, включая hello веб- [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] и [Visual Studio] [service-fabric-manage-application-in-visual-studio]. В результате создания кластера toohello два Azure AD приложений toocontrol доступа, одно веб-приложение и один собственное приложение.

Некоторые шаги hello участвующих в настройке Azure AD с кластера Service Fabric toosimplify, мы создали набор сценариев Windows PowerShell.

> [!NOTE]
> Необходимо выполнить следующие действия перед созданием кластера hello hello. Поскольку hello сценарии ожидается, что имена кластеров и конечные точки, значения hello следует планировать и не значения, что вы уже создали.

1. [Загрузите скрипты hello] [ sf-aad-ps-script-download] tooyour компьютера.
2. Щелкните правой кнопкой мыши hello ZIP-файл, выберите **свойства**выберите hello **Unblock** флажок и нажмите кнопку **применить**.
3. Извлеките ZIP-файл hello.
4. Запустите `SetupApplications.ps1`и укажите hello идентификатора клиента, Имя_кластера и WebApplicationReplyUrl в качестве параметров. Например:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Вашего идентификатора клиента можно найти, выполнив команду PowerShell hello `Get-AzureSubscription`. При выполнении данной команды отображение hello идентификатора клиента для каждой подписки.

    Имя_кластера — приложения hello Azure AD используется tooprefix, созданные скриптом hello. Имя фактического кластера toomatch hello не обязательно точно. Это предполагаемое только toomake его проще toomap Azure AD артефакты toohello кластера Service Fabric, они привыкли с.

    WebApplicationReplyUrl — конечную точку по умолчанию hello, Azure AD возвращает tooyour пользователей после их завершения вход. Установите эту конечную точку в качестве конечной точки Service Fabric Explorer hello для кластера, который по умолчанию является:

    https://&lt;cluster_domain&gt;:19080/Explorer

    Все запрашиваемые toosign tooan учетной записью, имеющей права администратора для клиента hello Azure AD. После входа в скрипт hello создает веб-hello и собственных приложений toorepresent кластера Service Fabric. Если взглянуть на приветствия клиента приложения в hello [классический портал Azure][azure-classic-portal], вы увидите два новых элемента:

   * *имя_кластера*\_Кластер
   * *имя_кластера*\_Клиент

   сценарий Hello печатает Привет открыть JSON, необходимых для шаблона Azure Resource Manager hello, при создании кластера hello в следующем разделе hello, это окно PowerShell рекомендуется tookeep hello.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Создание шаблона Resource Manager для кластера Service Fabric
В этом разделе hello выходных данных из предыдущей hello можно использовать команды PowerShell в шаблоне диспетчер ресурсов кластера Service Fabric.

Пример диспетчера ресурсов шаблоны доступны в hello [коллекции Azure краткое шаблонов на GitHub][azure-quickstart-templates]. Их можно использовать в качестве отправной точки для создания шаблона кластера.

### <a name="create-hello-resource-manager-template"></a>Создание шаблона диспетчера ресурсов hello
В этом руководстве используется hello [безопасного кластер 5] [ service-fabric-secure-cluster-5-node-1-nodetype] пример шаблона и параметров шаблона. Загрузить `azuredeploy.json` и `azuredeploy.parameters.json` tooyour компьютер и открыть оба файла в другом текстовом редакторе.

### <a name="add-certificates"></a>Добавление сертификатов
Добавление шаблона диспетчера ресурсов кластера tooa сертификаты, ссылаясь на хранилище ключей hello, содержащий ключи сертификатов hello. Рекомендуется размещать значения hello хранилище ключей в файле параметров шаблона диспетчера ресурсов. Таким образом отслеживает hello диспетчера ресурсов файл шаблона для повторного использования и не развертывания tooa конкретного значения.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Добавление набора масштабирования виртуальных машин toohello все сертификаты в osProfile
Каждый сертификат, устанавливаемый в кластере hello должен быть настроен в разделе osProfile hello hello шкалы набор ресурсов (Microsoft.Compute/virtualMachineScaleSets). Это действие указывает, что сертификат hello tooinstall поставщика ресурсов hello на hello виртуальных машин. Эта установка включает hello кластера сертификатов и сертификаты безопасности приложения, планирование toouse приложений:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Настройка сертификата кластера Service Fabric hello
сертификат проверки подлинности Hello кластера должен быть настроен в обеих ресурса кластера Service Fabric hello (Microsoft.ServiceFabric/clusters), и задает hello расширения Service Fabric для масштабирования виртуальных машин в ресурс набор масштабирования виртуальной машины hello. Такой подход позволяет tooconfigure поставщика ресурсов Service Fabric hello его использовать для проверки подлинности для кластера и сервера для конечных точек управления.

##### <a name="virtual-machine-scale-set-resource"></a>Ресурс масштабируемого набора виртуальных машин:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Ресурс Service Fabric.
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Получение конфигурации Azure AD
Конфигурация Hello Azure AD, созданный ранее могут быть вставлены непосредственно в шаблон диспетчера ресурсов. Тем не менее рекомендуется сначала извлечь значения hello в повторно используемый hello диспетчера ресурсов шаблона параметров файла tookeep и освободить развертывания tooa конкретного значения.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a>Настройка параметров шаблона Resource Manager
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
И наконец используйте hello выходные значения из хранилища ключей hello и файле параметров hello toopopulate команды Azure AD PowerShell.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
На этом этапе должно быть hello следующие элементы на месте:

* группа ресурсов хранилища ключей;
  * Хранилище ключей
  * сертификат проверки подлинности сервера кластера;
  * сертификат шифрования данных;
* клиент Azure Active Directory;
  * приложение Azure AD для управления через Интернет и Service Fabric Explorer;
  * приложение Azure AD для управления собственными клиентами.
  * Пользователи и назначенные им роли
* шаблон Resource Manager для кластера Service Fabric;
  * Сертификаты, настроенные с помощью хранилища ключей
  * настроенная среда Azure Active Directory.

Привет, следующая схема иллюстрирует где хранилище ключей и конфигурации Azure AD, помещаются в шаблон диспетчера ресурсов.

![Сопоставление зависимостей Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Создание кластера hello
Теперь вы находитесь готов toocreate hello кластера с помощью [развертывания шаблона ресурсов Azure][resource-group-template-deploy].

#### <a name="test-it"></a>Тестирование
С помощью файла параметров с помощью этого шаблона диспетчера ресурсов hello, следуя tootest команды PowerShell:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Развертывание
Если hello диспетчера ресурсов шаблона тест был пройден, используйте hello, следующая команда toodeploy PowerShell шаблона диспетчера ресурсов с помощью файла параметров:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Назначить пользователей tooroles
После создания toorepresent приложения hello кластера, ролям пользователей toohello поддерживаемые Service Fabric: только для чтения и администрирования. Hello роли можно назначить с помощью hello [классический портал Azure][azure-classic-portal].

1. В hello портал Azure, перейдите tooyour клиента, а затем выберите **приложений**.
2. Выберите веб-приложения hello, который имеет имя, например `myTestCluster_Cluster`.
3. Нажмите кнопку hello **пользователей** вкладки.
4. Выберите tooassign пользователя и нажмите кнопку hello **назначить** кнопку hello нижней части экрана приветствия.

    ![Назначить пользователей tooroles кнопки][assign-users-to-roles-button]
5. Выберите tooassign toohello hello роли пользователя.

    ![Диалоговое окно "Назначить пользователей"][assign-users-to-roles-dialog]

> [!NOTE]
> Дополнительные сведения о ролях в Service Fabric см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Создание безопасных кластеров в Linux
упрощает процесс hello toomake, мы предоставили [вспомогательный сценарий](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Прежде чем использовать этот вспомогательный сценарий, убедитесь, что интерфейс командной строки Azure уже установлен и указан в пути. Сценарий hello оставалось tooexecute разрешения, выполнив `chmod +x cert_helper.py` после его загрузки. Hello первым шагом является toosign в tooyour учетная запись Azure с помощью CLI с hello `azure login` команды. После входа в учетную запись Azure tooyour использовать hello вспомогательный сценарий с помощью центра сертификации подписанного сертификата, как hello, следующая команда показывает:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

параметр - ifile Hello может принимать в PFX-файл или PEM-файл в качестве выходных данных и hello тип сертификата (PFX-файла или pem или ss, если это самозаверяющий сертификат).
Hello параметр -h выводит текст справки hello.


Эта команда возвращает следующие три строки в качестве выходных данных hello hello:

* SourceVaultID, который является Идентификатором hello для hello новой группе ресурсов KeyVault, она создана для вас
* CertificateUrl для доступ к сертификату hello
* CertificateThumbprint — используется для аутентификации.

Hello в следующем примере показано, как toouse hello команды:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Выполнение hello предшествующий дает команду hello три строки, как показано ниже:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

Имя субъекта сертификата Hello должен соответствовать домену hello, использовать кластер Service Fabric tooaccess hello. Это совпадение является обязательным tooprovide SSL для конечных точек управления HTTPS hello кластера и обозреватель Service Fabric. Не удается получить SSL-сертификат из ЦС для hello `.cloudapp.azure.com` домена. Необходимо получить имя личного домена для кластера. При запросить сертификат от центра сертификации, hello имя субъекта сертификата должно соответствовать hello собственное доменное имя для вашего кластера.

Эти имена субъектов, hello записей необходимо toocreate безопасности кластера Service Fabric (без Azure AD), как описано в разделе [параметров шаблона настройки диспетчера ресурсов](#configure-arm). Подключении toohello безопасного кластера в соответствии с инструкциями hello для [проверки подлинности клиента доступа tooa кластера](service-fabric-connect-to-secure-cluster.md). Кластеры Linux предварительной версии не поддерживают аутентификацию Azure AD. Вы можете назначить роли администратора и клиента, как описано в hello [назначение ролей toousers](#assign-roles) раздела. При указании роли администратора и клиента для Linux предварительного просмотра кластера, у вас есть tooprovide отпечатки сертификатов для проверки подлинности. (Отсутствует имя субъекта hello, так как в этом предварительном выпуске выполняется без проверки цепочки или отзыва.)

Если требуется toouse самозаверяющего сертификата для тестирования, можно использовать hello же toogenerate сценарий один. Затем вы можете передать хранилища ключей tooyour сертификат hello, указав флаг hello `ss` вместо предоставления hello сертификат путь и имя сертификата. Например см. следующую команду для создания и передачи самозаверяющий сертификат hello:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Эта команда возвращает hello одинаковые три строки: SourceVault, CertificateUrl и CertificateThumbprint. Затем можно использовать строки toocreate hello безопасного кластеров Linux и расположение, куда помещается hello самозаверяющий сертификат. Вам потребуется hello самозаверяющий сертификат tooconnect toohello кластер. Подключении toohello безопасного кластера в соответствии с инструкциями hello для [проверки подлинности клиента доступа tooa кластера](service-fabric-connect-to-secure-cluster.md).

Имя субъекта сертификата Hello должен соответствовать домену hello, использовать кластер Service Fabric tooaccess hello. Это совпадение является обязательным tooprovide SSL для конечных точек управления HTTPS hello кластера и обозреватель Service Fabric. Не удается получить SSL-сертификат из ЦС для hello `.cloudapp.azure.com` домена. Необходимо получить имя личного домена для кластера. При запросить сертификат от центра сертификации, hello имя субъекта сертификата должно соответствовать hello собственное доменное имя для вашего кластера.

Можно заполнить hello параметры из сценария вспомогательный hello в hello портал Azure, как описано в hello [создания кластера в hello портал Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) раздела.

## <a name="next-steps"></a>Дальнейшие действия
На этом этапе у вас имеется защищенный кластер с Azure Active Directory для аутентификации управления. Далее, [подключения кластера tooyour](service-fabric-connect-to-secure-cluster.md) и узнайте, каким образом слишком[управление секретами приложения](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Устранение неполадок с настройкой Azure Active Directory для проверки подлинности клиента
Если возникли проблемы при установке Azure AD для проверки подлинности клиента, просмотрите hello возможные решения в этом разделе.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Обозреватель Service Fabric предлагает tooselect сертификата
#### <a name="problem"></a>Проблема
После входа в успешно tooAzure AD в обозреватель Service Fabric hello браузера возвращает toohello домашней страницы, но появится сообщение с запросом tooselect сертификат.

![Диалоговое окно выбора сертификата в Service Fabric Explorer][sfx-select-certificate-dialog]

#### <a name="reason"></a>Причина
Hello пользователю не назначен роли в hello кластерного приложения Azure AD. Таким образом, аутентификация Azure AD в кластере Service Fabric завершается ошибкой. Обозреватель Service Fabric возвращается toocertificate проверки подлинности.

#### <a name="solution"></a>Решение
Выполните инструкции hello настройки Azure AD и назначить роли пользователя. Кроме того, рекомендуется включить «Приложение требуется tooaccess назначение пользователя», как `SetupApplications.ps1` does.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Подключение с помощью PowerShell завершается с ошибкой: «hello указанные учетные данные недействительны»
#### <a name="problem"></a>Проблема
При использовании кластера toohello tooconnect PowerShell с помощью режима безопасности «Azureactivedirectory возникла ошибка», после входа в успешно tooAzure AD hello подключение завершается с ошибкой: «hello указано недопустимые учетные данные».

#### <a name="solution"></a>Решение
Это решение является таким же, как hello, предшествующие, приветствия.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer при входе возвращает ошибку "AADSTS50011"
#### <a name="problem"></a>Проблема
При попытке toosign в tooAzure AD в обозреватель Service Fabric, страница приветствия возвращает ошибку: «AADSTS50011: hello обратный адрес &lt;URL-адрес&gt; не соответствует hello адреса ответа, настроенного для приложения hello: &lt;guid&gt;."

![Несовпадение адреса ответа в Service Fabric Explorer][sfx-reply-address-not-match]

#### <a name="reason"></a>Причина
приложение Hello кластера (Интернет), представляющий Service Fabric Explorer пытается tooauthenticate от Azure AD, и как часть запроса hello предоставляет hello перенаправления URL-адреса возврата. Но hello URL-адрес не указан в приложение hello Azure AD **URL-адрес ОТВЕТА** списка.

#### <a name="solution"></a>Решение
На hello **Настройка** вкладка hello кластера (приложение), добавьте URL-адрес из Service Fabric Explorer toohello hello **URL-адрес ОТВЕТА** списка или заменить один из элементов hello в списке hello. После завершения сохраните изменения.

![URL-адрес ответа веб-приложения][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Подключите hello кластер с помощью проверки подлинности Azure AD с помощью PowerShell
кластер Service Fabric hello tooconnect, hello используйте следующий пример команды PowerShell:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn командлету Connect-ServiceFabricCluster hello. в разделе [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Можно использовать клиент hello же Azure AD в несколько кластеров
Да. Но следует помнить tooadd hello URL-адрес из Service Fabric Explorer tooyour кластера (Интернет) приложения. В противном случае — Service Fabric Explorer не работает.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Почему мне все еще нужен сертификат сервера при включенном Azure AD?
FabricClient и FabricGateway выполняют взаимную аутентификацию. Во время проверки подлинности Azure AD интеграция Azure AD предоставляет клиента сервер toohello удостоверений и сертификат сервера hello является удостоверение сервера используется tooverify hello. Дополнительные сведения о сертификатах Service Fabric см. в разделе [Сертификаты X.509 и Service Fabric][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

