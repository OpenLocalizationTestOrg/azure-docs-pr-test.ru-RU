---
title: "aaaGet работы с Azure Service Fabric и Azure CLI 2.0"
description: "Узнайте, как toouse hello Azure Service Fabric команды модуля в Azure CLI, версии 2.0. Узнайте, как tooconnect tooa кластера и как toomanage приложений."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="085da-104">Azure Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="085da-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="085da-105">Hello средство командной строки Azure (Azure CLI) версии 2.0 включает управление кластерами Azure Service Fabric toohelp команд.</span><span class="sxs-lookup"><span data-stu-id="085da-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="085da-106">Узнайте, как tooget работу с Azure CLI и Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="085da-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="085da-107">Установка Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="085da-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="085da-108">Можно использовать toointeract команды Azure CLI 2.0 с и позволяющая управлять кластерами Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="085da-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="085da-109">tooget hello последнюю версию Azure CLI, выполните hello [стандартного процесса Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="085da-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="085da-110">Дополнительные сведения см. в разделе hello [Обзор Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="085da-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="085da-111">Синтаксис Azure CLI</span><span class="sxs-lookup"><span data-stu-id="085da-111">Azure CLI syntax</span></span>

<span data-ttu-id="085da-112">Все команды Service Fabric в Azure CLI начинаются с префикса `az sf`.</span><span class="sxs-lookup"><span data-stu-id="085da-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="085da-113">Общие сведения о командах hello, можно использовать использовать `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="085da-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="085da-114">Для получения сведений об одной команде используйте `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="085da-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="085da-115">Команды Service Fabric в Azure CLI соответствуют такому шаблону именования:</span><span class="sxs-lookup"><span data-stu-id="085da-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="085da-116">`<object>`является целевым объектом hello `<action>`.</span><span class="sxs-lookup"><span data-stu-id="085da-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="085da-117">Выбор кластера</span><span class="sxs-lookup"><span data-stu-id="085da-117">Select a cluster</span></span>

<span data-ttu-id="085da-118">Прежде чем выполнять любые операции, необходимо выбрать tooconnect кластера для.</span><span class="sxs-lookup"><span data-stu-id="085da-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="085da-119">Пример см. в разделе hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="085da-119">For an example, see hello following code.</span></span> <span data-ttu-id="085da-120">Hello подключает tooan незащищенных кластеров.</span><span class="sxs-lookup"><span data-stu-id="085da-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="085da-121">Не используйте незащищенные кластеры Service Fabric в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="085da-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="085da-122">Конечная точка Hello кластера должен стоять `http` или `https`.</span><span class="sxs-lookup"><span data-stu-id="085da-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="085da-123">Она должна включать hello порт для шлюза hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="085da-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="085da-124">Hello порт и адрес hello равна hello Service Fabric Explorer URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="085da-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="085da-125">Для кластеров, защищенных с помощью сертификата, можно использовать не зашифрованные PEM-файлы или CRT-файлы и KEY-файлы.</span><span class="sxs-lookup"><span data-stu-id="085da-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="085da-126">Например:</span><span class="sxs-lookup"><span data-stu-id="085da-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="085da-127">Дополнительные сведения см. в разделе [кластера Azure Service Fabric безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="085da-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="085da-128">Hello `select` перед возвратом команда не действовать на все запросы.</span><span class="sxs-lookup"><span data-stu-id="085da-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="085da-129">tooverify, что вы указали кластер правильно, используйте команды, аналогичной `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="085da-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="085da-130">Убедитесь, что команда hello не возвращает все ошибки.</span><span class="sxs-lookup"><span data-stu-id="085da-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="085da-131">Базовые операции</span><span class="sxs-lookup"><span data-stu-id="085da-131">Basic operations</span></span>

<span data-ttu-id="085da-132">Сведения о подключении кластера сохраняется между различными сеансами Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="085da-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="085da-133">После выбора кластера Service Fabric, можно запустить любую команду Service Fabric на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="085da-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="085da-134">Например tooget hello состояние работоспособности кластера Service Fabric, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="085da-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="085da-135">Команда Hello приводит следующие hello, выходные данные (предполагается, что выходные данные JSON указан в конфигурации hello Azure CLI):</span><span class="sxs-lookup"><span data-stu-id="085da-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="085da-136">Рекомендации и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="085da-136">Tips and troubleshooting</span></span>

<span data-ttu-id="085da-137">Может оказаться hello следующие сведения, полезные при возникновении проблем при работе с Service Fabric команд в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="085da-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="085da-138">Преобразование из формата tooPEM PFX сертификата</span><span class="sxs-lookup"><span data-stu-id="085da-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="085da-139">Azure CLI поддерживает клиентские сертификаты, такие как PEM-файлы.</span><span class="sxs-lookup"><span data-stu-id="085da-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="085da-140">При использовании PFX-файлы из Windows, необходимо преобразовать формат tooPEM этих сертификатов.</span><span class="sxs-lookup"><span data-stu-id="085da-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="085da-141">tooconvert PEM tooa файл PFX-файла, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="085da-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="085da-142">Дополнительные сведения см. в разделе hello [OpenSSL документации](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="085da-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="085da-143">Проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="085da-143">Connection issues</span></span>

<span data-ttu-id="085da-144">Некоторые операции могут создавать hello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="085da-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="085da-145">Убедитесь, что указан hello, что конечные точки кластера доступен и прослушивания.</span><span class="sxs-lookup"><span data-stu-id="085da-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="085da-146">Кроме того убедитесь, что приветствия пользовательский Интерфейс обозревателя Service Fabric доступен на, узла и порта.</span><span class="sxs-lookup"><span data-stu-id="085da-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="085da-147">hello tooupdate конечной точки, используйте `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="085da-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="085da-148">Подробные журналы</span><span class="sxs-lookup"><span data-stu-id="085da-148">Detailed logs</span></span>

<span data-ttu-id="085da-149">Подробные журналы часто полезны при отладке или при сообщении о проблеме.</span><span class="sxs-lookup"><span data-stu-id="085da-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="085da-150">Предоставляет глобальный Azure CLI `--debug` флаг, который повышает уровень детализации hello файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="085da-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="085da-151">Справка и синтаксис для команд</span><span class="sxs-lookup"><span data-stu-id="085da-151">Command help and syntax</span></span>

<span data-ttu-id="085da-152">Выполните команды Service Fabric hello же соглашениями, что Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="085da-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="085da-153">Для получения справки по определенной команде или группы команд использовать hello `-h` флаг:</span><span class="sxs-lookup"><span data-stu-id="085da-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="085da-154">Вот еще один пример:</span><span class="sxs-lookup"><span data-stu-id="085da-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
