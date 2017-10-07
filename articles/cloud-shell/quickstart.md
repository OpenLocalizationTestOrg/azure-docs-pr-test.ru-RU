---
title: "Краткое руководство aaaAzure оболочки облака (Предварительная версия) | Документы Microsoft"
description: "Краткое руководство по hello оболочки облако Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Краткое руководство по использованию hello оболочки облако Azure

В этом документе описаны как toouse hello Azure облачной оболочки в hello [портал Azure](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Запуск Cloud Shell
1. Запустите **оболочки облака** hello верхней панели навигации hello портал Azure <br>
![](media/shell-icon.png)
2. Выберите подписку toocreate учетной записи хранилища и Azure общей папки
3. Нажмите кнопку "Создать хранилище".

> [!TIP]
> Вы автоматически проходите проверку подлинности для Azure CLI 2.0 в каждом сеансе.

### <a name="set-your-subscription"></a>Настройка подписки
1. Выведите список подписок, к которым у вас есть доступ: <br>
`az account list`
2. Задайте предпочитаемую подписку: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> Подписка будет сохранена для последующих сеансов в файле `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Создание группы ресурсов
Создайте группу ресурсов в WestUS с именем MyRG: <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Создание виртуальной машины Linux
Создайте виртуальную машину Ubuntu в новой группе ресурсов. Hello Azure CLI 2.0 создаются ключи SSH и hello установки виртуальной Машины с ними. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Здравствуйте, открытый и закрытый ключи, используемые tooauthenticate ВМ, помещаются в `/User/.ssh/id_rsa` и `/User/.ssh/id_rsa.pub` Azure CLI 2.0 по умолчанию. Папка в формате SSH сохраняется в образе размером 5 ГБ, размещенном в подключенной общей папке Azure.

Имя пользователя на этой виртуальной машине будет использоваться в Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH-подключение к виртуальной машине Linux
1. Поиск по имени виртуальной Машины в строке поиска Azure портала hello
2. Щелкните "Подключить" и выполните `ssh username@ipaddress`.

![](media/sshcmd-copy.png)

После установки подключения SSH hello, вы должны увидеть hello Ubuntu приветствия приглашения.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Очистка. 
Удалите группу ресурсов и все ее ресурсы. <br>
Запустите `az group delete -n MyRG`

## <a name="next-steps"></a>Дальнейшие действия
[Сохранение файлов в Azure Cloud Shell](persisting-shell-storage.md) <br>
[Справочник команд Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Знакомство с хранилищем файлов Azure](../storage/files/storage-files-introduction.md) <br>