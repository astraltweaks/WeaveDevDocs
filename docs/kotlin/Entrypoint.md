Creating an entrypoint in Weave is trivial, simply make your class implement the ModInitializer then implement an override function called preInit with instrumentation in the parameters and then all of that logic will be called before the game starts.
# Code Snippet
```kotlin
package com.example.mod

import net.weavemc.api.ModInitializer
import java.lang.instrument.Instrumentation

class Main : ModInitializer { // Implement ModInitializer!

    override fun preInit(inst: Instrumentation) { // Ensure you are using an override function with instrumentation parameters
        println("Hello, World!") // All logic from here on is called before the game starts.
    }
}
```
