---
title: "aaaEncrypt дисков на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Как tooencrypt виртуальных дисков на виртуальной Машине Linux для усиления безопасности с помощью hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Как tooencrypt виртуальных дисков на виртуальной Машине Linux
Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать. Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure. Вы будете управлять этими криптографическими ключами и проводить аудит их использования. В этой статье указаны как tooencrypt виртуальных дисков на виртуальной Машине Linux с помощью hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Быстрые команды
Если вам требуется tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовый команд tooencrypt виртуальным дискам на виртуальной Машине. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#overview-of-disk-encryption).

Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *myKey* и *myVM*.

Во-первых, включение hello поставщика хранилища ключей Azure в подписке Azure с [Регистрация поставщика az](/cli/azure/provider#register) и создайте группу ресурсов с [Создание группы az](/cli/azure/group#create). Hello следующий пример создает имя группы ресурсов *myResourceGroup* в hello *eastus* расположение:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Создание хранилища ключей Azure с [az keyvault создать](/cli/azure/keyvault#create) и включите hello хранилища ключей для шифрования диска. Укажите уникальное имя Key Vault для параметра *keyvault_name*, выполнив следующую команду:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Создайте криптографический ключ в своем Key Vault, выполнив команду [az keyvault key create](/cli/azure/keyvault/key#create). Hello следующий пример создает раздел с именем *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Создайте субъект-службу с помощью Azure Active Directory, выполнив команду [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). дескрипторы основной службы Hello hello проверки подлинности и обмена ключей шифрования из хранилища ключей. Следующий пример Hello считывает hello значениями hello участника-службы, идентификатор и пароль для использования в командах более поздней версии:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

пароль Hello выводится только при создании hello участника-службы. При необходимости, просмотр и запись hello пароль (`echo $sp_password`). Вы можете вывести список субъектов-служб, выполнив команду [az ad sp list](/cli/azure/ad/sp#list), и просмотреть дополнительные сведения о конкретном субъекте-службе, выполнив [az ad sp show](/cli/azure/ad/sp#show).

Задайте разрешение для Key Vault, выполнив команду [az keyvault set-policy](/cli/azure/keyvault#set-policy). В следующем примере hello hello идентификатор участника службы предоставляются из hello предшествующий команды:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Создайте виртуальною машину, выполнив команду [az vm create](/cli/azure/vm#create), и подключите диск данных емкостью 5 ГБ. Только некоторые образы Marketplace поддерживают шифрование диска. Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью **CentOS 7.2n** изображения:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` показано в выходные данные hello hello предшествующий команды. Создать раздел и файловой системы, а затем подключить диск данных hello. Дополнительные сведения см. в разделе [подключение нового диска ВМ Linux toomount hello tooa](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Закройте сеанс SSH.

Зашифруйте виртуальную машину, выполнив команду [az vm encryption enable](/cli/azure/vm/encryption#enable). Hello следующий пример использует hello `$sp_id` и `$sp_password` переменные из предыдущего hello `ad sp create-for-rbac` команды:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Потребуется некоторое время для toocomplete процесс шифрования диска hello. Мониторинг состояния hello hello процесса с [Показать шифрования ВМ az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Здравствуйте, показано состояние **EncryptionInProgress**. Подождать, пока состояние hello hello ОС диска отчетов **VMRestartPending**, затем перезапустите ВМ с [перезапуска ВМ az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Hello процесс шифрования диска финализируется во время процесса загрузки hello, поэтому Подождите несколько минут перед проверкой hello состояние шифрования с **Показать шифрования ВМ az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

состояние Hello теперь следует сообщать диска hello операционной системы и диска данных как **шифрование**.

## <a name="overview-of-disk-encryption"></a>Общие сведения о шифровании дисков
Виртуальные диски на виртуальных машинах Linux шифруются с помощью [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). В Azure за шифрование виртуальных дисков плата не взимается. Ключи шифрования хранятся в хранилище ключей Azure с помощью защиты программного обеспечения, или можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM) сертифицированные tooFIPS стандартов 140-2 уровня 2. Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования. Эти ключи шифрования, используемые tooencrypt и расшифровки tooyour подключенных виртуальных дисков виртуальной Машины. Субъект-служба Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.

Hello процесс шифрования виртуальной Машины выглядит следующим образом:

1. Создайте криптографический ключ в хранилище ключей Azure.
2. Настройте hello криптографических ключей toobe может использоваться для шифрования дисков.
3. tooread hello криптографический ключ из хранилища ключей Azure, hello создания участника службы Azure Active Directory с соответствующими разрешениями hello.
4. Выдавать виртуальных дисков, указание hello участника-службы Azure Active Directory и использовать соответствующие криптографических ключей toobe tooencrypt команда hello.
5. запросы основной службы Azure Active Directory Hello hello требуется криптографический ключ из хранилища ключей Azure.
6. виртуальные диски Hello шифруются с помощью предоставленных hello криптографический ключ.

## <a name="encryption-process"></a>Процесс шифрования
Шифрование диска основывается на hello следующие дополнительные компоненты:

* **Хранилище ключей Azure** -использовать toosafeguard криптографических ключей и используемая для шифрования и расшифровки диска hello.
  * При наличии можно воспользоваться имеющимся хранилищем ключей Azure. У вас toodedicate дисков tooencrypting хранилища ключей.
  * tooseparate административные границы и видимость ключа, можно создать выделенный хранилища ключей.
* **Azure Active Directory** - дескрипторы hello безопасный обмен необходимых ключей шифрования и проверки подлинности для запрошенного действия.
  * Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.
  * Субъект-служба Hello предоставляет toorequest безопасный механизм и выдаваться hello соответствующих криптографических ключей. При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.

## <a name="requirements-and-limitations"></a>Требования и ограничения
Поддерживаемые сценарии и требования для шифрования дисков:

* Здравствуйте, следуя Linux server SKU - Ubuntu, CentOS, SUSE и SUSE Linux Enterprise Server (SLES) и Red Hat Enterprise Linux.
* Все ресурсы (например, хранилище ключей, учетной записи хранилища и виртуальных Машин), должны быть в hello и подписка одного региона Azure.
* стандартные серии A, D, DS, G и GS виртуальных машин.

Шифрование диска не поддерживается в настоящее время в hello следующие сценарии:

* виртуальные машины уровня "Базовый";
* Виртуальные машины, созданные с помощью hello классической модели развертывания.
* отключение шифрования дисков ОС на виртуальных машинах Linux;
* Обновление криптографических ключей hello на Виртуальной машине уже зашифрованный Linux.

## <a name="create-azure-key-vault-and-keys"></a>Создание Azure Key Vault и ключей
Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *myKey* и *myVM*.

Hello первым шагом является toocreate toostore хранилище ключей Azure криптографические ключи. Хранилище ключей Azure можно хранить ключи секретные данные, или пароли, которые позволяют вам toosecurely их реализации в приложениях и службах. Для шифрования диска используйте хранилище ключей toostore криптографический ключ, который будет использоваться tooencrypt или расшифровать виртуальных дисков.

Включение hello поставщика хранилища ключей Azure в подписке Azure с [Регистрация поставщика az](/cli/azure/provider#register) и создайте группу ресурсов с [Создание группы az](/cli/azure/group#create). Hello следующий пример создает имя группы ресурсов *myResourceGroup* в hello `eastus` расположение:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Hello хранилище ключей Azure содержащего hello криптографических ключей и связанные вычислений, ресурсы, такие как хранилища и hello самой ВМ должны находиться в hello в одном регионе. Создание хранилища ключей Azure с [az keyvault создать](/cli/azure/keyvault#create) и включите hello хранилища ключей для шифрования диска. Укажите уникальное имя Key Vault для параметра *keyvault_name*, выполнив следующую команду:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM. Для использования HSM требуется хранилище ключей уровня "Премиум". Нет дополнительных затрат toocreating premium, хранилище ключей, а не стандартный хранилища ключей, которое хранит программно защищенных ключей. добавить premium хранилище ключей в предшествующих шаг hello toocreate `--sku Premium` toohello команды. Hello следующий пример использует программно защищенных ключей создания стандартных хранилища ключей.

Для обеих моделей защиты hello платформы Azure должен toobe предоставленные криптографические ключи доступа toorequest hello hello виртуальной Машины загружается toodecrypt hello виртуальных дисков. Создайте криптографический ключ в своем Key Vault, выполнив команду [az keyvault key create](/cli/azure/keyvault/key#create). Hello следующий пример создает раздел с именем *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Создать участника-службы Azure Active Directory hello
При виртуальные диски зашифрованные или расшифрованные, необходимо указать hello toohandle проверки подлинности учетной записи и обмена ключей шифрования из хранилища ключей. Эта учетная запись субъекта-службы Azure Active Directory, позволяет toorequest платформы Azure hello hello соответствующие криптографических ключей от имени hello виртуальной Машины. Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.

Создайте субъект-службу с помощью Azure Active Directory, выполнив команду [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). Следующий пример Hello считывает hello значениями hello участника-службы, идентификатор и пароль для использования в командах более поздней версии:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

пароль Hello отображается только при создании участника службы hello. При необходимости, просмотр и запись hello пароль (`echo $sp_password`). Вы можете вывести список субъектов-служб, выполнив команду [az ad sp list](/cli/azure/ad/sp#list), и просмотреть дополнительные сведения о конкретном субъекте-службе, выполнив [az ad sp show](/cli/azure/ad/sp#show).

toosuccessfully шифрования или расшифровки виртуальные диски, разрешения на hello криптографический ключ, хранящийся в хранилище ключей должно быть основной tooread ключей hello hello Azure Active Directory набора toopermit службы. Задайте разрешение для Key Vault, выполнив команду [az keyvault set-policy](/cli/azure/keyvault#set-policy). В следующем примере hello hello идентификатор участника службы предоставляются из hello предшествующий команды:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Создание виртуальной машины
tooactually шифрования некоторых виртуальных дисков, позволяет создать виртуальную Машину и добавьте диск данных. Создание виртуальной Машины tooencrypt с [создания виртуальной машины az](/cli/azure/vm#create) и присоединить диск данных 5 ГБ. Только некоторые образы Marketplace поддерживают шифрование диска. Hello следующий пример создает Виртуальную машину с именем *myVM* с помощью **CentOS 7.2n** изображения:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` показано в выходные данные hello hello предшествующий команды. Создать раздел и файловой системы, а затем подключить диск данных hello. Дополнительные сведения см. в разделе [подключение нового диска ВМ Linux toomount hello tooa](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Закройте сеанс SSH.


## <a name="encrypt-virtual-machine"></a>Шифрование виртуальной машины
tooencrypt hello виртуальные диски, можно объединить все предыдущие компоненты hello:

1. Укажите hello субъекта-службы Azure Active Directory и пароль.
2. Укажите метаданные hello toostore hello хранилища ключей для зашифрованных дисков.
3. Укажите toouse hello ключи шифрования для hello фактического шифрования и расшифровки.
4. Укажите, следует ли tooencrypt hello ОС диска, диски с данными hello или все.

Зашифруйте виртуальную машину, выполнив команду [az vm encryption enable](/cli/azure/vm/encryption#enable). Hello следующий пример использует hello `$sp_id` и `$sp_password` переменные из предыдущего hello `ad sp create-for-rbac` команды:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Потребуется некоторое время для toocomplete процесс шифрования диска hello. Мониторинг состояния hello hello процесса с [Показать шифрования ВМ az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hello выходные данные, аналогичные toohello следовать примере усеченные:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Подождать, пока состояние hello hello ОС диска отчетов **VMRestartPending**, затем перезапустите ВМ с [перезапуска ВМ az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Hello процесс шифрования диска финализируется во время процесса загрузки hello, поэтому Подождите несколько минут перед проверкой hello состояние шифрования с **Показать шифрования ВМ az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

состояние Hello теперь следует сообщать диска hello операционной системы и диска данных как **шифрование**.


## <a name="add-additional-data-disks"></a>Добавление дополнительных дисков данных
Зашифрованное диски с данными можно позднее добавить дополнительные виртуальные диски tooyour ВМ и шифровать также. Например позволяет добавить второй tooyour виртуальный диск виртуальной Машины следующим образом:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Повторно запустите виртуальные диски tooencrypt команда hello hello следующим образом:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения об управлении хранилищем ключей Azure, а также об удалении криптографических ключей и хранилищ см. в статье [Управление хранилищем ключей с помощью интерфейса командной строки](../../key-vault/key-vault-manage-with-cli2.md).
* Дополнительные сведения о шифровании диска, такие как подготовка зашифрованный пользовательский ВМ tooupload tooAzure, в разделе [шифрование диска Azure](../../security/azure-security-disk-encryption.md).
