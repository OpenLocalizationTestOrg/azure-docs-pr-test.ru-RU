---
title: "SSH-подключения aaaTroubleshoot выдает tooan виртуальной Машины Azure | Документы Microsoft"
description: "Как tootroubleshoot проблемы, например, «сбоем подключения SSH» или «SSH-подключение отклонено» для виртуальной Машины Azure под управлением Linux."
keywords: "отклонение SSH-подключения, ошибка SSH, Azure SSH, ошибка SSH-подключения"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Устранение неполадок подключения SSH tooan виртуальной Машине Linux Azure, происходит сбой, ошибки, или отклонен
Существует несколько причин, возникнут ошибки Secure Shell (SSH), ошибками соединения SSH, или SSH отклонено, при попытке tooconnect tooa Linux виртуальной машины (VM). Эта статья поможет вам найти и правильный hello проблем. Можно использовать для Linux tootroubleshoot hello портал Azure, Azure CLI или расширение доступа виртуальной Машины и решения проблем с подключением.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](http://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](http://azure.microsoft.com/support/options/) и выберите **получение поддержки**. Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Действия по устранению неполадок
После каждого действия по устранению неполадок выполните повторное подключение toohello виртуальной Машины.

1. Сброс конфигурации SSH hello.
2. Сбросьте учетные данные пользователя hello hello.
3. Проверьте hello [сетевой группы безопасности](../../virtual-network/virtual-networks-nsg.md) правила разрешают трафик SSH.
   * Убедитесь, что правило группы безопасности сети существует toopermit SSH трафика (по умолчанию, TCP-порт 22).
   * Нельзя использовать перенаправление и сопоставление портов, не используя Azure Load Balancer.
4. Проверьте hello [исправности ресурсов для виртуальной Машины](../../resource-health/resource-health-overview.md). 
   * Убедитесь, что hello ВМ отчеты как состоянию работоспособности.
   * Если включена Диагностика загрузки, убедитесь, что hello виртуальной Машины, не предоставляет загрузки ошибки в журналах hello.
5. Перезапустите hello виртуальной Машины.
6. Повторное развертывание hello виртуальной Машины.

Читайте статью дальше, если вам нужны более подробные инструкции или пояснения об исправлении неполадок.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Доступные методы tootroubleshoot SSH с подключением
Можно сбросить учетные данные или с помощью одного из следующих методов hello конфигурации SSH:

* [Портал Azure](#use-the-azure-portal) - нормально, если вам требуется tooquickly Сброс конфигурации SSH hello или ключ SSH, и не hello установлены средства Azure.
* [Azure CLI 2.0](#use-the-azure-cli-20) — Если вы уже находитесь в командной строке hello быстро Сброс конфигурации SSH hello или учетные данные. Можно также использовать hello [Azure CLI 1.0](#use-the-azure-cli-10)
* [Azure расширение VMAccessForLinux](#use-the-vmaccess-extension) — создайте и повторно использовать json определения файлов tooreset hello SSH конфигурации или учетные данные пользователя.

После каждого действия по устранению неполадок повторите попытку подключения tooyour виртуальной Машины. Если вы по-прежнему не удается подключиться, попробуйте hello следующий шаг.

## <a name="use-hello-azure-portal"></a>Использовать hello портал Azure
Hello портал Azure предоставляет быстрый способ tooreset hello SSH конфигурации или учетные данные пользователя без установки средства на локальном компьютере.

Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз toohello **поддержки + Устранение неполадок** , выберите **сброс пароля** как hello в следующем примере:

![Сброс конфигурации SSH или учетные данные в hello портал Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Сброс конфигурации SSH hello
В качестве первого шага, выберите `Reset configuration only` из hello **режим** раскрывающееся меню как hello предшествующий экрана, а затем нажмите кнопку hello **Сброс** кнопки. После завершения этого действия повторите tooaccess ВМ.

### <a name="reset-ssh-credentials-for-a-user"></a>Сброс учетных данных SSH пользователя
Выберите tooreset hello учетные данные существующего пользователя, либо `Reset SSH public key` или `Reset password` из hello **режим** раскрывающееся меню, как предшествующий экрана приветствия. Укажите имя пользователя hello и SSH-ключ или новый пароль, а затем щелкните hello **Сброс** кнопки.

Можно также создать пользователя с правами sudo на hello виртуальной Машины из этого меню. Введите новое имя пользователя и соответствующий пароль или ключ SSH и нажмите кнопку hello **Сброс** кнопки.

## <a name="use-hello-azure-cli-20"></a>Использовать hello Azure CLI 2.0
Если это еще не сделано, установите hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Если создан и загружен пользовательского образа диска Linux, убедитесь, что hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) версии 2.0.5 или более поздней. В виртуальных машинах, созданных с помощью образов из коллекции, это расширение для доступа уже установлено и настроено.

### <a name="reset-ssh-configuration"></a>Сбросьте конфигурацию SSH.
Изначально можно toodefault значения try Сброс hello SSH конфигурации и перезагрузку сервера SSH hello на hello виртуальной Машины. Обратите внимание, что это не изменяет hello имя учетной записи пользователя, пароль или ключей SSH.
Hello следующий пример использует [сброса пользователей виртуальной машины az-ssh](/cli/azure/vm/user#reset-ssh) tooreset конфигурации SSH hello на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Сброс учетных данных SSH пользователя
Hello следующий пример использует [обновление пользователя виртуальной машины az](/cli/azure/vm/user#update) tooreset hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Если используется проверка подлинности ключа SSH, можно сбросить hello SSH-ключ для данного пользователя. Hello следующий пример использует **az ВМ доступа пользователей для linux набор** tooupdate hello SSH ключа, хранимого в `~/.ssh/id_rsa.pub` для hello пользователя с именем `myUsername`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Использовать расширение VMAccess hello
в файле json, определяющий действия toocarry out считывает Hello расширения Access ВМ для Linux. При этом сбрасывается SSHD и ключ SSH или добавляется пользователь. По-прежнему использовать hello Azure CLI toocall hello расширения VMAccess, но можно повторно использовать файлы json hello в нескольких виртуальных машинах при необходимости. Такой подход позволяет toocreate хранилищем файлов json, которые можно вызывать для заданной сценариев.

### <a name="reset-sshd"></a>Сброс SSHD
Создайте файл с именем `settings.json` с hello после содержимого:

```json
{  
    "reset_ssh":"True"
}
```

С помощью hello Azure CLI, затем вызовите hello `VMAccessForLinux` tooreset расширения SSHD подключение, указав json-файла. Hello следующий пример использует [набор расширения ВМ az](/cli/azure/vm/extension#set) tooreset SSHD на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Сброс учетных данных SSH пользователя
Если SSHD toofunction правильно, можно сбросить учетные данные пользователя жабль hello. tooreset hello пароля для пользователя, создайте файл с именем `settings.json`. Hello следующий пример сбрасывает hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`. Введите следующие строки в hello вашей `settings.json` файл, используя свои собственные значения:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Или tooreset Здравствуйте SSH-ключ для пользователя, сначала создайте файл с именем `settings.json`. Hello следующий пример сбрасывает hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Введите следующие строки в hello вашей `settings.json` файл, используя свои собственные значения:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

После создания json-файла используйте hello Azure CLI toocall hello `VMAccessForLinux` расширения tooreset учетные данные пользователя SSH, указав json-файла. Hello следующий пример сбрасывает учетных данных на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Использовать hello Azure CLI 1.0
Если это еще не сделано, [Установка hello Azure CLI 1.0 и подключение tooyour подписки Azure](../../cli-install-nodejs.md). Убедитесь, что используется режим Resource Manager следующим образом:

```azurecli
azure config mode arm
```

Если создан и загружен пользовательского образа диска Linux, убедитесь, что hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) версии 2.0.5 или более поздней. В виртуальных машинах, созданных с помощью образов из коллекции, это расширение для доступа уже установлено и настроено.

### <a name="reset-ssh-configuration"></a>Сбросьте конфигурацию SSH.
неправильно сама конфигурация SSHD Hello, или произошла ошибка службы hello. Вы можете сбросить SSHD toomake убедиться, что конфигурация SSH hello сам является допустимой. Сброс SSHD должно быть hello устранения этой проблемы сначала выполнить.

Hello следующий пример сбрасывает SSHD на виртуальной Машине с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`. Используйте собственные имена для виртуальной машины и группы ресурсов следующим образом:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Сброс учетных данных SSH пользователя
Если SSHD toofunction правильно, вы можете сбросить пароль hello жабль пользователя. Hello следующий пример сбрасывает hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Если используется проверка подлинности ключа SSH, можно сбросить hello SSH-ключ для данного пользователя. Следующий пример обновляет Hello hello SSH-ключ, хранящийся в `~/.ssh/id_rsa.pub` для hello пользователя с именем `myUsername`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Перезапуск виртуальной машины
Если вы сбросить hello SSH конфигурации и учетные данные пользователя, или произошла ошибка при этом, попробуйте перезапуска tooaddress ВМ hello основной проблемы вычислений.

### <a name="azure-portal"></a>Портал Azure
toorestart виртуальной Машины с помощью hello Azure портала, выберите hello вашей виртуальной Машины и нажмите кнопку **перезапустите** кнопки как hello в следующем примере:

![Перезапустите виртуальную Машину в hello портал Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Следующий пример перезапускается Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Hello следующий пример использует [перезапуска ВМ az](/cli/azure/vm#restart) toorestart hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Повторное развертывание виртуальной машины
Можно повторно развернуть узел tooanother ВМ в Azure, который может исправить проблемы с базовой сети. Сведения о повторного развертывания виртуальной Машины см. в разделе [повторного развертывания виртуальной машины toonew узла Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> После завершения этой операции эфемерных диске данные будут потеряны и динамических IP-адресов, связанных с виртуальной машиной hello будет обновляться.
> 
> 

### <a name="azure-portal"></a>Портал Azure
tooredeploy виртуальной Машины с помощью hello Azure портала, выберите ВМ и прокрутите вниз toohello **поддержки + Устранение неполадок** раздела. Нажмите кнопку hello **повторно развернуть** кнопки как hello в следующем примере:

![Повторное развертывание виртуальной Машины в hello портал Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Следующий пример повторно развертывает Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Следующий пример использования Hello [повторного развертывания виртуальной машины az](/cli/azure/vm#redeploy) tooredeploy hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`. Используйте свои значения следующим образом:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Виртуальные машины, созданные с помощью hello классической модели развертывания
Повторите эти шаги tooresolve hello наиболее распространенные SSH сбоев подключения для виртуальных машин, которые были созданы с помощью hello классической модели развертывания. После выполнения каждого шага выполните повторное подключение toohello виртуальной Машины.

* Сбросьте удаленный доступ из hello [портал Azure](https://portal.azure.com). На hello портал Azure, выберите виртуальную Машину и щелкните hello **удаленный сброс...**  кнопки.
* Перезапустите hello виртуальной Машины. На hello [портал Azure](https://portal.azure.com), выберите виртуальную Машину и щелкните hello **перезапустите** кнопки.
    
* Повторное развертывание hello ВМ tooa новый узел Azure. Сведения о том, как tooredeploy виртуальной Машины, в разделе [повторного развертывания виртуальной машины toonew узла Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    После завершения этой операции эфемерных диске данные будут потеряны и динамических IP-адресов, связанных с виртуальной машиной hello будет обновляться.
* Следуйте инструкциям в разделе hello [как tooreset пароль или SSH для виртуальных машин под управлением Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) для:
  
  * Hello сброс пароля или ключа SSH.
  * Создайте учетную запись пользователя *sudo*.
  * Сброс конфигурации SSH hello.
* Проверьте работоспособность ресурсов виртуальной Машины hello для выявления проблем с платформой.<br>
     Выберите свою виртуальную машину и прокрутите вниз до раздела **Параметры** > **Проверка работоспособности**.

## <a name="additional-resources"></a>Дополнительные ресурсы
* Если по-прежнему не удается tooSSH tooyour ВМ после Здравствуйте, следующие после выполнения шагов, см. [дополнительные действия по устранению неполадок](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview дополнительных шагов tooresolve проблему.
* Дополнительные сведения об устранении неполадок доступа к приложениям см. в разделе [устранить неполадки доступа tooan приложение, работающее на виртуальной машине Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Дополнительные сведения об устранении неполадок виртуальных машин, которые были созданы с помощью hello классической модели развертывания см. в разделе [как tooreset пароль или SSH для виртуальных машин под управлением Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

