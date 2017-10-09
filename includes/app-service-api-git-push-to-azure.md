Используйте URL-адрес hello Azure CLI tooget hello удаленного развертывания для приложения API. В hello следующую команду, замените  *\<имя_приложения >* с именем веб-приложения.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Настройте ваш локальный Git развертывания toobe может toopush toohello удаленной.

```bash
git remote add azure <URI from previous step>
```

Принудительно toohello Azure toodeploy удаленного приложения. Запрашивается пароль hello, созданную ранее при создании пользователя развертывания hello. Убедитесь, что введено hello пароль, созданный в более ранней версии в кратком руководстве hello и не hello использовать toolog в toohello портал Azure.

```bash
git push azure master
```
