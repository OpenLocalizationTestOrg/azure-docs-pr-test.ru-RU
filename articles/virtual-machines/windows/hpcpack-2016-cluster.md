---
title: "aaaHPC 2016 пакет кластера в Azure | Документы Microsoft"
description: "Узнайте, как кластер toodeploy 2016 пакета HPC в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Развертывание кластера пакета HPC 2016 в Azure

Выполните действия hello в этой статье toodeploy [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) кластера на виртуальных машинах Azure. Пакет HPC — это бесплатное решение Майкрософт для высокопроизводительных вычислений, созданное на основе технологий Microsoft Azure и Windows Server, которое поддерживает широкий диапазон рабочих нагрузок высокопроизводительных вычислительных систем.

Используйте один из hello [шаблоны Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy кластера HPC Pack 2016 hello. Есть несколько вариантов топологии кластера с разным числом головных узлов кластера и с вычислительными узлами на основе Linux или Windows.

## <a name="prerequisites"></a>Предварительные требования

### <a name="pfx-certificate"></a>Сертификат PFX

Кластер Microsoft HPC Pack 2016 требует сообщение hello toosecure сертификата обмена личной информацией (PFX) между узлы HPC hello. Hello сертификат должен удовлетворять hello следующие требования:

* Он должен иметь закрытый ключ, поддерживающий обмен ключами.
* Для ключей используются цифровая подпись и шифрование.
* Расширенное использование ключей включает в себя аутентификацию клиента и сервера.

Если у вас еще нет сертификата, соответствующий требованиям, можно запросить hello сертификата из центра сертификации. Кроме того можно использовать следующие команды toogenerate hello самозаверяющий сертификат на основе hello операционной системы, на котором вы выполните команду hello и экспортировать сертификат в формате PFX hello закрытым ключом hello.

* **Для Windows 10 или Windows Server 2016**, запустите встроенный hello **New-SelfSignedCertificate** командлета PowerShell следующим образом:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Для операционных систем более ранних, чем Windows 10 или Windows Server 2016**, загрузите hello [генератор самозаверяющий сертификат](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) из центра сценариев Майкрософт hello. Извлеките его содержимое и выполните следующие команды в командной строке PowerShell hello:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Отправка сертификата tooan хранилища ключей Azure

Перед развертыванием кластера HPC hello, отправьте сертификат tooan hello [хранилища ключей Azure](../../key-vault/index.md) как hello секретным и записи, следующую информацию для использования во время развертывания hello: **имя хранилища**,  **Группа ресурсов хранилища**, **URL-адрес сертификата**, и **отпечаток сертификата**.

Использует сертификат образец tooupload сценария PowerShell hello. Дополнительные сведения об отправке сертификата tooan хранилища ключей Azure см. в разделе [приступить к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md).

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>Поддерживаемые топологии

Выберите один из hello [шаблоны Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy кластера HPC Pack 2016 hello. Ниже в общих чертах описана архитектура трех поддерживаемых топологий кластеров. Топологии с высоким уровнем доступности содержат несколько головных узлов кластера.

1. Высокодоступный кластер с доменом Active Directory

    ![Высокодоступный кластер в домене AD](./media/hpcpack-2016-cluster/haad.png)



2. Высокодоступный кластер без домена Active Directory

    ![Высокодоступный кластер без домена AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Кластер с одним головным узлом

   ![Кластер с одним головным узлом](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Развертывание кластера

toocreate hello кластера, выберите шаблон и нажмите кнопку **развертывание tooAzure**. В hello [портал Azure](https://portal.azure.com), укажите параметры для шаблона hello, как описано в hello следующие шаги. Каждый шаблон создает все ресурсы Azure, необходимые для hello инфраструктура кластера HPC. Эти ресурсы включают в себя виртуальную сеть Azure, общедоступный IP-адрес, балансировщик нагрузки (только для высокодоступного кластера), сетевые интерфейсы, группы доступности, учетные записи хранения и виртуальные машины.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Шаг 1: Выбор подписки hello, расположение и группу ресурсов

Hello **подписки** и hello **расположение** должна быть одинаковой указано, когда загруженный сертификат PFX-ФАЙЛ (см. предварительные условия). Мы рекомендуем создать **группы ресурсов** hello развертывания.

### <a name="step-2-specify-hello-parameter-settings"></a>Шаг 2: Укажите значения параметров hello

Введите или измените значения для параметров шаблона hello. Щелкните параметр значок Далее hello tooeach справочных сведений. Также см. руководство hello по [доступных размеров ВМ](sizes.md).

Укажите значения hello, записанные в hello необходимые условия для hello следующие параметры: **имя хранилища**, **группа ресурсов хранилища**, **URL-адрес сертификата**и **Отпечаток сертификата**.

### <a name="step-3-review-legal-terms-and-create"></a>Шаг 3. Просмотр юридических условий и создание
Нажмите кнопку **просмотрите условия** tooreview hello условия. Если вы согласны, нажмите кнопку **покупки**, а затем нажмите кнопку **создать** toostart hello развертывания.

## <a name="connect-toohello-cluster"></a>Подключите кластер toohello
1. После развертывания кластера HPC Pack hello go toohello [портал Azure](https://portal.azure.com). Нажмите кнопку **групп ресурсов**и в какой hello кластера была развернута группа ресурсов hello поиска. Можно найти hello головной узел виртуальных машин.

    ![Головного узла кластера на портале hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. Щелкните один головной узел (в кластере высокой доступности, щелкните любой из головного узла hello). В **Essentials**, можно найти hello общедоступный IP-адрес или полное DNS-имя кластера hello.

    ![Параметры подключения кластера](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Нажмите кнопку **Connect** toolog на tooany hello головного узлов, с помощью удаленного рабочего стола с вашим именем пользователя администратора указанного. При развертывании кластера hello в домене Active Directory, имя пользователя hello имеет вид hello <privateDomainName> \<adminUsername > (например, hpc.local\hpcadmin).

## <a name="next-steps"></a>Дальнейшие действия
* Отправка задания tooyour кластера. В разделе [отправки заданий tooHPC кластере HPC Pack в Azure](hpcpack-cluster-submit-jobs.md) и [управление кластер HPC Pack 2016 в Azure с помощью Azure Active Directory](hpcpack-cluster-active-directory.md).

