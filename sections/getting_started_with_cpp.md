## ⌛ Getting started with C++

Highly recommend taking a short class of native C++. Here is a video link to ~1h long [video tutorial from Mosh](https://www.youtube.com/watch?v=ZzaPdXTrSb8).

You can also watch a playlist from [GGameDev about getting started with Unreal Engine C++](https://youtube.com/playlist?list=PLaaDnVlfJwc4Lncf4XTYaTRG_osOk-T0N).

C++ is a statically typed, compiled, general-purpose programming language that offers a combination of high-level and low-level features. It was developed by [Bjarne Stroustrup](https://en.wikipedia.org/wiki/Bjarne_Stroustrup) at Bell Labs in 1979 as an enhancement to the [C language](https://en.wikipedia.org/wiki/C_(programming_language)), originally named C[^10] with Classes and later renamed [C++](https://en.wikipedia.org/wiki/C%2B%2B) in 1983.

You can read more about [C++ Language Reference from Microsoft Learn](https://learn.microsoft.com/en-us/cpp/cpp/cpp-language-reference?view=msvc-170).

Using C++ with Unreal Engine unlocks the engine's full feature set, allowing developers to harness advanced graphics rendering, physics simulations, networking, and AI capabilities. C++ provides a level of control, customization, and performance optimization that complements visual scripting.

Developing with C++ in Unreal Engine enables better debugging, profiling, and performance optimization through techniques such as multithreading and memory management. It also facilitates integration with third-party libraries, expanding the range of functionality and flexibility available to developers.

You can read more about it on [their docs](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-programming-and-scripting/).

To use C++ effectively in Unreal Engine, it is crucial to have a strong foundation in programming principles and understanding of Unreal Engine's architecture and conventions. Leveraging resources like the Unreal Engine documentation, community forums, and collaboration with other developers helps to gain knowledge and best practices.

*By combining the power of C++ and Unreal Engine, developers can create immersive experiences and unlock the full potential of the engine's capabilities.*

### 🌈 Integrated Development Environment

An Integrated Development Environment (IDE) provides tools for writing, debugging, and managing code.

Popular IDEs for Unreal Engine C++ development:

* [Visual Studio 2022](https://visualstudio.microsoft.com/) (recommended) or [Visual Studio 2026](https://visualstudio.microsoft.com/): Full C++ toolchain, .NET 10 support. `Free` for individual devs.
* [Visual Studio Code](https://code.visualstudio.com/): Lightweight editor with UE extensions. `Free`.
* [Rider](https://www.jetbrains.com/rider/): JetBrains IDE with deep UE integration. `Cost`.

### ⛏️ Tools to help your journey

Tools that integrate into your IDE for better performance and debugging:

* [Visual Assist](https://www.wholetomato.com/): A productivity tool for refactoring, reading, writing, navigating and generating C/C++/C# code. `Cost` and for `VS`.

* [UnrealMacroGenerator](https://marketplace.visualstudio.com/items?itemName=Naotsun.Naotsun-UE-UMG): Provides a macro editor used by Unreal C ++ of Unreal Engine. You can create macros and edit already written macros. `Free` and for `VS`.

### 🟢 Benefits of using C++ with Unreal Engine

* **High performance**: C++ runs directly on the CPU/GPU, making it possible to achieve very high performance levels.
* **Integration**: Easily integrate existing C++ codebases with UE projects.
* **Low-level access**: Fine-grained control over memory, data structures, and algorithms.
* **Garbage Collection**: UE provides a [garbage collector](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)) for UObject classes alongside manual memory management.

### 🔴 Drawbacks of using C++ with Unreal Engine

* More prone to errors: C++ is a strongly typed language, requiring the precise use of semicolons, braces and accurate syntax to ensure successful compilation. Rectifying these issues can be time-consuming. On the contrary, the Blueprint's node-based graph system operates without the need for "correct" syntax, offering a more "forgiving" environment.

* Tied to Unreal's API: Throughout the evolution of Unreal Engine, Epic Games may modify the [source code](https://en.wikipedia.org/wiki/Source_code), rendering certain functions and members as **obsolete**/**deprecated**. Consequently, Unreal might recommend the need to update the codebase with the latest [API](https://en.wikipedia.org/wiki/API) changes. Failure to do so can lead to compilation errors, in the future.

* Updating your codebase: C++ code compiles into a [.DLL](https://en.wikipedia.org/wiki/Dynamic-link_library) that UE loads. Epic provides [Live Coding](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-coding-in-unreal-engine) for iterating on C++ changes without restarting the editor. (Hot Reload was deprecated in UE 5.0 and removed in UE 5.8.)

* Requires more storage: When working with C++ within Unreal Engine, it often involves using "Editor Symbols for debugging," consuming approximately 60 GB of storage. Similarly, if you opt to build Unreal Engine from its source code (on their github page), you'll require around 200 GB of storage space.
