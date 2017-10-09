---
title: "Общие сведения об экземпляре метаданных службы aaaAzure | Документы Microsoft"
description: "Интерфейс rESTful tooget сведения о Виртуальных машин вычислительных, сети и предстоящем обслуживании события."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a>Служба метаданных экземпляров Azure 


Hello служба метаданных экземпляра Azure предоставляет сведения о выполнении экземпляров виртуальных машин, которые можно использовать toomanage и настроить виртуальные машины.
Сюда входят сведения о номере SKU, конфигурации сети и ближайших мероприятиях обслуживания. Дополнительные сведения о том, какие сведения доступны, см. в разделе [Категории данных метаданных экземпляров](#instance-metadata-data-categories).

Служба метаданных экземпляра Azure является конечной точкой REST, доступный tooall ВМ IaaS, созданные при помощи hello [диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/). Hello конечная точка доступна по хорошо известных немаршрутизируемый IP-адрес (`169.254.169.254`), можно обратиться только из hello виртуальной Машины.

### <a name="important-information"></a>Важные сведения

Эта служба является **общедоступной** в глобальных регионах Azure. Она находится в общедоступной предварительной версии для государственных организаций, облачной службы Azure для Китая и Германии. Регулярно, он получает обновления tooexpose новые сведения об экземплярах виртуальной машины. Эта страница отражает hello актуальные [категории данных](#instance-metadata-data-categories) доступны.

## <a name="service-availability"></a>Доступность службы
Служба Hello доступна во всех регионах общедоступной глобального Azure. Hello служба находится в общедоступной предварительной версии в регионах hello государственных организаций, Китай или Германии.

регионы                                        | Доступность?
-----------------------------------------------|-----------------------------------------------
[Все общедоступные глобальные регионы Azure](https://azure.microsoft.com/en-us/regions/)     | Общедоступная версия 
[Azure для государственных организаций](https://azure.microsoft.com/en-us/overview/clouds/government/)              | В предварительной версии 
[Azure для Китая](https://www.azure.cn/)                                                           | В предварительной версии
[Azure для Германии](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | В предварительной версии

Эта таблица обновляется, когда служба hello станет доступным в других облаках, Azure.

tootry out hello экземпляр метаданных службы, создайте виртуальную Машину из [диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/) или hello [портал Azure](http://portal.azure.com) в hello выше области и выполните hello примеры ниже.

## <a name="usage"></a>Использование

### <a name="versioning"></a>Управление версиями
Hello метаданных экземпляра службы с версиями. Версии являются обязательными, и текущая версия hello `2017-04-02`.

> [!NOTE] 
> Предыдущие выпуски Предварительный просмотр поддерживается {последние} в качестве hello api-version запланированные события. Этот формат не поддерживается и будет считаться устаревшей в будущем hello.

Так как мы добавляем новые версии, вы все еще можете получить доступ к предыдущим версиям для обеспечения совместимости, если используемый скрипт зависит от конкретных форматов данных. Однако обратите внимание, что этой version(2017-03-01) hello текущего предварительного просмотра может оказаться недоступным после общедоступной службы hello.

### <a name="using-headers"></a>Использование заголовков
При запросе hello экземпляр метаданных службы, необходимо указать заголовок hello `Metadata: true` tooensure hello запрос не был перенаправлен непреднамеренно.

### <a name="retrieving-metadata"></a>Получение метаданных

Используйте метаданные экземпляров для запуска виртуальных машин, созданных или управляемых с помощью [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Доступ к все категории данных для экземпляра виртуальной машины с помощью hello, следующий запрос:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Во всех запросах метаданных экземпляров учитывается регистр.

### <a name="data-output"></a>Выходные данные
По умолчанию hello метаданных экземпляра службы возвращает данные в формате JSON (`Content-Type: application/json`). Однако при необходимости другие API-интерфейсы могут возвращать данные в различных форматах.
Hello Следующая таблица представляет ссылки из других форматов данных, которые API-интерфейсы могут поддерживать.

API | Формат данных по умолчанию | Другие форматы
--------|---------------------|--------------
/instance | json | text
/scheduledevents | json | Нет

tooaccess формата ответа не по умолчанию, укажите запрошенный формат hello в качестве параметра строки запроса в запросе hello. Например:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Безопасность
Конечная точка службы метаданных экземпляра Hello доступна только из hello ОС немаршрутизируемый IP-адрес экземпляра виртуальной машины. Кроме того, любой запрос с `X-Forwarded-For` заголовок, отклоняется службой hello.
Мы также требуется toocontain запросы `Metadata: true` tooensure заголовок, hello сам запрос непосредственно было предназначено и не является частью непреднамеренного перенаправления. 

### <a name="error"></a>Ошибка
Если элемент данных не найден или имеет неправильный формат запроса hello метаданных экземпляра службы возвращает стандартные ошибки HTTP. Например:

Код состояния HTTP | Причина
----------------|-------
200 ОК |
400 — недопустимый запрос | Отсутствует заголовок `Metadata: true`
404 — не найдено | Hello does't запрошенный элемент существует 
405 — недопустимый метод | Поддерживаются только запросы `GET` и `POST`
429 — слишком много запросов | Hello API в настоящее время поддерживает не более 5 запросов в секунду
500 — ошибка службы     | Повторите попытку через некоторое время

### <a name="examples"></a>Примеры

> [!NOTE] 
> Все ответы API — это строки в формате JSON. Все следующие примеры ответов представлены в удобном для чтения формате.

#### <a name="retrieving-network-information"></a>Получение сведений о сети

**Запрос**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Ответ**

> [!NOTE] 
> Hello ответа представляет собой строку JSON. Следующий пример ответа Hello, представленное для удобства чтения.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Получение общедоступного IP-адреса

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Получение всех метаданных для экземпляра

**Запрос**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Ответ**

> [!NOTE] 
> Hello ответа представляет собой строку JSON. Следующий пример ответа Hello, представленное для удобства чтения.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Получение метаданных в виртуальной машине Windows

**Запрос**

Можно получить метаданные экземпляра в Windows через PowerShell программа hello `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Или с помощью hello `Invoke-RestMethod` командлета:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Ответ**

> [!NOTE] 
> Hello ответа представляет собой строку JSON. Следующий пример ответа Hello, представленное для удобства чтения.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Категории данных метаданных экземпляров
Привет, следующие категории данных доступны через hello экземпляр службы метаданных:

Данные | Описание
-----|------------
location | Hello Azure области ВМ работает
name | Имя виртуальной Машины hello 
offer | Предоставляют сведения для hello образа виртуальной Машины. Это значение доступно только для образов, развернутых из коллекции образов Azure.
publisher | Издатель образа ВМ hello
sku | Конфигурации для образа виртуальной Машины hello  
версия | Версия образа виртуальной Машины hello 
osType | Linux или Windows 
platformUpdateDomain |  [Домен обновления](virtual-machines-windows-manage-availability.md) hello в запущенной виртуальной Машине
platformFaultDomain | [Домен сбоя](virtual-machines-windows-manage-availability.md) hello в запущенной виртуальной Машине
vmId | [Уникальный идентификатор](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) для hello виртуальной Машины
vmSize | [Размер виртуальной машины](virtual-machines-windows-sizes.md)
ipv4/privateIpAddress | Локальный адрес IPv4 hello виртуальной Машины 
ipv4/publicIpAddress | Общедоступный адрес IPv4 hello виртуальной Машины
subnet/address | Адрес подсети hello виртуальной Машины
subnet/prefix | Префикс подсети, пример 24
ipv6/ipAddress | Локальный адрес IPv6 hello виртуальной Машины
macAddress | Mac-адрес виртуальной машины 
scheduledevents | Сейчас в общедоступной предварительной версии. Дополнительные сведения см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия)](virtual-machines-scheduled-events.md).

## <a name="example-scenarios-for-usage"></a>Примеры сценариев использования  

### <a name="tracking-vm-running-on-azure"></a>Отслеживание виртуальной машины в Azure

Как поставщик услуг может потребоваться tootrack hello число работающих виртуальных машин программного обеспечения или агентами, которые должны tootrack уникальность hello виртуальной Машины. возможности tooget toobe уникальный идентификатор для виртуальной Машины, используйте hello `vmId` из метаданных службы экземпляра.

**Запрос**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Ответ**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Размещение контейнеров и секций данных на основе домена сбоя или обновления 

В некоторых сценариях размещение разных реплик имеет первостепенное значение. Например [размещения реплики HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) или размещения контейнера через [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) может потребоваться tooknow hello `platformFaultDomain` и `platformUpdateDomain` hello, Виртуальная машина работает на.
Вы можете запрашивать эти данные напрямую через hello экземпляр метаданных службы.

**Запрос**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Ответ**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Получение дополнительных сведений о hello виртуальной Машины во время службу технической поддержки Майкрософт 

Как поставщик услуг то появляется поддержки по телефону куда tooknow Дополнительные сведения о hello виртуальной Машины. Запрос клиента tooshare hello hello вычислений метаданных может предоставить основные сведения для специалистов tooknow поддержки hello о hello типа ВМ в Azure. 

**Запрос**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Ответ**

> [!NOTE] 
> Hello ответа представляет собой строку JSON. Следующий пример ответа Hello, представленное для удобства чтения.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Примеры вызова метаданные службы с использованием различных языков внутри hello виртуальной Машины 

Язык | Пример 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Перейдите в локальную сеть   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
JavaScript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>Часто задаваемые вопросы
1. Я получаю hello ошибки `400 Bad Request, Required metadata header not specified`. Что это означает?
   * Hello служба метаданных экземпляра требуется заголовок hello `Metadata: true` toobe переданный запрос hello. Передача этого заголовка в вызове REST hello позволяет toohello доступ службы метаданных экземпляра. 
2. Почему я не получаю сведения о вычислениях для виртуальной машины?
   * Hello экземпляр метаданных службы, в настоящее время поддерживает только экземпляры, созданные с помощью диспетчера ресурсов Azure. В будущем hello Корпорация Майкрософт может расширить поддержку виртуальных машин облачной службы.
3. Виртуальная машина была недавно создана с помощью Azure Resource Manager. Почему не отображаются сведения о метаданных вычислений?
   * Все виртуальные машины, созданные после сентября 2016, добавьте [тега](../azure-resource-manager/resource-group-using-tags.md) toostart просматривают метаданные вычислений. Для более старых виртуальных машин (создан до сентября 2016) Добавление и удаление расширения или данных метаданных toorefresh дисков toohello виртуальной Машины.
4. Почему выдается ошибка hello `500 Internal Server Error`?
   * Повторите запрос в зависимости от экспоненциальной системы. Если hello проблема повторится, обратитесь в службу поддержки Azure.
5. Где можно задать дополнительные вопросы или оставить комментарии?
   * Оставьте комментарии на сайте http://feedback.azure.com.
7. Будет ли это работать для экземпляра масштабируемого набора виртуальных машин?
   * Да, служба метаданных доступна для экземпляров масштабируемого набора. 
6. Получение поддержки для службы hello
   * tooget поддержка hello службы, создайте возникшей проблемы на портале Azure для виртуальной Машины, где вы не может tooget ответа метаданных после нескольких попыток long hello 

   ![Поддержка метаданных экземпляров](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о hello [scheduledevents](virtual-machines-scheduled-events.md) API **в общедоступной предварительной версии** предоставляемые hello экземпляр метаданных службы.
