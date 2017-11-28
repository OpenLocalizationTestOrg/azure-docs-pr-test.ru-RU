---
title: "Начало работы с интерфейсом командной строки Azure Service Fabric (sfctl)"
description: "Сведения об использовании интерфейса командной строки Azure Service Fabric. Узнайте, как подключится к кластеру и как управлять приложениями."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: 5ce9adf6c82e3a5521883c5de1e0689d5bf0d94e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="506a7-104">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="506a7-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="506a7-105">Интерфейс командной строки Azure Service Fabric (sfctl) — служебная программа командной строки для взаимодействия с сущностями Azure Service Fabric и управления ими.</span><span class="sxs-lookup"><span data-stu-id="506a7-105">The Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="506a7-106">Sfctl можно использовать с кластерами Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="506a7-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="506a7-107">Sfctl выполняется на любой платформе, поддерживающей Python.</span><span class="sxs-lookup"><span data-stu-id="506a7-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="506a7-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="506a7-108">Prerequisites</span></span>

<span data-ttu-id="506a7-109">Прежде чем начать установку убедитесь, что в вашей среде установлены Python и PIP.</span><span class="sxs-lookup"><span data-stu-id="506a7-109">Prior to installation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="506a7-110">Дополнительные сведения см. в [кратком руководстве по началу работы с PIP](https://pip.pypa.io/en/latest/quickstart/) и официальной [документации по установке Python](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="506a7-110">For more information, take a look at the [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="506a7-111">Хотя поддерживается Python версий 2.7 и 3.6, рекомендуется использовать Python 3.6.</span><span class="sxs-lookup"><span data-stu-id="506a7-111">While both python 2.7 and 3.6 are supported, it is recommended to use python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="506a7-112">Установить</span><span class="sxs-lookup"><span data-stu-id="506a7-112">Install</span></span>

<span data-ttu-id="506a7-113">Интерфейс командной строки Azure Service Fabric представлен в виде пакета Python.</span><span class="sxs-lookup"><span data-stu-id="506a7-113">The Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="506a7-114">Чтобы установить последнюю версию, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="506a7-114">To install the latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="506a7-115">После установки выполните команду `sfctl -h`, чтобы получить сведения о доступных командах.</span><span class="sxs-lookup"><span data-stu-id="506a7-115">After installation, run `sfctl -h` to get information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="506a7-116">Синтаксис CLI</span><span class="sxs-lookup"><span data-stu-id="506a7-116">CLI syntax</span></span>

<span data-ttu-id="506a7-117">Команды всегда начинаются с префикса `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="506a7-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="506a7-118">Чтобы получить общие сведения о всех командах, которые можно применять, используйте `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="506a7-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="506a7-119">Для получения сведений об одной команде используйте `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="506a7-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="506a7-120">Команды подчиняются повторяющейся структуре, где целевой объект команды стоит перед командой (глаголом) или действием.</span><span class="sxs-lookup"><span data-stu-id="506a7-120">Commands follow a repeatable structure, with the target of the command preceding the verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="506a7-121">В этом примере `<object>` — целевой объект для `<action>`.</span><span class="sxs-lookup"><span data-stu-id="506a7-121">In this example, `<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="506a7-122">Выбор кластера</span><span class="sxs-lookup"><span data-stu-id="506a7-122">Select a cluster</span></span>

<span data-ttu-id="506a7-123">Перед выполнением любых операций выберите кластер, к которому нужно подключиться.</span><span class="sxs-lookup"><span data-stu-id="506a7-123">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="506a7-124">Например, выполните следующую команду, чтобы выбрать кластер `testcluster.com` и подключиться к нему.</span><span class="sxs-lookup"><span data-stu-id="506a7-124">For example, run the following to select and connect to the cluster with the name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="506a7-125">Не используйте незащищенные кластеры Service Fabric в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="506a7-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="506a7-126">Конечная точка кластера должна иметь префикс `http` или `https`.</span><span class="sxs-lookup"><span data-stu-id="506a7-126">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="506a7-127">Она должна включать порт для шлюза HTTP.</span><span class="sxs-lookup"><span data-stu-id="506a7-127">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="506a7-128">Этот порт и адрес аналогичны URL-адресу Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="506a7-128">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="506a7-129">Для кластеров, защищенных с помощью сертификата, можно указать сертификат в кодировке PEM.</span><span class="sxs-lookup"><span data-stu-id="506a7-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="506a7-130">Сертификат можно указать как один файл или как пару "сертификат — ключ".</span><span class="sxs-lookup"><span data-stu-id="506a7-130">The certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="506a7-131">Дополнительные сведения см. в статье [Безопасное подключение к кластеру](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="506a7-131">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="506a7-132">Базовые операции</span><span class="sxs-lookup"><span data-stu-id="506a7-132">Basic operations</span></span>

<span data-ttu-id="506a7-133">Сведения о подключении кластера сохраняются между разными сеансами sfctl.</span><span class="sxs-lookup"><span data-stu-id="506a7-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="506a7-134">Выбрав кластер Service Fabric, можно выполнить любую команду Service Fabric в кластере.</span><span class="sxs-lookup"><span data-stu-id="506a7-134">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="506a7-135">Например, чтобы получить сведения о работоспособности кластера Service Fabric, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="506a7-135">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="506a7-136">Результаты команды должны быть следующими:</span><span class="sxs-lookup"><span data-stu-id="506a7-136">The command results in the following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="506a7-137">Рекомендации и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="506a7-137">Tips and troubleshooting</span></span>

<span data-ttu-id="506a7-138">Некоторые рекомендации и советы по устранению распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="506a7-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="506a7-139">Преобразование сертификата PFX в формат PEM</span><span class="sxs-lookup"><span data-stu-id="506a7-139">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="506a7-140">Интерфейс командной строки Service Fabric поддерживает клиентские сертификаты, такие как PEM-файлы.</span><span class="sxs-lookup"><span data-stu-id="506a7-140">The Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="506a7-141">При использовании PFX-файлов из Windows эти сертификаты необходимо преобразовать в формат PEM.</span><span class="sxs-lookup"><span data-stu-id="506a7-141">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="506a7-142">Чтобы преобразовать PFX-файл в PEM-файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="506a7-142">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="506a7-143">Дополнительные сведения см. в [документации по OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="506a7-143">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="506a7-144">Проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="506a7-144">Connection issues</span></span>

<span data-ttu-id="506a7-145">Некоторые операции могут создавать следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="506a7-145">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="506a7-146">Убедитесь, что указанная конечная точка кластера доступна и ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="506a7-146">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="506a7-147">Также проверьте, доступен ли для этого узла и порта пользовательский интерфейс Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="506a7-147">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="506a7-148">Обновите конечную точку с помощью `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="506a7-148">To update the endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="506a7-149">Подробные журналы</span><span class="sxs-lookup"><span data-stu-id="506a7-149">Detailed logs</span></span>

<span data-ttu-id="506a7-150">Подробные журналы часто полезны при отладке или при сообщении о проблеме.</span><span class="sxs-lookup"><span data-stu-id="506a7-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="506a7-151">В интерфейсе командной строки Service Fabric предусмотрен глобальный флаг `--debug`, повышающий уровень детализации файлов журналов.</span><span class="sxs-lookup"><span data-stu-id="506a7-151">There is a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="506a7-152">Справка и синтаксис для команд</span><span class="sxs-lookup"><span data-stu-id="506a7-152">Command help and syntax</span></span>

<span data-ttu-id="506a7-153">Для получения справки по определенной команде или группе команд используйте флаг `-h`:</span><span class="sxs-lookup"><span data-stu-id="506a7-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="506a7-154">Другой пример:</span><span class="sxs-lookup"><span data-stu-id="506a7-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="506a7-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="506a7-155">Next steps</span></span>

* <span data-ttu-id="506a7-156">[Manage an Azure Service Fabric application by using Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) (Управление приложением Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="506a7-156">[Deploy an application with the Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md)</span></span>
* <span data-ttu-id="506a7-157">[Prepare your development environment on Linux](service-fabric-get-started-linux.md) (Подготовка среды разработки в Linux)</span><span class="sxs-lookup"><span data-stu-id="506a7-157">[Get started with Service Fabric on Linux](service-fabric-get-started-linux.md)</span></span>
