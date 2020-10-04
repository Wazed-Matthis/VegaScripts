#Client scripting

This is the official documentation of the Client scripting language

#Interpreters

#### _Functions_
Note that every function must be included in a Module. This means, that in order to execute a function the moduleName must be given like this: `ModuleName_EventName` 

 - EventTick 
   ```
   This Event is being executed every game tick (20 times a sec.)
   ```
- KeyEvent
   ```
   Event is getting executed every KeyPress 
   Key: event.getPressedKey();
   ```
 - EventPacket
    ```
    Event is getting executed on every sent Packet 
    Packet: event.getPacket();
    ```
 - PostRender3DEvent
    ```
    3D Render Pipeline
    ```
 - EventRender2D
    ```
    2D Render Pipeline
    ```
 - EventMotion
    ```
    Event is getting executed when the server sends the client info ( such as current pitch or yaw) to the server
       
    Available
    getPosX()
    getType()
    getPosY()
    getPosZ()
    getRotationYaw()
    getRotationPitch()
    isOnGround()  
    ```
 - VelocityEvent
    ```
    Event is getting executed when the player takes Velocity from a hit or from an explosion
    get/set MotionX
    get/set MotionY
    get/set MotionZ
    isCanceled()
    setCanceled()
    ```
   
 - EventEntityMove
   ```
   Event is getting executed when the player moves from a position to another
   get/set MotionX
   get/set MotionY
   get/set MotionZ
   isCanceled()
   setCanceled()
   ```
#### _Function example_
```JavaScript
var EventTick = function(event){
    //TODO: Do something
}
```

### Extraordinary Events

 - The EventRender2D is being called in the renderLoop constantly, wich means that you can always draw something on the canvas
 - The EventRender3D is being called in the renderLoop constantly, wich means taht you can always render something in the World with given positiions

#### _Fields_
 - mc
 - render_util
 - blur_util
 ```
 startBlur() enables drawing to the blurBuffer in order to blur a specific area u have to draw a rect with the given positions 
 stopBlur() disables drawing to the blurBuffer
 ```
 - module_manager \
   With the module_manager, you can add your own modules to the client like this:
   ```js
   //First, let the script know what a category is:
   var Category = Java.type("de.hush.client.modules.Category");
   
   //Then make a variable for the module you are going to add like this:
   var m = module_manager.addScriptingModule("Name","DisplayName","Description", /*Here comes your category*/ Category.MISC);
   /*
       Categories available:
       COMBAT, MISC, MOVEMENT, PLAYER, RENDER, WORLD
   */
   
   //Then you can add settings to the module
   //Your given moduleVariable.add<YourSettingType>Setting
   m.addBooleanSetting("Test",false);
   
   /*
        Available Setting types:
        addIntegerSetting
        addModeSetting
        addBooleanSetting
   */
   
   //You can also get the value of them like this:
   m.getIntegerSetting
   m.getModeSetting
   m.getBooleanSetting
   ```

