## ⌛ Getting started with C++

<table><tr><td>
This section was written in conjunction with ChatGPT.
</td></tr></table>

C++ serves as Unreal Engine's native programming language, providing direct access to the engine's complete feature set and maximum performance potential. While Blueprint visual scripting handles many tasks effectively, C++ becomes essential for performance-critical systems, complex algorithms, and deep engine customization.

Understanding C++ fundamentals, including memory management, object-oriented principles, and compilation processes, forms the foundation for effective Unreal development.

**The language's static typing and compile-time optimizations align well with game development's performance requirements.**

<table><tr><td>

**C++ Fundamentals:**
- [Learn C++ in 1 Hour by Mosh](https://www.youtube.com/watch?v=ZzaPdXTrSb8) (~1 hour video overview)
- [Microsoft C++ Language Reference](https://learn.microsoft.com/en-us/cpp/cpp/cpp-language-reference?view=msvc-170) (Microsoft learn documentation)
- [cppreference](https://cppreference.com) (community-maintained wiki)

**Unreal Engine C++:**
- [GGameDev Unreal C++ Playlist](https://youtube.com/playlist?list=PLaaDnVlfJwc4Lncf4XTYaTRG_osOk-T0N) (YouTube Playlist about UE c++)
- [Official Unreal Programming Documentation](https://docs.unrealengine.com/5.2/en-US/unreal-engine-programming-and-scripting/) (Official docs)
</td></tr></table>

Mastering both C++ principles and Unreal's architectural patterns enables developers to create optimized, maintainable systems that leverage the engine's full capabilities.

### 🌈 Integrated Development Environment

<table><tr><td>
This section was written in conjunction with ChatGPT.
</td></tr></table>

An Integrated Development Environment (IDE) is a software application that provides comprehensive tools for writing, debugging, and managing code. IDEs offer a streamlined and feature-rich environment for software development, making it easier for developers to work on their projects efficiently.

Popular IDEs used in Unreal Engine and C++ development include:

* [Visual Studio](https://visualstudio.microsoft.com/): The Visual Studio IDE for Unreal Engine development. It offers a powerful set of C++ tools and seamless integration with Unreal Engine, providing a robust development environment. `Free`.

* [Visual Studio Code (VSCode)](https://code.visualstudio.com/): Visual Studio Code is a lightweight, cross-platform code editor with a rich ecosystem of extensions, including ones for Unreal Engine development. `Free`.

* [Rider](https://www.jetbrains.com/rider/): Rider is a popular IDE developed by JetBrains, designed for game development, and it offers solid integration with Unreal Engine projects. `Free` (for personal use), `Cost` (for commercial use).

### ⛏️ Tools to help your journey

<table><tr><td>
This section was NOT written in conjunction with ChatGPT.
</td></tr></table>

Here are some tools that can be integrated into your IDE's for better performance, debugging or writing good code practices.

* [Visual Assist](https://www.wholetomato.com/): A productivity tool for refactoring, reading, writing, navigating and generating C/C++/C# code. `Cost` and for `VS`.

* [UnrealMacroGenerator](https://marketplace.visualstudio.com/items?itemName=Naotsun.Naotsun-UE-UMG): Provides a macro editor used by Unreal C ++ of Unreal Engine. You can create macros and edit already written macros. `Free` and for `VS`.

### 🟢 Benefits of using C++ with Unreal Engine

<table><tr><td>
This section was written in conjunction with ChatGPT.
</td></tr></table>

* High performance: C++ allows you to write code that can run directly on the CPU and GPU, making it possible to achieve very high performance levels in your game or application.

* Integration with existing codebases: If you have existing C++ code that you want to integrate with your Unreal Engine project, using C++ allows you to do so more easily.

* Access to low-level functionality: C++ gives you access to lower-level functionality than other programming languages, which can be especially useful in game development where fine-grained control over memory, data structures, and algorithms is often necessary.

* Garbage Collection and Memory Management: While C++ demands manual memory management, Unreal Engine provides a [garbage collector](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)) that efficiently clears out `UObject` classes from memory. With the control over manual memory handling, you can precisely dictate when to allocate and deallocate memory as necessary.

### 🔴 Drawbacks of using C++ with Unreal Engine

<table><tr><td>
This section was NOT written in conjunction with ChatGPT.
</td></tr></table>

* More prone to errors: C++ is a strongly typed language, requiring the precise use of semicolons, braces and accurate syntax to ensure successful compilation. Rectifying these issues can be time-consuming. On the contrary, the Blueprint's node-based graph system operates without the need for "correct" syntax, offering a more "forgiving" environment.

* Tied to Unreal's API: Throughout the evolution of Unreal Engine, Epic Games may modify the [source code](https://en.wikipedia.org/wiki/Source_code), rendering certain functions and members as **obsolete**/**deprecated**. Consequently, Unreal might recommend the need to update the codebase with the latest [API](https://en.wikipedia.org/wiki/API) changes. Failure to do so can lead to compilation errors, in the future.

* Updating your codebase: When working with C++ and Unreal Engine, your C++ code is compiled into a [.DLL](https://en.wikipedia.org/wiki/Dynamic-link_library) (in Windows OS) file that Unreal Engine can read and use within Blueprint graphs. However, this necessitates Unreal Engine to reload to incorporate your code changes. Epic Games has introduced [Hot Reload](https://unrealcommunity.wiki/live-compiling-in-unreal-projects-tp14jcgs), allowing for code reloading without editor restart, streamlining the development process. While Hot Reload often works for a while, it is unreliable and frequently causes blueprint corruption or other issues.

* Requires more storage: When working with C++ within Unreal Engine, it often involves using "Editor Symbols for debugging," consuming approximately 60 GB of storage. Similarly, if you opt to build Unreal Engine from its source code (on their github page), you'll require around 200 GB of storage space.
