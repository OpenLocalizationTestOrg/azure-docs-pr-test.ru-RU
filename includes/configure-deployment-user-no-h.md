<span data-ttu-id="b4a8a-101">Создайте учетные данные развертывания с hello [набора пользователей для развертывания веб-приложения az](/cli/azure/webapp/deployment/user#set) команды.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="b4a8a-102">Для FTP и локальное веб-приложение tooa Git развертывания требуется пользователя развертывания.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="b4a8a-103">Hello имя пользователя и пароль являются уровне учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-103">hello user name and password are account level.</span></span> <span data-ttu-id="b4a8a-104">_Они отличаются от учетных данных подписки Azure._</span><span class="sxs-lookup"><span data-stu-id="b4a8a-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="b4a8a-105">В hello следующую команду, замените  *\<имя пользователя >* и  *\<пароль >* новое имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="b4a8a-106">Hello имя пользователя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-106">hello user name must be unique.</span></span> <span data-ttu-id="b4a8a-107">Hello пароль должен содержать по крайней мере 8 символов, с двумя hello следующие три элемента: буквы, цифры, символы.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="b4a8a-108">Если вы получаете ` 'Conflict'. Details: 409` ошибки, имя пользователя изменить hello.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="b4a8a-109">Если появляется сообщение об ошибке ` 'Bad Request'. Details: 400`, используйте более надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="b4a8a-110">Пользователь развертывания создается один раз. Его можно использовать для всех развертываний Azure.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a8a-111">Запись hello имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-111">Record hello user name and password.</span></span> <span data-ttu-id="b4a8a-112">Они нужны toodeploy hello веб-приложения позже.</span><span class="sxs-lookup"><span data-stu-id="b4a8a-112">You need them toodeploy hello web app later.</span></span>
>
>