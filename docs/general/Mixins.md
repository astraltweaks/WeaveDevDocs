Spongepowered Mixins are used to modify Minecraft's existing code in a user friendly way. Mixins should **never** be written in Kotlin due to compatibility issues, thus this tutorial will be for Java. <br >
Make sure you have all of the mixin related stuff in your Gradle file, refer to [GradleSetup.md](https://github.com/astraltweaks/WeaveDevDocs/blob/main/docs/general/GradleSetup.md)! <br >
If you are unsure of how to write a mixin, this guide only shows a simple example and explanation of how they work, I highly recommend checking out [MixinCheatSheet](https://github.com/2xsaiko/mixin-cheatsheet)!
# Creating your mixins.json file
Create a file called `modid.mixins.json` (in this case example is in place of modid) in src/main/resources, it should look something like this.
```json
{
  "compatibilityLevel": "JAVA_8",
  "package": "com.example.mod.mixin",
  "mixins": [
    "MinecraftMixin"
  ]
}
```
Package is your mixin package, and each mixin is the name of the class, I recommend downloading the Minecraft development plugin for IntelliJ for Mixins, as it will autofill missing parameters and let you easily access your Mixin config.
# Adding it to Gradle
Refer to [GradleSetup.md](https://github.com/astraltweaks/WeaveDevDocs/blob/main/docs/general/GradleSetup.md) and in the place of the Mixins config, put the name of your mixin json.
# Creating a Mixin
Mixins are really simple to understand, and in this case I will show you can example mixin with comments on how to create a mixin to post that InitEvent I was talking about in the previous guide.
```java
package com.example.mod.mixin;

import com.example.mod.event.InitEvent;
import net.minecraft.client.Minecraft;
import net.weavemc.api.event.EventBus;
import org.spongepowered.asm.mixin.Mixin;
import org.spongepowered.asm.mixin.injection.At;
import org.spongepowered.asm.mixin.injection.Inject;
import org.spongepowered.asm.mixin.injection.callback.CallbackInfo;

@Mixin(Minecraft.class) // The class that you are mixining
public class MinecraftMixin {

    @Inject(method = "startGame", at = @At("TAIL")) // Add your code to the bottom of a method
    public void onStartGame(CallbackInfo ci) {
        EventBus.postEvent(new InitEvent()); // Use the eventbus to post the Initialization event
    }
}
```
MAKE SURE YOU ADD YOUR MIXIN TO YOUR JSON FILE!
