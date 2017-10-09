<span data-ttu-id="bb503-101">toounregister действия Hello сервера обработки отличается в зависимости от состояния соединения с hello сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bb503-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="bb503-102">Отмена регистрации сервера обработки, который находится в подключенном состоянии</span><span class="sxs-lookup"><span data-stu-id="bb503-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="bb503-103">Удаленное подключение сервера обработки hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bb503-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="bb503-104">Запустите hello **панели управления** и откройте **программы > Удаление программы**</span><span class="sxs-lookup"><span data-stu-id="bb503-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="bb503-105">Удаление программы с именем hello **сервера к конфигурации или процесс восстановления сайта Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="bb503-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="bb503-106">После завершения шага 3 удалите **зависимости сервера обработки и конфигурации Microsoft Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="bb503-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="bb503-107">Отмена регистрации сервера обработки, который находится в отключенном состоянии</span><span class="sxs-lookup"><span data-stu-id="bb503-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="bb503-108">Используйте hello ниже действия, следует использовать, если нет способа toorevive hello виртуальных компьютера, на какие приветствия был установлен сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="bb503-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="bb503-109">Войдите на сервер конфигурации tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bb503-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="bb503-110">Откройте командную строку администратора и перейдите в каталог toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="bb503-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="bb503-111">Теперь выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="bb503-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="bb503-112">Это будет использоваться для очистки сведений hello сервера обработки hello из системы hello.</span><span class="sxs-lookup"><span data-stu-id="bb503-112">This will purge hello details of hello process server from hello system.</span></span>
