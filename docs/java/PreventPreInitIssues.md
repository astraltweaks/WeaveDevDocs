# Preventing premature initialization
Premature initialization is when your mod loads before Minecraft, which would result in a crash since you are trying to use packages from Minecraft that at this time, aren't loaded. <br >
You'll want to subscribe an event in your `preInit`, which will call the logic for your mod when posted (after MC is initialized). In this case, InitEvent.
 
```java
package com.example.mod;

import com.example.mod.event.InitEvent;
import net.weavemc.api.ModInitializer;
import net.weavemc.api.event.EventBus;
import org.jetbrains.annotations.NotNull;

import java.lang.instrument.Instrumentation;

public class Main implements ModInitializer {

    @Override
    public void preInit(@NotNull Instrumentation inst) {
        EventBus.subscribe(InitEvent.class , event -> {
            init(); // I recommend using a method, but all logic here is called upon InitEvent being posted.
        });
    }

    private void init() {
        // All logic called upon InitEvent being posted..
    }
}

```
<br >
To actually create this event, it will look something like this:

```java
package com.example.mod.event;

import net.weavemc.api.event.Event;

public class InitEvent extends Event {}
```
YOU MUST POST THE EVENT ON YOUR OWN. I use this as an example in the [Mixin guide](https://github.com/astraltweaks/WeaveDevDocs/blob/main/docs/general/Mixins.md)! Please refer to it!
