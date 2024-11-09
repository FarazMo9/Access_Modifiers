# Access_Modifiers
Let's see a brief description of C# access modifiers.

The access modifiers are defined as a limitation on accessibility of a type or type’s members.

•	public: This kind of modifier lets the pointed type to be fully accessible.

•	internal: It’s only accessible inside the assembly or friend assemblies. That’s the default modifier for non-nested types.

•	private: Only accessible within the containing type. It’s the default accessibility for the members of a class or struct.

•	protected: Accessible only within the containing type or subclasses.

•	protected internal: The union of the “protected” and “internal” conditions. So, this would be accessible inside the assembly and subclasses of the containing assembly.

•	private protected: Accessible only within the containing type or subclasses of the same assembly.

Let's check by an example : 
Imagine we have three class classes named "ClassA" and "ClassAChild" and anoter one which is "ClassB".

```
namespace AccessModifiers
{
    class ClassA // Default modifier is the "internal"
    {
        int number=1; // Default modifier for the member is "private"
        protected int secondNumber;
        //The below property would be accessible through ClassAChild or the current namespace.
        protected internal int thirdNumber;
        //The below property would be accessible only through the curren class body or ClassAChild.
        private protected int forthNumber;
    }
}
```

```
namespace AccessModifiers
{
    internal class ClassAChild:ClassA
    {
        // The effect of protected modifier which is only accessible through ClassA or ClassAChild in this sample.
        public int relatedNumber=>this.secondNumber; 
    }
}
```

```
namespace AccessModifiers
{
    class ClassB // Default modifier is the "internal"
    {
        internal int number;
    }
}
```

As you can see, the class modifiers has been set to "internal" whether by default or explicitely.
So, they are accessible through the current namespace. Now let's assume they are going to be initialized on the Main method.

```
 internal class Program
 {
     static void Main(string[] args)
     {
   // The two below classes are accessible while they're in the same assembly because of having internal modifier as default.
   ClassA classA = new ClassA(); 
   ClassB classB = new ClassB();

   // It is obvious that the number property of the ClassA is not accessible while the default modifier is private. But the "secondNumber" property
   // can be accessed due to having proteted modifier inside a child member type of ClassA as below:
   ClassAChild classAChild = new ClassAChild();
   var classANumber= classAChild.relatedNumber;

   // The ClassB number property modifier is internal. So, it will be acceessible within the current assembly.
   classB.number = 2;

    }
}

```

I tried to describe what happens due to each access modifier by the comments of the above sample code.
Hope to be useful for undertanding the concept better.


