## 🛸 Reflection System

Unreal Engine's reflection system allows objects and their properties to be accessed and modified at runtime. It stores metadata about each class and its members, generated automatically by the Unreal Header Tool (UHT[^2]) during compilation via the `GENERATED_BODY()` macro and `[FileName].generated.h` header.

The generated header file is typically included in the source file that defines the corresponding class or struct, and it is also included in any other source files that use that class or struct. This ensures that the metadata is available to the engine at compile-time and runtime.

The reflection system is also used in many other areas of the engine, such as serialization and networking. When objects are saved to disk or sent over the network, their properties are serialized into a binary format. The reflection system is used to determine which properties to serialize, and how to convert them to and from their binary representation.

One of the key benefits of the header system is that it allows for very efficient compilation times. Because each C++ file has its own header file, changes to one file do not require recompilation of other files that depend on it. Instead, only the files that include the modified header file need to be recompiled.

You can read more about the [reflection system in the UE docs](https://dev.epicgames.com/documentation/en-us/unreal-engine/reflection-system-in-unreal-engine).
