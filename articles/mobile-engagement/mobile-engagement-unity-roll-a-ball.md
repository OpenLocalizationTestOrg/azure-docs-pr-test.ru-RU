---
title: "aaaUnity наката учебник шар"
description: "Действия toocreate hello классический наката Unity игры шарик, что является необходимым условием для всех учебниках Mobile Engagement Unity"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="e4bbb-103"><a id="unity-roll-a-ball"></a>Создание игры Roll a Ball на платформе Unity</span><span class="sxs-lookup"><span data-stu-id="e4bbb-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="e4bbb-104">Этот учебник поможет выполнить hello основные этапы для слегка измененный [Unity наката учебник шарик](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="e4bbb-105">Эта игра Образец состоит из объекта сферическую «проигрыватель», который контролируется пользователем приложения hello и цель hello hello игры — too'collect "собираемой объекты объектом конфликтующего hello проигрывателя с этими собираемой объектами.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="e4bbb-106">Для работы с примером предполагается знакомство со средой редактора Unity.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="e4bbb-107">Если возникли проблемы, вы должны обращаться toohello полный учебника.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="e4bbb-108">Настройка hello игры</span><span class="sxs-lookup"><span data-stu-id="e4bbb-108">Setting up hello game</span></span>
<span data-ttu-id="e4bbb-109">Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="e4bbb-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="e4bbb-110">Откройте **редактор Unity** и щелкните **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="e4bbb-111">Заполните поля **Project name** (Имя проекта) & **Location** (Расположение), выберите **3D** и щелкните **Create project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="e4bbb-112">Сохранить только что создана как часть hello нового проекта с помощью имени hello сцены по умолчанию hello **MiniGame** в новом  **\_сцен** папку **активы** папки:</span><span class="sxs-lookup"><span data-stu-id="e4bbb-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="e4bbb-113">Создание **трехмерный объект -> плоскости** как воспроизведение hello и переименования данного объекта плоскости как **Наземный**</span><span class="sxs-lookup"><span data-stu-id="e4bbb-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="e4bbb-114">Компонент преобразования hello сброса для этой **Наземный** таким образом, чтобы он находится на hello источника.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="e4bbb-115">Снимите флажок **Показать сетку** из **меню барахло** для hello **Наземный** объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="e4bbb-116">Обновление hello **шкалы** компонента для hello **Наземный** объекта toobe [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="e4bbb-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="e4bbb-117">Добавьте новый **трехмерный объект -> сфере** toohello проекта и имени объекта в этой сфере виде **проигрывателя**.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="e4bbb-118">Выберите hello **проигрывателя** объекта и нажмите кнопку **сбросить преобразования** похожих объектов toohello плоскость.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="e4bbb-119">Обновление **Преобразование -> позиции -> Y-координата** компонента для hello проигрывателя Y как 0,5.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="e4bbb-120">Создайте новую папку с именем **материалы** в проекте hello, где мы создадим hello материала toocolor hello проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="e4bbb-121">Создайте в этой папке новый **материал** с именем **Background**.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="e4bbb-122">Обновить, обновив hello hello цвет материала hello **Albedo** его свойства.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="e4bbb-123">Можно выбрать значения RGB hello [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="e4bbb-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="e4bbb-124">Перетащите этот материал в hello сцены представление tooapply цвет toohello **Наземный** объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="e4bbb-125">Наконец, обновите hello **Преобразование -> поворота -> Y** too60 hello объекта дневного света для ясности.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="e4bbb-126">Перемещение проигрывателя hello</span><span class="sxs-lookup"><span data-stu-id="e4bbb-126">Moving hello player</span></span>
<span data-ttu-id="e4bbb-127">Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="e4bbb-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="e4bbb-128">Добавить **RigidBody** toohello компонент **проигрывателя** объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="e4bbb-129">Создайте новую папку с именем **сценариев** в hello проекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="e4bbb-130">Щелкните **Add Component -> New Script -> C# Script** (Добавить компонент -> Новый скрипт -> Скрипт C#).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="e4bbb-131">Назовите его **PlayerController** и щелкните **Create and Add** (Создать и добавить).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="e4bbb-132">Будет создан и присоединить объект скрипта toohello проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="e4bbb-133">Переместить этот сценарий в группе hello **сценариев** папки в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="e4bbb-134">Откройте скрипт hello для редактирования в редакторе избранные скрипт, дополнить код скрипта hello после кода hello и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="e4bbb-135">Обратите внимание, этот скрипт hello выше используется **скорость** свойство.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="e4bbb-136">В редакторе Unity hello обновите свойство too10 hello скорости.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="e4bbb-137">Попаданий **воспроизведение** в редактор Unity hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="e4bbb-138">Теперь должны быть шарик hello toocontrol может с помощью клавиатуры hello и его следует поворот и перемещать.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="e4bbb-139">Перемещение hello камеры</span><span class="sxs-lookup"><span data-stu-id="e4bbb-139">Moving hello camera</span></span>
<span data-ttu-id="e4bbb-140">Hello шаги взяты из hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) и будет связывать hello **камеры Main** toohello **проигрывателя** объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="e4bbb-141">Обновление hello **Transform.Position** toobe X = 0, Y = 10.5 Z =-10.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="e4bbb-142">Обновление hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="e4bbb-143">Добавить новый сценарий с именем **CameraController** toohello **MainCamera** и переместить его в папку Scripts hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="e4bbb-144">Откройте скрипт hello для редактирования и добавьте следующий код в нем hello:</span><span class="sxs-lookup"><span data-stu-id="e4bbb-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="e4bbb-145">В среде Unity - перетащите переменную проигрывателя hello в слоте hello проигрывателя для hello объекта камеры Main hello два связаны друг с другом.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="e4bbb-146">Теперь если Слушайте в редакторе Unity hello и поворот hello объекта шара проигрыватель будет разделе hello следующий за ним в hello перемещения камеры.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="e4bbb-147">Настройка области воспроизведения hello</span><span class="sxs-lookup"><span data-stu-id="e4bbb-147">Setting up hello Play area</span></span>
<span data-ttu-id="e4bbb-148">Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="e4bbb-149">Мы создадим hello ячейками hello нуля, чтобы hello объекта шара проигрыватель не распределитель hello область воспроизведения при его перемещении.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="e4bbb-150">Щелкните **Create -> Create Empty -> Game Object** (Создать -> Создать пустой -> Игровой объект), чтобы создать объект, и назовите его **Walls**.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="e4bbb-151">В объекте Walls создайте новый объект, щелкнув **3D Object -> Cube** (Трехмерный объект -> Куб), и назовите его West wall.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="e4bbb-152">Обновление hello **Преобразование -> позиции** и **Преобразование -> Масштаб** для этого объекта Wall Западная.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="e4bbb-153">Дублировать hello Западная wall toocreate **wall Восточная** с помощью hello обновлены преобразовать положение и размер.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="e4bbb-154">Дублировать hello Восточная wall toocreate **wall Северная** с помощью hello обновлены преобразовать позиции и масштабирование.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="e4bbb-155">Дублировать wall Северная hello и создать **wall Южная** с помощью hello обновлены преобразовать позиции и масштабирование.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="e4bbb-156">Создание подбираемых объектов</span><span class="sxs-lookup"><span data-stu-id="e4bbb-156">Creating Collectible objects</span></span>
<span data-ttu-id="e4bbb-157">Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="e4bbb-158">Мы создадим некоторые привлекательным поиск объектов, составляющих набор hello собираемой объектов, какой объект шара проигрыватель hello должен too'collect ", конфликтуют с ними.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="e4bbb-159">Создайте новый **трехмерный куб** и назовите этот объект Pickup.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="e4bbb-160">Настройка hello **Преобразование -> поворота** & **Преобразование -> Масштаб** объекта подбора сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="e4bbb-161">Создание и присоединение **новый скрипт C#** вызывается **Rotator** toohello раскладки объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="e4bbb-162">Убедитесь, что скрипт hello tooput скрипты в папке hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="e4bbb-163">Откройте этот скрипт для изменения и обновить его hello toobe следующие:</span><span class="sxs-lookup"><span data-stu-id="e4bbb-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="e4bbb-164">Теперь режим воспроизведения попаданий hello в редактор Unity hello и презентации раскладки объект поворот по оси.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="e4bbb-165">Создайте новую папку **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="e4bbb-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="e4bbb-166">Перетащите hello **раскладки** объекта и сохраните его в папку Prefabs hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="e4bbb-167">Создайте новый **пустой игровой объект** с именем **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="e4bbb-168">Сбросить его tooorigin позиции, а затем перетащите объект подбора сообщений hello под этим объектом игры.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="e4bbb-169">Повторяющиеся hello **раскладки** объекта и распространить ее на hello **Наземный** объекта вокруг hello **проигрывателя** объекта путем обновления hello **X и Z его Transform.Position**  значения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="e4bbb-170">Создание **новый материал** вызывается **раскладки** и обновить toobe красным цветом, обновив hello **Albedo свойство** аналогичные toowhat мы обновления Наземный hello объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="e4bbb-171">Примените hello материала tooall hello 4 раскладки объекты.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="e4bbb-172">Сбор объектов подбора сообщений hello</span><span class="sxs-lookup"><span data-stu-id="e4bbb-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="e4bbb-173">Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="e4bbb-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="e4bbb-174">Корпорация Майкрософт будет обновлять hello проигрыватель, который позволяет доступ too'collect "hello раскладки объектов, возникает конфликт с ними.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="e4bbb-175">Откройте hello **PlayerController** скрипта toohello вложенного объекта проигрывателя для редактирования и обновить его toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="e4bbb-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="e4bbb-176">Создайте новый **тега** вызывается **выбрать копирование** (она должна соответствовать в скрипте hello)</span><span class="sxs-lookup"><span data-stu-id="e4bbb-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="e4bbb-177">Применить это **тега** toohello Prefab раскладки объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="e4bbb-178">Включить **IsTrigger** флажок для hello объекта Prefab.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="e4bbb-179">Добавьте объект Prefab tooPickup жесткая текста.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="e4bbb-180">Для оптимизации производительности мы обновим hello статических collider использования динамических collider tooa.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="e4bbb-181">Наконец, проверьте hello **IsKinematic** свойство для объекта prefab hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="e4bbb-182">Попаданий **воспроизведение** в редактор Unity hello и будет может tooplay данный **наката шарик** игры, перемещая hello объекта проигрывателя клавиши клавиатуры для направления входных данных.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="e4bbb-183">Обновление hello игры для мобильных устройств воспроизведения</span><span class="sxs-lookup"><span data-stu-id="e4bbb-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="e4bbb-184">разделы Hello выше завершения hello основам из Unity.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="e4bbb-185">Теперь нам предстоит изменить hello игры toomake его понятное мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="e4bbb-186">Обратите внимание, что мы использовали ввод с клавиатуры для hello игры в данный момент для тестирования.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="e4bbb-187">Теперь мы будет изменен так, что позволит управлять hello проигрывателя с помощью перемещения hello hello телефона, т. е. с помощью акселерометр вводу hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="e4bbb-188">Откройте hello **PlayerController** скрипт для изменения и обновления hello **FixedUpdate** метод toouse hello движения из hello акселерометр toomove hello Player объекта.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="e4bbb-189">Этот учебник завершает базовое игры создание с помощью Unity и его можно развернуть на устройстве игру Выбор tooplay hello.</span><span class="sxs-lookup"><span data-stu-id="e4bbb-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













