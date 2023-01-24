# Android-General-Interview-Question-Answer

**1. What is Application class ?**

    The Application class in Android is the base class within an Android app that contains all other components such as activities and services. The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.
    
**2. Difference between Activity and Service ?**

    Activity: An activity is the entry point for interacting with the user. It represents a single screen with a user interface.

	Service: A service is a general-purpose entry point for keeping an app running in the background for all kinds of reasons. It is a component that runs in the background to perform long-running operations or to perform work for remote processes. A service does not provide a user interface.
  
 **2. How does the activity respond when orientation is changed? ?**
 
    According to the documentation, Some device configurations can change during runtime (such as screen orientation, keyboard availability, and when the user enables multi-window mode). When such a change occurs, Android restarts the running Activity ( onDestroy() is called, followed by onCreate()). The restart behavior is designed to help your application adapt to new configurations by automatically reloading your application with alternative resources that match the new device configuration.	
  
  
