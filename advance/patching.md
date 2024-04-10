
### How to patch class method dynamically

```
obj.method = types.MethodType(patched_method, obj)

obj.method()   # this will call patched_method
```

## Why it works

Monkey patching works in Python because of the language's dynamic nature. Here's a breakdown of the key factors that enable it:

1. **First-Class Objects:** In Python, functions are first-class objects. This means you can treat them like any other data type: assign them to variables, pass them as arguments, and even return them from functions.

2. **Mutable Attributes:** Python allows modifying attributes of objects at runtime. This includes attributes that point to functions within modules or classes.

3. **Late Binding:** Python utilizes dynamic or late binding. This means the specific function that gets executed when you call a function name is determined at runtime based on the object's type and its attributes.

**How Monkey Patching Leverages These Features:**

1. **Replacing Function References:** When you monkey patch, you essentially modify the attribute in a module or class that points to the original function. You assign a new function object to this attribute.

2. **Late Binding Takes Over:** Since Python uses late binding, when you call the patched function name, the interpreter checks the object's current attribute for the function. It executes the newly assigned function instead of the original one.

**Benefits and Trade-offs:**

* **Flexibility:** Monkey patching offers flexibility for dynamic modifications at runtime. This can be useful for testing (replacing functionality with mocks), customizing behavior, or implementing workarounds for bugs.
* **Potential Issues:** However, monkey patching can also lead to unexpected behavior if not used cautiously. It can make code harder to understand and maintain since the actual function being executed might not be readily apparent. Additionally, if multiple parts of your code rely on the same module or class, unintended side effects can arise due to unexpected patches.

**Alternatives to Consider:**

* **Dependency Injection:** Dependency injection is a design pattern that promotes loose coupling. You can inject the desired functions as dependencies into your code, making it easier to test and manage different implementations.
* **Subclasses:** In some cases, creating subclasses that override specific methods can provide a more controlled way to modify behavior without directly patching the original code.

**In Conclusion:**

Monkey patching is a powerful technique in Python, but it's essential to weigh its benefits against potential drawbacks. Consider using it judiciously and explore alternative approaches like dependency injection or subclassing for better code maintainability and testability in the long run.

## Why we need `types.MethodType` while assigning new reference

In Python, `types.MethodType` is a class that represents the type of bound methods. Bound methods are methods that are attached to a specific object instance.

Here's a breakdown of what `types.MethodType` signifies:

* **Bound Methods:** When you define a method within a class, it's typically designed to operate on instances of that class. These methods take `self` as the first argument, which refers to the specific object instance the method is called on. When you call a method on an object instance (e.g., `obj.method_name()`), Python creates a bound method object that links the method with the object.
* **Internal Representation:** `types.MethodType` is the internal type that Python uses to represent these bound methods. It essentially combines the method function itself and the object instance (`self`) into a single entity. There's no direct way to create `types.MethodType` objects yourself in most cases.

**Why `types.MethodType` Exists (Although Hidden):**

Even though you don't typically create `types.MethodType` objects directly, it plays a role behind the scenes in how methods and objects interact:

* **Method Calls:** When you call a method on an object (`obj.method_name()`), Python retrieves the method object associated with that name in the class. It then creates a bound method object using `types.MethodType` that links the method function with the specific `obj` instance. This bound method is then invoked.
* **Descriptor Protocol:** Methods in Python classes leverage the descriptor protocol. When you access an attribute that refers to a method, the descriptor's `__get__()` method is called. This method typically returns a bound method object using `types.MethodType`.

**Key Points:**

* `types.MethodType` is an internal type used for bound methods in Python.
* You don't usually need to create `types.MethodType` objects directly.
* It plays a role in how method calls and the descriptor protocol work.

**Additional Context:**

* If you're curious about the descriptor protocol and how methods are implemented in Python, you can explore resources on these topics. However, for most developers, understanding `types.MethodType` at a basic level is sufficient.

I hope this explanation clarifies the concept of `types.MethodType` in Python!
