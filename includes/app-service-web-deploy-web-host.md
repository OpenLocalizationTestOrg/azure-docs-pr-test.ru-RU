### <a name="app-service-plan"></a><span data-ttu-id="c88fa-101">План службы приложений</span><span class="sxs-lookup"><span data-stu-id="c88fa-101">App Service plan</span></span>
<span data-ttu-id="c88fa-102">Создается план обслуживания hello для размещения веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c88fa-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="c88fa-103">Укажите имя hello плана hello через hello **hostingPlanName** параметра.</span><span class="sxs-lookup"><span data-stu-id="c88fa-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="c88fa-104">Hello hello план находится hello местоположения, используемое для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="c88fa-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="c88fa-105">Hello ценовую категорию и рабочие размер указываются в hello **sku** и **workerSize** параметров</span><span class="sxs-lookup"><span data-stu-id="c88fa-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

