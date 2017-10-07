---
title: "aaaInstall и настройки виртуальных машин tooprovision Terraform и другой инфраструктурой в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте Terraform toocreate Azure ресурсы"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Установка и настройка виртуальных машин tooprovision Terraform и другой инфраструктурой в Azure 
В этой статье описываются необходимые шаги tooinstall hello и настройки Terraform tooprovision ресурсов, таких как виртуальные машины в Azure. Вы узнаете, как toocreate и использование Azure учетные данные tooenable Terraform tooprovision облачные ресурсы в безопасном режиме.

HashiCorp Terraform предоставляет простой способ toodefine и развертывание облачной инфраструктуры с помощью языка настраиваемых шаблонов, называемый языком конфигурации HashiCorp (HCL). Этот пользовательский язык [toowrite легко и просто toounderstand](terraform-create-complete-vm.md). Кроме того, с помощью hello `terraform plan` команды, прежде чем зафиксировать их можно визуализировать hello изменения tooyour инфраструктуры. Выполните эти шаги toostart, с помощью Terraform с Azure.

## <a name="install-terraform"></a>Установка Terraform
tooinstall Terraform, [загрузки](https://www.terraform.io/downloads.html) для вашей операционной системы в каталог установки отдельный пакет hello. Hello загружаемый файл содержит один исполняемый файл, для которого следует задавать глобальный путь. Для инструкции о том, как tooset hello путь в Linux и Mac, посетите страницу слишком[веб-страницу](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Для инструкции как tooset hello пути в Windows, посетите страницу слишком[веб-страницу](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify установку, запустите hello `terraform` команды. В качестве выходных данных должен отобразиться список доступных параметров Terraform.

Далее необходимо tooallow Terraform доступа tooyour подписки Azure tooperform подготовку инфраструктуры.

## <a name="set-up-terraform-access-tooazure"></a>Настройка доступа tooAzure Terraform
tooenable Terraform tooprovision ресурсы в Azure, необходимо toocreate две сущности в Azure Active Directory (Azure AD): приложения Azure AD и субъект-служба Azure AD. Затем идентификаторы этих сущностей используются в сценариях Terraform. Субъект-служба — это локальный экземпляр глобального приложения Azure AD. Субъекта-службы позволяет ресурсы tooglobal управления детальные локального доступа.

Существует несколько способов toocreate приложения Azure AD и субъект-служба Azure AD. Hello простым и быстрым способом сегодняшний день является toouse Azure CLI 2.0, который [можно загрузить и установить на Windows, Linux или Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Также можно использовать PowerShell или Azure CLI 1.0 toocreate hello инфраструктуры безопасности. следующие инструкции Hello показывается, как tooconfigure Terraform для Azure с помощью всех этих подходов.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Использование Azure CLI 2.0 (для пользователей Windows, Mac и Linux) 
После загрузки и установки hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), войдите в tooadminister подписки Azure, выполнив следующую команду hello:

```
az login
```

>[!NOTE]
>При использовании hello Китай, Германия Azure или облаков Azure для государственных, необходимо toofirst Настройка toowork hello Azure CLI с помощью данного облака. Это можно сделать, выполнив следующие hello:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Если у вас несколько подписок Azure, подробные сведения об их возвращаемые hello `az login` команды. Набор hello `SUBSCRIPTION_ID` возвращено значение hello toohold переменной среды hello `id` из подписки hello требуется toouse. 

Задать hello подписки требуется toouse для этого сеанса.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

Запрос учетной записи tooget hello hello-идентификатор подписки и значения идентификатора клиента.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Затем создайте отдельные учетные данные для Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

Вы получите значения для параметров appId, password, sp_name и tenant. Запишите hello appId и пароль.

tooconfirm учетные данные (субъекта-службы), откройте новой оболочки и выполните следующие команды hello. Замена hello возвращаемые значения для sp_name и пароль клиента:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Использование PowerShell (для пользователей Windows) 
toouse Windows toowrite компьютер и выполнить вашей Terraform сценарии и toouse PowerShell для задач настройки настройки компьютера с помощью соответствующих средств PowerShell hello. 

1. Установка инструментов PowerShell с помощью инструкции hello в [Установка и настройка Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Загрузка и выполнение hello [azure setup.ps1 скрипт](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) из консоли PowerShell hello.

3. скрипт azure setup.ps1 toorun hello, загрузите и выполните hello `./azure-setup.ps1 setup` команду из консоли PowerShell hello. Затем войдите в tooyour подписки Azure с правами администратора.

4. При появлении запроса укажите имя приложения (произвольная строка, обязательно). При необходимости при появлении запроса введите надежный пароль. Если не указать пароль, то надежный пароль будет создан автоматически с помощью библиотек безопасности .NET.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Использование Azure CLI 1.0 (для пользователей Linux или Mac)
tooget работу с Terraform на компьютеры Linux и компьютерах Mac с помощью Azure CLI 1.0, соответствующие библиотеки hello установки на компьютере.  

1. Установка средств Azure xPlat CLI, следуя указаниям hello [установить CLI Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Загрузите и установите процессор JSON, следуя инструкциям hello [загрузки jq](https://stedolan.github.io/jq/download/).

3. Загрузка и выполнение hello [azure setup.sh скрипт](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash скрипт из консоли hello.

4. скрипт azure setup.sh toorun hello, загрузите и выполните hello `./azure-setup setup` команду из консоли hello. Затем войдите в tooyour подписки Azure с правами администратора.
 
5. При появлении запроса укажите имя приложения (произвольная строка, обязательно). При необходимости при появлении запроса введите надежный пароль. Если не указать пароль, то надежный пароль будет создан автоматически с помощью библиотек безопасности .NET.

Все предыдущие сценарии hello создание основного приложения Azure AD и службы. Участник службы Hello возвращает участника или доступ на уровне владельца на hello подписки. Из-за hello высокий уровень предоставлен доступ следует всегда защищать hello безопасности информации, создаваемой эти скрипты. Запишите все четыре блока сведений о безопасности, предоставленные этими скриптами: appId, password, subscription_id и tenant_id.

## <a name="set-environment-variables"></a>Настройка переменных среды
После создания и настройки участника-службы Azure AD, необходимо toolet Terraform знать hello ИД клиента, идентификатор подписки, идентификатор клиента и секрета toouse клиента. Вы можете сделать это, вставив эти значения в сценарии Terraform, как описано в статье [Создание базовой инфраструктуры в Azure с помощью Terraform](terraform-create-complete-vm.md). Кроме того можно задать следующие переменные среды hello (и тем самым избежать случайно извлечение или учетные данные для управления доступом):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Эти переменные могут использоваться tooset сценарий оболочки этот образец.

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Кроме того при использовании Terraform с Azure в Китае, или либо Azure для государственных или Германии Azure необходимо переменной среды tooset hello соответствующим образом.

## <a name="next-steps"></a>Дальнейшие действия
Вы установили Terraform и настроили учетные данные Azure, так что вы можете начать развертывание инфраструктуры в свою подписку Azure. Далее, узнайте, как слишком[создания инфраструктуры с Terraform](terraform-create-complete-vm.md).
