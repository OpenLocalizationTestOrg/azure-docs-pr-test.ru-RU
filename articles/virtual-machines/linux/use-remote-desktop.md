---
title: "tooa aaaUse удаленного рабочего стола виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить удаленный рабочий стол (xrdp) tooconnect tooa виртуальных Машин Linux в Azure с помощью графических средств"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Установка и настройка удаленного рабочего стола tooconnect tooa виртуальных Машин Linux в Azure
Linux виртуальных машин (ВМ) в Azure обычно осуществляется из командной строки hello, с использованием безопасного shell (SSH) подключения. Когда новый tooLinux или быстрого устранения неполадок при использовании hello использование удаленного рабочего стола может оказаться удобнее. Это статья сведения о том, как tooinstall и настройте рабочего стола ([xfce](https://www.xfce.org)) и удаленного рабочего стола ([xrdp](http://www.xrdp.org)) для ВМ Linux с помощью модели развертывания диспетчера ресурсов hello.


## <a name="prerequisites"></a>Предварительные требования
Для работы с этой статьей требуется существующая виртуальная машина Linux в Azure. Если вам требуется toocreate виртуальной Машины, используйте один из следующих методов hello:

- Hello [Azure CLI 2.0](quick-create-cli.md)
- Hello [портал Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Установка среды рабочего стола на виртуальной машине Linux
На большинстве виртуальных машин Linux в Azure по умолчанию не установлена среда рабочего стола. Управление виртуальными машинами Linux обычно осуществляется через SSH-подключения, а не с помощью рабочего стола. В Linux можно использовать различные среды рабочего стола. В зависимости от используемого рабочей среды он может использовать один too2 ГБ места на диске, занять tooinstall минут 5 too10 и настройте все пакеты необходимых hello.

Hello следующий пример устанавливает облегченного hello [xfce4](https://www.xfce.org/) рабочей среды на Виртуальной машине Ubuntu. Команды для других распределений, незначительно (используйте `yum` tooinstall в Red Hat Enterprise Linux и настроить соответствующие `selinux` правила или используйте `zypper` tooinstall на SUSE, например).

Во-первых, tooyour SSH виртуальной Машины. Hello следующий пример соединяет toohello виртуальной Машины с именем *myvm.westus.cloudapp.azure.com* с именем пользователя hello объекта *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Если вы используете Windows и требуются дополнительные сведения об использовании SSH, см. раздел [как toouse SSH ключей с Windows](ssh-from-windows.md).

Затем установите xfce с помощью `apt` следующим образом:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Установка и настройка сервера удаленных рабочих столов
Теперь, когда вы получите доступ к среде установлен, настройте toolisten служб удаленных рабочих столов для входящих подключений. [xrdp](http://xrdp.org) — это сервер RDP с открытым исходным кодом, доступный в большинстве дистрибутивов Linux и совместимый с xfce. Установите xrdp на виртуальной машине Ubuntu следующим образом:

```bash
sudo apt-get install xrdp
```

Сообщите xrdp какие toouse рабочей среды при запуске сеанса. Настройка xrdp toouse xfce в качестве рабочего стола следующим образом:

```bash
echo xfce4-session >~/.xsession
```

Перезапустите службу xrdp hello для эффекта tootake изменения hello следующим образом:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Настройка пароля локальной учетной записи пользователя
Если вы создали пароль для учетной записи пользователя при создании виртуальной машины, пропустите этот шаг. При использовании проверки подлинности SSH с ключом только и не иметь пароль локальной учетной записи задано, укажите пароль, прежде чем использовать xrdp toolog в tooyour виртуальной Машины. xrdp не принимает ключи SSH для проверки подлинности. Hello следующий пример указывает пароль для учетной записи пользователя hello *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Указание пароля не обновляет вашей SSHD конфигурации toopermit пароль входа, если он в настоящее время не поддерживает. С точки зрения безопасности могут обратиться в tooconnect tooyour ВМ с туннель SSH с использованием проверки подлинности на основе ключей, а затем подключите tooxrdp. Если Да, пропустите следующий шаг по созданию сетевой безопасности группы правил tooallow удаленного рабочего стола трафика hello.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Создание правила группы безопасности сети, разрешающего трафик с удаленного рабочего стола
tooreach трафика удаленного рабочего стола tooallow ВМ Linux, правило группы безопасности сети должен создать toobe разрешает TCP на порт 3389 tooreach ВМ. Дополнительные сведения о правилах групп безопасности сети см. в статье [Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Вы также можете [используйте hello Azure портала toocreate правило группы безопасности сети](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello следующие примеры создают правило группы безопасности сети с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) с именем *myNetworkSecurityGroupRule* слишком*Разрешить* трафика на *tcp* порт *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Подключение к виртуальной машине Linux с помощью клиента удаленного рабочего стола
Откройте ваш локальный клиент удаленного рабочего стола и подключения toohello IP-адрес или DNS-имя виртуальной Машины Linux. Введите hello имя пользователя и пароль для учетной записи пользователя hello на ВМ следующим образом:

![Подключение через клиент удаленного рабочего стола tooxrdp](./media/use-remote-desktop/remote-desktop-client.png)

После проверки подлинности рабочего стола xfce hello загрузки и выглядеть аналогично toohello в следующем примере:

![Среда рабочего стола xfce при подключении через xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Устранение неполадок
Если не удается подключиться tooyour виртуальных Машин Linux с помощью клиента удаленного рабочего стола, используйте `netstat` на вашей виртуальной Машине Linux tooverify, ВМ ожидающей подключений по протоколу RDP следующим образом:

```bash
sudo netstat -plnt | grep rdp
```

Следующий пример показывает Hello hello виртуальная машина прослушивает TCP-порт 3389 должным образом:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Если порт не прослушивается hello xrdp службы, на Виртуальной машине Ubuntu перезапустите службу hello следующим образом:

```bash
sudo service xrdp restart
```

Просмотрите журналы */var/log*Thug на ВМ для выяснения наличия Ubuntu как toowhy hello служба не отвечает. Также можно отслеживать hello syslog во время попытки подключения удаленного рабочего стола tooview ошибок:

```bash
tail -f /var/log/syslog
```

Службы toorestart различными способами и tooreview расположения файла журнала альтернативный, возможно других дистрибутивов Linux, например Red Hat Enterprise Linux и SUSE.

Если не получают ответа в клиенте удаленного рабочего стола и увидеть все события в системном журнале hello, это указывает, что трафика удаленного рабочего стола не может связаться с hello виртуальной Машины. Просмотрите tooensure правила сетевой безопасности группы имеется правило toopermit TCP через порт 3389. Дополнительные сведения см. в статье [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о создании и использовании ключей SSH на виртуальных машинах Linux см. в статье [Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux](mac-create-ssh-keys.md).

Сведения об использовании SSH из Windows см. в разделе [как toouse SSH ключей с Windows](ssh-from-windows.md).

