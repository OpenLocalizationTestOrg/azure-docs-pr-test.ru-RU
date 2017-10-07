---
title: "Быстрый запуск - aaaAzure создания виртуальной Машины портала | Документы Microsoft"
description: "Краткое руководство по созданию виртуальной машины с помощью портала Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a>Создание виртуальной машины Linux с hello портал Azure

Виртуальные машины Azure могут создаваться через портал Azure hello. В этом случае для создания и настройки виртуальных машин и всех связанных ресурсов Azure используется пользовательский интерфейс на основе браузера. Это краткое руководство пошаговые инструкции для создания виртуальной машины и установка веб-сервере, на hello виртуальной Машины.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

## <a name="create-ssh-key-pair"></a>Создание пары ключей SSH

В этом кратком руководстве вы должны toocomplete пару ключей SSH. Если у вас уже есть пара ключей SSH, этот шаг можно пропустить.

В оболочке Bash выполните следующую команду и следуйте hello на экране инструкциям. выходные данные команды Hello включает имя файла hello hello файла открытого ключа. Скопируйте содержимое буфера обмена toohello файла открытого ключа hello hello.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a>Войдите в tooAzure 

Войдите в систему toohello портал Azure по адресу http://portal.azure.com.

## <a name="create-virtual-machine"></a>Создание виртуальной машины

1. Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.

2. Выберите **Вычисления**, а затем — **Сервер Ubuntu 16.04 LTS**. 

3. Введите сведения о виртуальной машине hello. Для параметра **Тип проверки подлинности** выберите значение **Открытый ключ SSH**. При вставке в свой открытый ключ SSH, аккуратно tooremove все начальные и конечные пробелы. По завершении нажмите кнопку **ОК**.

    ![Ввести основные сведения о ВМ в колонке портала hello](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. Выберите размер виртуальной Машины hello. Выберите дополнительные размеры toosee **просмотреть все** или изменить hello **поддерживается тип диска** фильтра. 

    ![Снимок экрана, на котором показаны размеры виртуальных машин](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. В колонке параметров hello, оставьте значения по умолчанию hello и нажмите кнопку **ОК**.

6. На странице сводки hello щелкните **ОК** развертывания виртуальной машины toostart hello.

7. Hello виртуальной Машины будет закрепленных toohello Azure панели мониторинга портала. После завершения развертывания hello, автоматически откроется Сводка колонки hello виртуальной Машины.


## <a name="connect-toovirtual-machine"></a>Подключиться к компьютеру toovirtual

Создайте SSH-подключения с hello виртуальной машины.

1. Нажмите кнопку hello **Connect** кнопку hello колонке виртуальной машины. Hello подключиться кнопки отображает строку подключения SSH, можно использовать tooconnect toohello виртуальной машине.

    ![Портал 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. Выполнения hello следующая команда toocreate сеанс SSH. Замените строку соединения hello hello, один скопированной из hello портал Azure.

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>Установка nginx

Используйте hello ниже bash источники пакетов tooupdate сценария и установить последнюю версию пакета NGINX hello. 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

После этого завершите сеанс SSH hello и возвращает свойства виртуальной Машины hello hello портал Azure.


## <a name="open-port-80-for-web-traffic"></a>Открытие порта 80 для веб-трафика 

Группа безопасности сети (NSG) защищает входящий и исходящий трафик. При создании виртуальной Машины из портала Azure hello входящее правило создается на порт 22 для соединений по протоколу SSH. Поскольку эта виртуальная машина размещается веб-сервере, правило NSG должен toobe, созданное для порта 80.

1. На виртуальной машине hello, щелкните имя hello hello **группы ресурсов**.
2. Выберите hello **сетевой группы безопасности**. Hello NSG можно определить с помощью hello **тип** столбца. 
3. Hello слева в разделе Параметры меню **безопасности правила для входящих подключений**.
4. Щелкните **Добавить**.
5. В поле **Имя** введите **http**. Убедитесь, что **диапазон портов** задано too80 и **действия** задано слишком**Разрешить**. 
6. Нажмите кнопку **ОК**.


## <a name="view-hello-nginx-welcome-page"></a>Просмотр hello NGINX начальной страницы

С NGINX установлены и порт 80 откройте tooyour виртуальных Машин, веб-сервер hello, теперь доступны из hello Интернета. Откройте веб-браузер и введите hello общедоступный IP-адрес hello виртуальной Машины. Hello общедоступный IP-адрес можно найти на колонки виртуальной Машины hello в hello портал Azure.

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Очистка ресурсов

Когда больше не нужен, удалите hello группы ресурсов, виртуальные машины и все связанные ресурсы. toodo таким образом, выберите группу ресурсов hello hello колонке виртуальной машины и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера. toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Linux.

> [!div class="nextstepaction"]
> [Создание виртуальных машин Linux и управление ими с помощью Azure CLI](./tutorial-manage-vm.md)
