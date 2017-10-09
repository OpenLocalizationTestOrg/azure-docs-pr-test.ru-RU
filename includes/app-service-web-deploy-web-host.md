### <a name="app-service-plan"></a>План службы приложений
Создается план обслуживания hello для размещения веб-приложения hello. Укажите имя hello плана hello через hello **hostingPlanName** параметра. Hello hello план находится hello местоположения, используемое для группы ресурсов hello. Hello ценовую категорию и рабочие размер указываются в hello **sku** и **workerSize** параметров

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

