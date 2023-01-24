# Android-General-Interview-Question-Answer

**1. What is Application class ?** 

    The Application class in Android is the base class within an Android app that contains all other components such as activities and services.    
    The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.
    
**2. Difference between Activity and Service ?**

    Activity: An activity is the entry point for interacting with the user. It represents a single screen with a user interface.

    Service: A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.    
    It is a component that runs in the background to perform long-running operations or to perform work for remote processes. 
    A service does not provide a user interface.
  
 **3. How does the activity respond when orientation is changed ?** 
 
    According to the documentation, Some device configurations can change during runtime (such as screen orientation, keyboard availability, and when the user enables       multi-window mode). When such a change occurs, Android restarts the running Activity ( onDestroy() is called, followed by onCreate()). The restart behavior is           designed to help your application adapt to new configurations by automatically reloading your application with alternative resources that match the new device           configuration. 	
    
    
 **4. How to know configChange happens in onDestroy() function ?**
 
    Once an activity is in the process of finishing then isFinishing() method is returned true value, otherwise false when 
    the system is temporarily destroying the instance of the activity.
    
 **5. How to prevent the data from reloading when orientation is changed ?** 
 
    The most basic approach would be to use a combination of ViewModels and onSaveInstanceState(). A ViewModel is LifeCycle-Aware. 
    In other words, a ViewModel will not     be destroyed if its owner is destroyed for a configuration change (e.g. rotation). 
    The new instance of the owner will just re-connected to the existing ViewModel.  
    
    So if you rotate an Activity three times, you have just created three different Activity instances, but you only have one ViewModel.
    So the common practice is to store data in the ViewModel class (since it persists data during configuration changes) 
    and use OnSaveInstanceState() to store small amounts of UI data.
    
 **6. How to handle multiple screen sizes ?** 
 
    It's a long debate but in a very nutshell, you can do it in these ways:

	Use flexible layout like ConstraintLayout unless create alternative layout in different layout folders. 
    (e.g. layout-sw480, layout-sw600, layout-sw720 ...)
	Provide different bitmap drawables for different screen densities or use vector assets.
	Be aware of the screen orientation change approach in your application.
    If you don't want to handle it enforce to use just one orientation (portrait or landscape) through declaring it in the manifest file.
    
 **7. Difference between Service and IntentService ?**   
 
    Service is the base class for Android services that can be extended to create any service. 
    A class that directly extends Service runs on the main thread so it will block the UI (if there is one) 
    and should therefore either be used only for short tasks or should make use of other threads for longer tasks.

	IntentService is a subclass of Service that handles asynchronous requests (expressed as Intents) on demand. 
    Clients send requests through startService(Intent) calls. 
    The service is started as needed, handles each Intent in turn using a worker thread, and stops itself when it runs out of work. Read More on Mindorks's blog
    
 **8. What is Fragment ?** 
 
    A Fragment is a piece of an activity which enable more modular activity design. A fragment has its layout, its behavior, 
    and its life cycle callbacks. You can add or remove fragments in an activity while the activity is running. 
    You can combine multiple fragments in a single activity to build a multi-pane UI. A fragment can also be used in multiple activities. 
    The fragment life cycle is closely related to its host activity which means when the activity is paused, 
    all the fragments available in the activity will also be stopped.
  
 **9. Which method in fragment runs only once ?** 
 
 	According to the documentation, the onCreate() method is called once a fragment is created. Within your implementation, 
	you should initialize essential components of the fragment that you want to retain when the fragment is paused or stopped, then resumed.
	
 **10. What is the difference between Thread and AsyncTask ?** 
 
 	** AsyncTask
	
	AsyncTask enables proper and easy use of the UI thread. This class allows performing background operations and 
	publishing results on the UI thread without  having to manipulate threads and/or handlers. An asynchronous task is defined by a 
	computation that runs on a background thread and whose result is published on the UI thread.

	When, how, where?
		When to use?

		Small task having to communicate with main thread
		For tasks in parallel use multiple instances OR Executor
		Disk-bound tasks that might take more than a few milliseconds
		Trigger: Call to method execute()

		Triggered from: Main Thread

		Runs on: Worker thread. However, Main thread methods may be invoked in between to publish progress.
		
		Limitations / Drawbacks
		
		One instance can only be executed once (hence cannot run in a loop)
		Must be created and executed from the Main thread
		
	**Thread
		
	A Thread is a concurrent unit of execution. It has its own call stack. There are two methods to implement threads in applications. 
	One is providing a new class that extends Thread and overriding its run() method. 
	The other is providing a new Thread instance with a Runnable object during its creation.

	When, how, where?
	When to use?

	Long task in general (Network operations which involve moderate to large amounts of data either uploading or downloading)
	High-CPU tasks which need to be run in the background
	For tasks in parallel use Multiple threads (traditional mechanisms)
	Any task where you want to control the CPU usage relative to the GUI thread
	Trigger: Thread start() method. You can set the “Priority” of a thread by calling its setPriority(int) method.

	Triggered from: Any Thread

	Runs on: It’s own thread

	Limitations / Drawbacks
		
	Manual thread management
	Code may become difficult to read.
  
**11. What is Lopper and how it works ?** 

	Looper is a class which is used to execute the Messages(Runnables) in a queue. Normal threads have no such queue, 
	e.g. simple thread does not have any queue. It executes once and after method execution finishes, the thread will not run another Message(Runnable).
	
	If someone wants to execute multiple messages(Runnables) then he should use the Looper class which is responsible for creating a queue in the thread. 
	For example, while writing an application that downloads files from the internet, we can use Looper class to put files to be downloaded in the queue.
	
**12. What are Handlers ?** 	

	Handlers are objects for managing threads. It receives messages and writes code on how to handle the message.
	They run outside of the activity’s lifecycle, so they need to be cleaned up properly or else you will have thread leaks.
	Handlers allow communicating between the background thread and the main thread.
	
**13. Describe different types of Services in Android  ?**

	A Service is an application component that can perform long-running operations in the background, and it doesn't provide a user interface. 
	It can run in the background, even when the user is not interacting with your application. These are the three different types of services:

	Foreground Service: 
	A foreground service performs some operation that is noticeable to the user. For example, we can use a foreground service to play an audio track.

	Background Service: 
	A background service performs an operation that isn’t directly noticed by the user. In Android API level 26 and above, there are restrictions to using background services and it is recommended to use WorkManager in these cases.

	Bound Service: A service is bound when an application component binds to it by calling bindService(). A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results. A bound service runs only as long as another application component is bound to it.

	
	
