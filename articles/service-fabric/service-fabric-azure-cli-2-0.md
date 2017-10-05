---
title: "Начало работы с Azure Service Fabric и Azure CLI 2.0"
description: "Узнайте, как использовать команды модуля Service Fabric в Azure CLI версии 2.0 Узнайте, как подключится к кластеру и как управлять приложениями."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="2017c-104">Azure Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2017c-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="2017c-105">Интерфейс командной строки Azure (Azure CLI) версии 2.0 включает команды для управления кластерами Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2017c-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="2017c-106">Узнайте, как начать работу с Azure CLI и Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2017c-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="2017c-107">Установка Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2017c-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="2017c-108">Команды Azure CLI 2.0 можно использовать для взаимодействия с кластерами Service Fabric и управления ими.</span><span class="sxs-lookup"><span data-stu-id="2017c-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="2017c-109">Чтобы получить последнюю версию Azure CLI, следуйте [стандартному процессу установки Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2017c-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="2017c-110">Дополнительные сведения см. в [обзоре Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2017c-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="2017c-111">Синтаксис Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2017c-111">Azure CLI syntax</span></span>

<span data-ttu-id="2017c-112">Все команды Service Fabric в Azure CLI начинаются с префикса `az sf`.</span><span class="sxs-lookup"><span data-stu-id="2017c-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="2017c-113">Чтобы получить общие сведения о командах, которые можно применять, используйте `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="2017c-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="2017c-114">Для получения сведений об одной команде используйте `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="2017c-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="2017c-115">Команды Service Fabric в Azure CLI соответствуют такому шаблону именования:</span><span class="sxs-lookup"><span data-stu-id="2017c-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="2017c-116">Здесь `<object>` является целевым объектом для `<action>`.</span><span class="sxs-lookup"><span data-stu-id="2017c-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="2017c-117">Выбор кластера</span><span class="sxs-lookup"><span data-stu-id="2017c-117">Select a cluster</span></span>

<span data-ttu-id="2017c-118">Перед выполнением любых операций выберите кластер, к которому нужно подключиться.</span><span class="sxs-lookup"><span data-stu-id="2017c-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="2017c-119">В качестве примера ниже приведен код.</span><span class="sxs-lookup"><span data-stu-id="2017c-119">For an example, see the following code.</span></span> <span data-ttu-id="2017c-120">Код подключается к незащищенному кластеру.</span><span class="sxs-lookup"><span data-stu-id="2017c-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="2017c-121">Не используйте незащищенные кластеры Service Fabric в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2017c-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="2017c-122">Конечная точка кластера должна иметь префикс `http` или `https`.</span><span class="sxs-lookup"><span data-stu-id="2017c-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="2017c-123">Она должна включать порт для шлюза HTTP.</span><span class="sxs-lookup"><span data-stu-id="2017c-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="2017c-124">Этот порт и адрес аналогичны URL-адресу Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="2017c-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="2017c-125">Для кластеров, защищенных с помощью сертификата, можно использовать не зашифрованные PEM-файлы или CRT-файлы и KEY-файлы.</span><span class="sxs-lookup"><span data-stu-id="2017c-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="2017c-126">Например:</span><span class="sxs-lookup"><span data-stu-id="2017c-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="2017c-127">Дополнительные сведения см. в статье [Безопасное подключение к кластеру](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="2017c-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2017c-128">Команда `select` не обрабатывает запросы до возвращения.</span><span class="sxs-lookup"><span data-stu-id="2017c-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="2017c-129">Чтобы убедиться, что вы указали кластер правильно, используйте команды, аналогичные `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="2017c-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="2017c-130">Убедитесь, что команда не возвращает каких-либо ошибок.</span><span class="sxs-lookup"><span data-stu-id="2017c-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="2017c-131">Базовые операции</span><span class="sxs-lookup"><span data-stu-id="2017c-131">Basic operations</span></span>

<span data-ttu-id="2017c-132">Сведения о подключении кластера сохраняется между различными сеансами Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2017c-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="2017c-133">Выбрав кластер Service Fabric, можно выполнить любую команду Service Fabric в кластере.</span><span class="sxs-lookup"><span data-stu-id="2017c-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="2017c-134">Например, чтобы получить сведения о работоспособности кластера Service Fabric, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2017c-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="2017c-135">При условии, что в конфигурации Azure CLI указаны выходные данные JSON, будет получен следующий результат:</span><span class="sxs-lookup"><span data-stu-id="2017c-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="2017c-136">Рекомендации и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2017c-136">Tips and troubleshooting</span></span>

<span data-ttu-id="2017c-137">Следующие сведения могут оказаться полезными в случае возникновения проблем при использовании команд Service Fabric в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2017c-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="2017c-138">Преобразование сертификата PFX в формат PEM</span><span class="sxs-lookup"><span data-stu-id="2017c-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="2017c-139">Azure CLI поддерживает клиентские сертификаты, такие как PEM-файлы.</span><span class="sxs-lookup"><span data-stu-id="2017c-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="2017c-140">При использовании PFX-файлов из Windows эти сертификаты необходимо преобразовать в формат PEM.</span><span class="sxs-lookup"><span data-stu-id="2017c-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="2017c-141">Чтобы преобразовать PFX-файл в PEM-файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2017c-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="2017c-142">Дополнительные сведения см. в [документации по OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="2017c-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="2017c-143">Проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="2017c-143">Connection issues</span></span>

<span data-ttu-id="2017c-144">Некоторые операции могут создавать следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="2017c-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="2017c-145">Убедитесь, что указанная конечная точка кластера доступна и ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="2017c-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="2017c-146">Также проверьте, доступен ли для этого узла и порта пользовательский интерфейс Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="2017c-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="2017c-147">Обновите конечную точку с помощью `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="2017c-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="2017c-148">Подробные журналы</span><span class="sxs-lookup"><span data-stu-id="2017c-148">Detailed logs</span></span>

<span data-ttu-id="2017c-149">Подробные журналы часто полезны при отладке или при сообщении о проблеме.</span><span class="sxs-lookup"><span data-stu-id="2017c-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="2017c-150">В Azure CLI предусмотрен глобальный флаг `--debug`, повышающий уровень детализации файлов журналов.</span><span class="sxs-lookup"><span data-stu-id="2017c-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="2017c-151">Справка и синтаксис для команд</span><span class="sxs-lookup"><span data-stu-id="2017c-151">Command help and syntax</span></span>

<span data-ttu-id="2017c-152">Команды Service Fabric соответствуют тому же соглашению, что и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2017c-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="2017c-153">Для получения справки по определенной команде или группе команд используйте флаг `-h`:</span><span class="sxs-lookup"><span data-stu-id="2017c-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="2017c-154">Вот еще один пример:</span><span class="sxs-lookup"><span data-stu-id="2017c-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
