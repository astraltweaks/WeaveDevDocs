This tutorial will contain only Kotlin snippets, as literally as I was creating this I got messaged about how cluttered events were in Java. I will provide an explanation for them, but I won't be writing them. The premature initialization guide has an event created in Java.
# Creating Custom Events
It's really simple, just extend the Event class and if you have any extra data that you need to get out of the Event, you can add it as a value in the constructor. Kotlin will automatically generate getters and setters so that if you need to get these values or set them, you don't have to create getters and setters like you do in Java. Get wrekt, Java users!!!! (I'm a Kotlin advocate)
```kotlin
package com.example.mod

import net.weavemc.api.event.Event

class ChatEvent(val message: String) : Event()
```
# Creating Custom Cancellable Events
Really all you have to change to make a cancellable event is extend cancellable event, then you can make logic for if it's cancelled. In a mixin, ci.cancel will act as a return statement being added within the Minecraft code at that location. This can be used in the following way to make a cancellable event:
```java
@Inject(method = "sendChatMessage", at = @At("HEAD"), cancellable = true)
public void onChatMessage(String message, CallbackInfo ci) {
    ChatEvent chatEvent = new ChatEvent(message);
    EventBus.postEvent(chatEvent);
    if (chatEvent.isCancelled()) ci.cancel();
}
```
This can be used in practice like this:
```kotlin
@SubscribeEvent
fun onChat(e: ChatEvent) {
    if (e.message == hi) {
      e.cancelled = true
      println("Message was hi, therefore it wasn't sent.")
  }
}
```
