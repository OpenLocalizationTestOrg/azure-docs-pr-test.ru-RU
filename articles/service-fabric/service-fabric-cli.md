---
title: "aaaGet работы с Azure Service Fabric CLI (sfctl)"
description: "Узнайте, как toouse hello Azure Service Fabric CLI. Узнайте, как tooconnect tooa кластера и как toomanage приложений."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="91018-104">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="91018-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="91018-105">Hello Azure Service Fabric CLI (sfctl) — программа командной строки для взаимодействия и управления сущностями Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="91018-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="91018-106">Sfctl можно использовать с кластерами Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="91018-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="91018-107">Sfctl выполняется на любой платформе, поддерживающей Python.</span><span class="sxs-lookup"><span data-stu-id="91018-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91018-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="91018-108">Prerequisites</span></span>

<span data-ttu-id="91018-109">Предыдущий tooinstallation убедитесь, что в вашей среде есть python и pip установлен.</span><span class="sxs-lookup"><span data-stu-id="91018-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="91018-110">Дополнительные сведения, взгляните на hello [pip документации quickstart](https://pip.pypa.io/en/latest/quickstart/)и официальные [python установите документацию](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="91018-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="91018-111">Хотя оба python 2.7 и 3.6 поддерживаются, рекомендуется toouse python 3.6.</span><span class="sxs-lookup"><span data-stu-id="91018-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="91018-112">Установить</span><span class="sxs-lookup"><span data-stu-id="91018-112">Install</span></span>

<span data-ttu-id="91018-113">Hello Azure Service Fabric CLI (sfctl), представлена в виде пакета python.</span><span class="sxs-lookup"><span data-stu-id="91018-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="91018-114">tooinstall hello последнюю версию запуска:</span><span class="sxs-lookup"><span data-stu-id="91018-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="91018-115">После установки, выполните `sfctl -h` tooget сведения о доступных команд.</span><span class="sxs-lookup"><span data-stu-id="91018-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="91018-116">Синтаксис CLI</span><span class="sxs-lookup"><span data-stu-id="91018-116">CLI syntax</span></span>

<span data-ttu-id="91018-117">Команды всегда начинаются с префикса `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="91018-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="91018-118">Чтобы получить общие сведения о всех командах, которые можно применять, используйте `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="91018-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="91018-119">Для получения сведений об одной команде используйте `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="91018-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="91018-120">Выполните команды repeatable структуры, с целью hello hello команд выше команда hello или действие:</span><span class="sxs-lookup"><span data-stu-id="91018-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="91018-121">В этом примере `<object>` является целевым объектом hello `<action>`.</span><span class="sxs-lookup"><span data-stu-id="91018-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="91018-122">Выбор кластера</span><span class="sxs-lookup"><span data-stu-id="91018-122">Select a cluster</span></span>

<span data-ttu-id="91018-123">Прежде чем выполнять любые операции, необходимо выбрать tooconnect кластера для.</span><span class="sxs-lookup"><span data-stu-id="91018-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="91018-124">Выполните следующие tooselect hello и подключите toohello кластер с именем hello `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="91018-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="91018-125">Не используйте незащищенные кластеры Service Fabric в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="91018-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="91018-126">Конечная точка Hello кластера должен стоять `http` или `https`.</span><span class="sxs-lookup"><span data-stu-id="91018-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="91018-127">Она должна включать hello порт для шлюза hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="91018-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="91018-128">Hello порт и адрес hello равна hello Service Fabric Explorer URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="91018-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="91018-129">Для кластеров, защищенных с помощью сертификата, можно указать сертификат в кодировке PEM.</span><span class="sxs-lookup"><span data-stu-id="91018-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="91018-130">Hello сертификата можно указать как один файл или сертификат и пара ключей.</span><span class="sxs-lookup"><span data-stu-id="91018-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="91018-131">Дополнительные сведения см. в разделе [кластера Azure Service Fabric безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="91018-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="91018-132">Базовые операции</span><span class="sxs-lookup"><span data-stu-id="91018-132">Basic operations</span></span>

<span data-ttu-id="91018-133">Сведения о подключении кластера сохраняются между разными сеансами sfctl.</span><span class="sxs-lookup"><span data-stu-id="91018-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="91018-134">После выбора кластера Service Fabric, можно запустить любую команду Service Fabric на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="91018-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="91018-135">Например tooget hello состояние работоспособности кластера Service Fabric, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91018-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="91018-136">результаты выполнения команды Hello в hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91018-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="91018-137">Рекомендации и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="91018-137">Tips and troubleshooting</span></span>

<span data-ttu-id="91018-138">Некоторые рекомендации и советы по устранению распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="91018-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="91018-139">Преобразование из формата tooPEM PFX сертификата</span><span class="sxs-lookup"><span data-stu-id="91018-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="91018-140">Hello службы структуры CLI поддерживает клиентские сертификаты как PEM-файлы (с расширением .pem).</span><span class="sxs-lookup"><span data-stu-id="91018-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="91018-141">При использовании PFX-файлы из Windows, необходимо преобразовать формат tooPEM этих сертификатов.</span><span class="sxs-lookup"><span data-stu-id="91018-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="91018-142">tooconvert PEM tooa файл PFX-файла, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91018-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="91018-143">Дополнительные сведения см. в разделе hello [OpenSSL документации](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="91018-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="91018-144">Проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="91018-144">Connection issues</span></span>

<span data-ttu-id="91018-145">Некоторые операции могут создавать hello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="91018-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="91018-146">Убедитесь, что указан hello, что конечные точки кластера доступен и прослушивания.</span><span class="sxs-lookup"><span data-stu-id="91018-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="91018-147">Кроме того убедитесь, что приветствия пользовательский Интерфейс обозревателя Service Fabric доступен на, узла и порта.</span><span class="sxs-lookup"><span data-stu-id="91018-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="91018-148">hello tooupdate конечной точки, используйте `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="91018-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="91018-149">Подробные журналы</span><span class="sxs-lookup"><span data-stu-id="91018-149">Detailed logs</span></span>

<span data-ttu-id="91018-150">Подробные журналы часто полезны при отладке или при сообщении о проблеме.</span><span class="sxs-lookup"><span data-stu-id="91018-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="91018-151">Имеется глобальный `--debug` флаг, который повышает уровень детализации hello файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="91018-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="91018-152">Справка и синтаксис для команд</span><span class="sxs-lookup"><span data-stu-id="91018-152">Command help and syntax</span></span>

<span data-ttu-id="91018-153">Для получения справки по определенной команде или группы команд использовать hello `-h` флаг:</span><span class="sxs-lookup"><span data-stu-id="91018-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="91018-154">Другой пример:</span><span class="sxs-lookup"><span data-stu-id="91018-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="91018-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91018-155">Next steps</span></span>

* [<span data-ttu-id="91018-156">Развертывание приложения с hello Azure Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="91018-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* <span data-ttu-id="91018-157">[Prepare your development environment on Linux](service-fabric-get-started-linux.md) (Подготовка среды разработки в Linux)</span><span class="sxs-lookup"><span data-stu-id="91018-157">[Get started with Service Fabric on Linux](service-fabric-get-started-linux.md)</span></span>
