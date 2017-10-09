## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="10dc3-101">Общие сведения о шаблонах диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="10dc3-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="10dc3-102">Шаблоны диспетчера ресурсов Azure позволяют toodeclaratively укажите инфраструктуры Azure IaaS hello языке Json, определяя hello зависимости между ресурсами.</span><span class="sxs-lookup"><span data-stu-id="10dc3-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="10dc3-103">Подробный обзор шаблонов диспетчера ресурсов Azure можно найти в статье toohello ниже:</span><span class="sxs-lookup"><span data-stu-id="10dc3-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="10dc3-104">Общие сведения о группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="10dc3-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="10dc3-105">Фрагмент примера шаблона для расширений виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="10dc3-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="10dc3-106">Развертывание расширений ВМ, как часть шаблона диспетчера ресурсов Azure требует toodeclaratively указать конфигурацию расширения hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="10dc3-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="10dc3-107">Вот hello формат для указания конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="10dc3-107">Here is hello format for specifying hello extension configuration.</span></span>

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

<span data-ttu-id="10dc3-108">Как видно из hello выше hello расширения шаблон содержит две основные части:</span><span class="sxs-lookup"><span data-stu-id="10dc3-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="10dc3-109">Имя, издатель и версия расширения.</span><span class="sxs-lookup"><span data-stu-id="10dc3-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="10dc3-110">Конфигурация расширения.</span><span class="sxs-lookup"><span data-stu-id="10dc3-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="10dc3-111">Идентификация издателя hello, тип и typeHandlerVersion для любого расширения</span><span class="sxs-lookup"><span data-stu-id="10dc3-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="10dc3-112">Расширений ВМ Azure опубликованные корпорацией Майкрософт и доверенных издателей сторонних производителей и каждое расширение однозначно идентифицируется typeHandlerVersion его издателя, тип и hello.</span><span class="sxs-lookup"><span data-stu-id="10dc3-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="10dc3-113">Эти сведения можно определить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="10dc3-113">These can be determined as following:</span></span>  

