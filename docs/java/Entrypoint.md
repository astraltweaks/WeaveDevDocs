Creating an entrypoint in Weave is trivial, simply make the class implement the ModInitializer and implement and override method called preInit with instrumentation (Add @NotNull since we're using Java) and then all of that logic will be called before the game starts. <br >
# Code Snippet
```java
package com.example.mod;

import net.weavemc.api.ModInitializer;
import org.jetbrains.annotations.NotNull;

import java.lang.instrument.Instrumentation;

public class Main implements ModInitializer { // Implement ModInitializer!

    @Override //Ensure you annotate this method with @Override, otherwise it won't work.
    public void preInit(@NotNull Instrumentation inst) { // ENSURE that you use @NotNull, otherwise you'll probably crash.
        System.out.println("Hello, World!"); // All logic from here on is called before the game starts.
    }
}
```
