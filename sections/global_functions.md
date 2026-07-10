## 🌍 Global Functions

Global functions are defined outside of any class and are accessible from any part of the codebase. They are commonly used for utility and helper functions.

-   `IsValid()`: Check if a pointer or object reference is valid. This is important to avoid accessing or modifying null pointers, which can cause crashes or other unexpected behavior.

-   `Swap()`: Swaps the contents of two `TObjectPtr` objects.

-   `Exchange()`: Exchanges the contents of a `TObjectPtr` with a new object, returning the previous object.

-   `MakeWeakObjectPtr()`: Creates a weak pointer (`TWeakObjectPtr`) from a `TObjectPtr`, allowing for non-owning references to the object.

-   `Cast()`: Dynamically cast to another object. If the cast object is not of the specified type, it will return a nullptr. If the object is of the specified type or a subclass of it, the function will return a pointer to the object cast to the specified type.

-   `CastChecked()`: Similar to `Cast()`, but it also performs a runtime check in debug builds to ensure that the object is of the specified type. If the check fails, it will trigger an assertion. This function is useful when you are certain that an object should be of a particular type and want to catch errors early in development.

-   `StaticCast()`: Tries to cast at compile-time. However, some code might only work at runtime, therefore the compiler will decide if static cast is "appropriate" to do so.

> [!NOTE]
> The `StaticCast()` function is just forwarding the built-in cast operation from C++, which is called `static_cast()`. Which means, there is no saftey garunete with Unreal Engine `UObject`s.
