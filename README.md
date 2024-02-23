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



