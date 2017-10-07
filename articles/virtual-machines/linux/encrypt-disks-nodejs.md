---
title: "aaaEncrypt дисков на виртуальной Машине Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Как hello tooencrypt дисков на виртуальной Машине Linux с помощью Azure CLI 1.0 и модели развертывания диспетчера ресурсов hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI 1.0
Для улучшения уровня безопасности и соответствия требованиям виртуальной машины содержание виртуальных дисков в Azure можно зашифровать при хранении. Диски можно зашифровать с использованием криптографических ключей, защищенных в хранилище ключей Azure. Вы будете управлять этими криптографическими ключами и проводить аудит их использования. В этой статье указаны как hello tooencrypt виртуальных дисков на виртуальной Машине Linux с помощью Azure CLI 1.0 и модели развертывания диспетчера ресурсов hello.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="quick-commands"></a>Быстрые команды
Если вам требуется tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовый команд tooencrypt виртуальным дискам на виртуальной Машине. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#overview-of-disk-encryption).

Требуется hello [последние Azure CLI 1.0](../../xplat-cli-install.md) установлен и вход с помощью режима диспетчера ресурсов hello следующим образом:

```azurecli
azure config mode arm
```

В hello следующих примерах замените примеры имен параметров собственные значения. Используемые имена параметров: `myResourceGroup`, `myKeyVault` и `myVM`.

Во-первых включите hello поставщика хранилища ключей Azure в подписке Azure и создайте группу ресурсов. Hello следующий пример создает имя группы ресурсов `myResourceGroup` в hello `WestUS` расположение:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Создайте хранилище ключей Azure. Hello следующий пример создает хранилище ключей с именем `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Создайте криптографический ключ в своем хранилище ключей и включите его для шифрования дисков. Hello следующий пример создает раздел с именем `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Создайте конечную точку с помощью Azure Active Directory для управления проверкой подлинности hello и обмен ключей шифрования из хранилища ключей. Hello `--home-page` и `--identifier-uris` toobe фактическое маршрутизируемый адрес не обязательно. Для hello высокого уровня безопасности секреты клиента можно использовать вместо паролей. Hello Azure CLI в настоящее время не удается создать секреты клиента. Секреты клиента может быть создана только в hello портал Azure. Hello следующий пример создает конечную точку Azure Active Directory с именем `myAADApp` и использует пароль по `myPassword`. Укажите собственный пароль следующим образом:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Примечание hello `applicationId` показано в выходных данных hello из предшествующих команда hello. Этот идентификатор приложения используется в hello следующие шаги:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Добавление существующей виртуальной Машины tooan диска данных. Hello следующий пример добавляет tooa диска данных виртуальной Машины с именем `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Просмотрите сведения о hello созданный ключа хранилища ключей и hello. Требуется hello идентификатор ключа хранилища, URI и ключ URL-адреса на заключительном этапе hello. Hello следующий пример просматривает hello сведения для хранилища ключей с именем `myKeyVault` и ключ с именем `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Зашифруйте диски следующим образом, введя собственные имена параметров в следующих расположениях:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello Azure CLI не предоставляет подробные ошибки во время процесса шифрования hello. Дополнительные сведения об устранении неполадок см. в файле `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Как hello предшествующий команда имеет много переменных и не может получить много указание как toowhy hello завершилось неудачно, пример полностью команда будет выглядеть следующим:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Наконец, просмотрите состояние шифрования hello снова tooconfirm, что теперь были зашифрованы виртуальных дисков. Hello следующий пример проверяет hello состояние виртуальной машины с именем `myVM` в hello `myResourceGroup` группа ресурсов:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Общие сведения о шифровании дисков
Виртуальные диски на виртуальных машинах Linux шифруются с помощью [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). В Azure за шифрование виртуальных дисков плата не взимается. Ключи шифрования хранятся в хранилище ключей Azure с помощью защиты программного обеспечения, или можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM) сертифицированные tooFIPS стандартов 140-2 уровня 2. Вы сохраняете контроль над этими криптографическими ключами и можете проводить аудит их использования. Эти ключи шифрования, используемые tooencrypt и расшифровки tooyour подключенных виртуальных дисков виртуальной Машины. Конечная точка Azure Active Directory предоставляет безопасный механизм для выдачи этих криптографических ключей при включении и отключении виртуальных машин.

Hello процесс шифрования виртуальной Машины выглядит следующим образом:

1. Создайте криптографический ключ в хранилище ключей Azure.
2. Настройте hello криптографических ключей toobe может использоваться для шифрования дисков.
3. tooread hello криптографический ключ из хранилища ключей Azure, hello создается конечная точка, с помощью Azure Active Directory с соответствующими разрешениями hello.
4. Выдавать виртуальных дисков, указание конечной точки hello Azure Active Directory и использовать соответствующие криптографических ключей toobe tooencrypt команда hello.
5. Конечная точка Azure Active Directory Hello запросы hello требуется криптографический ключ из хранилища ключей Azure.
6. виртуальные диски Hello шифруются с помощью предоставленных hello криптографический ключ.

## <a name="supporting-services-and-encryption-process"></a>Вспомогательные службы и процесс шифрования
Шифрование диска основывается на hello следующие дополнительные компоненты:

* **Хранилище ключей Azure** -использовать toosafeguard криптографических ключей и используемая для шифрования и расшифровки диска hello.
  * При наличии можно воспользоваться имеющимся хранилищем ключей Azure. У вас toodedicate дисков tooencrypting хранилища ключей.
  * tooseparate административные границы и видимость ключа, можно создать выделенный хранилища ключей.
* **Azure Active Directory** - дескрипторы hello безопасный обмен необходимых ключей шифрования и проверки подлинности для запрошенного действия.
  * Как правило, для размещения приложения можно использовать имеющийся экземпляр Azure Active Directory.
  * приложение Hello несколько конечную точку для hello хранилища ключей и toorequest службы виртуальной машины и получить выданный hello соответствующих криптографических ключей. При этом вы не разрабатываете фактическое приложение, которое интегрируется с Azure Active Directory.

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

## <a name="create-hello-azure-key-vault-and-keys"></a>Создание hello хранилище ключей Azure и ключи
toocomplete hello других разделах этого руководства, необходимо hello [последние Azure CLI 1.0](../../xplat-cli-install.md) установлен и вход с помощью режима диспетчера ресурсов hello следующим образом:

```azurecli
azure config mode arm
```

В примерах команд hello замените все параметры в примере с именами, расположение и значения ключа. Hello следующих примерах используется соглашение о `myResourceGroup`, `myKeyVault`, `myAADApp`и т. д.

Hello первым шагом является toocreate toostore хранилище ключей Azure криптографические ключи. Хранилище ключей Azure можно хранить ключи секретные данные, или пароли, которые позволяют вам toosecurely их реализации в приложениях и службах. Для шифрования диска используйте хранилище ключей toostore криптографический ключ, который будет использоваться tooencrypt или расшифровать виртуальных дисков.

Включите hello поставщика хранилища ключей Azure в подписке Azure, а затем создайте группу ресурсов. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `WestUS` расположение:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Hello хранилище ключей Azure содержащего hello криптографических ключей и связанные вычислений, ресурсы, такие как хранилища и hello самой ВМ должны находиться в hello в одном регионе. Hello следующий пример создает хранилище ключей Azure с именем `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Хранить криптографические ключи можно с помощью программного обеспечения или защиты HSM. Для использования HSM требуется хранилище ключей уровня "Премиум". Нет дополнительных затрат toocreating premium, хранилище ключей, а не стандартный хранилища ключей, которое хранит программно защищенных ключей. добавить premium хранилище ключей в предшествующих шаг hello toocreate `--sku Premium` toohello команды. Hello следующий пример использует программно защищенных ключей создания стандартных хранилища ключей.

Для обеих моделей защиты hello платформы Azure должен toobe предоставленные криптографические ключи доступа toorequest hello hello виртуальной Машины загружается toodecrypt hello виртуальных дисков. Создайте ключ шифрования в своем хранилище ключей, а затем включите его для шифрования виртуальных дисков. Hello следующий пример создает раздел с именем `myKey` и затем активирует его для шифрования диска:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Создание приложения hello Azure Active Directory
При виртуальные диски зашифрованные или расшифрованные, вы используете проверку подлинности конечной точки toohandle hello и обмена ключей шифрования из хранилища ключей. Эта конечная точка приложения Azure Active Directory, позволяет toorequest платформы Azure hello hello соответствующие криптографических ключей от имени hello виртуальной Машины. Экземпляр Azure Active Directory по умолчанию доступен в вашей подписке, хотя во многих организациях есть выделенные каталоги Azure Active Directory.

Здравствуйте, как завершенное приложение Azure Active Directory не создается, `--home-page` и `--identifier-uris` параметров в следующий пример hello не обязательно toobe фактическое маршрутизируемый адрес. Hello в примере также задает секрет, основанный на пароле, а не генерации ключей из внутри hello портал Azure. В настоящее время невозможно выполнить создание ключей из hello Azure CLI.

Создайте приложение Azure Active Directory. Hello в примере создается приложение с именем `myAADApp` и использует пароль по `myPassword`. Укажите собственный пароль следующим образом:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Запишите hello `applicationId` возвращается в выходных данных hello из предшествующих команда hello. Этот идентификатор приложения используется в некоторых hello, оставшиеся шаги. Создайте имя участника-службы (SPN), чтобы приложение hello доступно в вашей среде. toosuccessfully шифрования или расшифровки виртуальные диски, разрешения на hello криптографический ключ, хранящийся в хранилище ключей должно быть tooread ключей hello hello Azure Active Directory набора toopermit приложения.

Создайте hello имени участника-службы и задайте соответствующие разрешения hello следующим образом:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Добавление виртуального диска и просмотр состояния шифрования
tooactually шифрования некоторых виртуальных дисков, позволяет добавить tooan диск существующей виртуальной Машины. Добавьте tooan диск 5 ГБ данных, существующей виртуальной Машины следующим образом:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

виртуальные диски Hello в настоящее время не шифруются. Просмотрите текущее состояние шифрования hello вашей виртуальной машины следующим образом:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Шифрование виртуальных дисков
toonow шифрования hello виртуальные диски, объедините все предыдущие компоненты hello:

1. Укажите приложение hello Azure Active Directory и пароль.
2. Укажите метаданные hello toostore hello хранилища ключей для зашифрованных дисков.
3. Укажите toouse hello ключи шифрования для hello фактического шифрования и расшифровки.
4. Укажите, следует ли tooencrypt hello ОС диска, диски с данными hello или все.

Позволяет просмотреть сведения о hello ключа хранилища ключей Azure и hello, созданный, hello идентификатор ключа хранилища, URI, а затем ключа URL-адрес на заключительном этапе hello:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Шифрование виртуальных дисков с выходными данными hello hello `azure keyvault show` и `azure keyvault key show` команд следующим образом:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Как hello предыдущая команда имеет много переменных, hello следующий пример является полностью команда hello для ссылки:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello Azure CLI не предоставляет подробные ошибки во время процесса шифрования hello. Дополнительные сведения об устранении неполадок, просмотрите `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` на hello виртуальной Машины, шифруются.

Наконец, позволяет просмотреть состояние шифрования hello снова tooconfirm, что теперь были зашифрованы виртуальных дисков:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Добавление дополнительных дисков данных
Зашифрованное диски с данными можно позднее добавить дополнительные виртуальные диски tooyour ВМ и шифровать также. При запуске hello `azure vm enable-disk-encryption` command, версия последовательности hello приращение, с помощью hello `--sequence-version` параметра. Этот параметр версии последовательности позволяет tooperform последовательные операции с hello одной виртуальной Машины.

Например позволяет добавить второй tooyour виртуальный диск виртуальной Машины следующим образом:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Повторно запустите hello команда tooencrypt hello виртуальные диски, это время добавления hello `--sequence-version` параметр и hello значение приращения от наших первого запуска следующим образом:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения об управлении хранилищем ключей Azure, а также об удалении криптографических ключей и хранилищ см. в статье [Управление хранилищем ключей с помощью интерфейса командной строки](../../key-vault/key-vault-manage-with-cli2.md).
* Дополнительные сведения о шифровании диска, такие как подготовка зашифрованный пользовательский ВМ tooupload tooAzure, в разделе [шифрование диска Azure](../../security/azure-security-disk-encryption.md).
