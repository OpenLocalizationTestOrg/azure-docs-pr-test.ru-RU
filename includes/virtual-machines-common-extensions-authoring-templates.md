## <a name="overview-of-azure-resource-manager-templates"></a>Общие сведения о шаблонах диспетчера ресурсов Azure
Шаблоны диспетчера ресурсов Azure позволяют toodeclaratively укажите инфраструктуры Azure IaaS hello языке Json, определяя hello зависимости между ресурсами. Подробный обзор шаблонов диспетчера ресурсов Azure можно найти в статье toohello ниже:

[Общие сведения о группе ресурсов](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Фрагмент примера шаблона для расширений виртуальной машины
Развертывание расширений ВМ, как часть шаблона диспетчера ресурсов Azure требует toodeclaratively указать конфигурацию расширения hello в шаблоне hello.
Вот hello формат для указания конфигурации расширения hello.

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

Как видно из hello выше hello расширения шаблон содержит две основные части:

1. Имя, издатель и версия расширения.
2. Конфигурация расширения.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Идентификация издателя hello, тип и typeHandlerVersion для любого расширения
Расширений ВМ Azure опубликованные корпорацией Майкрософт и доверенных издателей сторонних производителей и каждое расширение однозначно идентифицируется typeHandlerVersion его издателя, тип и hello. Эти сведения можно определить следующим образом:  

