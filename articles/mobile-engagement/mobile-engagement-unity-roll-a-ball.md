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
# <a id="unity-roll-a-ball"></a>Создание игры Roll a Ball на платформе Unity
Этот учебник поможет выполнить hello основные этапы для слегка измененный [Unity наката учебник шарик](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Эта игра Образец состоит из объекта сферическую «проигрыватель», который контролируется пользователем приложения hello и цель hello hello игры — too'collect "собираемой объекты объектом конфликтующего hello проигрывателя с этими собираемой объектами. Для работы с примером предполагается знакомство со средой редактора Unity. Если возникли проблемы, вы должны обращаться toohello полный учебника. 

### <a name="setting-up-hello-game"></a>Настройка hello игры
Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Откройте **редактор Unity** и щелкните **New** (Создать). 
   
    ![][51] 
2. Заполните поля **Project name** (Имя проекта) & **Location** (Расположение), выберите **3D** и щелкните **Create project** (Создать проект).
   
    ![][52]
3. Сохранить только что создана как часть hello нового проекта с помощью имени hello сцены по умолчанию hello **MiniGame** в новом  **\_сцен** папку **активы** папки:
   
    ![][53]
4. Создание **трехмерный объект -> плоскости** как воспроизведение hello и переименования данного объекта плоскости как **Наземный**
   
    ![][1]
5. Компонент преобразования hello сброса для этой **Наземный** таким образом, чтобы он находится на hello источника. 
   
    ![][3]
6. Снимите флажок **Показать сетку** из **меню барахло** для hello **Наземный** объекта.
   
    ![][4]
7. Обновление hello **шкалы** компонента для hello **Наземный** объекта toobe [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Добавьте новый **трехмерный объект -> сфере** toohello проекта и имени объекта в этой сфере виде **проигрывателя**. 
   
    ![][6]
9. Выберите hello **проигрывателя** объекта и нажмите кнопку **сбросить преобразования** похожих объектов toohello плоскость. 
10. Обновление **Преобразование -> позиции -> Y-координата** компонента для hello проигрывателя Y как 0,5.  
    
    ![][7]
11. Создайте новую папку с именем **материалы** в проекте hello, где мы создадим hello материала toocolor hello проигрывателя. 
12. Создайте в этой папке новый **материал** с именем **Background**. 
    
    ![][8]
13. Обновить, обновив hello hello цвет материала hello **Albedo** его свойства. Можно выбрать значения RGB hello [0,32,64]. 
    
    ![][9]
14. Перетащите этот материал в hello сцены представление tooapply цвет toohello **Наземный** объекта. 
    
    ![][10]
15. Наконец, обновите hello **Преобразование -> поворота -> Y** too60 hello объекта дневного света для ясности. 
    
    ![][12]

### <a name="moving-hello-player"></a>Перемещение проигрывателя hello
Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Добавить **RigidBody** toohello компонент **проигрывателя** объекта. 
   
    ![][13]
2. Создайте новую папку с именем **сценариев** в hello проекта. 
3. Щелкните **Add Component -> New Script -> C# Script** (Добавить компонент -> Новый скрипт -> Скрипт C#). Назовите его **PlayerController** и щелкните **Create and Add** (Создать и добавить). Будет создан и присоединить объект скрипта toohello проигрывателя.  
   
    ![][14]
4. Переместить этот сценарий в группе hello **сценариев** папки в проекте hello. 
5. Откройте скрипт hello для редактирования в редакторе избранные скрипт, дополнить код скрипта hello после кода hello и сохраните его. 
   
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
6. Обратите внимание, этот скрипт hello выше используется **скорость** свойство. В редакторе Unity hello обновите свойство too10 hello скорости.  
   
    ![][15]
7. Попаданий **воспроизведение** в редактор Unity hello. Теперь должны быть шарик hello toocontrol может с помощью клавиатуры hello и его следует поворот и перемещать. 

### <a name="moving-hello-camera"></a>Перемещение hello камеры
Hello шаги взяты из hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) и будет связывать hello **камеры Main** toohello **проигрывателя** объекта. 

1. Обновление hello **Transform.Position** toobe X = 0, Y = 10.5 Z =-10.  
2. Обновление hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Добавить новый сценарий с именем **CameraController** toohello **MainCamera** и переместить его в папку Scripts hello. 
   
    ![][17]
4. Откройте скрипт hello для редактирования и добавьте следующий код в нем hello:
   
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
5. В среде Unity - перетащите переменную проигрывателя hello в слоте hello проигрывателя для hello объекта камеры Main hello два связаны друг с другом. 
   
    ![][18]
6. Теперь если Слушайте в редакторе Unity hello и поворот hello объекта шара проигрыватель будет разделе hello следующий за ним в hello перемещения камеры.  

### <a name="setting-up-hello-play-area"></a>Настройка области воспроизведения hello
Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Мы создадим hello ячейками hello нуля, чтобы hello объекта шара проигрыватель не распределитель hello область воспроизведения при его перемещении. 

1. Щелкните **Create -> Create Empty -> Game Object** (Создать -> Создать пустой -> Игровой объект), чтобы создать объект, и назовите его **Walls**.
   
    ![][19]
2. В объекте Walls создайте новый объект, щелкнув **3D Object -> Cube** (Трехмерный объект -> Куб), и назовите его West wall. 
   
    ![][20]
3. Обновление hello **Преобразование -> позиции** и **Преобразование -> Масштаб** для этого объекта Wall Западная. 
   
    ![][21]
4. Дублировать hello Западная wall toocreate **wall Восточная** с помощью hello обновлены преобразовать положение и размер. 
   
    ![][22]
5. Дублировать hello Восточная wall toocreate **wall Северная** с помощью hello обновлены преобразовать позиции и масштабирование. 
   
    ![][23]
6. Дублировать wall Северная hello и создать **wall Южная** с помощью hello обновлены преобразовать позиции и масштабирование. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Создание подбираемых объектов
Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Мы создадим некоторые привлекательным поиск объектов, составляющих набор hello собираемой объектов, какой объект шара проигрыватель hello должен too'collect ", конфликтуют с ними. 

1. Создайте новый **трехмерный куб** и назовите этот объект Pickup. 
2. Настройка hello **Преобразование -> поворота** & **Преобразование -> Масштаб** объекта подбора сообщений hello. 
   
    ![][25]
3. Создание и присоединение **новый скрипт C#** вызывается **Rotator** toohello раскладки объекта. Убедитесь, что скрипт hello tooput скрипты в папке hello. 
   
    ![][26]
4. Откройте этот скрипт для изменения и обновить его hello toobe следующие: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Теперь режим воспроизведения попаданий hello в редактор Unity hello и презентации раскладки объект поворот по оси.
6. Создайте новую папку **Prefabs** 
   
    ![][27]
7. Перетащите hello **раскладки** объекта и сохраните его в папку Prefabs hello.
   
    ![][28]
8. Создайте новый **пустой игровой объект** с именем **Pickups**. Сбросить его tooorigin позиции, а затем перетащите объект подбора сообщений hello под этим объектом игры.  
   
    ![][29]
9. Повторяющиеся hello **раскладки** объекта и распространить ее на hello **Наземный** объекта вокруг hello **проигрывателя** объекта путем обновления hello **X и Z его Transform.Position**  значения соответствующим образом. 
   
    ![][30]
10. Создание **новый материал** вызывается **раскладки** и обновить toobe красным цветом, обновив hello **Albedo свойство** аналогичные toowhat мы обновления Наземный hello объекта. 
    
    ![][31]
11. Примените hello материала tooall hello 4 раскладки объекты.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Сбор объектов подбора сообщений hello
Приведенные ниже действия Hello принадлежат hello [Unity учебника](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Корпорация Майкрософт будет обновлять hello проигрыватель, который позволяет доступ too'collect "hello раскладки объектов, возникает конфликт с ними. 

1. Откройте hello **PlayerController** скрипта toohello вложенного объекта проигрывателя для редактирования и обновить его toohello следующие:  
   
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
2. Создайте новый **тега** вызывается **выбрать копирование** (она должна соответствовать в скрипте hello)  
   
    ![][33]
   
    ![][34]
3. Применить это **тега** toohello Prefab раскладки объекта. 
   
    ![][35]
4. Включить **IsTrigger** флажок для hello объекта Prefab.
   
    ![][36]
5. Добавьте объект Prefab tooPickup жесткая текста. Для оптимизации производительности мы обновим hello статических collider использования динамических collider tooa. 
   
    ![][37]
6. Наконец, проверьте hello **IsKinematic** свойство для объекта prefab hello. 
   
    ![][38]
7. Попаданий **воспроизведение** в редактор Unity hello и будет может tooplay данный **наката шарик** игры, перемещая hello объекта проигрывателя клавиши клавиатуры для направления входных данных. 

### <a name="updating-hello-game-for-mobile-play"></a>Обновление hello игры для мобильных устройств воспроизведения
разделы Hello выше завершения hello основам из Unity. Теперь нам предстоит изменить hello игры toomake его понятное мобильного устройства. Обратите внимание, что мы использовали ввод с клавиатуры для hello игры в данный момент для тестирования. Теперь мы будет изменен так, что позволит управлять hello проигрывателя с помощью перемещения hello hello телефона, т. е. с помощью акселерометр вводу hello. 

Откройте hello **PlayerController** скрипт для изменения и обновления hello **FixedUpdate** метод toouse hello движения из hello акселерометр toomove hello Player объекта. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Этот учебник завершает базовое игры создание с помощью Unity и его можно развернуть на устройстве игру Выбор tooplay hello. 

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













