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

An IDE provides comprehensive tools for writing, debugging, and managing code efficiently.

Popular IDEs for Unreal Engine C++ development:

* **[Visual Studio](https://visualstudio.microsoft.com/)**: Microsoft's flagship IDE with robust C++ tools and seamless Unreal integration. `Free`

* **[Visual Studio Code](https://code.visualstudio.com/)**: Lightweight, cross-platform editor with extensive Unreal Engine extensions. `Free`

* **[Rider](https://www.jetbrains.com/rider/)**: JetBrains IDE primarily designed for C#, with strong C++ support for Unreal Engine development. `Free` (personal), `Paid` (commercial)

* **[CLion](https://www.jetbrains.com/clion/)**: JetBrains C++-focused IDE with intelligent code assistance and debugging capabilities. `Free` (personal), `Paid` (commercial)

### ⛏️ Tools to help your journey

<table><tr><td>
This section was NOT written in conjunction with ChatGPT.
</td></tr></table>

Here are some tools that can be integrated into your IDE's for better performance, debugging or writing good code practices.

* [Visual Assist](https://www.wholetomato.com/): A productivity tool for refactoring, reading, writing, navigating and generating C/C++/C# code. `Paid` and for `VS`.

* [UnrealMacroGenerator](https://marketplace.visualstudio.com/items?itemName=Naotsun.Naotsun-UE-UMG): Provides a macro editor used by Unreal C ++ of Unreal Engine. You can create macros and edit already written macros. `Free` and for `VS`.

### 🟢 Benefits of using C++ with Unreal Engine

<table><tr><td>
This section was written in conjunction with ChatGPT.
</td></tr></table>

* **High performance**: Direct CPU/GPU execution enables maximum performance for critical systems.
* **Code integration**: Seamless integration with existing C++ codebases.
* **Low-level control**: Fine-grained memory, data structure, and algorithm management.
* **Hybrid memory management**: Manual control combined with Unreal's garbage collector for UObject classes.

### 🔴 Drawbacks of using C++ with Unreal Engine

<table><tr><td>
This section was written in conjunction with ChatGPT.
</td></tr></table>

* **Error-prone syntax**: Strict typing and compilation requirements compared to Blueprint's forgiving node system.
* **API dependency**: Engine updates may deprecate functions, requiring codebase maintenance for compilation compatibility.
* **Development friction**: Hot Reload is unreliable and often causes blueprint corruption, requiring full editor restarts.
* **Storage overhead**: Editor symbols consume ~60GB; building from source requires ~200GB (may vary in the future).
