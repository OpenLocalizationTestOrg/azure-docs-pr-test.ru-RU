---
title: "aaaCustomize виртуальной Машины Linux при первой загрузке в Azure | Документы Microsoft"
description: "Узнайте, как toouse облака init и хранилище ключей toocustomze виртуальных машин Linux hello первый раз они загружаются в Azure"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Как toocustomize виртуальной машины Linux при первой загрузке
В предыдущем учебнике вы узнали, как tooSSH tooa виртуальной машины (VM) и вручную установить NGINX. Обычно требуется toocreate виртуальных машин в виде краткое и согласованное, средства автоматизации. Общие toocustomize подход при первом запуске виртуальной Машины — toouse [init облака](https://cloudinit.readthedocs.io). Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * создать файл конфигурации cloud-init;
> * создать виртуальную машину, использующую файл конфигурации cloud-init;
> * Просмотр работающего приложения Node.js после hello создания виртуальной Машины
> * Использовать хранилище ключей toosecurely хранилище сертификатов
> * автоматизировать безопасные развертывания nginx с помощью файла конфигурации cloud-init.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Обзор cloud-Init
[Облако init](https://cloudinit.readthedocs.io) является виртуальной Машины Linux toocustomize широко используемый метод загрузки для hello первый раз. Можно использовать пакеты tooinstall init облака и записывать файлы, tooconfigure пользователи и безопасности. Во время выполнения init облака во время начальной загрузки hello нет никаких дополнительных действий или tooapply агентов, необходимых вашей конфигурации.

Кроме того, cloud-init работает с разными дистрибутивами. Например, вы не используете **install apt get** или **yum установить** tooinstall пакета. Вместо этого можно определить список tooinstall пакетов. Init облака автоматически использует средство управления hello пакета машинного кода для hello дистрибутив при выборе.

Можно работать с наших партнеров tooget облака init включены и работу в том, что они предоставляют tooAzure образы hello. Привет, в следующей таблице описаны hello текущей доступности init облака на платформе Azure образы.

| Alias | Издатель | ПРЕДЛОЖЕНИЕ | SKU | Version (версия) |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04-LTS |последних |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |последних |
| CoreOS |CoreOS |CoreOS |Stable |последних |


## <a name="create-cloud-init-config-file"></a>Создание файла конфигурации cloud-init
облака init toosee в действии, создайте виртуальную Машину, NGINX устанавливается и запускается простое приложение Node.js «Hello, World!». Следующая конфигурация облака init Hello устанавливает hello необходимые пакеты, создает приложение Node.js, а затем инициализировать и запускает приложение hello.

В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация. Например можно создайте файл hello в hello облака оболочки не на локальном компьютере. Вы можете использовать любой редактор. Введите `sensible-editor cloud-init.txt` toocreate hello файла и просмотреть список доступных редакторов. Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

Чтобы узнать больше о параметрах конфигурации cloud-init, ознакомьтесь с [примерами конфигурации cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Создание виртуальной машины
Прежде чем создать виртуальную машину, выполните команду [az group create](/cli/azure/group#create), чтобы создать группу ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupAutomate* в hello *eastus* расположение:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create). Используйте hello `--custom-data` toopass параметр в файле конфигурации облака init. Укажите полный путь toohello hello *init.txt облака* конфигурации, если вы сохранили файл hello за пределами имеется рабочий каталог. Hello следующий пример создает Виртуальную машину с именем *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Он занимает несколько минут для создания toobe ВМ hello tooinstall пакеты hello и toostart приложения hello. Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки. Он может быть другой несколько минут, чтобы получить доступ к приложение hello. При создании виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI. Этот адрес будет приложение Node.js hello используется tooaccess из веб-браузера.

tooallow веб-трафика tooreach виртуальной Машины, откройте порт 80 с hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Тестирование веб-приложения
Теперь можно открыть веб-браузер и введите *http://<publicIpAddress>*  в адресную строку hello. Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс. Как и следующий пример hello отображается ваше приложение Node.js:

![Просмотр работающего сайта NGINX](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Внедрение сертификатов из Key Vault
Этот дополнительный раздел показывает, как можно безопасно хранить сертификаты в хранилище ключей Azure и внедрить их во время развертывания виртуальной Машины hello. Вместо того чтобы использовать настраиваемое изображение, которое включает сертификаты hello помещенного в этот процесс гарантирует, что наиболее актуальные сертификаты hello вводится tooa виртуальной Машины во время первой загрузки. Во время процесса hello hello сертификат никогда не покидает hello платформы Azure или предоставляется в скрипт, командной строки журнала или шаблона.

Azure Key Vault защищает криптографические ключи и секреты, в том числе сертификаты и пароли. Хранилище ключей помогает ускорить процесс управления ключами hello и позволяет toomaintain управление ключами, которые обращаются к и шифрование данных. Этот сценарий представлены некоторые основные понятия toocreate хранилище ключей и использовать сертификат, но не является исчерпывающим Общие сведения о том, как toouse хранилища ключей.

Hello, следующие шаги показывают, как вы можете:

- Создание Azure Key Vault
- Создать или отправить сертификат toohello хранилища ключей
- Создание секрета из tooinject сертификат hello в tooa виртуальной Машины
- Создайте виртуальную Машину и вставляют hello сертификата

### <a name="create-an-azure-key-vault"></a>Создание Azure Key Vault
Сначала создайте Key Vault командой [az keyvault create](/cli/azure/keyvault#create) и включите его использование при развертывании виртуальной машины. У каждого Key Vault должно быть уникальное имя в нижнем регистре. Замените *mykeyvault* в hello следующий пример с собственное уникальное имя хранилища ключей:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Создание сертификата и его сохранение в Key Vault
Для использования в рабочей среде следует импортировать действительный сертификат, подписанный доверенным поставщиком, выполнив команду [az keyvault certificate import](/cli/azure/keyvault/certificate#import). В этом учебнике hello следующем примере показано, как можно создать самозаверяющий сертификат с [Создание сертификата keyvault az](/cli/azure/keyvault/certificate#create) , использующий hello политика по умолчанию:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Подготовка сертификата для использования с виртуальной машиной
сертификат hello toouse во время hello ВМ создать процесс, получить hello Удостоверение сертификата с [az keyvault списка версии секрета](/cli/azure/keyvault/secret#list-versions). Hello виртуальной Машины, необходим сертификат hello в определенных tooinject формат его во время загрузки, поэтому преобразование hello сертификат с [формат секретный ВМ az](/cli/azure/vm#format-secret). Следующий пример Hello назначает hello выходные данные этих команд toovariables для простоты использования в hello следующие шаги:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Создание конфигурации облака init toosecure NGINX
При создания виртуальной Машины, сертификаты и ключи хранятся в защищенных hello */var/lib/waagent/* каталога. сертификат toohello tooautomate Добавление hello виртуальных Машин и настройки NGINX, можно использовать обновленный инициализацией облачной конфигурации из предыдущего примера hello.

Создайте файл с именем *облака init-secured.txt* и вставить hello следующая конфигурация. Снова при использовании hello оболочки облака, создайте файл конфигурации облачной init hello отсутствует, а не на локальном компьютере. Используйте `sensible-editor cloud-init-secured.txt` toocreate hello файла и просмотреть список доступных редакторов. Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>Создание безопасной виртуальной машины
Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create). данные сертификата Hello, введенный в hello из хранилища ключей `--secrets` параметра. Как hello в предыдущем примере, можно также передавать hello init облачные конфигурации с hello `--custom-data` параметр:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Он занимает несколько минут для создания toobe ВМ hello tooinstall пакеты hello и toostart приложения hello. Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки. Он может быть другой несколько минут, чтобы получить доступ к приложение hello. При создании виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI. Этот адрес будет приложение Node.js hello используется tooaccess из веб-браузера.

tooallow secure tooreach трафика web виртуальной Машины, откройте порт 443 из hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Тестирование защищенного веб-приложения
Теперь можно открыть веб-браузер и введите *https://<publicIpAddress>*  в адресную строку hello. Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс. Примите предупреждение о безопасности hello, если используется самозаверяющий сертификат:

![Принятие предупреждения о безопасности веб-браузера](./media/tutorial-automate-vm-deployment/browser-warning.png)

Защищенные NGINX сайта и Node.js приложения отображается как hello в следующем примере:

![Просмотр работающего защищенного сайта NGINX](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Дальнейшие действия
В рамках этого руководства вы настроили виртуальные машины при первой загрузке с помощью файла конфигурации cloud-init. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * создавать файл конфигурации cloud-init;
> * создать виртуальную машину, использующую файл конфигурации cloud-init;
> * Просмотр работающего приложения Node.js после hello создания виртуальной Машины
> * Использовать хранилище ключей toosecurely хранилище сертификатов
> * автоматизировать безопасные развертывания nginx с помощью файла конфигурации cloud-init.

Как переместить следующий учебник toolearn toohello toocreate пользовательских образов виртуальной Машины.

> [!div class="nextstepaction"]
> [Создание образа настраиваемой виртуальной машины](./tutorial-custom-images.md)
