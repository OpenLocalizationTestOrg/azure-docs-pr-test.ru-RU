---
title: "aaaPass сложных значений между шаблоны Azure | Документы Microsoft"
description: "Отображает рекомендуется подходов к использованию данных о состоянии tooshare сложные объекты с помощью шаблонов диспетчера ресурсов Azure и связанных шаблонов."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Tooand состояния общего ресурса на основе шаблонов диспетчера ресурсов Azure
В этой статье приводятся рекомендации по управлению и совместному использованию состояния в шаблонах. Hello параметры и переменные, приведенные в этом разделе приведены примеры hello типов объектов, можно определить tooconveniently организовать требований к развертыванию. На основе этих примеров можно реализовать собственные объекты со значениями свойств, которые имеют смысл для вашей среды.

Данная тема является частью другого технического документа. загрузить полной бумага hello tooread [вопросы World класс ресурса диспетчера шаблонов и проверенные методики](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Указание стандартных параметров конфигурации
А не реализует шаблон, который обеспечивает общее гибкость и множество вариантов, распространенный подход заключается в tooprovide набора известных конфигураций. Фактически размеры песочницы определяются по аналогии со стандартными размерами футболки (малый, средний и большой). Другие примеры использования этого подхода включают такие продукты, как Community Edition или Enterprise Edition. Другие случаи могут быть представлены конфигурациями технологий, зависящими от рабочей нагрузки, включая решения Map/Reduce или NoSQL.

С сложные объекты можно создать переменные, содержащие наборы данных, которую иногда называют «контейнеры свойств» и использовать ресурс объявления hello этого toodrive данных в шаблон. Такой подход позволяет использовать хорошие и известные конфигурации разных размеров, предварительно настроенные для клиентов. Без известной конфигурации пользователей hello шаблона необходимо определить изменения размера кластера на собственные, фактором ограничения ресурсов платформы и выполнять математические tooidentify hello возникающие секционирование учетные записи хранения и другие ресурсы (из-за размера toocluster и ограничения ресурсов). Кроме toomaking для повышения удобства для клиента hello несколько известных конфигураций, проще toosupport и может помочь вам предоставлять более высокий уровень плотности.

Следующий пример показывает как Hello toodefine переменных, содержащих сложные объекты для представления коллекции данных. коллекции Hello определяют значения, используемые для размера виртуальной машины, параметры сети, параметры операционной системы и доступности.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

Обратите внимание, что hello **tshirtSize** переменной Сцепляет hello размер футболки, предоставляемые через параметр (**небольшой**, **Средний**, **большой**) текст toohello **tshirtSize**. Эта переменная связанного сложный объект переменной tooretrieve hello используется для такой размер футболки.

Затем можно ссылаться на эти переменные позже в шаблоне hello. Hello возможность tooreference с именем переменных и их свойства упрощает синтаксис шаблона hello и делает его легко toounderstand контекста. Следующий пример Hello определяет toodeploy ресурсов с помощью объектов hello, показанному ранее tooset значения. Например, hello размер виртуальной Машины будет задано, получая значение hello `variables('tshirtSize').vmSize` while hello значение для hello места на диске, извлекается из `variables('tshirtSize').diskSize`. Кроме того, hello URI для связанного шаблона задается значением hello для `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Передать состояние tooa шаблона
Общий доступ к состоянию в шаблоне предоставляется с помощью параметров, которые вы указываете во время развертывания.

Здравствуйте, следуя таблице перечислены часто используемые параметры в шаблонах.

| Имя | Значение | Описание |
| --- | --- | --- |
| location |Строка из ограниченного списка регионов Azure |Hello расположение, где развернуты ресурсы hello. |
| storageAccountNamePrefix |Строка |Уникальное имя DNS для учетной записи хранилища, там, где размещены диски ВМ hello hello |
| domainName |Строка |Имя домена общедоступный jumpbox hello виртуальной Машины в формате hello: **{domainName}. {} расположение}.cloudapp.com** пример: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |Строка |Имя пользователя для hello виртуальные машины |
| adminPassword |Строка |Пароль для hello виртуальные машины |
| tshirtSize |Строка из ограниченного списка предлагаемых размеров |Здравствуйте, с именем tooprovision размер единицы масштабирования. Например, Small, Medium, Large |
| virtualNetworkName |Строка |Имя виртуальной сети hello, hello потребитель хочет toouse. |
| enableJumpbox |Строка из ограниченного списка (enabled, disabled) |Параметр, определяющий ли tooenable jumpbox для hello среды. Значения: enabled, disabled |

Hello **tshirtSize** параметр, используемый в предыдущем разделе hello определяется как:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Передать состояние toolinked шаблонов
При подключении toolinked шаблоны, часто использовать как статический, созданные переменные.

### <a name="static-variables"></a>Статические переменные
Статические переменные чаще используется tooprovide базового значения, такие как URL-адреса, которые используются в шаблоне.

В следующий фрагмент шаблона hello `templateBaseUrl` указывает hello корневой путь для шаблона hello в GitHub. Следующая строка Hello создает новую переменную `sharedTemplateUrl` , объединяет hello базовый URL-адрес с известным именем hello hello общих ресурсов шаблона. Ниже этой линии сложный объект переменной находится используется toostore размер футболки, базовый URL-адрес hello сцепленные toohello известно расположение шаблонов конфигурации и хранятся в hello `vmTemplate` свойство.

Преимущество этого подхода Hello —, если изменяется расположение шаблонов hello, достаточно лишь toochange hello статической переменной в одном месте, который передает его на протяжении hello связанных шаблонов.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Создаваемые переменные
В переменных toostatic сложения динамически создаются несколько переменных. В этом разделе определяет некоторые из распространенных типов hello созданный переменных.

#### <a name="tshirtsize"></a>tshirtSize
Вы знакомы с этой переменной, созданный из вышеприведенных примерах hello.

#### <a name="networksettings"></a>networkSettings
В емкости, возможностей или решение с областью начала до конца шаблона, hello связанных шаблонов обычно Создание ресурсов, которые существуют в сети. Один простой подход является toouse параметров сети toostore сложный объект и передавать их toolinked шаблонов.

Ниже приведен пример взаимодействующих сетевых параметров.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Ресурсы, созданные в связанных шаблонах, часто помещаются в группу доступности. В следующем примере hello имя набора доступности hello указан и также hello домен сбоя и обновление домена toouse число.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Если требуется несколько групп доступности (например, один для главных узлов), а другой для узлов данных можно использовать имя с префиксом, указать несколько наборов доступности или выполните hello модели приведенный выше, для создания переменной для определенного размера футболки.

#### <a name="storagesettings"></a>storageSettings
Информация о хранилище часто совместно используется со связанными шаблонами. В следующем примере hello *storageSettings* объект предоставляет сведения о hello имена учетной записи и контейнера хранилища.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
С помощью связанных шаблонов может понадобиться типы узлов toovarious параметры операционной системы toopass через различные известные типы конфигураций. Сложный объект информационное легко toostore и общую папку операционной системы, а также делает проще toosupport множественный выбор операционной системы для развертывания.

Hello пример объекта для *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Создаваемая переменная *machineSettings* представляет собой составной объект, содержащий набор основных переменных для создания виртуальной машины. переменные Hello включают имя пользователя администратора и пароль, префикс для имен виртуальных Машин hello и ссылка на изображение операционной системы.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Обратите внимание, что *osImageReference* Здравствуйте, извлекает значения из hello *osSettings* переменную, заданную в главном шаблоне hello. Это означает, что можно легко изменить hello операционной системы для виртуальной Машины — полностью или в зависимости от предпочтений hello шаблон потребителя.

#### <a name="vmscripts"></a>vmScripts
Hello *vmScripts* объекта содержит подробные сведения о сценарии toodownload hello и выполнить на экземпляре виртуальной Машины, включая внешней и внутренней ссылки. За пределами ссылки включать hello инфраструктуры.
Ссылки внутри включать hello установлено программное обеспечение и конфигурации.

Использовать hello *scriptsToDownload* свойство toolist hello скрипты toodownload toohello виртуальной Машины. Этот объект также содержит ссылки на toocommand строки для различных типов действий. Эти действия включают выполнение hello установки по умолчанию для каждого отдельного узла, установки, выполняемый после развертывания все узлы и любые дополнительные сценарии, которые могут быть конкретных tooa заданный шаблон.

Этот пример взят из шаблона, который использовался toodeploy MongoDB, требующий арбитр toodeliver высокого уровня доступности. Hello *arbiterNodeInstallCommand* добавлено слишком*vmScripts* tooinstall арбитр hello.

раздел Hello переменные — где найти hello переменные, которые определяют скрипт hello tooexecute hello определенного текста с использованием соответствующих значений hello.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Возвращение состояния из шаблона
Не только передавать данные в виде шаблона, вы также можете шаблон вызывающий задней toohello данных общей папки. В hello **выводит** раздел связанного шаблона, можно указать пары "ключ значение", который может быть использован hello исходный шаблон.

Hello следующем примере показано, как toopass hello частный IP-адрес, созданный в связанного шаблона.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

В главном шаблоне hello можно использовать эти данные hello, используя синтаксис:

    "[reference('master-node').outputs.masterip.value]"

Можно использовать это выражение в разделе выходы hello или раздел ресурсов hello hello основного шаблона. Нельзя использовать выражение hello в разделе "переменные" hello, поскольку он зависит от состояния выполнения hello. tooreturn это значение из основного шаблона hello, используйте:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Пример использования hello выводит раздел дисков данных tooreturn связанного шаблона, для виртуальной машины, см. в разделе [Создание несколько дисков данных для виртуальной машины](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Определение параметров проверки подлинности для виртуальной машины
Можно использовать hello же шаблону, показанному ранее для параметров проверки подлинности hello toospecify параметры конфигурации для виртуальной машины. Создание параметра для передачи в hello тип проверки подлинности.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Можно добавить переменные для hello различные типы проверки подлинности и переменной toostore, какой тип используется для развертывания на основе значения параметра hello hello.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

При определении hello виртуальной машины, можно задать hello **osProfile** toohello переменной, созданной.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Дальнейшие действия
* toolearn о разделах hello шаблона hello. в разделе [разработки шаблонов диспетчера ресурсов Azure](resource-group-authoring-templates.md)
* toosee hello функций, доступных в шаблоне, в разделе [функции шаблона диспетчера ресурсов Azure](resource-group-template-functions.md)
