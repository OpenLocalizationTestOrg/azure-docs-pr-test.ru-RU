<span data-ttu-id="33c69-101">Каждый BLOB-объект в Azure должен располагаться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="33c69-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="33c69-102">формы контейнера Hello часть hello имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="33c69-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="33c69-103">Например `mycontainer` — имя контейнера hello в этих blob образец идентификаторы URI hello:</span><span class="sxs-lookup"><span data-stu-id="33c69-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="33c69-104">Имя контейнера должно быть допустимым именем DNS, соответствующие требованиям toohello следующие правила именования:</span><span class="sxs-lookup"><span data-stu-id="33c69-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="33c69-105">Имена контейнеров должны начинаться с буквы или цифры и может содержать только буквы, цифры и знак дефиса (-) hello.</span><span class="sxs-lookup"><span data-stu-id="33c69-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="33c69-106">Каждое тире (-) должно стоять непосредственно перед буквой или цифрой и после нее. В именах контейнеров запрещено использовать несколько тире подряд.</span><span class="sxs-lookup"><span data-stu-id="33c69-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="33c69-107">Все знаки в имени контейнера должны быть строчными.</span><span class="sxs-lookup"><span data-stu-id="33c69-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="33c69-108">Имя контейнера должно содержать от 3 до 63 знаков.</span><span class="sxs-lookup"><span data-stu-id="33c69-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33c69-109">Обратите внимание, что hello имя контейнера всегда должны быть строчными.</span><span class="sxs-lookup"><span data-stu-id="33c69-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="33c69-110">Если включить буквой верхнего регистра в имени контейнера или иным образом нарушать правила именования контейнера hello, может появиться ошибку 400 (неправильный запрос).</span><span class="sxs-lookup"><span data-stu-id="33c69-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

