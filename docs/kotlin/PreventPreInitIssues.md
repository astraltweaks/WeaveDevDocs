# Preventing premature initialization
Premature initialization is your mod loads before Minecraft, which would result in a crash since you are trying to use packages from Minecraft that at this time, aren't loaded. <br >
You'll want to subscribe an event in your preinit, which when posted (after MC is initialized) will call the logic for your mod. In this case, InitEvent.

```kotlin
package com.example.mod

import com.example.mod.InitEvent
import net.weavemc.api.ModInitializer
import net.weavemc.api.event.EventBus
import java.lang.instrument.Instrumentation

class Main : ModInitializer {

    override fun preInit(inst: Instrumentation) {
        EventBus.subscribe(InitEvent::class.java) {
            init() // I recommend using a method, but all logic here is called upon InitEvent being posted.
        }
    }

    private fun init() {
        // All logic called upon InitEvent being posted..
    }
}
```

<br >
To actually create this event, it will look something like this:

```kotlin
package com.example.mod

import net.weavemc.api.event.Event

class InitEvent : Event()
```

YOU MUST POST THE EVENT ON YOUR OWN. I use this as an example in the [Mixin guide](https://github.com/astraltweaks/WeaveDevDocs/new/main/docs/general/Mixins.md)! Please refer to it!
