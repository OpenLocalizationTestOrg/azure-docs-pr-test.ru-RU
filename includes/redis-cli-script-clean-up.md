## <a name="clean-up-deployment"></a><span data-ttu-id="234ff-101">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="234ff-101">Clean up deployment</span></span> 

<span data-ttu-id="234ff-102">После выполнения сценария образец hello hello команда может быть группа ресурсов используется tooremove hello, экземпляр кэша Redis для Azure и все связанные ресурсы в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="234ff-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```