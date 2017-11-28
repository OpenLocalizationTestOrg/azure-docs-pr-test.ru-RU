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
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="76090-103">Защита веб-сервера с помощью SSL-сертификатов на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="76090-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="76090-104">toosecure веб-серверов, сертификат позже SSL (Secure Sockets) можно использовать tooencrypt веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="76090-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="76090-105">SSL-сертификаты могут храниться в хранилище ключей Azure и разрешать безопасного развертывания сертификатов tooLinux виртуальных машин (ВМ) в Azure.</span><span class="sxs-lookup"><span data-stu-id="76090-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="76090-106">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="76090-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76090-107">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="76090-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="76090-108">Создать или отправить сертификат toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="76090-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="76090-109">Создайте виртуальную Машину и установите веб-сервер NGINX hello</span><span class="sxs-lookup"><span data-stu-id="76090-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="76090-110">Вставить сертификат hello в hello виртуальной Машины и настроить NGINX с SSL-привязка.</span><span class="sxs-lookup"><span data-stu-id="76090-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="76090-111">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="76090-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="76090-112">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="76090-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="76090-113">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="76090-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="76090-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="76090-114">Overview</span></span>
<span data-ttu-id="76090-115">Azure Key Vault защищает криптографические ключи и секреты, в том числе сертификаты или пароли.</span><span class="sxs-lookup"><span data-stu-id="76090-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="76090-116">Хранилище ключей помогает ускорить процесс управления сертификата hello и позволяет toomaintain управление ключами, которые обращаются к этих сертификатов.</span><span class="sxs-lookup"><span data-stu-id="76090-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="76090-117">Можно создать самозаверяющий сертификат в Key Vault или передать существующий доверенный сертификат.</span><span class="sxs-lookup"><span data-stu-id="76090-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="76090-118">Вместо того чтобы использовать образ виртуальной машины, включающий встроенные сертификаты, можно внедрить сертификаты в работающую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="76090-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="76090-119">Этот процесс гарантирует, что hello наиболее актуальные сертификаты установлены на веб-сервере во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="76090-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="76090-120">Если обновления или замены сертификата, также нет toocreate нового пользовательского образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76090-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="76090-121">Hello последние сертификаты добавляются автоматически при создании дополнительных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="76090-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="76090-122">В процессе hello всей hello сертификаты никогда не оставить hello платформы Azure или, представлены в скрипт, командной строки журнала или шаблона.</span><span class="sxs-lookup"><span data-stu-id="76090-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="76090-123">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="76090-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="76090-124">Прежде чем создать Key Vault и сертификаты, выполните командлет [az group create](/cli/azure/group#create), чтобы создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="76090-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="76090-125">Hello следующий пример создает группу ресурсов с именем *myResourceGroupSecureWeb* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="76090-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="76090-126">Затем создайте Key Vault с помощью [az keyvault create](/cli/azure/keyvault#create) и включите его использование при развертывании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="76090-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="76090-127">У каждого Key Vault должно быть уникальное имя в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="76090-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="76090-128">Замените  *<mykeyvault>*  в hello следующий пример с собственное уникальное имя хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="76090-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="76090-129">Создание сертификата и его сохранение в Key Vault</span><span class="sxs-lookup"><span data-stu-id="76090-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="76090-130">Для использования в рабочей среде следует импортировать действительный сертификат, подписанный доверенным поставщиком, выполнив команду [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="76090-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="76090-131">В этом учебнике hello следующем примере показано, как можно создать самозаверяющий сертификат с [Создание сертификата keyvault az](/cli/azure/certificate#create) , использующий hello политика по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="76090-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="76090-132">Подготовка сертификата для использования с виртуальной машиной</span><span class="sxs-lookup"><span data-stu-id="76090-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="76090-133">сертификат hello toouse во время hello ВМ создать процесс, получить hello Удостоверение сертификата с [az keyvault списка версии секрета](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="76090-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="76090-134">Преобразование hello сертификата с [формат секретный ВМ az](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="76090-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="76090-135">Следующий пример Hello назначает hello выходные данные этих команд toovariables для простоты использования в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="76090-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="76090-136">Создание облачных init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="76090-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="76090-137">[Облако init](https://cloudinit.readthedocs.io) является виртуальной Машины Linux toocustomize широко используемый метод загрузки для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="76090-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="76090-138">Можно использовать пакеты tooinstall init облака и записывать файлы, tooconfigure пользователи и безопасности.</span><span class="sxs-lookup"><span data-stu-id="76090-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="76090-139">Во время выполнения init облака во время начальной загрузки hello нет никаких дополнительных действий или tooapply агентов, необходимых вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76090-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="76090-140">При создания виртуальной Машины, сертификаты и ключи хранятся в защищенных hello */var/lib/waagent/* каталога.</span><span class="sxs-lookup"><span data-stu-id="76090-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="76090-141">Добавление tooautomate hello toohello сертификатов виртуальной Машины и настройке hello веб-сервера, используйте облачные init.</span><span class="sxs-lookup"><span data-stu-id="76090-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="76090-142">В этом примере мы установите и настройте веб-сервер NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="76090-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="76090-143">Можно использовать hello же процессе tooinstall и настроить Apache.</span><span class="sxs-lookup"><span data-stu-id="76090-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="76090-144">Создайте файл с именем *облака init-web-server.txt* и вставить hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="76090-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="76090-145">Создание защищенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="76090-145">Create a secure VM</span></span>
<span data-ttu-id="76090-146">Теперь создайте виртуальную машину командой [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="76090-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="76090-147">данные сертификата Hello, введенный в hello из хранилища ключей `--secrets` параметра.</span><span class="sxs-lookup"><span data-stu-id="76090-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="76090-148">Передать в конфигурацию hello init облака с hello `--custom-data` параметр:</span><span class="sxs-lookup"><span data-stu-id="76090-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

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

<span data-ttu-id="76090-149">Он занимает несколько минут для создания toobe ВМ hello tooinstall пакеты hello и toostart приложения hello.</span><span class="sxs-lookup"><span data-stu-id="76090-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="76090-150">При создании виртуальной Машины hello запишите hello `publicIpAddress` отображаемого hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="76090-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="76090-151">Этот адрес является используется tooaccess сайт в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="76090-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="76090-152">tooallow secure tooreach трафика web виртуальной Машины, откройте порт 443 из hello Интернета с [az виртуальной машины откройте порт-](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="76090-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="76090-153">Тест hello безопасного веб-приложения</span><span class="sxs-lookup"><span data-stu-id="76090-153">Test hello secure web app</span></span>
<span data-ttu-id="76090-154">Теперь можно открыть веб-браузер и введите *https://<publicIpAddress>*  в адресную строку hello.</span><span class="sxs-lookup"><span data-stu-id="76090-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="76090-155">Укажите ваши собственные общедоступные IP-адрес из виртуальной Машины hello создать процесс.</span><span class="sxs-lookup"><span data-stu-id="76090-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="76090-156">Примите предупреждение о безопасности hello, если используется самозаверяющий сертификат:</span><span class="sxs-lookup"><span data-stu-id="76090-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Принятие предупреждения о безопасности веб-браузера](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="76090-158">Защищенные NGINX узла отображается как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="76090-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Просмотр работающего защищенного сайта NGINX](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="76090-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76090-160">Next steps</span></span>

<span data-ttu-id="76090-161">С помощью этого руководства вы защитили веб-сервер NGINX SSL-сертификатом, который хранится в Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="76090-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="76090-162">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="76090-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76090-163">Создание Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="76090-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="76090-164">Создать или отправить сертификат toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="76090-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="76090-165">Создайте виртуальную Машину и установите веб-сервер NGINX hello</span><span class="sxs-lookup"><span data-stu-id="76090-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="76090-166">Вставить сертификат hello в hello виртуальной Машины и настроить NGINX с SSL-привязка.</span><span class="sxs-lookup"><span data-stu-id="76090-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="76090-167">Выполните этот toosee ссылку готовые примеры скриптов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="76090-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76090-168">Примеры скриптов для виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="76090-168">Windows virtual machine script samples</span></span>](./cli-samples.md)