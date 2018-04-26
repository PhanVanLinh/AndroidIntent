# AndroidIntent

> An Intent is a messaging object you can use to request an action from another app component. 


basically, intent help communicate between app components (activity, service, broadcast receiver, content provider) 

### THREE fundamental use cases
- Start activity  
`startActivity(Intent service)`
- Start service  
`startService(Intent service)`
- Delivering a broadcast  
`sendBroadcast(Intent, String)`

### Intent types
- **Explicit intents**   
Specific the component will start   
Example `startActivity(new Intent(this, TargetActivity.class))`

- **Implicit intents**  
Do not name a specific component, but instead declare a general action to perform  
Example `startActivity(new Intent(Intent.ACTION_VIEW, url);`  
*How implicit intent work?*  
When we start implicit intent, Android System will search **all apps manifests in the devices** to find **intent filter that matches the intent**. 
If it found 1 app, it will start, if it found multiple apps it will display dialog for choose which app will start

### Build Intent
1) Component name  
`setComponent()`, `setClass()`, `setClassName()`
2) Action  
`ACTION_VIEW`, `ACTION_SEND`, `ACTION_EDIT`
3) Data  
`setData(Uri data)`  
For example, if the action is ACTION_EDIT, the data should contain the URI of the document to edit
4) Category  
Kind of component that should handle the intent (most of intent don't need category)  
Example  
`CATEGORY_BROWSABLE` => will start a web browser
`CATEGORY_LAUNCHER` => will start a launcher

5) Extras  
Key-value pairs that carry additional information
`putExtras()`

6) Flags  
The flags may instruct the Android system how to launch an activity (for example, which task the activity should belong to) and how to treat it after it's launched (for example, whether it belongs in the list of recent activities)

### Why use IntentChooser?
By default, user can choose `ALWAYS` (instead of `JUST ONCE`) to force open a specific application every time.  
This is good in most case but if we don't want it, we can use `IntentChooser`.  `IntentChooser` force user select the app every time start intent.

### Receiving an implicit intent
Declare `intent-filter` to your app manifest for allow your app receive intent

### Restricting access to components
Use `android:exported`  
If "false", the activity can be launched only by components of the same application  or applications with the same user ID

We can also use `<permission android:name=""` to limit access to own app component

### Reference
https://developer.android.com/guide/components/intents-filters