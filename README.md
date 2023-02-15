# Android-Basic-Interview-Question-Answer

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

**3. Android Debug Bridge (ADB ?**
	The ADB is a command-line debugging application doled out with the SDK. It enables developers to communicate with the device,
	and facilitates actions such as the installation and debugging of an application.
	
**4. Android Asset Packaging Tool (AAPT) ?**
	
	The AAPT builds the ‘.apk’ distributable Android package file.
	
**5. What is Android Runtime ?**

	Android Runtime (ART) is an application used by the Android OS as a runtime environment. 
	It has now replaced Dalvik, a discontinued Virtual Machine (VM). ART translates the bytecode of the application into native instructions,
	which are carried out by the device’s runtime environment
	
**6. What are Sensors in Android ?**
	
	Android-based devices have an assortment of built-in sensors in them, which measure certain parameters such as motion, orientation, and more. 
	These sensors help to monitor the positioning and movement of the device with high accuracy. They can be both software and hardware-based on nature.
	The three prominent categories of sensors in Android devices are:
	
	1.Position Sensor: 
	It is used to measure the physical position of the Android device. This includes orientation sensors and magnetometers
	
	2.Motion Sensors: These sensors include gravity, rotational activity, and acceleration sensors which measure the rotation 
	of the device or the acceleration and 	much more.
	
	3.Environmental Sensor: It includes sensors that measure temperature, pressure, humidity, and other environmental factors
	
**7. xplain DDMS in brief ?**

	The Dalvik Debug Monitor Server (DDMS) is a debugging tool in Android Studio. It has a wide range of debugging features, such as:

	Port forwarding
	Location data spoofing
	Screen capture
	Logcat
	Radio state information
	Thread and Heap information
	The DDMS tool is now deprecated and Android now suggests the users use Android Profiler instead.
	
**8. What is the AndroidManifest.xml file and why do you need this ?**

	The AndroidManifest.xml file contains information about the application, which is then provided to the Android system. 
	This data may include the package name, components such as activity, services, content providers, and more. This file executes the following tasks:

	Providing a unique name to the Java package
	Describing various components of the application, such as activity, services, and more. It also defines the classes which will implement these components.
	Declaring the Android API which will be used by the application
	Holding the library file details linked to the application
	
**9. What are the different data types supported by AIDL ?**

	AIDL or Android Interface Definition Language facilitates the communication between the client and service.
	Data Types supported by AIDL are as follows:

	String
	List
	Map
	charSequence
	INT, Long, Char, Boolean (Java data types)
	
**10. What is Application class ?** 

    The Application class in Android is the base class within an Android app that contains all other components such as activities and services.    
    The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.
    
**11. Tell all the Android application components ?**

	There are four different types of app components:
	1.Activities
	2.Services
	3.Broadcast receivers
	4.Content providers
    
**12. Difference between Activity and Service ?**

    Activity: An activity is the entry point for interacting with the user. It represents a single screen with a user interface.

    Service: A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.    
    It is a component that runs in the background to perform long-running operations or to perform work for remote processes. 
    A service does not provide a user interface.
  
 **13. How does the activity respond when orientation is changed ?** 
 
    According to the documentation, Some device configurations can change during runtime (such as screen orientation, keyboard availability, and when the user enables       multi-window mode). When such a change occurs, Android restarts the running Activity ( onDestroy() is called, followed by onCreate()). The restart behavior is           designed to help your application adapt to new configurations by automatically reloading your application with alternative resources that match the new device           configuration. 	
    
    
 **14. How to know configChange happens in onDestroy() function ?**
 
    Once an activity is in the process of finishing then isFinishing() method is returned true value, otherwise false when 
    the system is temporarily destroying the instance of the activity.
    
 **15. How to prevent the data from reloading when orientation is changed ?** 
 
    The most basic approach would be to use a combination of ViewModels and onSaveInstanceState(). A ViewModel is LifeCycle-Aware. 
    In other words, a ViewModel will not     be destroyed if its owner is destroyed for a configuration change (e.g. rotation). 
    The new instance of the owner will just re-connected to the existing ViewModel.  
    
    So if you rotate an Activity three times, you have just created three different Activity instances, but you only have one ViewModel.
    So the common practice is to store data in the ViewModel class (since it persists data during configuration changes) 
    and use OnSaveInstanceState() to store small amounts of UI data.
    
 **16. How to handle multiple screen sizes ?** 
 
    It's a long debate but in a very nutshell, you can do it in these ways:

	Use flexible layout like ConstraintLayout unless create alternative layout in different layout folders. 
    (e.g. layout-sw480, layout-sw600, layout-sw720 ...)
	Provide different bitmap drawables for different screen densities or use vector assets.
	Be aware of the screen orientation change approach in your application.
    If you don't want to handle it enforce to use just one orientation (portrait or landscape) through declaring it in the manifest file.
    
 **17. Difference between Service and IntentService ?**   
 
    Service is the base class for Android services that can be extended to create any service. 
    A class that directly extends Service runs on the main thread so it will block the UI (if there is one) 
    and should therefore either be used only for short tasks or should make use of other threads for longer tasks.

    IntentService is a subclass of Service that handles asynchronous requests (expressed as Intents) on demand. 
    Clients send requests through startService(Intent) calls. 
    The service is started as needed, handles each Intent in turn using a worker thread, and stops itself when it runs out of work. Read More on Mindorks's blog
    
 **18. What is Fragment ?** 
 
    A Fragment is a piece of an activity which enable more modular activity design. A fragment has its layout, its behavior, 
    and its life cycle callbacks. You can add or remove fragments in an activity while the activity is running. 
    You can combine multiple fragments in a single activity to build a multi-pane UI. A fragment can also be used in multiple activities. 
    The fragment life cycle is closely related to its host activity which means when the activity is paused, 
    all the fragments available in the activity will also be stopped.
  
 **19. Which method in fragment runs only once ?** 
 
 	According to the documentation, the onCreate() method is called once a fragment is created. Within your implementation, 
	you should initialize essential components of the fragment that you want to retain when the fragment is paused or stopped, then resumed.
	
 **20. What is the difference between Thread and AsyncTask ?** 
 
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
  
**21. What is Lopper and how it works ?** 

	Looper is a class which is used to execute the Messages(Runnables) in a queue. Normal threads have no such queue, 
	e.g. simple thread does not have any queue. It executes once and after method execution finishes, the thread will not run another Message(Runnable).
	
	If someone wants to execute multiple messages(Runnables) then he should use the Looper class which is responsible for creating a queue in the thread. 
	For example, while writing an application that downloads files from the internet, we can use Looper class to put files to be downloaded in the queue.
	
**22. What are Handlers ?** 	

	Handlers are objects for managing threads. It receives messages and writes code on how to handle the message.
	They run outside of the activity’s lifecycle, so they need to be cleaned up properly or else you will have thread leaks.
	Handlers allow communicating between the background thread and the main thread.
	
**23. Describe different types of Services in Android  ?**

	A Service is an application component that can perform long-running operations in the background, and it doesn't provide a user interface. 
	It can run in the background, even when the user is not interacting with your application. These are the three different types of services:

	Foreground Service: 
	A foreground service performs some operation that is noticeable to the user. For example, we can use a foreground service to play an audio track.

	Background Service: 
	A background service performs an operation that isn’t directly noticed by the user. In Android API level 26 and above, there are restrictions to using background services and it is recommended to use WorkManager in these cases.

	Bound Service: A service is bound when an application component binds to it by calling bindService(). A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results. A bound service runs only as long as another application component is bound to it.
	
**24. What are the major differences between ListView and RecyclerView  ?**	

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
	
**25. What is the difference between margin and padding  ?**	

	Padding will be space added inside the container, for instance, if it is a button, padding will be added inside the button.

	Margin will be space added outside the container.
	
**26. What is sw keyword in layout-sw600 folder meaning ?**

	The sw keywrod which stands on "smallest width" is an screen size qualifier that allow you to provide alternative 
	layouts for screens that have a minimum width measured in dp. The smallest width qualifier specifies the smallest 
	of the screen's two sides, regardless of the device's current orientation, so it's a simple way to specify the overall screen size available for your layout.    	 Here is some useful values:

	320dp: a typical phone screen (240x320 ldpi, 320x480 mdpi, 480x800 hdpi, etc).
	480dp: a large phone screen ~5" (480x800 mdpi).
	600dp: a 7” tablet (600x1024 mdpi).
	720dp: a 10” tablet (720x1280 mdpi, 800x1280 mdpi, etc).
	
**27. How to pass items to fragment ?**
	
	Using Bundle you can pass items to the fragment.
	
**28. How would you communicate between two fragments ?**

	There are several ways to communicate two fragments. Using interfaces are a common way to do that. 
	You can connect two fragments through interfaces that are implemented in the parent activity.
	
**29. Difference between adding/replacing fragment in backstack ?**

	replace removes the existing fragment and adds a new fragment. 
	This means when you press back button the fragment that got replaced will be created with its onCreateView being invoked.

	add retains the existing fragments and adds a new fragment that means existing fragment will be active and they wont be 
	in 'paused' state hence when a back button is pressed onCreateView is not called for the existing 
	fragment(the fragment which was there before new fragment was added).

	In terms of fragment’s life cycle events onPause(), onResume(), onCreateView() and other life cycle events will be 
	invoked in case of replace but they wont be invoked in case of add.
	
**30. What is the difference between dialog and dialogFragment ?**


	THe dialog is a small window that prompts the user to make a decision or enter additional information. 
	Instead, dialogFragment is a fragment that displays a dialog windows and contains a dialog object.

	DialogFragment does various things to keep the fragment's lifecycle driving it, instead of the Dialog. 
	Dialogs are generally autonomous entities -- they are their own window, receiving their own input events, 
	and often deciding on their own when to disappear. DialogFragment needs to ensure that what is happening 
	with the Fragment and Dialog states remains consistent. To do this, it watches for dismiss events from 
	the dialog and takes care of removing its own state when they happen.
	
**31. What is the difference between Foreground and Background and Bounded service ?**

	Foreground Service: A foreground service performs some operation that is noticeable to the user. 
	For example, we can use a foreground service to play an audio track. A Notification must be displayed to the user.

	Background Service: A background service performs an operation that isn’t directly noticed by the user. 
	In Android API level 26 and above, there are restrictions to using background services and it is recommended to use WorkManager in these cases

	Bound Service: A service is bound when an application component binds to it by calling bindService(). 
	A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results. 
	A bound service runs only as long as another application component is bound to it.
	
**32. What is contentProvider and what is typically used for ?**

	A ContentProvider provides data from one application to another, when requested. It manages access to a structured set of data. 
	It provides mechanisms for defining data security. Learn more. For further reading see the official android documentation
	
**33. What is the difference between apply() and commit() in sharedPreferences ?**

	commit() writes the data synchronously and returns a boolean value of success or failure depending on the result immediately.

	apply() is asynchronous and it won’t return any boolean response. Also if there is an apply() outstanding and we perform another commit(),
	The commit() will be blocked until the apply() is not completed.
	
**34. What Is the Singleton Pattern ?**

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

**35. What Is serializable and parcelable and find difference ?**

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

**36. Describe different Activity Launch Mode ?**

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

**37. What is Context in Android ?**

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
		
**38. Android Activity Lifecycle methods ?**	

	onCreate  called when activity is first created.
	onStart	  called when activity is becoming visible to the user.
	onResume  called when activity will start interacting with the user.
	onPause	  called when activity is not visible to the user.
	onStop	  called when activity is no longer visible to the user.
	onRestart called after your activity is stopped, prior to start.
	onDestroy called before the activity is destroyed.
	
**39. What is the difference between onCreate() and onStart() ?**

	onCreate() method gets called when activity gets created, and its called only once in whole Activity life cycle. 
	where as onStart() is called when activity is stopped... I mean it has gone to background and its onStop() method is called by the os. 
	onStart() may be called multiple times in Activity life cycle
	
**40. When only onDestroy is called for an activity without onPause() and onStop() ?**

	if you call finish() while creating the Activity in onCreate(), the system will invoke onDestroy() directly.
	
**41. What is onSavedInstanceState() and onRestoreInstanceState() in activity ?**

	1.onSavedInstanceState() - This method is used to store data before pausing the activity.
	2.onRestoreInstanceState() - This method is used to recover the saved state of an activity when the activity is recreated after destruction. 
	So, the onRestoreInstanceState() receive the bundle that contains the instance state information.
	
**42. Fragment Lifecycler ?**

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
	
**43. what is ViewBinding ?**

	ViewBinding is a feature in an android that allows you to access all of the UI components directly via generated Binding classes. 
	Once you enable the view binding in a build.gradle file, it generates Binding classes which contain all UI components references.

	If your layout file name is like game_score.xml then it will generate its class with the name like GameScoreBinding.

	Advantages of View Binding:
	Null safety:
	Because View Binding directly creates a reference to views, there is not any risk of a null pointer exception.
	Type safety:
	The Generated binding class has the same class types fields as present in the XML file, so there are no risks for class cast exceptions.
	
**44. What is data binding in Android ?**

	Data binding is the process of integrating views in an XML layout with data objects. The Data Binding Library 
	is responsible for generating the classes required for this procedure.
	
**45: How do you protect an Android app from reverse engineering ?**
	
	Make sure you are well aware of prevention tactics and tools such as tamper detection, ProGuard Assistance, and SafetyNet. 
	List other best practices such as using C++ for important code, securing user credentials, server-side database encryption, 
	and altering Android's shared library loading process.
	
**46. What is the difference between getContext(), getApplicationContext(), getBaseContext(), and this ?**

	View.getContext(): Returns the context the view is currently running in. Usually the currently active Activity.

	Activity.getApplicationContext(): Returns the context for the entire application (the process all the Activities are running inside of). 
	Use this instead of the current Activity context if you need a context tied to the lifecycle of the entire application, 
	not just the current Activity.

	ContextWrapper.getBaseContext(): If you need access to a Context from within another context, you use a ContextWrapper. 
	The Context referred to from inside that ContextWrapper is accessed via getBaseContext().

	this is refer current class object always. this and getContext()are not always same e.g. in Activity class, 
	you can use this because Activity inherits from Context but method getContext() is not in Activity class.
	
**47 What is the difference between compileSdkVersion and targetSdkVersion ?**

	The compileSdkVersion is the version of the API the app is compiled against. This means you can use Android API features 
	included in that version of the API (as well as all previous versions, obviously). If you try and use API 16 features 
	but set compileSdkVersion to 15, you will get a compilation error. If you set compileSdkVersion to 16 you can still run 
	the app on a API 15 device as long as your app's execution paths do not attempt to invoke any APIs specific to API 16.

	The targetSdkVersion has nothing to do with how your app is compiled or what APIs you can utilize. The targetSdkVersion is 
	supposed to indicate that you have tested your app on (presumably up to and including) the version you specify. 
	This is more like a certification or sign off you are giving the Android OS as a hint to how it should handle your app in terms of OS features.
	
**48 What are the permission protection levels in Android ?**

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
	
**49 What are dex files are used for ?**

	A .java file is given to the java compiler (javac) to generate the .class file. All .class files are given to dx tool to generate a single dex file. 
	The dex file is given to the Dalvik VM to generate the final machine code. The final machine code is given to the CPU to execute.

	.apk file contains .dex file in zip format which can be run on Dalvik VMs
	
**50 What is the main difference between View Binding and Data Binding ?**

	-> With ViewBinding, the layouts do not need a layout tag.
	-> ViewBinding is simply to bind your UI components to your code. While Data Binding is used to Bind your UI components to your Data Source.
	-> ViewBinding is faster than Data Binding because there is no usage of an annotation processor to generate Binding classes.
	-> ViewBinding does not support two-way binding.
	
**51 Explain when would you call getApplicationContext() and why ?**

	Use getApplicationContext() if you need something tied to a Context that itself will have global scope.
	I use getApplicationContext(), for example, in WakefulIntentService, for the static WakeLock to be used for the service. 
	Since that WakeLock is static, and I need a Context to get at PowerManager to create it, it is safest to use getApplicationContext().
	
	Use getApplicationContext() when you bind to a Service from an Activity, if you wish to pass the ServiceConnection 
	(i.e., the handle to the binding) between Activity instances via onRetainNonConfigurationInstance(). 
	Android internally tracks bindings via these ServiceConnections and holds references to the Contexts that create the bindings.
	If you bind from the Activity, then the new Activity instance will have a reference to the ServiceConnection which has an implicit 
	reference to the old Activity, and the old Activity cannot be garbage collected.
	
**52 What is Intent,PendingIntent and StickyIntent ?**

	1.Intent: Intent is a message passing mechanism between components of android, except for Content Provider. 
	You can use intent to start any component.
	
	2.PendingIntent : 
	A PendingIntent is a token that you give to a foreign application (e.g. NotificationManager, AlarmManager, Home Screen 
	AppWidgetManager or other 3rd party applications), which allows the foreign application to use your application’s permissions 
	to execute a predefined piece of code.
	If you want a foreign application to perform any Intent operation at future point of time, then we will use PendingIntent.
	Example: If you building a SMS app and you want to open your application when new message notification come. 
	In that situation you have to use PendingIntent.
	
	3.Sticky Intent:
	Sticks with android, for future broadcast listeners. For example if BATTERY_LOW event occurs then that intent will be stick 
	with android so that if any future user requested for BATTER_LOW, it will be fired.
	An intent that is used with sticky broadcast, is called as sticky intent. This intent will stick with android system for future broadcast receiver requests.

**53 Explain the difference between implicit and explicit intent ?**

	Explicit Intent: An explicit intent is where you inform the system about which activity or system component 
	it should use to generate a response to this intent.
	Implicit Intent: An implicit intent allows you to declare the action you wish to carry out, after which the 
	Android system will check which components are registered to handle that specific action.
	
**54 What is Intent Filter ?**

	An intent filter is an expression in an app's manifest file that specifies the type of intents that the component would like to receive.

	When you create an implicit intent, the Android system finds the appropriate component to start by comparing the contents of the intent 
	to the intent filters declared in the manifest file of other apps on the device. If the intent matches an intent filter, 
	the system starts that component and delivers it the Intent object.

	<activity android:name=".HelloWorld" android:label="@string/app_name">
    		<intent-filter>
        	<action android:name="android.intent.action.VIEW"/>
        	<category android:name="android.intent.category.DEFAULT"/>
        	<category android:name="android.intent.category.BROWSABLE"/>
        	<data android:scheme="http" android:host="androidium.org"/>
    		</intent-filter>
	</activity>
	
**55 What is AIDL file ?**

	The Android Interface Definition Language (AIDL) allows you to define the programming interface that both the client 
	and service agree upon in order to communicate with each other using interprocess communication (IPC).

	On Android, one process cannot normally access the memory of another process. So to talk, they need to decompose 
	their objects into primitives that the operating system can understand, and marshall the objects across that boundary for you. 
	The code to do that marshalling is tedious to write, so Android handles it for you with AIDL.
	
**56 What is Doze? What about App Standby ?**

	Starting from Android 6.0 (API level 23), Android introduces two power-saving features that extend battery life for users by 
	managing how apps behave when a device is not connected to a power source.

	Doze reduces battery consumption by deferring background CPU and network activity for apps when the device is unused for long periods of time. 
	In Doze mode, the system attempts to conserve battery by restricting apps' access to network and CPU-intensive services. 
	It also prevents apps from accessing the network and defers their jobs, syncs, and standard alarms.

	Periodically, the system exits Doze for a brief time to let apps complete their deferred activities. 
	During this maintenance window, the system runs all pending syncs, jobs, and alarms, and lets apps access the network.

	App Standby defers background network activity for apps with which the user has not recently interacted. 
	App Standby allows the system to determine that an app is idle when the user is not actively using it. 
	The system makes this determination when the user does not touch the app for a certain period of time. 
	When the user plugs the device into a power supply, the system releases apps from the standby state, allowing them to freely 
	access the network and to execute any pending jobs and syncs. If the device is idle for long periods of time, the system 
	allows idle apps network access around once a day.
		
**57 How would you communicate between two Fragments ?**

	All Fragment-to-Fragment communication is done either through a shared ViewModel or through the associated Activity. 
	Two Fragments should never communicate directly.

	The recommended way to communicate between fragments is to create a shared ViewModel object. Both fragments can access 
	the ViewModel through their containing Activity. The Fragments can update data within the ViewModel and if the data is exposed using 
	LiveData the new state will be pushed to the other fragment as long as it is observing the LiveData from the ViewModel.
	
**58 Why do we need to call setContentView() in onCreate() of Activity class ?**

	As onCreate() of an Activity is called only once, this is the point where most initialization should go: 
	calling setContentView(int) to inflate the activity's UI, using findViewById to programmatically interact with widgets in the UI, 
	calling managedQuery(android.net.Uri, String[], String, String[], String) to retrieve cursors for data being displayed, etc.

	It is inefficient to set the content in onResume() or onStart() (which are called multiple times) as the setContentView() is a heavy operation.
	
**59. What is the purpose of addToBackStack() while commiting fragment transaction ?**

	By calling addToBackStack(), the replace transaction is saved to the back stack so the user can reverse the transaction 
	and bring back the previous fragment by pressing the Back button.
	
**60. What are ViewGroups and how they are different from the Views ?**

	View: View objects are the basic building blocks of User Interface(UI) elements in Android. View is a simple rectangle box which 
	responds to the user’s actions. Examples are EditText, Button, CheckBox etc. View refers to the android.view.View class, 
	which is the base class of all UI classes.
	
	ViewGroup: ViewGroup is the invisible container. It holds View and ViewGroup. For example, LinearLayout is the 
	ViewGroup that contains Button(View), and other Layouts also. ViewGroup is the base class for Layouts
	
**61. What is a SpannableString ?**

	A SpannableString has immutable text, but its span information is mutable. Use a SpannableString when your text doesn't need to be 
	changed but the styling does. Spans are ranges over the text that include styling information like color, heighliting, italics, links, etc
	
**62. How would you save Activity state during a screen rotation ?**

	When your orientation changes, you don’t have to manually change to the landscape layout file. Android does this automatically for you. 
	When orientation changes, Android destroys your current activity and creates a new activity again, this is why you are losing the text.

	Basically, whenever Android destroys and recreates your Activity for orientation change, it calls onSaveInstanceState() before destroying 
	and calls onCreate() after recreating. Whatever you save in the bundle in onSaveInstanceState, you can get back from the onCreate() parameter.

	private TextView mTextView;
	private static final String KEY_TEXT_VALUE = "textValue";
	@Override
	protected void onCreate(Bundle savedInstanceState) {
  		super.onCreate(savedInstanceState);
  		mTextView = (TextView) findViewById(R.id.main);
  		if (savedInstanceState != null) {
      			CharSequence savedText = savedInstanceState.getCharSequence(KEY_TEXT_VALUE);
      			mTextView.setText(savedText);
  		}
	}
	@Override
	protected void onSaveInstanceState (Bundle outState) {
   		super.onSaveInstanceState(outState);
   		outState.putCharSequence(KEY_TEXT_VALUE, mTextView.getText());
	}
	
**63. What is the relationship between the life cycle of an AsyncTask and an Activity? What problems can this result in? 
	How can these problems be avoided ?**
	
	AsyncTask allows you to perform background operations and publish results on the UI thread without having to manipulate threads and/or handlers.

	AsyncTask is not tied to the life cycle of the Activity. If you execute an AsyncTask inside an Activity, and the user rotates the device, 
	the Activity will be destroyed and a new Activity instance will be created. but the AsyncTask will not die but instead goes on living until it completes. 
	This results in 2 problems:

	exception

	Then when the AsyncTask does complete, it updates the old activity instance rather the new activity. This can lead to an Exception:

 	java.lang.IllegalArgumentException:View not attached to window manager if you use.memory leak

	And because the AsyncTask maintains a reference to the old Activty, which prevents the Activity from being garbage collected as long as the 
	AsyncTask remains alive. This results in a memory leak.

	For these reasons, using AsyncTasks for long-running background tasks is generally a bad idea . 
	Rather, for long-running background tasks, a different mechanism (such as a service) should be employed.
	
**64. What are the four states of the Activity Lifecycle ?**

	[active/running, paused, stopped, destroyed]
	
**65. How can Activity communicate with services ?**

	Binding services
	Using Callbacks interfaces
	
**66. What is a 9patch image? does it tile or stretch ?**

	9 Patch images are stretchable, repeatable images reduced to their smallest size
	
**68. Why we should use MVP / MVVM architectures ?**

	to avoid too much logic code in the UI layer and god activities
	reusable code that's easier to test
	avoid duplicated code between common views
	Easier to maintain
	we can test logic without using instrumentation tests
	
**69. Explain unit test? What does Unit Testing suppose to do ?**

	Unit testing involves breaking your program into pieces and subjecting each piece to a series of tests.
	These tests can run on a Continues Integration (CI) (namely GitHub actions, Circle Ci, or Travis Ci) and keep the code quality
	Unit testing is done to ensure that developers write high-quality and errorless code. It is advised to write Unit tests before 
	writing the actual app, you will write tests beforehand and the actual code will have to adhere to the design guidelines laid out by the test
	
**70. What is Instrumentation Test ?**

	Instrumentation tests run on a device or an emulator. In the background, your app will be installed and then a testing app will 
	also be installed which will control your app, lunching it and running UI tests as needed.

	Instrumentation tests can be used to test none UI logic as well. They are especially useful when you need to test 
	code that has a dependency on a context.
	
**71. What is Espresso Test ?**

	Espresso is a UI test framework (part of the Android Testing Support Library) that allows you to create automated UI tests for your Android app. 
	Espresso tests run on actual device or emulator (they are instrumentation based tests) and behave as if an actual user is using the 
	app (i.e. if a particular view is off screen, the test won't be able to interact with it).

	Espresso's simple and extensible API, automatic synchronization of test actions with the UI of the app under test, and rich failure information
	make it a great choice for UI testing. In many circles Espresso is considered to be a full replacement for Robotium (see this stack overflow 
	post that compares Robotium to Espresso).
	
**72. What is Robolectric Test ?**

	It allows Android applications to be tested on the JVM without an emulator or device. Running Android tests on the JVM usually fails because
	the Android core libraries included with the SDK, specifically the android.jar file, only contain stub implementations of the Android classes. 
	The actual implementations of the core libraries are built directly on the device or emulator, so running tests usually 
	requires one to be active in order to execute.

	So for all of us that want faster executing tests on the JVM, Robolectric saves the day. Robolectric provides implementations of the Android SDK
	by rewriting the Android core libraries using shadow classes. This gives us the ability to execute our tests on the JVM and achieve much faster 
	test execution times than if we were running on a device or emulator. in the Project Window. This will show us a full view of everything 
	contained in the project. The default setting (the Android perspective) hides certain directories (including the unit tests!):
 
 **73. What is Mokito Test ?**

	Mockito is a mocking framework with a delicious flavor. It has a clean and simple API that allows you to construct beautiful tests. 
	The tests in Mockito are very readable and provide clear verification errors, so you won’t get a hangover. Now, let’s look at an example 
	of how to use mockito.
	
	Mockito is a mocking framework that tastes really good. It lets you write beautiful tests with a clean & simple API. 
	Mockito doesn’t give you hangover because the tests are very readable and they produce clean verification errors.
	
**74. What is a Canvas ?**

	Canvas is a class in Android that performs 2D drawing of different objects onto the screen. The saying “a blank canvas” is very 
	similar to what a Canvas object is on Android. It is basically, an empty space to draw onto.
	
**75. What is ANR and how to prevent it ?**

	ANR stands for Application Not Responding. An ANR will occur if you’re running a process on the UI thread which takes an extended time, 
	usually around 5 seconds. During this point, the GUI (Graphical User Interface) will lock up which can end in anything the user presses 
	won’t be actioned. After the 5 seconds approx. has occurred, if the thread still hasn’t recovered then an ANR dialogue box is shown informing 
	the user that the appliance isn’t responding and can give the user the choice to either wait, in the hope that the app will eventually recover, 
	or to force close the app.
	
	*How to prevent an ANR?
	
	Stop doing heavy tasks on the main thread. Instead use worker threads such as IntentService, AsyncTask Handler, or another Thread simply. 
	Detecting where ANRs happen is straightforward if it’s a permanent block (deadlock acquiring some locks for instance), but harder if it’s 
	just a short-lived delay. First, re-evaluate your code and appearance for vulnerable spots and long-running operations. 
	Examples may include using sockets, locks, thread sleeps, and other blocking operations from within the event thread. You should make 
	sure these all happen in separate threads. If nothing seems the matter, use DDMS and enable the thread view. This shows all the threads 
	in your application similar to the trace you have. Reproduce the ANR, and refresh the most thread at an equivalent time. 
	That should show you exactly what’s happening at the time of the ANR. An ANR is going to be triggered for your app when one among the subsequent conditions.
	
**76. What is an AsyncTask(Deprecated in API level 30) ?**

	AsyncTask (Asynchronous Task) in Android is an abstract class, or rather a helper class that lets the application perform tedious tasks in 
	the background and parallelly perform UI changes in the front-end. This is quite similar to Threading but does not constitute any 
	threading framework. Background tasks such as loading images, downloading music, pictures, files, etc can be performed using AsyncTask
	
	Associated member functions are:

	onPreExecute() Optional
	doInBackground(Params…) Required
	onProgressUpdate(Progress…) Optional
	onPostExecute(Result) Optional
	
**77. What is a Loader ?**

	Loader is a set of APIs, known as Loader APIs given by Android, to load data asynchronously in activity/fragment.
	It can fetch data asynchronously without blocking the main thread and it manages it's own lifecycle during onDestroy() and configuration changes.
	
	Loaders in Android is an abstract class implementation of Loader and two default classes, which are provided by Android, 
	I.E. AsyncTaskLoader, and cursor loaders.
	
**78. What is bitmap pooling ?**

	Bitmap pooling is an implementation that tries to reuse the memory of the bitmaps already available instead of allocating new memory every time. 
	Suppose we need to load a bitmap, we first check our pool to see if there is any bitmap available. If it is available, we take a bitmap from the
	pool and reuse its memory to load our new bitmap otherwise we create a new bitmap. In case, if we do not need any bitmap, we put that bitmap into
	that pool instead of recycling it so that we can reuse the memory of that bitmap when needed for a new bitmap.
	
**79. What is Multidex ?**

	In Java, if we compile our code then that code is converted into a .class file by the compiler because our machine understands that .class file. 
	The same is the process for the Android Application. In Android, the compiler converts our source code into DEX (Dalvik Executable) file.
	
	Before understand Multidex we have to understand DEX and Build System in Android.
	
	*Android Build System
	
	Before moving on to DEX, let's revise some concepts of the build system of Android. Android compiles the resources and source code of our 
	app and packages them into APKs. Conversion of our project into an APK requires many tools and involves many processes. 
	
	The build process of a typical Android App can be summarized as below:

	The compilers convert the source code into DEX (Dalvik Executable) files, which include the bytecode that runs on Android devices.
	After having the DEX files, the APK Packager combines the DEX files and compiled resources into a single APK.
	After that, the APK Packager signs the APK.
	Before generating the final APK, various methods are followed to optimize the code so as to avoid the unused code.
	
	*Multidex in Android
	
	In Android, the compilers convert your source code into DEX files. This DEX file contains the compiled code used to run the app. 
	But there is a limitation with the DEX file. The DEX file limits the total number of methods that can be referenced within a single 
	DEX file to 64K i.e. 65,536 methods. So, you can't use more than 64K methods in a particular DEX file. These 64K methods include 
	Android framework methods, library methods, and methods in our code also. This limit of 64K is referred to as the " 64K reference limit ".

	So, if our app exceeds 65,536 methods, we will encounter a build error that indicates our app has reached the limit of the Android 
	build architecture. The error is as follows:

	Too many field references: 131000; max is 65536.
	You may try using --multi-dex option.
	
	*try the following strategies to avoid using 64K reference methods:

	Manage dependencies: While importing some dependencies for our project, sometimes we import each and every library and use only a few of them.
	So, instead of keeping all those dependencies, we can keep only the required one.
	
	Remove unused code: Enable code shrinking in your project. By doing so, we are not shipping unused code with our APK.
	
	*Limitations of Multidex support library
	
	1.If your secondary DEX file is larger than the primary DEX file, then you may encounter some Application Not Responding (ANR) error. 
	In this case, you should apply code shrinking to minimize the size of DEX files and remove unused portions of code.
	
	2.If you are targeting API levels lower than 21, test thoroughly on those versions of the platform, because your app might have 
	issues at startup or when particular groups of classes are loaded.
	
	Code Shrinking can reduce or possibly eliminate these issues.
	
**80. Difference between ViewModel and AndroidViewModel ?**

	AndroidViewModel is subclass of ViewModel. The Difference between them is we can pass Application Context which can be used 
	whenever Application Context is required for example to instantiate Database in Repository.

	AndroidViewModel is a Application context aware ViewModel.

	*AndroidViewModel:
	
	public class PriceViewModel extends AndroidViewModel {
		private PriceRepository priceRepository;
		public PriceViewModel(@NonNull Application application) {
    		super(application);
    		priceRepository= new PriceRepository(application);
    		allPrices = priceRepository.getAllPrices();
	}

	*ViewModel:
	
	public class PriceViewModel extends ViewModel {
		public PriceViewModel() {
    		super();
	}
	You Should use AndroidViewModel only when you require Application Context.
	
	Apart from the difference that AndroidViewModel gives you an application context whereas ViewModel does not. 
	The important thing that you must understand is that Google itself recommends using ViewModel and not AndroidViewModel.

	So, don't use AndroidViewModel unless it is really necessary.
	
**81. What is the difference between compileSdkVersion and targetSdkVersion ?**

	The compileSdkVersion is the version of the API the app is compiled against. This means you can use Android API features included 
	in that version of the API (as well as all previous versions, obviously). If you try and use API 16 features but set compileSdkVersion to 15, 
	you will get a compilation error. If you set compileSdkVersion to 16 you can still run the app on a API 15 device as long as your app's 
	execution paths do not attempt to invoke any APIs specific to API 16.

	The targetSdkVersion has nothing to do with how your app is compiled or what APIs you can utilize. The targetSdkVersion is supposed 
	to indicate that you have tested your app on (presumably up to and including) the version you specify. This is more like a certification 
	or sign off you are giving the Android OS as a hint to how it should handle your app in terms of OS features.
	
**82. Types of Dialog box in Android ?**

	1. AlertDialog 2.DatePicker 3. TimePicker 4.CustomDialog 5.ProgressDialog
	
**83.  Jetpack Architecture Components in Android ?**

	Android Jetpack is a set of software components, libraries, tools, and guidance to help in developing robust Android applications.
	Launched by Google in 2018
	
	Its software components have been divided into 4 categories:

	1.Foundation Components
	2.Architecture Components
	3.Behavior Components
	4.UI Components


	Further, the following are the list of all Foundation components:

	AppCompat
	Android KTX
	Test
	Multidex

	Further, Architecture Components could be classified as follows: 

	Room
	WorkManager
	Lifecycle
	ViewModel
	LiveData
	Navigation
	Paging
	Data Binding
	
	Further, the following are the list of all Behavior components:

	DownloadManager
	Media & Playback
	Permissions
	Notifications
	Sharing
	Slices
	
	Further, the following are the list of all UI components:

	Animation & Transition
	Auto
	Emoji
	Fragment
	Layout
	Palette
	TV
	Wear

**84.  Lifecycle in Android Architecture Components ?**

	Lifecycle is one of the Android Architecture Components which was released by Google to make it easier for all the Android developers. 
	The Lifecycle is a class/interface which holds the information about the state of an activity/fragment and also it allows other objects to 
	observe this state by keeping track of it. 
	
	The LifeCycle component is concerned with the Android LifeCycle events of a component such as an Activity or a Fragment, 
	it has three main classes that we’ll deal with:

	Lifecycle
	Lifecycle Owner
	Lifecycle Observer
	
	1. Lifecycle
	Lifecycle is a process that tells us about the Events performed on an Activity/Fragment. We have a lifecycle as a class that has
	two types of enumerations to track the components, State and Event. Event and State are used to determine the lifecycle. 
	Each event has its own state.
	
	2.Lifecycle Owner
	Every Activity has a Lifecycle. This Activity will be a Lifecycle Owner(any activity or fragment can be called a lifecycle owner).
	When an activity is initialized LifecycleOwner is the one that will be constructed initially. Any class that implements the 
	LifeCycleOwner interface indicates that it has Android LifeCycle. For example, starting from Support Library 26.1.0 Fragments 
	and Activities implement the LifeCycleOwner interface. One can create custom LifeCycleOwner components by implementing the 
	interface and using a LifeCycleRegistry as described here.

	3. Lifecycle Observer
	Lifecycle Observer, which observes the activity and keeps track of the lifecycle, and performs an action. The action performed by this 
	lifecycle Observer depends on the lifecycle of the lifecycle Owner. Every lifecycle owner has a lifecycle and based on the event or state 
	of the lifecycle of the owner, the lifecycle observer performs the action.
	
**85. What is ViewModel in Android Architecture Components ?**

	ViewModel is part of the android architecture component.The ViewModel class is designed to store and manage UI-related data in 
	a lifecycle-conscious way. ViewModel classes are used to store the data even the configuration changes like rotating screen. 
	ViewModel is one of the most critical class of the Android Jetpack Architecture Component that support data for UI components. 
	Its purpose is to hold and manage the UI-related data. Moreover, its main function is to maintain the integrity and allows data
	to service during configuration changes like screen rotations.

**86. what is andorid:exported tag in AndroidManifest file ?**

	This element sets whether the activity can be launched by components of other applications:
	
	If "true", the activity is accessible to any app, and is launchable by its exact class name.
	If "false", the activity can be launched only by components of the same application, applications with the same user ID, 
	or privileged system components. This is the default value when there are no intent filters.
	
	If an activity in your app includes intent filters, set this element to "true" to allow other apps to start it. For example, 
	if the activity is the main activity of the app and includes the category "android.intent.category.LAUNCHER".

	If this element is set to "false" and an app tries to start the activity, the system throws an ActivityNotFoundException.

	This attribute is not the only way to limit an activity's exposure to other applications. Permissions can also be used to 
	limit the external entities that can invoke the activity (see the permission attribute).
	
**87. Difference between ACCESS_FINE_LOCATION and ACCESS_COARSE_LOCATION permission ?**

	Location can be determined by two ways:
	
	Using NETWORK_PROVIDER
	Using GPS_PROVIDER
	
	*Using NETWORK_PROVIDER
	
	The network provider determines the location of the users using cell towers,wifi access points etc. Distance between towers 
	and user’s position are considered in the case of cell towers. This location provider offers a faster response. Commonly used 
	for determining location inside the rooms or buildings. Here the GPS coordinates are not able to be obtained. Android permissions 
	required for using this provider are either,
	
	ACCESS_COARSE_LOCATION <uses-permission android:name=”android.permission.ACCESS_COARSE_LOCATION” />
	Or,
	ACCESS_FINE_LOCATION <uses-permission android:name=”android.permission.ACCESS_FINE_LOCATION” />
	
	*Using GPS_PROVIDER
	
	The GPS provider determines the location of the users using satellites. For this, the GPS coordinates are obtained 
	and used for positioning. The GPS receiver in the smartphone receives the signals from satellites. These signals are 
	processed and precise locations are determined. It takes more time for response and causes delay in location determination. 
	It works better in outdoors – direct sky/satellite views and communication occurs. Android permissions required for using
	this provider only,
	
	ACCESS_FINE_LOCATION <uses-permission android:name=”android.permission.ACCESS_FINE_LOCATION” />
	
	Difference Between Fine and Coarse Locations

	Fine Location :
	The Fine location provides better and accurate locations. Requires permission,
	ACCESS_FINE_LOCATION <uses-permission android:name=”android.permission.ACCESS_FINE_LOCATION” />
	It gives permission for using both GPS_PROVIDER and NETWORK_PROVIDER or  GPS_PROVIDER only for determining the position.
	
	Coarse Location :
	The Coarse location provides less accurate locations. Requires permission,
	ACCESS_COARSE_LOCATION <uses-permission android:name=”android.permission.ACCESS_COARSE_LOCATION” />
	It gives permission for using NETWORK_PROVIDER only for determining the position.

**88. Difference between Livedata and MutableLiveData ?**

	LiveData has no public method to modify its data.
	The MutableLiveData class exposes the setValue(T) and postValue(T) methods public and you must use these if you need to 
	edit the value stored in a LiveData object.
	
	LiveData<User> getUser() {
    		if (userMutableLiveData == null) {
        		userMutableLiveData = new MutableLiveData<>();
    		}
    		return userMutableLiveData
	}
	You can't update its value like getUser().setValue(userObject) or getUser().postValue(userObject)

	So when you don't want your data to be modified use LiveData If you want to modify your data later use MutableLiveData
	
**89. What is the difference between setValue() and postValue() ?**

	So, if you’re familiar with LiveData, you’ve probably come across these two LiveData methods: setValue() and postValue(). 
	So, one question that may have occurred to you is why there is a requirement for two methods setValue and postValue for 
	the same functionality. Let’s look at an example to find out. Assume you want to use LiveData to update a value. As a result,
	you will have two options: either update the data on the main thread or update the data on the background thread. 
	As a result, the use-case of setValue and postValue is limited to these two scenarios.

	When changing the data on the Main thread, use the MutableLiveData class’s setValue method, and when changing the LiveData 
	on the background thread, use the MutableLiveData class’s postValue method
	
**90. Memory Leak in Andorid ?**

	A memory leak is basically a failure of releasing unused objects from the memory. As a developer one does not need 
	to think about memory allocation, memory deallocation, and garbage collection. All of these are the automatic process 
	that the garbage collector does by itself, but the situation becomes difficult for the garbage collector when the 
	user is referencing the object, which is in not use anymore, but since that object is being referenced by another 
	object, garbage collector feels that the unused object is being used by another object and due to this garbage collector 
	does not free-up the memory of that object, due to which available heap memory get decreases leading to memory shortage
	and memory leak. The unfreed object is basically called as leaks.
	
	Memory leaks are the common causes of application crashes in android apps. Every developer must know how to avoid memory 
	leaks and what are the circumstances which can lead to memory leaks in android applications. When the RAM resources are 
	not released when they are no longer needed and if this is done several times, the part of the memory that the operating
	system has assigned to that particular application may exceed the upper limit and the system can terminate the application
	causing the application to crash. Holding the references of the object and resources that are no longer needed is the main 
	cause of the memory leaks in android applications.  As it is known that the memory for the particular object is allocated 
	within the heap and the object point to certain resources using some object reference. But when the work is completed, 
	the object references should be freed. But when it is not done, the heap space increases continuously and the rest of the 
	application has to run on whatever heap space that is left, and ultimately there are high chances that it can lead to memory 
	leaks in the application. Thus it can be said that memory leaks are a term used when our app goes short of the memory because 
	some object which is not used but still there are being pointed out by the references and continually occupying the heap space,
	which ultimately leads to a shortage of space for the other components of the application and thus eventually causing the app to crash.
	
	
*Causes of Memory Leaks and Their Solutions

	1. Using Static Views
	
	One should not use static views while developing the application, as static views are never destroyed.
	
	2. Using Static Context
	
	One should never use the Context as static, because that context will be available through the life of the application, 
	and will not be restricted to the particular activity.
	
	3. Using Code Abstraction Frequently 

	Developers often take the advantage of the abstraction property because it provides the code maintenance and flexibility in code, 
	but using abstraction might cost a bit to the developer, as while using abstraction one needs to write more code, more code means
	more time to execute the space and more RAM. So whenever one can avoid the abstraction in the code, it is code as it can lead to fewer memory leaks.
	
	4. Unregistered  Listeners

	When the developer uses any kind of listener in his application code, then the developer should not forget to unregister the listener.

	5. Unregistered  Receivers

	Many times the developer needs to register the local broadcast receiver in an activity. However, if the developer does not 
	unregisters the broadcast receiver there is a strong chance that our app can lead to the memory leak problem as the receiver 
	will hold a strong reference to the activity. So even if the activity is of no use, it will prevent the garbage collector to 
	collect the activity for garbage collection, which will ultimately cause the memory leak.
	
	6. Inner class Reference

	An inner class is often used by the android developers within their code. However, the nonstatic class will hold the implicit 
	reference of the parent class which can cause the memory leak problem. 
	So there can be two solutions that can be proposed to solve this problem:

	One can make the inner class static
	If one wants to pass the reference of the non-static inner class, then it can be passed using weak reference.
	
*Tools to Detect Memory Leak

	1. Leak Canary

	Leak Canary is a memory detection library in Android. It is developed by a square cup company. This library has a unique 
	ability to decrease down the memory leak and helping developers to get less “MemoryOutOfError”. Leak canary even helps us 
	to notify where the leak is actually happening.
	
	Once the leak canary is installed it automatically detects and reports memory leaks in 4 steps:

	Detecting retained objects.
	Dumping the heap.
	Analyzing the heap.
	Categorizing leaks.

	2. Android Profiler

	It is basically a tool that helps to keep track of memory usage of every application in android. It replaced Android Monitor 
	in the android version 3.0 and higher. The Android Profiler is compatible with Android 5.0 (API level 21) and higher. 
	Android Profiler detects the performance of the application in the real-time on the parameters like:

	Battery
	Memory (In MB)
	CPU Usage (In %)
	Network Rate(Rate of uploading and receiving)
	
**91. EncryptedSharedPreferences in android ?**

	Android Jetpack provides a new library Security which allows you to encrypt/decrypt data with a more robust and secure 
	mechanism using a much friendly API. This helps you avoid using third-party libraries or writing your own custom 
	encryption implementations like AES etc. It also recommends to not use Android Keystore System 
	(previously used for such purposes in Android) and choose Android’s Jetpack Security instead.
	
	EncryptedSharedPreferences Wraps the SharedPreferences class and automatically encrypts keys and values using a two-scheme method:

	Keys are encrypted using a deterministic encryption algorithm such that the key can be encrypted and properly looked up.
	Values are encrypted using AES-256 GCM and are non-deterministic.
	
	Required Min-sdk As of today, 23 (Android 6.0)
	
	Add Dependency implementation "androidx.security:security-crypto:1.0.0-alpha02"
	
	Initialize / Open
	
	Just create or fetch a Master Key from the Android Keystore for you, and use it to initialize/open a EncryptedSharedPreferences instance:
	// Step 1: Create or retrieve the Master Key for encryption/decryption
	val masterKeyAlias = MasterKeys.getOrCreate(MasterKeys.AES256_GCM_SPEC)

	// Step 2: Initialize/open an instance of EncryptedSharedPreferences
	val sharedPreferences = EncryptedSharedPreferences.create(
    		"PreferencesFilename",
    		masterKeyAlias,
    		applicationContext,
    		EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
    		EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM)
		
	Save entries
	sharedPreferences.edit().putString("DATA", saveText.text.toString()).apply()
	Read entries
	val value = sharedPreferences.getString("DATA", "")
	
	If I put the valueakaita into EncryptedSharedPreferences, though, I get something very different:
	
	<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
	<map>
    	<string name="AVz2qCVxm1KudCCJKYuxuoaAXoPeWKjG0w==">ASnO9uni11t3m9sNgDJbiYllL/tE+i99TYKfQ0h8XV6AUN0O3rBxBsMmcpw2DCY=</string>
	<stringname="__androidx_security_crypto_encrypted_prefs_key_keyset__">12a901eb372af4775b09f5b51d20d49428931c5d8e0b17dd103d2169c1879b8b13958274d7e25d3cc052f301461495fd40b70806ae244f456726802460318bdf19dce444e7a60f20c903c5a57140ea8e90a19a1b48559961d145a50000d1c0e22ca918b02ea0cc34e433900f44c00e9c791ecb678f26d293c0226d6c2a9e25e610616ec34241b06410481427a850eeedf85ee4c725d5dbd715b5a8d0e017be9a568a9f960989271d14d2d0531a4408a5d0dae705123c0a30747970652e676f6f676c65617069732e636f6d2f676f6f676c652e63727970746f2e74696e6b2e4165735369764b6579100118a5d0dae7052001</string>
    <string name="__androidx_security_crypto_encrypted_prefs_value_keyset__">12880189e734bbbf9cfa3bc15b5e53ea8df03341269cf97112a60a1f6482732dd33248b3f821397fb04ef3372ff54336e9045a0b0c0fb7afdf475dbc98a1107d09de66afcc5ad063e5e5b59a7d616e14834e19769bc84de7e5c8716a811814a6cd7a6d72a1c64ce4317f2f482181c437b70f010219ca6407a98bac18f1101c02fd8e2c4a9009ad2a1ebbdc1a4408e9edbbce02123c0a30747970652e676f6f676c65617069732e636f6d2f676f6f676c652e63727970746f2e74696e6b2e41657347636d4b6579100118e9edbbce022001</string>
</map>

	Even more, the encrypted file will change every time we save, making it pretty difficult for anybody to come and crack it.







