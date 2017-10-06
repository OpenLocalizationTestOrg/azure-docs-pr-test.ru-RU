---
title: "aaaBest и рекомендации по созданию шаблонов диспетчера ресурсов | Документы Microsoft"
description: "Рекомендации по упрощению шаблонов Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Рекомендации по созданию шаблонов Azure Resource Manager
Эти рекомендации помогут создать шаблоны Azure Resource Manager, надежное и легко toouse. Hello рекомендации предназначены только для примера. не являются обязательными (если это явно не обозначено). Сценарий может потребоваться вариантом hello следующие подходы и примеры.

## <a name="resource-names"></a>Имена ресурсов
Обычно в Resource Manager вы работаете с именами ресурсов трех типов:

* имена ресурсов, которые должны быть уникальными;
* Имена ресурсов, которые не требуется уникальный toobe, но выберите tooprovide имя, которое может помочь определить ресурс на основе контекста.
* имена ресурсов, которые могут быть универсальными.

 Сведения об ограничениях имен ресурсов см. в статье [Рекомендуемые соглашения об именовании для ресурсов Azure](../guidance/guidance-naming-conventions.md).

### <a name="unique-resource-names"></a>Уникальные имена ресурсов
Необходимо указать уникальное имя для любого типа ресурса, который имеет конечную точку доступа к данным. Ниже приведено несколько распространенных типов ресурсов, для которых требуются уникальные имена:

* служба хранилища Azure<sup>1</sup>; 
* веб-приложения службы приложений Azure;
* SQL Server
* Хранилище ключей Azure
* кэш Azure Redis
* Пакетная служба Azure
* Azure Traffic Manager
* поиск Azure;
* Azure HDInsight

<sup>1</sup> Имена учетных записей хранения также должны содержать до 24 знаков в нижнем регистре без дефисов.

При указании параметра имени ресурса, необходимо указать уникальное имя, при развертывании ресурсов hello. При необходимости можно создать переменную, которая использует hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate имя функции. 

Необходимо также может собирать tooadd префикс или суффикс toohello **uniqueString** результат. Изменение hello уникальное имя может помочь более легко определить тип ресурса hello из имени hello. Например можно создать уникальное имя для учетной записи хранилища с помощью следующих переменной hello:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Имена ресурсов для идентификации
Некоторые типы ресурсов может потребоваться tooname, но их имена могут не toobe уникальным. Для этих типов ресурсов можно предоставить имя, которое определяет контекст ресурса hello и тип ресурса hello. Укажите описательное имя, которое помогает определить hello ресурс в список ресурсов. При необходимости toouse имя другого ресурса для различных развертываний можно использовать параметр для имени hello:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Если во время развертывания toopass в имени не требуется, можно использовать переменную: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

Вы также можете использовать жестко заданное значение:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Универсальные имена ресурсов
Для типов ресурсов, которые обычно открываются другого ресурса можно использовать универсального имени, которое жестко запрограммированы в шаблоне hello. Например, можно задать стандартное универсальное имя для правил брандмауэра на SQL Server:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>Параметры
Hello следующие сведения могут оказаться полезными при работе с параметрами:

* Используйте как можно меньше параметров. По возможности используйте переменную или литеральное значение. Используйте параметры только для следующих сценариев:
   
   * Параметры, которые должны toouse различные виды tooenvironment (SKU, размер, емкость) в соответствии с.
   * Имена ресурсов, что требуется toospecify для упрощения идентификации.
   * Значения, которые часто используются toocomplete других задач (например, имя пользователя администратора).
   * секреты (например, пароли);
   * Номер Hello или массив значений toouse при создании нескольких экземпляров типа ресурса.
* Имена для параметров необходимо указывать в нижнем регистре.
* Описание каждого параметра в hello метаданных:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Определите значения по умолчанию для параметров (за исключением паролей и ключей SSH).
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Используйте **securestring** для всех паролей и секретов. 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Когда это возможно, не используйте параметр toospecify расположение. Вместо этого используйте hello **расположение** свойства группы ресурсов hello. С помощью hello **.location () в группе ресурсов** выражение для всех ресурсов, ресурсы в шаблоне hello развертываются в hello местоположения hello группа ресурсов:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Если тип ресурса поддерживается только ограниченное число расположений, может потребоваться toospecify допустимое расположение непосредственно в шаблоне hello. Если необходимо использовать **расположение** параметра, совместно используют значение этого параметра максимальной с ресурсами, скорее всего, toobe в hello местоположения. Это сводит к минимуму hello количество раз, когда пользователям предлагается tooprovide сведения о расположении.
* Избегайте использования параметра или переменной для hello версии API-интерфейса для типа ресурса. Свойства и значения ресурса могут отличаться для разных версий. IntelliSense в редакторе кода не может определить правильную схему hello при tooa параметра или переменной, задана версия API hello. Вместо этого следует жестко кодировать hello версии API-интерфейса в шаблоне hello.

## <a name="variables"></a>Переменные
Hello следующие сведения могут оказаться полезными при работе с переменными:

* Используйте переменные для значений, необходимость toouse более одного раза в шаблоне. Если значение используется только один раз, жестко запрограммированных значений делает проще tooread ваш шаблон.
* Нельзя использовать hello [ссылки](resource-group-template-functions-resource.md#reference) функции hello **переменных** раздел hello шаблона. Hello **ссылки** функции является производным свое значение из состояния среды выполнения hello ресурса. Однако переменные разрешаются во время начальной синтаксический анализ шаблона hello hello. Создать значения, которые необходимо hello **ссылки** функции непосредственно в hello **ресурсов** или **выводит** раздел hello шаблона.
* Добавьте переменные для имен ресурсов, которые должны быть уникальными, как описано в разделе [Имена ресурсов](#resource-names).
* Переменные можно группировать в составные объекты. Используйте hello **variable.subentry** формата tooreference значение из сложного объекта. Группирование переменных помогает следить за связанными переменными Она также повышает удобочитаемость hello шаблона. Ниже приведен пример:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Составной объект не может содержать выражение, которое ссылается на значение из составного объекта. Для этого определите отдельную переменную.
   > 
   > 
   
     Расширенные примеры использования составных объектов в качестве переменных доступны в статье [Передача состояния в шаблоны Azure Resource Manager и из них](best-practices-resource-manager-state.md).

## <a name="resources"></a>Ресурсы
Hello следующие сведения могут оказаться полезными при работе с ресурсами:

* toohelp других участников понимать назначение hello hello ресурса, укажите **комментарии** для каждого ресурса в шаблоне hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* Можно использовать теги tooadd метаданные tooresources. Используйте метаданные tooadd сведения о ресурсах. Например можно добавить toorecord тарификация метаданные для ресурса. Дополнительные сведения см. в разделе [использование теги tooorganize ресурсам Azure](resource-group-using-tags.md).
* При использовании *общедоступную конечную точку* в шаблоне (например, больших двоичных объектов Azure хранилища общей конечной точки), *не следует жестко кодировать* hello пространства имен. Используйте hello **ссылки** функция toodynamically Получение имен hello. Можно использовать этот подход toodeploy hello шаблона toodifferent открытых пространствах имен без изменения конечной точки hello в шаблоне hello вручную. Задать hello API версии toohello же версии, которая используется для учетной записи хранения hello в шаблоне:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Если учетная запись хранения hello развернут в hello того же шаблона, который вы создаете, не требуется пространство имен поставщика hello toospecify при ссылке на ресурс hello. Это hello упрощенный синтаксис:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Если у вас есть другие значения в шаблон, настроенный toouse имен public, измените значения этих tooreflect hello же **ссылки** функции. Например, можно задать hello **storageUri** свойство профиля диагностики hello виртуальной машины:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Вы также можете использовать функцию reference для ссылки на учетную запись хранения в другой группе ресурсов:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Назначьте открытый IP адресов tooa виртуальную машину, только в том случае, если она требуется приложению. tooconnect tooa виртуальной машины (VM) для отладки, или для управления или административных задач, используйте правила для входящих подключений NAT, шлюз виртуальной сети или jumpbox.
   
     Дополнительные сведения о подключении toovirtual машин см. в разделе:
   
   * [Run Windows VMs for an N-tier application](../guidance/guidance-compute-n-tier-vm.md) (Запуск виртуальных машин Windows в n-уровневом приложении)
   * [Настройка доступа WinRM для виртуальных машин в Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Разрешить внешний доступ tooyour виртуальной Машины с помощью портала Azure hello](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Разрешить внешний доступ tooyour виртуальной Машины с помощью PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Разрешить внешний доступ tooyour виртуальных Машин Linux с помощью Azure CLI](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Hello **domainNameLabel** свойства для общих IP-адресов должны быть уникальными. Hello **domainNameLabel** значение должно находиться в диапазоне от 3 до 63 символов и выполните hello правил, заданных это регулярное выражение: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Поскольку hello **uniqueString** функция создает строку, которая является 13 символов hello **dnsPrefixString** параметр является ограниченной too50 символов:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* При добавлении расширение пользовательского скрипта tooa пароля используйте hello **commandToExecute** свойство в hello **protectedSettings** свойства:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure, секреты представляют шифруется при передаче в качестве параметров tooVMs и расширения, используйте hello **protectedSettings** свойство применимо расширений hello.
   > 
   > 

## <a name="outputs"></a>outputs
При использовании шаблона toocreate общих IP-адресов, включите **выводит** раздел, в котором для извлечения сведений о hello IP-адрес и hello полное доменное имя (FQDN). После развертывания можно использовать выходные данные значения tooeasily извлечь подробности открытый IP-адреса и полные доменные имена. При ссылке на ресурс hello, использовать версию hello API, которое вы использовали toocreate его: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Отдельный шаблон и вложенные шаблоны
toodeploy решение, можно использовать один шаблон или основного шаблона с несколькими шаблонами вложенных. Вложенные шаблоны обычно используются для более сложных сценариев. С помощью вложенных шаблонов дает, hello следующие преимущества:

* вы можете разбить решение на целевые компоненты;
* вложенные шаблоны можно повторно использовать в разных основных шаблонах.

При выборе toouse вложенные шаблоны hello, следование правилам может помочь стандартизировать макет шаблона. Эти рекомендации основаны на статье [Приемы разработки шаблонов Azure Resource Manager при развертывании сложных решений](best-practices-resource-manager-design-templates.md). Рекомендуется разработать проект, который имеет hello следующие шаблоны:

* **Основной шаблон** (azuredeploy.json). Используйте для hello входных параметров.
* **Шаблон общих ресурсов**. Используйте toodeploy общих ресурсов, использующих другие ресурсы (например, виртуальной сети и доступность наборов). Используйте hello **dependsOn** tooensure выражения, что шаблон будет развернут перед другими шаблонами.
* **Шаблон дополнительных ресурсов**. Используйте tooconditionally развертывания ресурсов на основе параметра (например, jumpbox).
* **Шаблон элемента ресурсов.** У каждого типа экземпляра в пределах уровня приложения есть собственная конфигурация. В пределах уровня можно определить разные типы экземпляров. (Например, hello первый экземпляр создает кластер, а дополнительные экземпляры будут добавлены toohello существующего кластера.) У каждого типа экземпляра есть собственный шаблон развертывания.
* **Сценарии**. Повторно используемые сценарии, которые можно применить к каждому типу экземпляра (например, для инициализации и форматирования дополнительных дисков). Пользовательские сценарии, создаваемые в целях, определенные настройки отличаются, на основе типа экземпляра hello.

![Вложенный шаблон](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Дополнительные сведения см. в статье [Использование связанных шаблонов при развертывании ресурсов Azure](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Условно связать toonested шаблонов
Можно использовать параметр tooconditionally ссылку toonested шаблонов. параметр Hello становится частью hello URI для hello шаблона:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Формат шаблона
Это toopass хорошей практикой шаблон через проверяющем элементе управления JSON. чтобы удалить лишние запятые, скобки и квадратные скобки, которые могут привести к ошибке во время развертывания. Попробуйте [JSONlint](http://jsonlint.com/) или пакет linter для предпочитаемой среды редактирования (Visual Studio Code, Atom, Sublime Text, Visual Studio).

Это также tooformat хорошее представление JSON для повышения удобочитаемости. Вы можете использовать пакет модуля форматирования данных JSON для своего локального редактора. В Visual Studio, tooformat hello документа, нажмите клавишу **Ctrl + K, Ctrl + D**. В Visual Studio Code нажмите клавиши **ALT+SHIFT+F**. Если ваш локальный редактор не форматировать документ hello, можно использовать [online форматирования](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Дальнейшие действия
* Рекомендации по разработке архитектуры решения для виртуальных машин см. в статьях [Run a Windows VM on Azure](../guidance/guidance-compute-single-vm.md) (Запуск виртуальной машины Windows в Azure) и [Run a Linux VM on Azure](../guidance/guidance-compute-single-vm-linux.md) (Запуск виртуальной машины Linux в Azure).
* Рекомендации по настройке учетной записи хранения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](../storage/common/storage-performance-checklist.md).
* toolearn об использовании диспетчера ресурсов tooeffectively предприятия управление подписками см. в разделе [формирования шаблонов Azure enterprise: управление конкретные подписки](resource-manager-subscription-governance.md).

