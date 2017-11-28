<span data-ttu-id="38a37-101">Действия для отмены регистрации сервера обработки зависят от состояния соединения с сервером конфигурации.</span><span class="sxs-lookup"><span data-stu-id="38a37-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="38a37-102">Отмена регистрации сервера обработки, который находится в подключенном состоянии</span><span class="sxs-lookup"><span data-stu-id="38a37-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="38a37-103">Установите удаленное подключение к серверу обработки от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="38a37-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="38a37-104">Запустите **панель управления** и откройте **Программы > Удаление программы**.</span><span class="sxs-lookup"><span data-stu-id="38a37-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="38a37-105">Удалите программу с именем **Сервер обработки и конфигурации Microsoft Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="38a37-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="38a37-106">После завершения шага 3 удалите **зависимости сервера обработки и конфигурации Microsoft Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="38a37-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="38a37-107">Отмена регистрации сервера обработки, который находится в отключенном состоянии</span><span class="sxs-lookup"><span data-stu-id="38a37-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="38a37-108">Используйте следующие шаги, только если невозможно восстановить виртуальную машину, на которой установлен сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="38a37-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="38a37-109">Войдите на сервер конфигурации от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="38a37-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="38a37-110">Откройте административную командную строку и перейдите в каталог `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="38a37-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="38a37-111">Теперь выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="38a37-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="38a37-112">Она очистит сведения о сервере обработки из системы.</span><span class="sxs-lookup"><span data-stu-id="38a37-112">This will purge the details of the process server from the system.</span></span>
