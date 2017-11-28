### <a name="app-service-plan"></a><span data-ttu-id="6f227-101">План обслуживания приложения</span><span class="sxs-lookup"><span data-stu-id="6f227-101">App Service plan</span></span>
<span data-ttu-id="6f227-102">Создает план обслуживания для размещения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6f227-102">Creates the service plan for hosting the web app.</span></span> <span data-ttu-id="6f227-103">Имя плана задается с помощью параметра **hostingPlanName** .</span><span class="sxs-lookup"><span data-stu-id="6f227-103">You provide the name of the plan through the **hostingPlanName** parameter.</span></span> <span data-ttu-id="6f227-104">Расположение плана совпадает с расположением группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f227-104">The location of the plan is the same location used for the resource group.</span></span> <span data-ttu-id="6f227-105">Ценовая категория и размер рабочего процесса задаются с помощью параметров **sku** и **workerSize**</span><span class="sxs-lookup"><span data-stu-id="6f227-105">The pricing tier and worker size are specified in the **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

