Using the EventBus in Weave is quite simple. While Weave's EventBus doesn't come with any events, you can use your own custom events, which will be discussed in the next guide.
# Posting Events
To post an event you just need to do this: <br >
(Java)
```java
EventBus.postEvent(new EventType());
```
(Kotlin)
```kotlin
EventBus.postEvent(EventType())
```
# Subscribing/Unsubscribing
By subscribing, you subscribe a new instance of a class, and every method set to an event in that class will be called based on the event they are using. <br >
Because you are creating a new instance of a class, it is recommended to store it in a variable so you don't just create duplicates over and over. Then you are like me, with instancing issues (not required for singletons). <br >
(Java)
```java
EventListener eventListener = new EventListener();

EventBus.subscribe(eventListener);
```
(Kotlin)
```kotlin
val eventListener: EventListener = EventListener()

EventBus.subscribe(eventListener)
```
# Creating a listener
To create a listener, the parameter of an event has to be an event type, and you must annotate it with @SubsribeEvent, then when the event is subscribed, it will be called according to its event. <br >
(Java)
```java
@SubscribeEvent
public void onEvent(EventType e) {
    e.getEventInfo(); // If you want to get data from the event you can do something like this
}
```
(Kotlin)
```kt
@SubscribeEvent
fun onEvent(e: EventType) {
    e.info // If you want to get data from the event you can do something like this, because it's Kotlin getters and setters are automatically generated so you can use it like this
}
