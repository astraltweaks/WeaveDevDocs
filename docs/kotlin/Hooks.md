This tutorial will not be written in Java due to the sheer pain it is to do in Java. <br >
Hooks insert raw bytecode into existing code, this is basically just a lot more complicated of a Mixin. <br >
This is NOT the place to learn how to write a hook, just to learn how to create one in Weave. That's way too complicated for this tiny guide. 

# Code Snippet
This code posts an InitEvent. I'll add comments so you can understand what's going on. This does the exact same thing as the Mixin I gave as example in the mixin guide.
```kotlin
package com.example.mod

import com.example.mod.InitEvent
import net.weavemc.api.Hook
import net.weavemc.api.event.Event
import net.weavemc.api.event.EventBus
import net.weavemc.internals.asm
import net.weavemc.internals.internalNameOf
import net.weavemc.internals.named
import org.objectweb.asm.tree.ClassNode
import org.objectweb.asm.Opcodes.RETURN

class MinecraftHook : Hook("net/minecraft/client/Minecraft") { // The constructor is the target

    override fun transform(node: ClassNode, cfg: AssemblerConfig) {
        val initMethod = node.methods.named("startGame") // Iterates through methods in this class to find the one named startGame and then stores it as a variable
        initMethod.instructions.insertBefore(initMethod.instructions.findLast {it.opcode == RETURN}, asm { // Finds the final return statement (end of method), uses Weave's ASM DSL
            new(internalNameOf<InitEvent>()) // Creates a new instance of InitEvent
            dup // You are supposed to add dup after creating a new instance of a class
            invokespecial(internalNameOf<InitEvent>(), "<init>", "()V") // Invokes the InitEvent
            invokestatic(
                internalNameOf<EventBus>(),
                "postEvent", // Calls postEvent from the EventBus
                "(L${internalNameOf<Event>()};)V" // Parameter type is event
            ) // Post the event
        })
    }
}
```
MAKE SURE YOU ADD YOUR HOOK TO THE GRADLE FILE AS SHOWN IN [GRADLESETUP.MD](https://github.com/astraltweaks/WeaveDevDocs/blob/main/docs/general/GradleSetup.md)!
