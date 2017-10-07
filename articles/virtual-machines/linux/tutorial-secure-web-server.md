---
title: "aaaSecure веб-сервере с помощью SSL-сертификаты в Azure | Документы Microsoft"
description: "Узнайте, как веб-сервер NGINX toosecure hello с SSL-сертификаты на виртуальной Машине Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Защита веб-сервера с помощью SSL-сертификатов на виртуальной машине Linux в Azure
toosecure веб-серверов, сертификат позже SSL (Secure Sockets) можно использовать tooencrypt веб-трафика. SSL-сертификаты могут храниться в хранилище ключей Azure и разрешать безопасного развертывания сертификатов tooLinux виртуальных машин (ВМ) в Azure. Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Создание Azure Key Vault
> * Создать или отправить сертификат toohello хранилища ключей
> * Создайте виртуальную Машину и установите веб-сервер NGINX hello
> * Вставить сертификат hello в hello виртуальной Машины и настроить NGINX с SSL-привязка.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Обзор
Azure Key Vault защищает криптографические ключи и секреты, в том числе сертификаты или пароли. Хранилище ключей помогает ускорить процесс управления сертификата hello и позволяет toomaintain управление ключами, которые обращаются к этих сертификатов. Можно создать самозаверяющий сертификат в Key Vault или передать существующий доверенный сертификат.

Вместо того чтобы использовать образ виртуальной машины, включающий встроенные сертификаты, можно внедрить сертификаты в работающую виртуальную машину. Этот процесс гарантирует, что hello наиболее актуальные сертификаты установлены на веб-сервере во время развертывания. Если обновления или замены сертификата, также нет toocreate нового пользовательского образа виртуальной Машины. Hello последние сертификаты добавляются автоматически при создании дополнительных виртуальных машин. В процессе hello всей hello сертификаты никогда не оставить hello платформы Azure или, представлены в скрипт, командной строки журнала или шаблона.


## <a name="create-an-azure-key-vault"></a>Создание Azure Key Vault
Прежде чем создать Key Vault и сертификаты, выполните командлет [az group create](/cli/azure/group#create), чтобы создать группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupSecureWeb* в hello *eastus* расположение:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Затем создайте Key Vault с помощью [az keyvault create](/cli/azure/keyvault#create) и включите его использование при развертывании виртуальной машины. У каждого Key Vault должно быть уникальное имя в нижнем регистре. Замените  *<mykeyvault>*  в hello следующий пример с собственное уникальное имя хранилища ключей:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Создание сертификата и его сохранение в Key Vault
Для использования в рабочей среде следует импортировать действительный сертификат, подписанный доверенным поставщиком, выполнив команду [az keyvault certificate import](/cli/azure/certificate#import). В этом учебнике hello следующем примере показано, как можно создать самозаверяющий сертификат с [Создание сертификата keyvault az](/cli/azure/certificate#create) , использующий hello политика по умолчанию:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Подготовка сертификата для использования с виртуальной машиной
сертификат hello toouse во время hello ВМ создать процесс, получить hello Удостоверение сертификата с [az keyvault списка версии секрета](/cli/azure/keyvault/secret#list-versions). Преобразование hello сертификата с [формат секретный ВМ az](/cli/azure/vm#format-secret). Следующий пример Hello назначает hello выходные данные этих команд toovariables для простоты использования в hello следующие шаги:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Создание облачных init config toosecure NGINX
[Облако init](https://cloudinit.readthedocs.io) является виртуальной Машины Linux toocustomize широко используемый метод загрузки для hello первый раз. Можно использовать пакеты tooinstall init облака и записывать файлы, tooconfigure пользователи и безопасности. Во время выполнения init облака во время начальной загрузки hello нет никаких дополнительных действий или tooapply агентов, необходимых вашей конфигурации.

При создания виртуальной Машины, сертификаты и ключи хранятся в защищенных hello */var/lib/waagent/* каталога. Добавление tooautomate hello toohello сертификатов виртуальной Машины и настройке hello веб-сервера, используйте облачные init. В этом примере мы установите и настройте веб-сервер NGINX hello. Можно использовать hello же процессе tooinstall и настроить Apache. 

Создайте файл с именем *облака init-web-server.txt* и вставить hello следующая конфигурация:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>Создание защищенной виртуальной машины
Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create). данные сертификата Hello, введенный в hello из хранилища ключей `--secrets` параметра. Передать в конфигурацию hello init облака с hello `--custom-data` параметр:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Он занимает несколько минут для создания toobe ВМ hello tooinstall пакеты hello и toostart приложения hello. При создании виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI. Этот адрес является используется tooaccess сайт в веб-браузере.

tooallow secure tooreach трафика web виртуальной Машины, откройте порт 443 из hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Тест hello безопасного веб-приложения
Теперь можно открыть веб-браузер и введите *https://<publicIpAddress>*  в адресную строку hello. Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс. Примите предупреждение о безопасности hello, если используется самозаверяющий сертификат:

![Принятие предупреждения о безопасности веб-браузера](./media/tutorial-secure-web-server/browser-warning.png)

Защищенные NGINX узла отображается как hello в следующем примере:

![Просмотр работающего защищенного сайта NGINX](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Дальнейшие действия

С помощью этого руководства вы защитили веб-сервер NGINX SSL-сертификатом, который хранится в Azure Key Vault. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Key Vault
> * Создать или отправить сертификат toohello хранилища ключей
> * Создайте виртуальную Машину и установите веб-сервер NGINX hello
> * Вставить сертификат hello в hello виртуальной Машины и настроить NGINX с SSL-привязка.

Выполните этот toosee ссылку готовые примеры скриптов для виртуальной машины.

> [!div class="nextstepaction"]
> [Примеры скриптов для виртуальной машины Windows](./cli-samples.md)