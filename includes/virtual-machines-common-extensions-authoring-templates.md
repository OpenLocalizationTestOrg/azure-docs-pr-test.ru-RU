## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="836e4-101">Общие сведения о шаблонах диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="836e4-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="836e4-102">Шаблон Azure Resource Manager позволяет декларативно задать инфраструктуру IaaS Azure на языке JSON, установив зависимости между ресурсами.</span><span class="sxs-lookup"><span data-stu-id="836e4-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="836e4-103">Более подробно шаблоны Azure Resource Manager рассматриваются в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="836e4-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="836e4-104">Общие сведения о группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="836e4-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="836e4-105">Фрагмент примера шаблона для расширений виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="836e4-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="836e4-106">При развертывании расширений виртуальной машины в шаблоне Azure Resource Manager в нем необходимо декларативно задать конфигурацию расширения.</span><span class="sxs-lookup"><span data-stu-id="836e4-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="836e4-107">Ниже приведен формат для указания конфигурации расширения.</span><span class="sxs-lookup"><span data-stu-id="836e4-107">Here is the format for specifying the extension configuration.</span></span>

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

<span data-ttu-id="836e4-108">Как видно из указанного выше, расширение шаблона содержит две основные части:</span><span class="sxs-lookup"><span data-stu-id="836e4-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="836e4-109">Имя, издатель и версия расширения.</span><span class="sxs-lookup"><span data-stu-id="836e4-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="836e4-110">Конфигурация расширения.</span><span class="sxs-lookup"><span data-stu-id="836e4-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="836e4-111">Определение значений publisher, type и typeHandlerVersion для любого расширения</span><span class="sxs-lookup"><span data-stu-id="836e4-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="836e4-112">Расширения виртуальной машины Azure публикуются корпорацией Майкрософт и надежными сторонними издателями. Каждое расширение однозначно определяется по значениям publisher, type и typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="836e4-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="836e4-113">Эти сведения можно определить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="836e4-113">These can be determined as following:</span></span>  

