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




