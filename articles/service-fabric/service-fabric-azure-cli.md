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
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Использование hello toointeract XPlat-CLI с кластера Service Fabric

Вы можете взаимодействовать с кластером Service Fabric с компьютеров Linux с помощью hello XPlat-CLI в Linux.

Hello первый шаг получить последнюю версию hello hello CLI из hello git rep и набор его в пути с помощью hello, следующие команды:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Для каждой команды он поддерживает, можно ввести имя hello tooobtain hello hello команду справки для этой команды.
Для команды hello поддерживается функция автозавершения. Например следующая команда позволяет справки для всех команд приложения hello hello. 

```sh
 azure servicefabric application 
```

Можно отфильтровать hello справки tooa конкретной команды, как следующий пример показывает hello:

```sh
 azure servicefabric application  create
```

tooenable автоматическое заполнение в hello CLI, запустите hello, следующие команды:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

следующие команды Hello соединения кластера toohello Показать hello узлов в кластере hello:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse именованных параметров и найти их, можно ввести — помочь после команды. Например:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

При подключении нескольких машин кластера tooa на машине **, не является частью кластера hello**, использовать hello следующую команду:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Замените тег PublicIPorFQDN hello hello реальные IP-адрес или полное доменное имя соответствующим образом. При подключении нескольких машин кластера tooa на машине **, являющийся частью кластера hello**, использовать hello следующую команду:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Можно использовать PowerShell или создать toointeract CLI с вашего кластера Service Fabric Linux с помощью hello портал Azure.

> [!WARNING]
> Эти кластеры незащищенные, таким образом, вы может открыть один-поле путем добавления hello общедоступный IP-адрес в манифесте кластера hello.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>С помощью hello кластера Service Fabric tooa tooconnect XPlat-CLI

следующие команды Azure CLI Hello описывают, как tooconnect tooa обеспечивать безопасность кластера. сведения о сертификате Hello должно соответствовать сертификат на узлах кластера hello.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Если сертификат имеет центров сертификации (ЦС), необходимо параметр--ЦС cert путь к hello tooadd как следующий пример hello. 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Если у вас есть несколько центров сертификации, используйте запятую в качестве разделителя hello.

Если ваш общее имя в сертификате hello не соответствует hello конечной точки подключения, можно использовать параметр hello `--strict-ssl-false` toobypass hello проверки, как показано в hello следующую команду:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

При желании проверки tooskip hello ЦС, можно добавить hello--параметр отклонить, доступ запрещен ЛОЖЬ, как показано в hello следующую команду: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

После подключения должен быть доступ toorun других toointeract команд CLI с hello кластера.

## <a name="deploying-your-service-fabric-application"></a>Развертывание приложения Service Fabric

Выполните следующие команды toocopy, зарегистрировать и запустить приложение service fabric hello hello:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Обновление приложения

Hello выполняется аналогично toohello [процесса в Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Выполняйте сборку, копирование, регистрацию и создание приложения в корневом каталоге проекта. Если именованный экземпляр приложения `fabric:/MySFApp`и тип hello MySFApp, hello команды будет выглядеть следующим образом:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Сделайте hello tooyour применение изменений и заново создайте hello изменения службы.  Обновление hello изменить службы файл манифеста (ServiceManifest.xml) с версиями hello обновлен для hello службы (и кода или конфигурации или данных соответствующим образом). Также изменить манифест приложения hello (ApplicationManifest.xml) с hello обновить номер версии для приложения hello и hello измененные службы.  Теперь скопировать и зарегистрировать обновленные приложения с помощью hello, следующие команды:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Теперь можно начать обновление приложения hello с hello следующую команду:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Теперь можно отслеживать с помощью SFX обновление приложения hello. Через несколько минут hello приложения будут обновлены. Также попробуйте обновленные приложения с ошибкой и проверьте возможность отката автоматически hello в service fabric.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>Преобразование из PFX tooPEM и наоборот

Может потребоваться tooinstall сертификат в ваш локальный компьютер (с Windows или Linux) tooaccess защищенных кластеров, в другой среде. Например при доступе к защищенным кластеров Linux с компьютером Windows и наоборот нужно tooconvert сертификата из PFX-ФАЙЛ tooPEM и наоборот. 

tooconvert из PEM файл tooa PFX-файла, hello используйте следующую команду:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert из файла PEM tooa файла PFX, hello используйте следующую команду:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

См. слишком[OpenSSL документации](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) подробные сведения.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Устранение неполадок


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Копирование пакета приложения hello завершилась с ошибками

Проверьте, установлен ли клиент `openssh`. Так как по умолчанию он отсутствует в Ubuntu Desktop, Установите его с помощью hello следующую команду:

```sh
sudo apt-get install openssh-server openssh-client**
```

При повторном возникновении проблемы hello, попробуйте отключить PAM для ssh, изменив hello `sshd_config` файла с помощью hello, следующие команды:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Если hello проблема сохраняется, попробуйте использовать hello увеличивающихся ssh сеансы, выполнив следующие команды hello.

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

С помощью ключей для ssh проверки подлинности (как противоположность toopasswords) еще не поддерживается (поскольку hello платформа использует ssh toocopy пакетов), поэтому вместо этого используйте пароль проверки подлинности.

## <a name="next-steps"></a>Дальнейшие действия

[Настройка среды разработки hello и развертывание кластера Service Fabric tooa приложения Linux.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Связанные статьи

* [Service Fabric и Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
