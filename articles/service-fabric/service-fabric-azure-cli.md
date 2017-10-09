---
title: "aaaGetting работы с Azure Service Fabric XPlat CLI"
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
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="47bf6-103">Использование hello toointeract XPlat-CLI с кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="47bf6-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="47bf6-104">Вы можете взаимодействовать с кластером Service Fabric с компьютеров Linux с помощью hello XPlat-CLI в Linux.</span><span class="sxs-lookup"><span data-stu-id="47bf6-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="47bf6-105">Hello первый шаг получить последнюю версию hello hello CLI из hello git rep и набор его в пути с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="47bf6-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="47bf6-106">Для каждой команды он поддерживает, можно ввести имя hello tooobtain hello hello команду справки для этой команды.</span><span class="sxs-lookup"><span data-stu-id="47bf6-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="47bf6-107">Для команды hello поддерживается функция автозавершения.</span><span class="sxs-lookup"><span data-stu-id="47bf6-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="47bf6-108">Например следующая команда позволяет справки для всех команд приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="47bf6-109">Можно отфильтровать hello справки tooa конкретной команды, как следующий пример показывает hello:</span><span class="sxs-lookup"><span data-stu-id="47bf6-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="47bf6-110">tooenable автоматическое заполнение в hello CLI, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="47bf6-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="47bf6-111">следующие команды Hello соединения кластера toohello Показать hello узлов в кластере hello:</span><span class="sxs-lookup"><span data-stu-id="47bf6-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="47bf6-112">toouse именованных параметров и найти их, можно ввести — помочь после команды.</span><span class="sxs-lookup"><span data-stu-id="47bf6-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="47bf6-113">Например:</span><span class="sxs-lookup"><span data-stu-id="47bf6-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="47bf6-114">При подключении нескольких машин кластера tooa на машине **, не является частью кластера hello**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="47bf6-115">Замените тег PublicIPorFQDN hello hello реальные IP-адрес или полное доменное имя соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="47bf6-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="47bf6-116">При подключении нескольких машин кластера tooa на машине **, являющийся частью кластера hello**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="47bf6-117">Можно использовать PowerShell или создать toointeract CLI с вашего кластера Service Fabric Linux с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="47bf6-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="47bf6-118">Эти кластеры незащищенные, таким образом, вы может открыть один-поле путем добавления hello общедоступный IP-адрес в манифесте кластера hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="47bf6-119">С помощью hello кластера Service Fabric tooa tooconnect XPlat-CLI</span><span class="sxs-lookup"><span data-stu-id="47bf6-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="47bf6-120">следующие команды Azure CLI Hello описывают, как tooconnect tooa обеспечивать безопасность кластера.</span><span class="sxs-lookup"><span data-stu-id="47bf6-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="47bf6-121">сведения о сертификате Hello должно соответствовать сертификат на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="47bf6-122">Если сертификат имеет центров сертификации (ЦС), необходимо параметр--ЦС cert путь к hello tooadd как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="47bf6-123">Если у вас есть несколько центров сертификации, используйте запятую в качестве разделителя hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="47bf6-124">Если ваш общее имя в сертификате hello не соответствует hello конечной точки подключения, можно использовать параметр hello `--strict-ssl-false` toobypass hello проверки, как показано в hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="47bf6-125">При желании проверки tooskip hello ЦС, можно добавить hello--параметр отклонить, доступ запрещен ЛОЖЬ, как показано в hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="47bf6-126">После подключения должен быть доступ toorun других toointeract команд CLI с hello кластера.</span><span class="sxs-lookup"><span data-stu-id="47bf6-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="47bf6-127">Развертывание приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="47bf6-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="47bf6-128">Выполните следующие команды toocopy, зарегистрировать и запустить приложение service fabric hello hello:</span><span class="sxs-lookup"><span data-stu-id="47bf6-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="47bf6-129">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="47bf6-129">Upgrading your application</span></span>

<span data-ttu-id="47bf6-130">Hello выполняется аналогично toohello [процесса в Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="47bf6-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="47bf6-131">Выполняйте сборку, копирование, регистрацию и создание приложения в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="47bf6-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="47bf6-132">Если именованный экземпляр приложения `fabric:/MySFApp`и тип hello MySFApp, hello команды будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="47bf6-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="47bf6-133">Сделайте hello tooyour применение изменений и заново создайте hello изменения службы.</span><span class="sxs-lookup"><span data-stu-id="47bf6-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="47bf6-134">Обновление hello изменить службы файл манифеста (ServiceManifest.xml) с версиями hello обновлен для hello службы (и кода или конфигурации или данных соответствующим образом).</span><span class="sxs-lookup"><span data-stu-id="47bf6-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="47bf6-135">Также изменить манифест приложения hello (ApplicationManifest.xml) с hello обновить номер версии для приложения hello и hello измененные службы.</span><span class="sxs-lookup"><span data-stu-id="47bf6-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="47bf6-136">Теперь скопировать и зарегистрировать обновленные приложения с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="47bf6-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="47bf6-137">Теперь можно начать обновление приложения hello с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="47bf6-138">Теперь можно отслеживать с помощью SFX обновление приложения hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="47bf6-139">Через несколько минут hello приложения будут обновлены.</span><span class="sxs-lookup"><span data-stu-id="47bf6-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="47bf6-140">Также попробуйте обновленные приложения с ошибкой и проверьте возможность отката автоматически hello в service fabric.</span><span class="sxs-lookup"><span data-stu-id="47bf6-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="47bf6-141">Преобразование из PFX tooPEM и наоборот</span><span class="sxs-lookup"><span data-stu-id="47bf6-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="47bf6-142">Может потребоваться tooinstall сертификат в ваш локальный компьютер (с Windows или Linux) tooaccess защищенных кластеров, в другой среде.</span><span class="sxs-lookup"><span data-stu-id="47bf6-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="47bf6-143">Например при доступе к защищенным кластеров Linux с компьютером Windows и наоборот нужно tooconvert сертификата из PFX-ФАЙЛ tooPEM и наоборот.</span><span class="sxs-lookup"><span data-stu-id="47bf6-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="47bf6-144">tooconvert из PEM файл tooa PFX-файла, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="47bf6-145">tooconvert из файла PEM tooa файла PFX, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="47bf6-146">См. слишком[OpenSSL документации](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="47bf6-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="47bf6-147">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="47bf6-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="47bf6-148">Копирование пакета приложения hello завершилась с ошибками</span><span class="sxs-lookup"><span data-stu-id="47bf6-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="47bf6-149">Проверьте, установлен ли клиент `openssh`.</span><span class="sxs-lookup"><span data-stu-id="47bf6-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="47bf6-150">Так как по умолчанию он отсутствует в Ubuntu Desktop,</span><span class="sxs-lookup"><span data-stu-id="47bf6-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="47bf6-151">Установите его с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47bf6-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="47bf6-152">При повторном возникновении проблемы hello, попробуйте отключить PAM для ssh, изменив hello `sshd_config` файла с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="47bf6-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="47bf6-153">Если hello проблема сохраняется, попробуйте использовать hello увеличивающихся ssh сеансы, выполнив следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="47bf6-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="47bf6-154">С помощью ключей для ssh проверки подлинности (как противоположность toopasswords) еще не поддерживается (поскольку hello платформа использует ssh toocopy пакетов), поэтому вместо этого используйте пароль проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="47bf6-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47bf6-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47bf6-155">Next steps</span></span>

[<span data-ttu-id="47bf6-156">Настройка среды разработки hello и развертывание кластера Service Fabric tooa приложения Linux.</span><span class="sxs-lookup"><span data-stu-id="47bf6-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="47bf6-157">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="47bf6-157">Related articles</span></span>

* [<span data-ttu-id="47bf6-158">Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="47bf6-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
