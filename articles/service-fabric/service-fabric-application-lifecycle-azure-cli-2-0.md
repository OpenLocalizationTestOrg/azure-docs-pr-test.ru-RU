---
title: "приложения Azure Service Fabric aaaManage, с помощью Azure CLI 2.0"
description: "Узнайте, как toodeploy и удаление приложений с Azure Service Fabric кластера с помощью Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Управление приложением Azure Service Fabric с помощью Azure CLI 2.0

Узнайте, как toocreate и удаление приложений, работающих в кластере Azure Service Fabric.

## <a name="prerequisites"></a>Предварительные требования

* Установите Azure CLI 2.0 и выберите кластер Service Fabric. Дополнительные сведения можно найти в документации по [началу работы с Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

* У Service Fabric приложения пакет готов toobe развертывания. Дополнительные сведения о том, как tooauthor и пакет приложения, узнайте, как hello [модель приложения Service Fabric](service-fabric-application-model.md).

## <a name="overview"></a>Обзор

toodeploy нового приложения, выполните следующие действия.

1. Отправка образа хранилища Service Fabric toohello пакета приложений.
2. Подготовьте тип приложения.
3. Укажите приложение и создайте его.
4. Укажите службы и создайте их.

tooremove существующего приложения, выполните следующие действия.

1. Удаление приложения hello.
2. Отключение hello связанный тип приложения.
3. Удаляет содержимое хранилища hello изображения.

## <a name="deploy-a-new-application"></a>Развертывание нового приложения

toodeploy нового приложения, завершения hello следующие задачи.

### <a name="upload-a-new-application-package-toohello-image-store"></a>Отправить новый образ хранилище toohello приложения пакета

Прежде чем создавать приложения, отправьте изображение хранилище Service Fabric toohello hello приложения пакета. 

Например, если пакет приложения hello `app_package_dir` directory hello используйте следующие команды tooupload hello каталога:

```azurecli
az sf application upload --path ~/app_package_dir
```

Для больших пакетов приложений, вы можете указать hello `--show-progress` параметр toodisplay hello ход выполнения передачи hello.

### <a name="provision-hello-application-type"></a>Тип приложения hello подготовки

После завершения передачи hello подготовить приложение hello. приложение hello tooprovision, hello используйте следующую команду:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Здравствуйте, значение для `application-type-build-path` — имя hello hello каталога, где загруженный пакет приложения.

### <a name="create-an-application-from-an-application-type"></a>Создание приложения из типа приложения

После их инициализации приложения hello, используйте следующие команды tooname hello и создания приложения:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`— Имя hello, что требуется toouse для экземпляра приложения hello. Дополнительные параметры можно получить из манифеста предварительно подготовленные приложения hello.

Имя приложения Hello должно начинаться с префикса hello `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Создание служб для нового приложения hello

После создания приложения можно создайте службы из приложения hello. В следующем примере hello создадим новый без отслеживания состояния службы из нашего приложения. Hello служб, которые можно создать из приложения, определенные в манифест службы в пакет предварительно подготовленные приложения hello.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Проверка развертывания и работоспособности приложения

tooverify, что приложения и службы были успешно развернуты, проверьте, указаны hello приложения и службы:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

tooverify, что служба hello находится в работоспособном состоянии, используйте аналогичные команды tooretrieve hello работоспособности hello службы и приложения hello.

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Параметр `HealthState` работоспособных служб и приложений должен иметь значение `Ok`.

## <a name="remove-an-existing-application"></a>Удаление имеющегося приложения

tooremove приложения, завершения hello следующие задачи.

### <a name="delete-hello-application"></a>Удаление приложения hello

приложение hello toodelete, hello используйте следующую команду:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Отменить подготовку типа приложения hello

После удаления приложения hello, можно отменить подготовку типа приложения hello, если оно больше не требуется. Тип приложения hello toounprovision, hello используйте следующую команду:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

версия по имени и типа тип Hello должна соответствовать hello имени и версии в манифесте предварительно подготовленные приложения hello.

### <a name="delete-hello-application-package"></a>Удалить пакет приложения hello

После отменил инициализацию типа приложения hello, можно удалить пакет приложения hello из хранилища образов hello, если оно больше не требуется. Удалите пакеты приложения, чтобы освободить место на диске. 

пакет приложения hello toodelete из хранилища образов hello, hello используйте следующую команду:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`должно быть именем hello hello каталога, который загружен при создании приложения hello.

## <a name="related-articles"></a>Связанные статьи

* [Service Fabric и Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Использование интерфейса командной строки Azure для взаимодействия с кластером Service Fabric](service-fabric-azure-cli.md)
