% MAD - Android 2: Context, Resources & Layout
% Patrick Sturm
% 21.09.2016

## Information

* Any issues with this presentation? Write a ticket or send me a pull request ;).
* Repo: [https://github.com/siyb/tw-mad-2-context-resources-layout](https://github.com/siyb/tw-mad-2-context-resources-layout)

# Agenda

## Agenda

* Context
* Providing Resources

# Context

## Context - 1 - Basics

* Context objects provide access to the global context of your application
* Stuff you can access using Context (to name a few)
    * res/ information (for instance: strings defined in string.xml)
    * asset/ files
    * the ContentResolver - vital! - ContentProvider
    * SharedPreferences
    * service binding - vital!
    * application specific external dir
    
## Context - 2 - Basics cont.

* Important classes which extend the abstract Context Class
    * Activity
    * Application - for those who need to keep a global application state
    * Service
* Problems (I have) with Context objects
    * They are the swiss-army-knife of Android (Eierlegendewollmilchsau)
    * They can lead to memory leaks if not handled carefully
    * Due to their swiss-army-knife nature, Context objects are real heavyweights
    
## Context - 3 - Basics cont.

* If you program on Android, there is no way you can circumvent Context objects!
    * If you need a Context in part of your code, try not to save it
    * Never, ever, ever, ever keep static references to a Context
* Next Up: Context memory leak, happens to a lot of beginners, that’s why it’s important to talk about it

## Context - 4 -  Memory Leak

```java
public class MyLeakActivity extends Activity { 
  // static reference to evil 
  private static final Evil e; 

  public MyLeakActivity() { 
    e = new Evil(); 
  } 

  private final class Evil { 
  } 
}
```

## Context - 4 - Memory Leak Explained

* An non static inner class saves an instance of the enclosing class
    * Can be accessed using MyLeakActivity.this and NOT MyLeakActivity _this = this;
* When the Activity is destroyed, the static instance of Evil is retained
    * Evil still holds a reference to MyLeakActivity -> MEMLEAK
* Beware OC!

# Providing Resources

## Providing Resource - 1 - 

* The reason we discussed Context implementations, is that we need a Context to access resources.
* We actually did access resources before:
    * setContentView(R.layout.activity_myactivity);
    * findViewById(R.id.myTextView);
* Now, we are going to find out how to provide resources and how we can use them in our Android Applications
* There is a complete lesson dedicated to providing resources, you can find it here: [http://developer.android.com/guide/topics/resources/providing-resources.html](http://developer.android.com/guide/topics/resources/providing-resources.html)
