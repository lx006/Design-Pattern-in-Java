# DESIGN PATTERN IN JAVA :

By reading the above heading the first question which comes to our mind is –

1). What is Design Pattern? Why is it important in software industry?

- Design Pattern is an Industry Approach to solve the more complex and recurring problem.
- It promotes reusability which leads to robust and maintainable code.
- It makes our code easy to understand and can be easily debugged.

-
# Types of Design Pattern in Java :

![image](https://user-images.githubusercontent.com/76866301/113558718-ccda2b00-961d-11eb-9379-edd5938cd4bf.png)


-
# Creational Design Pattern :

- Creational Design Patterns allows us to create the object in best possible way.

![image](https://user-images.githubusercontent.com/76866301/113558766-e1b6be80-961d-11eb-8fc7-de7924ecbf38.png)

-
# Structural Design Pattern :

- Structural design pattern describes how objects and classes can be combined to form the largest structure.

![image](https://user-images.githubusercontent.com/76866301/113558816-f6935200-961d-11eb-9d71-63c4bafceb0b.png)

-
# Behavioral Design Pattern :

- Behavioral Design Pattern describes how one class communicate with other class in a loose couple manner.

![image](https://user-images.githubusercontent.com/76866301/113558853-07dc5e80-961e-11eb-84b1-8020196ba32c.png)

-
# Singleton Design Pattern :

- It allows us to create only one instance of the class.
- We must make sure that singleton class must provide the global access point to get the instance
- i.e. we must have at least one public method in a class which returns instance of a class.

-
# Different approaches to implement singleton design pattern :

- Eager initialization
- Static Block initialization
- Lazy initialization
- Thread safe singleton
- Bill pugh singleton implementation
- Using Reflection to destroy singleton pattern
- Enum singleton
- Using clone to destroy/prevent singleton
- Using serialization destroy/prevent singleton
- Example of singleton within JDK

-
# Steps to create Singleton Pattern :

1. Always create your constructor private so that multiple objects cannot be created from other classes.
2. Create private static variable so that it is the only instance of the class.
3. Create public static method to return the instance of a class and it remains the global access for the instance of the singleton class.

-
# Eager initialization :

- In eager initialization the instance/object of the class is created at the time of class loading.
- The drawback for this is the instance of class is created whether the client is using it or not.
- Exception handling cannot be done.

**Step 1:**

**package** pack\_Singleton;

**public**** class** Singleton

{

**private**** static ****final** Singleton _ **instance** _ = **new** Singleton();

**private** Singleton()

{

}

**public**** static** Singleton getinstance()

{

**return** _ **instance** _;

}

}

**Step 2:**

**package** pack\_Singleton;

**public**** class** Test {

**public**** static ****void** main(String[] args)

{

Singleton obj1 = Singleton._getinstance_();

Singleton obj2 = Singleton._getinstance_();

System._ **out** _.println(obj1.hashCode());

System._ **out** _.println(obj2.hashCode());

}

}

**Output :**

![image](https://user-images.githubusercontent.com/76866301/113558926-24789680-961e-11eb-9c8b-c933d37308a8.png)

- The above output show that the unique code for both the objects are same that means the object is created only once and is shared while calling the method.

-
# Static Block Initialization :

- In static block initialization we need to create one static block and inside that block we give memory to the instance of a class.
- We can handle exception inside the static block.

**Step 1 :**

**package** pack\_Singleton;

**public**** class** Singleton

{

**private**** static **Singleton _instance_ =** null**;

**private** Singleton()

{

}

**static**

{

**try**

{

**if** (_instance_ == **null** )

{

_instance_ = **new** Singleton();

}

} **catch** (Exception e)

{

e.printStackTrace();

}

}

**public**** static** Singleton getinstance()

{

**return** _instance_;

}

}

**Step 2 :**

**package** pack\_Singleton;

**public**** class** Test {

**public**** static ****void** main(String[] args)

{

Singleton obj1 = Singleton._getinstance_();

Singleton obj2 = Singleton._getinstance_();

System._ **out** _.println(obj1.hashCode());

System._ **out** _.println(obj2.hashCode());

}

}

**Output :**

![image](https://user-images.githubusercontent.com/76866301/113558967-34907600-961e-11eb-81ba-2c7aa76b1d62.png)

- The above output show that the unique code for both the objects are same that means the object is created only once and is shared while calling the method.

-
# Lazy Initialization :

- In lazy initialization the instance is given memory inside the getinstance method.
- This approach is good for single threaded environment for multithreaded it creates problem as more than one thread can come inside the if block.
- So it is not thread safe.

**Step 1 :**

**package** pack\_Singleton;

**public**** class** Singleton

{

**private**** static **Singleton _instance_ =** null**;

**private** Singleton()

{

}

**public**** static** Singleton getinstance()

{

**if** (_instance_ == **null** )

{

_instance_ = **new** Singleton();

}

**return** _instance_;

}

}

Step 2 and output will be same as that of the above 2 approaches.

-
# **Thread Safe Singleton :**

- Always used for multithreaded environment.
- Always make use of synchronized method or double locking to prevent breakage of singleton pattern.

**Step 1 :**

First create one class with main method to create and maintain a reusable pool of threads.

**package** pack\_Singleton;

**import** java.util.concurrent.ExecutorService;

**import** java.util.concurrent.Executors;

**public**** class** Test {

**public**** static ****void** main(String[] args)

{

ExecutorService executorService = **null** ;

MyThread mythread = **new** MyThread();

**try**

{

executorService = Executors._newFixedThreadPool_(3);

executorService.execute(mythread);

executorService.execute(mythread);

executorService.execute(mythread);

} **catch** (Exception e)

{

e.printStackTrace();

}

**finally**

{

**if** (executorService != **null** )

{

executorService.shutdown();

}

}

}

}

**Step 2:**

Create a class to implement runnable interface

**package** pack\_Singleton;

**public**** class **MyThread** implements** Runnable

{

@Override

**public**** void** run()

{

Singleton obj1 = Singleton._getinstance_();

System._ **out** _.println(Thread._currentThread_().getName()+&quot; &quot;+obj1.hashCode());

}

}

**Step 3:**

Create a class to implement singleton pattern

**package** pack\_Singleton;

**public**** class** Singleton

{

**private**** static **Singleton _instance_ =** null**;

**private** Singleton()

{

}

**public**** static ****synchronized** Singleton getinstance()

{

**if** (_instance_ == **null** )

{

**try**

{

Thread._sleep_(2000);

} **catch** (Exception e)

{

e.printStackTrace();

}

_instance_ = **new** Singleton();

}

**return** _instance_;

}

}

**Output:**

![image](https://user-images.githubusercontent.com/76866301/113559023-4eca5400-961e-11eb-820f-b13b4072ed27.png)

-
# Bill pugh singleton implementation :

- To prevent the issue of memory modelling in java bill pugh is used.
- When any client call the getinstance method then only the instance is created.
- When we use this with multithreaded environment we don&#39;t need to synchronized the class, therefore it is thread safe.

**Step 1:**

**package** pack\_Singleton;

**public**** class** Singleton

{

**private** Singleton()

{

}

**public**** static ****class** SingletonFolder

{

**public**** static ****final** Singleton _ **instance** _ = **new** Singleton();

}

**public**** static** Singleton getinstance()

{

**return** SingletonFolder._ **instance** _;

}

}

**Step 2:**

**package** pack\_Singleton;

**public**** class** Test {

**public**** static ****void** main(String[] args)

{

Singleton obj1 = Singleton._getinstance_();

Singleton obj2 = Singleton._getinstance_();

System._ **out** _.println(obj1.hashCode());

System._ **out** _.println(obj2.hashCode());

}

}

**Output:**

![image](https://user-images.githubusercontent.com/76866301/113559079-66094180-961e-11eb-895e-0f4013abcfd2.png)

-
# **Using Reflection to destroy singleton pattern :**

- Using reflection we can break singleton pattern created by above all the approaches.
- So if we want that our singleton shouldn&#39;t be broked by reflection we should use enum.

**Step 1:**

**package** pack\_Singleton;

**public**** class** Singleton

{

**public**** static **Singleton _instance_ =** null**;

**private** Singleton()

{

}

**public**** static** Singleton getinstance()

{

**if** (_instance_ == **null** )

{

_instance_ = **new** Singleton();

}

**return** _instance_;

}

}

**Step 2:**

**package** pack\_Singleton;

**import** java.lang.reflect.Constructor;

**import** java.lang.reflect.InvocationTargetException;

**public**** class** Test {

**public**** static ****void** main(String[] args) **throws** InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException

{

Singleton obj1 = Singleton._getinstance_();

Singleton obj2 = **null** ;

Constructor\&lt;?\&gt;[] constructors = Singleton. **class**.getDeclaredConstructors();

**for** (Constructor\&lt;?\&gt; constructor : constructors)

{

constructor.setAccessible( **true** );

Object object = constructor.newInstance();

obj2 = (Singleton)object;

**break** ;

}

System._ **out** _.println(obj1.hashCode());

System._ **out** _.println(obj2.hashCode());

}

}

**Output :**

![image](https://user-images.githubusercontent.com/76866301/113559120-73bec700-961e-11eb-8590-6d399953820d.png)

-
# **Singleton using enum :**

- Using enum we can avoid breakage of singleton using reflection .
- In enum, java allow instantiation only once because it has global access.
- Drawback of enum is that it doesn&#39;t allow Lazy initialization.

**Step 1 :**

**package** pack\_enumDesign;

**public**** enum** Singleton

{

_ **Getinstance** _;

**public** String printMessage()

{

**return**&quot;Enum Implemented Successfully !&quot; ;

}

}

**Step 2 :**

**package** pack\_enumDesign;

**public**** class** ClassTest

{

**public**** static ****void** main(String[] args)

{

Singleton obj1 = Singleton._ **Getinstance** _;

Singleton obj2 = Singleton._ **Getinstance** _;

System._ **out** _.println(obj1.hashCode());

System._ **out** _.println(obj2.hashCode());

System._ **out** _.println(obj1.printMessage());

}

}

**Output :**

![image](https://user-images.githubusercontent.com/76866301/113559146-820ce300-961e-11eb-9374-0dee2d01be74.png)

-
# **How to prevent cloning to break a Singleton Class Pattern :**

- While creating a clone there is the chance of breakage of singleton pattern .
- For that we just need to throw exception of clone not supported from inside the overriden method clone.

**Step 1:**

**package** pack\_Singleton;

**public**** class **Singleton** implements** Cloneable

{

**public**** static **Singleton _instance_ =** null**;

**private** Singleton()

{

}

**public**** static** Singleton getinstance()

{

**if** (_instance_ == **null** )

{

_instance_ = **new** Singleton();

}

**return** _instance_;

}

@Override

**protected** Object clone() **throws** CloneNotSupportedException

{

**throw**** new** CloneNotSupportedException(&quot;You cannot create clone of singleton&quot;);

//return super.clone();

}

}

**Step 2:**

**package** pack\_Singleton;

**import** java.io.ObjectOutput;

**public**** class** Test {

**public**** static ****void** main(String[] args)

{

Singleton obj1 = Singleton._getinstance_();

//Singleton obj2 = (Singleton)obj1.clone();

Singleton obj2 = Singleton._getinstance_();

System._ **out** _.println(obj1.hashCode());

System._ **out** _.println(obj2.hashCode());

}

}

**Output :**

![image](https://user-images.githubusercontent.com/76866301/113559190-9224c280-961e-11eb-8ecd-a21eb7d3164b.png)

-
# **Examples of Singleton Design Pattern in JDK :**

# **1). Runtime class**

![image](https://user-images.githubusercontent.com/76866301/113559211-9c46c100-961e-11eb-9eb0-873005c2eb8a.png)

- As you can see Runtime class is implementing singleton design pattern, instance of class is created while loading of class and it has private constructor.

# **2). System class**

![image](https://user-images.githubusercontent.com/76866301/113559239-a5d02900-961e-11eb-95bd-8a458ac00075.png)

# **3). Desktop**

![image](https://user-images.githubusercontent.com/76866301/113559274-b2548180-961e-11eb-9a8b-06b32375ec8d.png)
