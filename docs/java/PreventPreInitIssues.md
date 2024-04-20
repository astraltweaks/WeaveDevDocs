# Preventing premature initialization
Premature initialization is your mod loads before Minecraft, which would result in a crash since you are trying to use packages from Minecraft that at this time, aren't loaded. <br >
We'll learn more about this later, so if you are just learning I would recommend skipping over this part, reading the other docs and then when you are ready to make a mod consider this part. <br >
You'll want to subscribe an event in your preinit, which when posted (after MC is initialized) will call the logic for your mod. In this case, InitEvent.
 
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
