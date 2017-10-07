---
title: "tooFreeBSD aaaIntroduction в Azure | Документы Microsoft"
description: "Узнайте о том, как использовать виртуальные машины FreeBSD в Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>TooFreeBSD введение в Azure
В этом разделе представлен обзор запуска виртуальной машины FreeBSD в Azure.

## <a name="overview"></a>Обзор
FreeBSD для Microsoft Azure — Дополнительно операционной системы используется toopower современных серверов, настольных компьютеров и внедренные платформы.

Корпорация Майкрософт предоставление FreeBSD образы в Azure с hello [гостевой агент виртуальной Машины Azure](https://github.com/Azure/WALinuxAgent/) предварительно настроен. В настоящее время hello следующие версии FreeBSD предлагается как изображения корпорацией Майкрософт:

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

агент Hello отвечает за обмен данными между hello FreeBSD ВМ и hello Azure fabric для операции, такие как подготовка hello виртуальной Машины на первом использовании (имя пользователя, пароль или ключ SSH, имя узла, т. д.) и включение функций для выборочного расширения виртуальной Машины.

Как и для будущих версий FreeBSD стратегии hello toostay текущего и сделать hello последних выпусках доступных вскоре после их публикации hello FreeBSD выпуска инженеров.

## <a name="deploying-a-freebsd-virtual-machine"></a>Развертывание виртуальной машины FreeBSD
Развертывание виртуальной машины FreeBSD представляет собой простой процесс, с помощью образа из hello Azure Marketplace из hello портала Azure:

- [10.3 FreeBSD на hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 FreeBSD на hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Создайте виртуальную машину FreeBSD с помощью Azure CLI 2.0 в FreeBSD.
Сначала необходимо tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) хотя следующую команду на компьютере FreeBSD.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Если bash не установлены на компьютере FreeBSD, выполните следующую команду перед установкой hello. 

```bash
sudo pkg install bash
```

Если python не установлены на компьютере FreeBSD, выполните следующие команды перед установкой hello. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Во время установки hello, будет предложено `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. При выборе варианта `y` и введите `/etc/rc.conf` как `a path tooan rc file tooupdate`, может отвечать hello проблема `ERROR: [Errno 13] Permission denied`. tooresolve эту проблему, следует предоставить hello записи справа toocurrent пользователя по файлу hello `etc/rc.conf`.

Теперь можно войти в Azure и создать виртуальную машину FreeBSD. Ниже приведен пример toocreate 11.0 FreeBSD виртуальной Машины. Можно также добавить параметр hello `--public-ip-address-dns-name` глобально уникальное имя DNS для только что созданный общедоступный IP-адрес. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

Затем вы можете войти tooyour FreeBSD ВМ через hello IP-адрес, печатаются в hello выше выходных данных для развертывания. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Расширения виртуальной машины для FreeBSD
Ниже приведены поддерживаемые во FreeBSD расширения виртуальной машины.

### <a name="vmaccess"></a>VMAccess
Hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) расширения можно:

* Сброс пароля hello hello исходного пользователя sudo.
* Создайте нового пользователя sudo задан пароль hello.
* Задать ключ hello общедоступного узла с заданным ключом hello.
* Сброс ключа общедоступного узла hello, указанные во время подготовки, если не указан ключ hello узла виртуальной Машины.
* Откройте порт SSH hello (22) и восстановления hello sshd_config, если reset_ssh tootrue.
* Удаление существующего пользователя hello.
* проверка дисков;
* восстановление добавленного диска.

### <a name="customscript"></a>CustomScript
Hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) расширения можно:

* Если указано, загрузите hello пользовательские скрипты из хранилища Azure или открытый внешнего хранилища (например, GitHub).
* Запустите сценарий точки входа hello.
* поддержка встроенных команд;
* автоматическое преобразование символа новой строки в стиле Windows в сценариях оболочки и Python;
* автоматическое удаление спецификации в сценариях оболочки и Python;
* защита конфиденциальных данных в commandToExecute.

> [!NOTE]
> В настоящий момент виртуальная машина FreeBSD поддерживает только CustomScript версии 1.x.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Аутентификация: имена пользователей, пароли и ключи SSH
При создании FreeBSD виртуальной машины с помощью hello портал Azure, необходимо указать имя пользователя, пароль или открытый ключ SSH.
Имена пользователей для развертывания виртуальной машины в Azure FreeBSD не должны совпадать с именами системных учетных записей (UID < 100) уже существует в виртуальной машине hello (например, «root»).
В настоящее время поддерживается только hello RSA SSH-ключа. Многострочный ключ SSH должен начинаться с `---- BEGIN SSH2 PUBLIC KEY ----` и заканчиваться `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Получение привилегий суперпользователя
Hello учетная запись пользователя, который указывается в процессе развертывания экземпляр виртуальной машины в Azure является привилегированной учетной записи. Hello пакет sudo установлена в hello опубликованных FreeBSD изображения.
После выполнен вход с этой учетной записью пользователя, команды запускаются как корень, используя синтаксис команды hello.

```
$ sudo <COMMAND>
```

При необходимости можно получить доступ к оболочке root с помощью команды `sudo -s`.

## <a name="known-issues"></a>Известные проблемы
Hello [гостевой агент виртуальной Машины Azure](https://github.com/Azure/WALinuxAgent/) версии 2.2.2 [известная проблема] (https://github.com/Azure/WALinuxAgent/pull/517), вызывает сбой подготовки hello для FreeBSD виртуальной Машины в Azure. Hello исправление было захвачено [гостевой агент виртуальной Машины Azure](https://github.com/Azure/WALinuxAgent/) версии 2.2.3 и более поздние версии. 

## <a name="next-steps"></a>Дальнейшие действия
* Go слишком[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD виртуальной Машины.
* Следует toobring собственные tooAzure FreeBSD ссылаться слишком[Создание и отправка виртуального жесткого диска FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).
