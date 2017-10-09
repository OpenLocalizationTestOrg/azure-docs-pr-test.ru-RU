---
title: "aaaUse корневой права на виртуальных машинах Linux | Документы Microsoft"
description: "Узнайте, как корневой toouse права доступа на виртуальной машине Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Использование прав корневой учетной записи на виртуальных машинах Linux в Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

По умолчанию hello `root` пользователь отключен на виртуальных машинах Linux в Azure. Пользователи могут запускать команды с повышенными привилегиями, используя hello `sudo` команды. Тем не менее в зависимости от того, как была создана система hello зависит hello качества.

1. **SSH-ключ и пароль или пароль только** -hello виртуальной машины была создана с сертификатом (`.CER` файл) или ключ SSH, а также пароль, или только имя пользователя и пароль. В этом случае `sudo` предложит ввести пароль пользователя hello перед выполнением команды hello.
2. **SSH-ключ только** -hello виртуальной машины, была создана с помощью сертификата (`.cer`, `.pem`, или `.pub` файл) или ключа SSH, но без пароля.  В этом случае `sudo` **не будет** запрашивать hello пароль перед выполнением команды hello.

## <a name="ssh-key-and-password-or-password-only"></a>Ключ и пароль или только пароль SSH
Войдите на виртуальную машину Linux hello, с помощью ключа или пароля для проверки подлинности SSH, а затем выполните команды с помощью `sudo`, например:

    # sudo <command>
    [sudo] password for azureuser:

В этом случае пользователь hello предложит ввести пароль. После ввода пароля hello `sudo` будет выполнена команда hello с `root` права.

Можно также включить passwordless sudo, изменив hello `/etc/sudoers.d/waagent` файла, например:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Это изменение позволит passwordless sudo пользователем hello «azureuser».

## <a name="ssh-key-only"></a>Только ключ SSH
Войдите на виртуальной машине Linux hello, с помощью проверки подлинности SSH с ключом, а затем выполните команды с помощью `sudo`, например:

    # sudo <command>

В этом случае будет hello пользователя **не** предложено ввести пароль. После нажатия `<enter>`, `sudo` будет выполнена команда hello с `root` права.

