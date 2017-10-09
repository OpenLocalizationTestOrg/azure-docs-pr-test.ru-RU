---
title: "aaaCertificate средств автоматизации Azure | Документы Microsoft"
description: "Сертификаты могут быть безопасно сохранены в службе автоматизации Azure, они могли быть доступны модули Runbook или tooauthenticate конфигурации DSC для Azure и ресурсы сторонних поставщиков.  В этой статье подробно описывается hello сертификатов и как toowork с ними в текстовых и графических разработки."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Сертификация активов в службе автоматизации Azure

Сертификаты могут быть безопасно сохранены в службе автоматизации Azure, чтобы они могли быть доступны модули Runbook или конфигурации DSC с помощью hello **Get AzureRmAutomationRmCertificate** действия для ресурсов диспетчера ресурсов Azure. Это позволяет вам toocreate Runbook и конфигураций DSC, которые используют сертификаты для проверки подлинности или добавляет их tooAzure и сторонних поставщиков ресурсов.

> [!NOTE] 
> Безопасные средства в службе автоматизации Azure включают учетные данные, сертификаты, подключения и зашифрованные переменные. Эти ресурсы шифруются и хранятся в hello автоматизации Azure, используя уникальный ключ, который создается для каждой учетной записи автоматизации. Ключ шифруется главным сертификатом и хранится в службе автоматизации Azure. Перед сохранением безопасного ресурса, hello ключ для учетной записи автоматизации hello расшифровывается с помощью шаблона сертификата hello и затем использовать tooencrypt hello активов.
> 

## <a name="windows-powershell-cmdlets"></a>Командлеты Windows PowerShell

командлеты Hello в следующей таблице hello, используемые toocreate и управлять ресурсами сертификатов автоматизации с помощью Windows PowerShell. Они поставляются как часть hello [модуля Azure PowerShell](../powershell-install-configure.md) доступный для использования в Runbook автоматизации и конфигураций DSC.

|Командлеты|Описание|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Извлекает сведения о toouse сертификата в конфигурации DSC или runbook. Из действия Get-AutomationCertificate можно извлечь только сам сертификат hello.|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Создает сертификат в службе автоматизации Azure.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Удаляет сертификат из службы автоматизации Azure.|Создает сертификат в службе автоматизации Azure.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Задает свойства hello для существующего сертификата, включая Отправка файла сертификата hello и параметр hello пароль для PFX-файла.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Отправка сертификата службы для hello указан облачной службы.|


## <a name="creating-a-new-certificate"></a>Создание нового сертификата

При создании нового сертификата, загруженный CER или PFX файл tooAzure автоматизации. Если пометить hello сертификат как экспортируемый, можно перенести его из хранилища сертификатов службы автоматизации Azure hello. Если он не может быть экспортирован, затем он может использоваться только для подписи в пределах hello runbook или конфигурации DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate новый сертификат с hello портал Azure

1. Из учетной записи автоматизации, нажмите кнопку hello **активы** плитки приветствия tooopen **активы** колонку.
1. Щелкните hello **сертификаты** плитки приветствия tooopen **сертификаты** колонку.
1. Нажмите кнопку **Добавление сертификата** hello верхней части колонки hello.
2. Введите имя для сертификата hello в hello **имя** поле.
2. Нажмите кнопку **выберите файл** под **загрузить файл сертификата** toobrowse файл CER или PFX.  Если выбран PFX-файл, укажите пароль и ли ему должен быть разрешен toobe экспортированы.
1. Нажмите кнопку **создать** toosave hello нового сертификата актива.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate новый сертификат с помощью Windows PowerShell

Hello следующем примере показано, как toocreate новый автоматизации сертификатов и пометить его экспортируемым. Вследствие этого импортируется существующий PFX-файл.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Использование сертификата

Необходимо использовать hello **Get-AutomationCertificate** toouse действия сертификата. Нельзя использовать hello [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) командлета, поскольку он возвращает сведения о ресурсе сертификата hello, а не самого сертификата hello.

### <a name="textual-runbook-sample"></a>Пример текстового Runbook

Привет, следующий пример кода показывает, как tooadd tooa сертификата облачной службы в модуле runbook. В этом образце hello пароль извлекается из зашифрованной переменной автоматизации.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Пример графического Runbook

Добавить **Get-AutomationCertificate** tooa графический runbook, щелкнув сертификат hello в области библиотеки hello графического редактора hello и выбрав **добавить toocanvas**.

![Добавление сертификата toohello холста](media/automation-certificates/automation-certificate-add-to-canvas.png)

Hello следующем рисунке показан пример использование сертификата в графический runbook.  Это hello примера, показанного выше для добавления сертификата tooa облачной службы из текстовой runbook.

![Пример графической разработки ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Дальнейшие действия

- tooperform разработан toolearn больше о работе с ссылки toocontrol hello логический поток действий runbook, см. в разделе [ссылки в графический разработки](automation-graphical-authoring-intro.md#links-and-workflow). 
