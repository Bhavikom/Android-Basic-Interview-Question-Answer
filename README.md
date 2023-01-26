# Android-General-Interview-Question-Answer

**1: What is the architecture of Android ?**

	Android architecture features five main components:
	
	Applications
	Android Framework
	Android Runtime
	Platform Libraries
	Linux Kernel
**2. How Android apps compiled and run ?**

	First step involves compiling the resources folder (/res) using the aapt (android asset packaging tool) tool. 
	These are compiled to a single class file called R.java. This is a class that just contains constants.

	Second step involves the java source code being compiled to .class files by javac, and then the class files are 
	converted to Dalvik bytecode by the “dx” tool, which is included in the sdk ‘tools’. The output is classes.dex.

	The final step involves the android apkbuilder which takes all the input and builds the apk (android packaging key) file.

**3. What is Application class ?** 

    The Application class in Android is the base class within an Android app that contains all other components such as activities and services.    
    The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.
    
**4. Tell all the Android application components ?**

	There are four different types of app components:
	1.Activities
	2.Services
	3.Broadcast receivers
	4.Content providers
    
**5. Difference between Activity and Service ?**

    Activity: An activity is the entry point for interacting with the user. It represents a single screen with a user interface.

    Service: A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.    
    It is a component that runs in the background to perform long-running operations or to perform work for remote processes. 
    A service does not provide a user interface.
  
 **6. How does the activity respond when orientation is changed ?** 
 
    According to the documentation, Some device configurations can change during runtime (such as screen orientation, keyboard availability, and when the user enables       multi-window mode). When such a change occurs, Android restarts the running Activity ( onDestroy() is called, followed by onCreate()). The restart behavior is           designed to help your application adapt to new configurations by automatically reloading your application with alternative resources that match the new device           configuration. 	
    
    
 **7. How to know configChange happens in onDestroy() function ?**
 
    Once an activity is in the process of finishing then isFinishing() method is returned true value, otherwise false when 
    the system is temporarily destroying the instance of the activity.
    
 **8. How to prevent the data from reloading when orientation is changed ?** 
 
    The most basic approach would be to use a combination of ViewModels and onSaveInstanceState(). A ViewModel is LifeCycle-Aware. 
    In other words, a ViewModel will not     be destroyed if its owner is destroyed for a configuration change (e.g. rotation). 
    The new instance of the owner will just re-connected to the existing ViewModel.  
    
    So if you rotate an Activity three times, you have just created three different Activity instances, but you only have one ViewModel.
    So the common practice is to store data in the ViewModel class (since it persists data during configuration changes) 
    and use OnSaveInstanceState() to store small amounts of UI data.
    
 **9. How to handle multiple screen sizes ?** 
 
    It's a long debate but in a very nutshell, you can do it in these ways:

	Use flexible layout like ConstraintLayout unless create alternative layout in different layout folders. 
    (e.g. layout-sw480, layout-sw600, layout-sw720 ...)
	Provide different bitmap drawables for different screen densities or use vector assets.
	Be aware of the screen orientation change approach in your application.
    If you don't want to handle it enforce to use just one orientation (portrait or landscape) through declaring it in the manifest file.
    
 **10. Difference between Service and IntentService ?**   
 
    Service is the base class for Android services that can be extended to create any service. 
    A class that directly extends Service runs on the main thread so it will block the UI (if there is one) 
    and should therefore either be used only for short tasks or should make use of other threads for longer tasks.

    IntentService is a subclass of Service that handles asynchronous requests (expressed as Intents) on demand. 
    Clients send requests through startService(Intent) calls. 
    The service is started as needed, handles each Intent in turn using a worker thread, and stops itself when it runs out of work. Read More on Mindorks's blog
    
 **11. What is Fragment ?** 
 
    A Fragment is a piece of an activity which enable more modular activity design. A fragment has its layout, its behavior, 
    and its life cycle callbacks. You can add or remove fragments in an activity while the activity is running. 
    You can combine multiple fragments in a single activity to build a multi-pane UI. A fragment can also be used in multiple activities. 
    The fragment life cycle is closely related to its host activity which means when the activity is paused, 
    all the fragments available in the activity will also be stopped.
  
 **12. Which method in fragment runs only once ?** 
 
 	According to the documentation, the onCreate() method is called once a fragment is created. Within your implementation, 
	you should initialize essential components of the fragment that you want to retain when the fragment is paused or stopped, then resumed.
	
 **13. What is the difference between Thread and AsyncTask ?** 
 
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
	
**14. What are Handlers ?** 	

	Handlers are objects for managing threads. It receives messages and writes code on how to handle the message.
	They run outside of the activity’s lifecycle, so they need to be cleaned up properly or else you will have thread leaks.
	Handlers allow communicating between the background thread and the main thread.
	
**15. Describe different types of Services in Android  ?**

	A Service is an application component that can perform long-running operations in the background, and it doesn't provide a user interface. 
	It can run in the background, even when the user is not interacting with your application. These are the three different types of services:

	Foreground Service: 
	A foreground service performs some operation that is noticeable to the user. For example, we can use a foreground service to play an audio track.

	Background Service: 
	A background service performs an operation that isn’t directly noticed by the user. In Android API level 26 and above, there are restrictions to using background services and it is recommended to use WorkManager in these cases.

	Bound Service: A service is bound when an application component binds to it by calling bindService(). A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results. A bound service runs only as long as another application component is bound to it.
	
**16. What are the major differences between ListView and RecyclerView  ?**	

	1. ViewHolder Pattern: 
	Recyclerview implements the ViewHolders pattern whereas it is not mandatory in a ListView. 
	A ViewHolder object stores each of the component views inside the tag field of the Layout, 
	so you can immediately access them without the need to look them up repeatedly. 
	In ListView, the code might call findViewById() frequently during the scrolling of ListView, which can slow down performance. 
	Even when the Adapter returns an inflated view for recycling, you still need to look up the elements and update them. 
	A way around repeated use of findViewById() is to use the "view holder" design pattern.

	2. LayoutManager: 
	In a ListView, the only type of view available is the vertical ListView. 
	A RecyclerView decouples list from its container so we can put list items easily at run time 
	in the different containers (linearLayout, gridLayout) by setting LayoutManager.

	3. Item Animator: 
	ListViews are lacking in support of good animations, but the RecyclerView brings a whole new dimension to it.
	
**17. What is the difference between margin and padding  ?**	

	Padding will be space added inside the container, for instance, if it is a button, padding will be added inside the button.

	Margin will be space added outside the container.
	
**18. What is sw keyword in layout-sw600 folder meaning ?**

	The sw keywrod which stands on "smallest width" is an screen size qualifier that allow you to provide alternative 
	layouts for screens that have a minimum width measured in dp. The smallest width qualifier specifies the smallest 
	of the screen's two sides, regardless of the device's current orientation, so it's a simple way to specify the overall screen size available for your layout.    	 Here is some useful values:

	320dp: a typical phone screen (240x320 ldpi, 320x480 mdpi, 480x800 hdpi, etc).
	480dp: a large phone screen ~5" (480x800 mdpi).
	600dp: a 7” tablet (600x1024 mdpi).
	720dp: a 10” tablet (720x1280 mdpi, 800x1280 mdpi, etc).
	
**19. How to pass items to fragment ?**
	
	Using Bundle you can pass items to the fragment.
	
**20. How would you communicate between two fragments ?**

	There are several ways to communicate two fragments. Using interfaces are a common way to do that. 
	You can connect two fragments through interfaces that are implemented in the parent activity.
	
**21. Difference between adding/replacing fragment in backstack ?**

	replace removes the existing fragment and adds a new fragment. 
	This means when you press back button the fragment that got replaced will be created with its onCreateView being invoked.

	add retains the existing fragments and adds a new fragment that means existing fragment will be active and they wont be 
	in 'paused' state hence when a back button is pressed onCreateView is not called for the existing 
	fragment(the fragment which was there before new fragment was added).

	In terms of fragment’s life cycle events onPause(), onResume(), onCreateView() and other life cycle events will be 
	invoked in case of replace but they wont be invoked in case of add.
	
**22. What is the difference between dialog and dialogFragment ?**


	THe dialog is a small window that prompts the user to make a decision or enter additional information. 
	Instead, dialogFragment is a fragment that displays a dialog windows and contains a dialog object.

	DialogFragment does various things to keep the fragment's lifecycle driving it, instead of the Dialog. 
	Dialogs are generally autonomous entities -- they are their own window, receiving their own input events, 
	and often deciding on their own when to disappear. DialogFragment needs to ensure that what is happening 
	with the Fragment and Dialog states remains consistent. To do this, it watches for dismiss events from 
	the dialog and takes care of removing its own state when they happen.
	
**23. What is the difference between Foreground and Background and Bounded service ?**

	Foreground Service: A foreground service performs some operation that is noticeable to the user. 
	For example, we can use a foreground service to play an audio track. A Notification must be displayed to the user.

	Background Service: A background service performs an operation that isn’t directly noticed by the user. 
	In Android API level 26 and above, there are restrictions to using background services and it is recommended to use WorkManager in these cases

	Bound Service: A service is bound when an application component binds to it by calling bindService(). 
	A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results. 
	A bound service runs only as long as another application component is bound to it.
	
**24. What is contentProvider and what is typically used for ?**

	A ContentProvider provides data from one application to another, when requested. It manages access to a structured set of data. 
	It provides mechanisms for defining data security. Learn more. For further reading see the official android documentation
	
**25. What is the difference between apply() and commit() in sharedPreferences ?**

	commit() writes the data synchronously and returns a boolean value of success or failure depending on the result immediately.

	apply() is asynchronous and it won’t return any boolean response. Also if there is an apply() outstanding and we perform another commit(),
	The commit() will be blocked until the apply() is not completed.
	
**26. What Is the Singleton Pattern ?**

	The Singleton Pattern is a software design pattern that guarantees a class has one instance only and a global point of 
	access to it is provided by that class. Anytime multiple classes or clients request for that class, they get the same instance of the class. 
	This Singleton class may be responsible for instantiating itself, or you can delegate the object creation to a factory class
	
	In a typical Android app, there are many objects for which we only need one global instance, whether you are using 
	it directly or simply passing it to another class. Examples include caches, OkHttpClient, HttpLoggingInterceptor, 
	Retrofit, Gson, SharedPreferences, the repository class, etc. If we were to instantiate more than one of these 
	types of objects, we'd run into problems like incorrect app behaviour, resource overuse, and other confusing results. 
	
	It's quite easy to implement this pattern. The following code snippet shows how a Singleton is created.

	public class Singleton  {
    		private static Singleton INSTANCE = null;
    		// other instance variables can be here 
    
    		private Singleton() {};
    		public static Singleton getInstance() {
        	if (INSTANCE == null) {
            		INSTANCE = new Singleton();
        	}
        	return(INSTANCE);
    	}
 	// other instance methods can follow 
}

**27. What Is serializable and parcelable and find difference ?**

	While developing android applications, we often used to transfer the data from one activity to another. 
	When we have data like boolean values, int values, String values we can pass these data very easily through intent. For example:-

	intent.putExtra("INT_KEY", 100); // we can pass like this
	getIntent().getBundleExtra("INT_KEY"); // we can get Values from Intent like this
	
	But In some cases, we have to pass complex POJO class objects (e.x. Student, Employee, Vehicle etc.) to another activity. 
	In this scenario, we have to do some extra stuff with the POJO class that makes object to be easily transferrable from one activity to another.

	We can achieve this by using two concepts which are Serializable and Parcelable.
	
	1. Serializable : 
	
	Serializable is a standard Java interface which belongs to java.io.Serializable. It is not part of the Android SDK. Here is an example:-
	
	public class Employee implements Serializable {

		private String name;
		private int age;
		public String address;

		public Employee(String name, int age, String address)   {
			super();
			this.name = name;
			this.age = age;
			this.address = address;
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public String getAddress() {
			return address;
		}

		//we can pass data like this from activity
		Employee employee = new Employee("ABC", 23, "XYZ 03");
		mIntent.putExtra("EMPLOYEE_KEY", employee);
		//we can get data like this in other activity
		getIntent().getSerializableExtra("EMPLOYEE_KEY");
	}
	
	2. Parcelable : 
	
	Parcelable is also an interface that belongs to android.os.Parcelable. It is part of the Android SDK. 
	It converts the object into a byte stream and passes the data between activities. To implement this with POJO class 
	we have to override some methods and write Creators method. Here is an example:-
	
	public class Employee implements Parcelable {
    		private int age;
    		private String name;
    		private String address;
    		public Employee(String name, int age, String address) {
        		this.name = name;
        		this.age = age;
        		this.address = address;
    		}
    		public Employee(Parcel source) {
        		age = source.readInt();
        		name = source.readString();
        		address = source.readString();
    		}
    		@Override
    		public int describeContents() {
        		return 0;
   		}
    		@Override
    		public void writeToParcel(Parcel dest, int flags) {
        		dest.writeInt(age);
        		dest.writeString(name);
        		dest.writeString(address);
    		}
    		public int getAge() {
        		return age;
    		}
   		public String getName() {
        		return name;
    		}
    		public String getAddress() {
            		return address;
    		}
   	 	public static final Creator<Employee> CREATOR = new Creator<Employee>() {
        		@Override
        		public Employee[] newArray(int size) {
            			return new Employee[size];
        		}
        		@Override
        		public Employee createFromParcel(Parcel source) {
            			return new Employee(source);
        		}
    		};
	}
	//we can pass data like this from activity
	Employee employee = new Employee("ABC", 23, "XYZ 03");
	mIntent.putExtra("EMPLOYEE_KEY", employee);
	//we can get data like this in other activity
	getIntent().getParcelableExtra("EMPLOYEE_KEY");
	
	**Difference between Serializable and Parcelable

	1.Serializable is a slow process whereas Parcelable is fast.
	2.Parcelable interface takes more time to implement in comparison to Serializable.
	3.Serializable creates lots of temporary objects in comparison to Parcelable.
	4.Serializable is not reflection safe whereas Parcelable is reflection safe.

**28. Describe different Activity Launch Mode ?**

	There are four types of launch modes:
	Standard
	Single top
	Single task
	Single instance
	
	1. Standard
	When you don't specify any launch mode, standard is the default one. It creates a new instance of the activity every time you start it
	
	2. Single top
	In this launch mode, if an activity is at the top of the task and you create its instance again, then a new instance will not be created. 
	Instead onNewIntent() will be called with updated data. If activity is not on top, a new instance will be pushed
	
	3. Single task
	In this launch mode, if the activity doesn't exist in the task, a new instance is created otherwise onNewIntent() is called. 
	Additionally, activities above it get destroyed
	
	4. Single instance
	For an activity that has a single instance launch mode, a new task is created.

**29. What is Context in Android ?**

	-The Context in Android is actually the context of what we are talking about and where we are currently present. 
	This will become more clear as we go along with this.

	-Few important points about the context:

	-It is the context of the current state of the application.
	-It can be used to get information regarding the activity and application.
	-It can be used to get access to resources, databases, and shared preferences, and etc.
	-Both the Activity and Application classes extend the Context class.
	-Context is almost everywhere in Android Development and it is the most important thing in Android Development, 
	so we must understand to use it correctly.

	-Wrong use of Context can easily lead to memory leaks in an android application.

	-As there are different types of context in Android, we as an Android Developer often get confused about which 
	context to use at which place. So let’s understand what are those, how to use those, and when to use which one.

	-Mainly two types of context:

	-Application Context: It is the application and we are present in Application. For example - MyApplication(which extends Application class). 
	It is an instance of MyApplication only.
	-Activity Context: It is the activity and we are present in Activity. For example - MainActivity. It is an instance of MainActivity only.
		
**30. Android Activity Lifecycle methods ?**	

	onCreate  called when activity is first created.
	onStart	  called when activity is becoming visible to the user.
	onResume  called when activity will start interacting with the user.
	onPause	  called when activity is not visible to the user.
	onStop	  called when activity is no longer visible to the user.
	onRestart called after your activity is stopped, prior to start.
	onDestroy called before the activity is destroyed.
	
**31. What is the difference between onCreate() and onStart() ?**

	onCreate() method gets called when activity gets created, and its called only once in whole Activity life cycle. 
	where as onStart() is called when activity is stopped... I mean it has gone to background and its onStop() method is called by the os. 
	onStart() may be called multiple times in Activity life cycle
	
**32. When only onDestroy is called for an activity without onPause() and onStop() ?**

	if you call finish() while creating the Activity in onCreate(), the system will invoke onDestroy() directly.
	
**33. What is onSavedInstanceState() and onRestoreInstanceState() in activity ?**

	1.onSavedInstanceState() - This method is used to store data before pausing the activity.
	2.onRestoreInstanceState() - This method is used to recover the saved state of an activity when the activity is recreated after destruction. 
	So, the onRestoreInstanceState() receive the bundle that contains the instance state information.
	
**34. Fragment Lifecycler ?**

	onAttach() = 
	The very first method to be called when the fragment has been 	associated with the activity. 
	This method executes only once during the lifetime of a fragment.  
	
	onCreate() = 
	This method initializes the fragment by adding all the required attributes and components.
	
	onCreateView()	= 
	System calls this method to create the user interface of the fragment. The root of the fragment’s layout is returned as the View 
	component by this method to draw the UI.
	
	onActivityCreated() = 
	It indicates that the activity has been created in which the fragment exists. 
	View hierarchy of the fragment also instantiated before this function call. 
	
	onStart()	= The system invokes this method to make the fragment visible on the user’s device.
	onResume()	= This method is called to make the visible fragment interactive.
	onPause()	= It indicates that the user is leaving the fragment. System call this method to commit the changes made to the fragment. 
	onStop()	= Method to terminate the functioning and visibility of fragment from the user’s screen. 
	onDestroyView()	= System calls this method to clean up all kinds of resources as well as view hierarchy associated with the fragment.
	onDestroy()	= It is called to perform the final clean up of fragment’s state and its lifecycle.
	onDetach()	= The system executes this method to disassociate the fragment from its host activity.
	
**35. what is ViewBinding ?**

	ViewBinding is a feature in an android that allows you to access all of the UI components directly via generated Binding classes. 
	Once you enable the view binding in a build.gradle file, it generates Binding classes which contain all UI components references.

	If your layout file name is like game_score.xml then it will generate its class with the name like GameScoreBinding.

	Advantages of View Binding:
	Null safety:
	Because View Binding directly creates a reference to views, there is not any risk of a null pointer exception.
	Type safety:
	The Generated binding class has the same class types fields as present in the XML file, so there are no risks for class cast exceptions.
	
**36. What is data binding in Android ?**

	Data binding is the process of integrating views in an XML layout with data objects. The Data Binding Library 
	is responsible for generating the classes required for this procedure.
	
**37: How do you protect an Android app from reverse engineering?
	
	Make sure you are well aware of prevention tactics and tools such as tamper detection, ProGuard Assistance, and SafetyNet. 
	List other best practices such as using C++ for important code, securing user credentials, server-side database encryption, 
	and altering Android's shared library loading process.
	
**40. What is the difference between getContext(), getApplicationContext(), getBaseContext(), and this ?**

	View.getContext(): Returns the context the view is currently running in. Usually the currently active Activity.

	Activity.getApplicationContext(): Returns the context for the entire application (the process all the Activities are running inside of). 
	Use this instead of the current Activity context if you need a context tied to the lifecycle of the entire application, 
	not just the current Activity.

	ContextWrapper.getBaseContext(): If you need access to a Context from within another context, you use a ContextWrapper. 
	The Context referred to from inside that ContextWrapper is accessed via getBaseContext().

	this is refer current class object always. this and getContext()are not always same e.g. in Activity class, 
	you can use this because Activity inherits from Context but method getContext() is not in Activity class.
	
**41. What is the difference between compileSdkVersion and targetSdkVersion ?**

	The compileSdkVersion is the version of the API the app is compiled against. This means you can use Android API features 
	included in that version of the API (as well as all previous versions, obviously). If you try and use API 16 features 
	but set compileSdkVersion to 15, you will get a compilation error. If you set compileSdkVersion to 16 you can still run 
	the app on a API 15 device as long as your app's execution paths do not attempt to invoke any APIs specific to API 16.

	The targetSdkVersion has nothing to do with how your app is compiled or what APIs you can utilize. The targetSdkVersion is 
	supposed to indicate that you have tested your app on (presumably up to and including) the version you specify. 
	This is more like a certification or sign off you are giving the Android OS as a hint to how it should handle your app in terms of OS features.
	
**42. What are the permission protection levels in Android ?**

	Normal — A lower-risk permission that gives requesting applications access to isolated application-level features, 
	with minimal risk to other applications, the system, or the user. The system automatically grants this type of 
	permission to a requesting application at installation, without asking for the user’s explicit approval.
	
	Dangerous — A higher-risk permission. Any dangerous permissions requested by an application may be displayed to the 
	user and require confirmation before proceeding, or some other approach may be taken to avoid the user automatically 
	allowing the use of such facilities.
	
	Signature — A permission that the system grants only if the requesting application is signed with the same certificate 
	as the application that declared the permission. If the certificates match, the system automatically grants the permission 
	without notifying the user or asking for the user’s explicit approval.
	
	SignatureOrSystem — A permission that the system grants only to applications that are in the Android system image or that 
	are signed with the same certificate as the application that declared the permission.
	
**43. What are dex files are used for ?**

	A .java file is given to the java compiler (javac) to generate the .class file. All .class files are given to dx tool to generate a single dex file. 
	The dex file is given to the Dalvik VM to generate the final machine code. The final machine code is given to the CPU to execute.

	.apk file contains .dex file in zip format which can be run on Dalvik VMs
	
**44. What is the main difference between View Binding and Data Binding ?**

	-> With ViewBinding, the layouts do not need a layout tag.
	-> ViewBinding is simply to bind your UI components to your code. While Data Binding is used to Bind your UI components to your Data Source.
	-> ViewBinding is faster than Data Binding because there is no usage of an annotation processor to generate Binding classes.
	-> ViewBinding does not support two-way binding.
	
**45. Explain when would you call getApplicationContext() and why ?**

	Use getApplicationContext() if you need something tied to a Context that itself will have global scope.
	I use getApplicationContext(), for example, in WakefulIntentService, for the static WakeLock to be used for the service. 
	Since that WakeLock is static, and I need a Context to get at PowerManager to create it, it is safest to use getApplicationContext().
	
	Use getApplicationContext() when you bind to a Service from an Activity, if you wish to pass the ServiceConnection 
	(i.e., the handle to the binding) between Activity instances via onRetainNonConfigurationInstance(). 
	Android internally tracks bindings via these ServiceConnections and holds references to the Contexts that create the bindings.
	If you bind from the Activity, then the new Activity instance will have a reference to the ServiceConnection which has an implicit 
	reference to the old Activity, and the old Activity cannot be garbage collected.
	
	

	


	
	
