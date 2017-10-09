---
title: "aaaIntegrate хранилища ключей с SQL Server на виртуальных машинах Windows в Azure (классические) | Документы Microsoft"
description: "Узнайте, как tooautomate hello конфигурация шифрования SQL Server для использования с хранилищем ключей Azure. В этом разделе объясняется, как создать toouse интеграция хранилища ключей Azure с SQL Server виртуальными машинами в hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Настройка интеграции хранилища ключей Azure для SQL Server на виртуальных машинах Azure (классическая модель)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Классический](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Обзор
Существует несколько функций шифрования SQL Server, например [прозрачное шифрование данных (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [шифрование на уровне столбцов (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) и [шифрование резервной копии](https://msdn.microsoft.com/library/dn449489.aspx). Эти формы шифрования требуют toomanage и хранения hello криптографических ключей, который используется для шифрования. Hello службы хранилища ключей Azure (AKV) — спроектированный tooimprove hello безопасности и управления из этих ключей в расположении высокой надежности и безопасности. Hello [соединителя SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) позволяет SQL Server toouse эти ключи из хранилища ключей Azure.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

Если вы используете SQL Server с локальными компьютерами, [действия можно выполнить tooaccess хранилище ключей Azure с локального компьютера SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Но для SQL Server в виртуальных машинах Azure, вы можете сэкономить время с помощью hello *интеграция хранилища ключей Azure* компонентов. С несколько tooenable командлеты Azure PowerShell эту функцию, можно автоматизировать hello хранилища ключей конфигурации, необходимые для tooaccess SQL виртуальной Машины.

Если эта функция включена, автоматически устанавливает hello соединителя SQL Server, настраивает tooaccess поставщика расширенного управления Ключами hello хранилище ключей Azure и создает tooallow hello учетных данных вы tooaccess вашего хранилища. Если был рассмотрен hello инструкциям hello упомянутых выше локальной документации, вы увидите, что эта функция автоматизирует шаги 2 и 3. Единственное Hello по-прежнему необходимо toodo вручную — хранилище ключей toocreate hello и ключи. После этого выполняется автоматически hello всю настройку ВМ SQL. После завершения программы установки эту функцию можно выполнить toobegin инструкции T-SQL, шифрование баз данных или резервного копирования, как обычно.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Настройка интеграции AKV
С помощью PowerShell tooconfigure интеграция хранилища ключей Azure. Привет, в следующих разделах предоставляют обзор hello необходимые параметры, а затем образец скрипта PowerShell.

### <a name="install-hello-sql-server-iaas-extension"></a>Установка расширения SQL Server IaaS hello
Во-первых, [установки расширения SQL Server IaaS hello](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Понимать hello входные параметры
Hello следующие параметры hello списки таблицы требуется сценарий PowerShell toorun hello в следующем разделе hello.

| Параметр | Описание | Пример |
| --- | --- | --- |
| **$akvURL** |**URL-адрес хранилища ключей Hello** |https://contosokeyvault.vault.azure.net/ |
| **$spName** |**Имя субъекта-службы** |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **$spSecret** |**Секрет субъекта-службы** |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **$credName** |**Имя учетных данных**: интеграция с хранилищем ключей AZURE создает учетные данные в SQL Server, позволяя hello ВМ toohave доступа toohello хранилища ключей. Выберите имя для этих учетных данных. |mycred1 |
| **$vmName** |**Имя виртуальной машины**: hello имя ранее созданной виртуальной Машины SQL. |myvmname |
| **$serviceName** |**Имя службы**: hello имя облачной службы, связанный с hello SQL виртуальной Машины. |mycloudservicename |

### <a name="enable-akv-integration-with-powershell"></a>Включение интеграции AKV с помощью PowerShell
Hello **New AzureVMSqlServerKeyVaultCredentialConfig** командлет создает объект конфигурации для функции hello интеграция хранилища ключей Azure. Hello **набор AzureVMSqlServerExtension** настраивает такая интеграция с hello **KeyVaultCredentialSettings** параметра. Здравствуйте, следующие шаги Показать как toouse этих команд.

1. В Azure PowerShell сначала настройте входные параметры hello особые значения как описано в предыдущих подразделах этого раздела hello. Hello следующий сценарий — пример.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Затем используйте следующие hello скрипт tooconfigure и обеспечить интеграцию с хранилищем ключей AZURE.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Hello расширения SQL IaaS агента будут обновлены hello виртуальной Машине SQL новая конфигурация.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

