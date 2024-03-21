# Android-Interviews-Prep

### Q1. Difference b/w activity and services


### Q2. Is main thread the same as UI thread?

### Q3. How Android system Render/draw layout on screen?

### Q4. Activity Launch Modes?

### Q5. Do viewmodels survive process death? if not what should we use to retain the data?
No, ViewModels do not survive process death by default. This means when the Android system kills your app process due to low memory or other reasons, the ViewModel and any data it holds are lost.

Here's a breakdown:

#### ViewModels survive configuration changes: 
They persist data through events like screen rotations or device configuration changes. This is their main purpose, and they handle it automatically.
ViewModels don't survive process death: If the system kills your app, the entire process is terminated, including the ViewModel.
However, there are ways to persist data across process death:

#### onSaveInstanceState: 
You can use this method in your Activity or Fragment to save data before the process ends and restore it when the app restarts.
ViewModel + SavedStateHandle: Introduced in AndroidX Lifecycle library, you can use SavedStateHandle within your ViewModel to store and retrieve data during process death. This approach keeps your logic separate from the Activity/Fragment lifecycle.

### Q6. What is process death in Android?

Process death in Android refers to the unexpected termination of your app's process. This means the entire system holding your app's running state and data abruptly shuts down, usually due to resource constraints or user actions.

Here are the main causes of process death:

System-initiated:

Low memory: When the device runs out of memory and needs to free some up, it might kill background apps based on their priority.
System updates: During updates, some apps might need to be restarted to adapt to the new system state.
App crashes: Bugs or unexpected situations can also lead to the system forcefully stopping the app.
User-initiated:

Swiping the app away: Users can manually remove background apps from the recent apps list, triggering process death.
Force stopping the app: Users might force stop apps from settings to free up resources or troubleshoot issues.
What happens during process death?

All components within the process (activities, services, broadcast receivers) are terminated.
Any data held in memory by these components is lost.
The app essentially starts fresh when it's launched again.
This can cause issues for users if the app loses important data or state information upon relaunch.

How to handle process death:

Understand your app's priority: Different processes have different priorities based on user interaction. Foreground apps are less likely to be killed compared to background ones.
Save essential data: Use methods like onSaveInstanceState or SavedStateHandle to save critical data before the process ends. This allows you to restore it when the app restarts.
Design your app to recover gracefully: Implement logic to handle situations where data might be lost due to process death. This can involve prompting users to refresh data or displaying appropriate error messages.
By understanding process death and implementing proper handling techniques, you can ensure your app provides a smooth and consistent experience for users even when unexpected interruptions occur.

### Q7. There are 100 data showing in recyclerview then how many times onCreateViewHolder, onBindViewHolder and viewholder are going to be called?
In a RecyclerView with 100 data items, the number of times onCreateViewHolder, onBindViewHolder, and ViewHolder methods are called depends on several factors:

1. Visibility of ViewHolders:

Initially visible:

onCreateViewHolder: Called only for the minimum number of ViewHolders required to fill the visible area of the RecyclerView. This is optimized for performance and memory usage.
onBindViewHolder: Called for each of the initially visible ViewHolders to bind data to their UI elements.
ViewHolder: Each created ViewHolder object is used exactly once during the initial rendering.
Scrolling and recycling:

As the user scrolls, more ViewHolders might need to be created and bound to display new data.
ViewHolders that are no longer visible (scrolled out of view) are recycled and reused to display new data, avoiding unnecessary creation.
onCreateViewHolder might be called again if additional ViewHolders are needed for scrolling or if the RecyclerView layout changes.
onBindViewHolder is called for each visible ViewHolder on every screen refresh (including scrolling), ensuring the UI reflects the latest data.
ViewHolder objects are reused and rebound with different data as needed during scrolling and recycling.
2. RecyclerView LayoutManager:

Different LayoutManagers (linear, grid, etc.) have different strategies for arranging and recycling ViewHolders, affecting the number of calls.
3. Data Updates:

If data changes and the adapter is notified, onBindViewHolder is called for affected ViewHolders to update their UI.
4. Customizations:

If you implement custom logic in onCreateViewHolder or onBindViewHolder, the number of calls will depend on that logic.
Example:

Assume a linear layout with 10 items visible on screen.
On initial load:
onCreateViewHolder: Called 10 times (one for each visible item).
onBindViewHolder: Called 10 times (to bind data to each visible item).
Scrolling down to reveal 5 new items:
onCreateViewHolder: Might be called 5 times (if no reusable ViewHolders are available).
onBindViewHolder: Called 15 times (10 for existing items, 5 for new items).
Key Points:

The exact number of calls varies based on your specific situation.
onCreateViewHolder is called less frequently than onBindViewHolder due to recycling.
Understanding these concepts is crucial for optimizing RecyclerView performance and memory usage.

Resources::
1. https://medium.com/@balsikandar/mastering-recyclerview-optimizations-in-android-f937919d4dd7


### Q8. How to send data from child fragment to parent fragment?

There are several ways to send data from a child fragment to its parent fragment in Android, each with its own advantages and disadvantages. Here are some common methods:

1. Interfaces:

Define an interface in the parent fragment that declares a method to receive the data.
Implement this interface in the child fragment and call the method when you have data to send.
This is a clean and decoupled approach, but requires more code and can be cumbersome for complex data structures.
2. Shared ViewModel:

Use a ViewModel shared between the parent and child fragments.
Both fragments can access and modify data in the ViewModel to share information.
This avoids tight coupling and is well-suited for data that needs to be shared across multiple fragments.
Requires understanding of ViewModel architecture and LiveData.
3. Activity as Mediator:

Access the parent Activity from the child fragment and call a method on the Activity to pass the data.
The Activity can then forward the data to the parent fragment.
This can be simpler than interfaces but can lead to tighter coupling with the Activity lifecycle.
4. Back Stack and Result Callbacks:

Set a result in the child fragment using getParentFragment().setResult() and include the data in the result bundle.
When the parent fragment pops the child fragment from the back stack, it will receive the result in its onActivityResult() method.
This method is suitable for passing data when the child fragment completes a specific task and needs to return data to the parent.
5. Event Bus:

Use a third-party library like EventBus to create a global event bus that both fragments can subscribe to.
The child fragment can publish an event with the data, and the parent fragment can listen for the event and receive the data.
This is useful for complex applications with multiple components that need to communicate.
Choosing the right method:

The best method depends on several factors, including:

Complexity of data: Interfaces might be simpler for basic data types, while ViewModels or event buses are better for complex data structures.
Coupling: Interfaces and Shared ViewModels are more decoupled than Activity as Mediator.
Lifecycle: Back Stack and Result Callbacks are good for specific tasks, while interfaces and ViewModels work well for ongoing communication.

### Q9. How views draw in its layout?


### Q9. Let's an activity is opened and we locked and then unlocked the phone, then what lefecycle are going to be called?

![Screenshot (402)](https://github.com/amitYadavDev/Android-Interviews-Prep/assets/45551012/c8106d8f-6d7c-4afb-8833-ae314a10fcbe)


### Q10. How views are rendered in Android xml?

### Q11. What do you understand by thread safe?

### Q12. Diff b/w const val and val in Kotlin?

### Q13. hashmap vs hashtable vs hashset

### Q14. How ViewModels survive activity re-creation?

### Q15. How layouts are drawn and best ways to develop efficient ui?

### Q16. Where livedata is observed? why in onCreate() why not in onResume() or onStart()
Ans. In most cases, an app component's onCreate() method is the right place to begin observing a LiveData object for the following reasons: To ensure the system doesn't make redundant calls from an activity or fragment's onResume() method.

### Q17. Creating a generic HashMap in Java/Kotlin

 // Creating a generic HashMap(Java)
 
        HashMap<String, Object> hashMap = new HashMap<>();
        // Adding key-value pairs
        hashMap.put("name", "John");
        hashMap.put("age", 30);
        hashMap.put("isStudent", true);
        
// Kotlin
 // Creating a generic HashMap
 
    val hashMap = HashMap<String, Any>()
    // Adding key-value pairs
    hashMap["name"] = "John"
    hashMap["age"] = 30
    hashMap["isStudent"] = true


### Q18. How will you filter in large data set in Android or any frontend while data is coming from web services?
