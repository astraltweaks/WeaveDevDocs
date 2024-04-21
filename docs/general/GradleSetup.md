We will be using the Kotlin DSL for our Gradle file. <br >
We'll start by creating a `build.gradle.kts` and `settings.gradle.kts` file. Read the comments accordingly to understand what's going on. <br >
(Weave requires Gradle 8.4 or newer)
# build.gradle.kts
```kotlin
plugins {
    kotlin("jvm") version "1.9.23" // OPTIONAL, ADD THIS ONLY IF YOU ARE USING KOTLIN!
    id("net.weavemc.gradle") version "1.0.0-PRE2" // Add Weave Gradle plugin
}

group = "com.example" // Group, set correspondingly.
version = "1.0" // Version

weave {
    configure {
        name = "ExampleMod" // Name of your mod
        modId = "example" // Mod ID
        entryPoints = listOf("com.example.mod.Main") // Class of Entrypoint, will be called upon the game starting.
        mixinConfigs = listOf("example.mixins.json") // If you plan to use mixins, name this to name of your mixin configuration json, which should be created in resources.
        hooks = listOf("com.example.mod.hook.ExampleHook") // Hooks if you plan on using any.
        mcpMappings() // Mappings type, available are MCP mappings and yarn.
    }
    version("1.8.9") // Minecraft version
}

repositories {
    mavenCentral() // For Weave
    maven("https://repo.weavemc.dev/releases") // For Weave
    maven("https://repo.spongepowered.org/maven") // For Mixins
}

dependencies {
    implementation("net.weavemc.api:common:1.0.0-PRE2") // For Weave
    implementation("net.weavemc:internals:1.0.0-PRE2") // For Weave
    compileOnly("org.spongepowered:mixin:0.8.5") // For Mixins

}

// Keep this if you plan on using Kotlin, you can change the Java version as you'd like, but since we are using Minecraft 1.8, it's generally recommended to use Java 8, however Java 8 SUCKS!
kotlin {
    jvmToolchain(8)
}
```
# settings.gradle.kts
```kotlin
rootProject.name = "ExampleMod" // Name of your project

pluginManagement {
    repositories {
        gradlePluginPortal()
        maven("https://repo.weavemc.dev/releases") // Add the weave plugin
    }
}
```
