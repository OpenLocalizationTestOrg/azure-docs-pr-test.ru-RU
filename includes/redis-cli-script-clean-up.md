## <a name="clean-up-deployment"></a><span data-ttu-id="993ac-101">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="993ac-101">Clean up deployment</span></span> 

<span data-ttu-id="993ac-102">Выполнив пример скрипта, вы можете удалить группу ресурсов, экземпляр кэша Redis для Azure и любые связанные ресурсы и группы ресурсов с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="993ac-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```