---
title: "Начало работы с Azure Service Fabric и XPlat CLI"
description: "Начало работы с Azure Service Fabric и XPlat CLI"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="4bf8c-103">Использование XPlat CLI для взаимодействия с кластером Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4bf8c-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="4bf8c-104">Вы можете взаимодействовать с кластером Service Fabric с компьютера под управлением Linux с помощью XPlat CLI для Linux.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="4bf8c-105">Для этого сначала нужно получить и установить последнюю версию CLI из репозитория Git с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="4bf8c-106">По всем командам можно получить справку. Наберите имя нужной команды, чтобы узнать о ее возможностях.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="4bf8c-107">Для команд также поддерживается функция автозавершения.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="4bf8c-108">Например, следующая команда отобразит справку по всем командам application.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="4bf8c-109">Можно ограничить справочную информацию одной конкретной командой, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="4bf8c-110">Чтобы включить в интерфейсе командной строки функцию автозавершения, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="4bf8c-111">Следующие команды позволяют подключиться к кластеру и просмотреть список узлов кластера:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="4bf8c-112">Чтобы узнать, какие можно использовать именованные параметры и для чего они нужны, введите после команды оператор --help.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="4bf8c-113">Например:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="4bf8c-114">Чтобы подключиться к кластеру с несколькими компьютерами с компьютера, **который не входит в кластер**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="4bf8c-115">Замените тег PublicIPorFQDN нужным IP-адресом или полным доменным именем.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="4bf8c-116">Чтобы подключиться к кластеру с несколькими компьютерами с компьютера, **который входит в кластер**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="4bf8c-117">Можно использовать PowerShell или CLI для взаимодействия с кластером Service Fabric, созданным с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="4bf8c-118">Эти кластеры не являются защищенными, и вы можете поставить ваш компьютер под угрозу, добавив общедоступный IP-адрес в манифест кластера.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="4bf8c-119">Использование XPlat CLI для подключения к кластеру Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4bf8c-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="4bf8c-120">Следующие команды интерфейса командной строки Azure позволяют подключиться к безопасному кластеру.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="4bf8c-121">Сведения о сертификате должны соответствовать сертификату на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="4bf8c-122">Если ваш сертификат выдан центром сертификации, следует добавить параметр --ca-cert-path, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="4bf8c-123">Если вы используете несколько центров сертификации, перечислите их все, разделив запятыми.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="4bf8c-124">Если параметр "Общее имя" в сертификате не соответствует конечной точке подключения, для обхода проверки можно использовать параметр `--strict-ssl-false` , как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="4bf8c-125">Если вы хотите пропустить проверку центра сертификации, можно добавить параметр --reject-unauthorized-false, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="4bf8c-126">После подключения вы сможете взаимодействовать с кластером с помощью дополнительных команд интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="4bf8c-127">Развертывание приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4bf8c-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="4bf8c-128">Выполните следующие команды, чтобы скопировать, зарегистрировать и запустить приложение Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="4bf8c-129">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="4bf8c-129">Upgrading your application</span></span>

<span data-ttu-id="4bf8c-130">Процесс выполняется так же, [как и в среде Windows](service-fabric-application-upgrade-tutorial-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4bf8c-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="4bf8c-131">Выполняйте сборку, копирование, регистрацию и создание приложения в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="4bf8c-132">Если экземпляр приложения имеет имя `fabric:/MySFApp` и тип MySFApp, команда будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="4bf8c-133">Внесите изменения в приложение и выполните повторную сборку службы в измененном виде.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="4bf8c-134">Замените файл манифеста измененной службы (ServiceManifest.xml) обновленной версией для этой службы (а также все необходимые файлы из каталогов Code, Config и Data).</span><span class="sxs-lookup"><span data-stu-id="4bf8c-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="4bf8c-135">Также замените манифест приложения (ApplicationManifest.xml) обновленной версией для приложения и измененной службы.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="4bf8c-136">Теперь скопируйте и зарегистрируйте обновленное приложение с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="4bf8c-137">Теперь можно запустить обновление приложения с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="4bf8c-138">Обновление приложения можно отслеживать с помощью SFX.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="4bf8c-139">Процесс обновления завершится через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="4bf8c-140">Можно также проверить обновленное приложение на наличие ошибок или использовать возможность автоматического отката в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="4bf8c-141">Преобразование из PFX в PEM и обратно</span><span class="sxs-lookup"><span data-stu-id="4bf8c-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="4bf8c-142">Для доступа к безопасным кластерам, работающим в разных средах, может потребоваться установить сертификат на локальном компьютере (под управлением Windows или Linux).</span><span class="sxs-lookup"><span data-stu-id="4bf8c-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="4bf8c-143">Например, при доступе к защищенному кластеру Linux с компьютера Windows (или наоборот) может потребоваться преобразовать сертификат из формата PFX в PEM (или наоборот).</span><span class="sxs-lookup"><span data-stu-id="4bf8c-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="4bf8c-144">Чтобы преобразовать PEM-файл в PFX-файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="4bf8c-145">Чтобы преобразовать PFX-файл в PEM-файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="4bf8c-146">Дополнительные сведения см. в [документации по OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html).</span><span class="sxs-lookup"><span data-stu-id="4bf8c-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="4bf8c-147">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="4bf8c-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="4bf8c-148">Копирование пакета приложения завершается ошибками</span><span class="sxs-lookup"><span data-stu-id="4bf8c-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="4bf8c-149">Проверьте, установлен ли клиент `openssh`.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="4bf8c-150">Так как по умолчанию он отсутствует в Ubuntu Desktop,</span><span class="sxs-lookup"><span data-stu-id="4bf8c-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="4bf8c-151">установите его с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="4bf8c-152">Если проблема сохранится, попробуйте отключить PAM для SSH, изменив файл `sshd_config` с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="4bf8c-153">Если проблема сохранится, попробуйте число количество сеансов ssh, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4bf8c-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="4bf8c-154">Использование ключей (вместо паролей) для проверки подлинности ssh пока не поддерживается (так как платформа использует ssh для копирования пакетов), поэтому используйте только проверку пароля.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bf8c-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4bf8c-155">Next steps</span></span>

[<span data-ttu-id="4bf8c-156">Настройте среду разработки и разверните приложение Service Fabric в кластер Linux.</span><span class="sxs-lookup"><span data-stu-id="4bf8c-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="4bf8c-157">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="4bf8c-157">Related articles</span></span>

* [<span data-ttu-id="4bf8c-158">Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4bf8c-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
