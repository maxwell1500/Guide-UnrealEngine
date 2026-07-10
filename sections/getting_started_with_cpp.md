## ⌛ Getting started with C++

New to C++? Start with this ~1 hour [crash course from Mosh](https://www.youtube.com/watch?v=ZzaPdXTrSb8). Already know the basics? Jump straight into UE-specific stuff with [GGameDev's playlist](https://youtube.com/playlist?list=PLaaDnVlfJwc4Lncf4XTYaTRG_osOk-T0N).

**Why C++ in Unreal?** Blueprints are great for prototyping, but C++ gives you:
- Full control over memory, data structures, and algorithms
- Direct access to engine internals (rendering, physics, networking, AI)
- Better debugging and profiling
- Integration with third-party C++ libraries

> [!TIP]
> If you're coming from Blueprints, think of C++ as the "unlock" — things you couldn't do or that ran slowly in BP become possible. The trade-off? You write more code and wait for compiles.

### 🌈 IDE Setup

You need somewhere to write code. Here are the options:

| IDE | Cost | Best for |
|-----|------|----------|
| [Visual Studio 2022/2026](https://visualstudio.microsoft.com/) | Free (Community) | Full C++ toolchain, .NET 10, UE project integration |
| [Visual Studio Code](https://code.visualstudio.com/) | Free | Lightweight editing with UE extensions |
| [Rider](https://www.jetbrains.com/rider/) | Paid | Deep UE integration, refactoring tools |

### ⛏️ IDE Add-ons

| Tool | Cost | What it does |
|------|------|-------------|
| [Visual Assist](https://www.wholetomato.com/) | Paid (VS only) | Refactoring, navigation, code generation for C/C++/C# |
| [UnrealMacroGenerator](https://marketplace.visualstudio.com/items?itemName=Naotsun.Naotsun-UE-UMG) | Free (VS only) | Edit Unreal Header Tool macros without memorizing every specifier |

### 🟢 Pros of C++ in UE

- **Performance** — runs on CPU/GPU directly. No interpreter overhead.
- **Integration** — plug in existing C++ libraries (physics, networking, etc.)
- **Control** — manage memory, choose data structures, optimize hot paths
- **GC** — UE's garbage collector handles `UObject` cleanup, but you still manage non-UObject memory yourself

### 🔴 Cons of C++ in UE

- **Strict syntax** — missing a semicolon or brace means a compile error. Blueprints don't have that problem.
- **API churn** — Epic deprecates and removes APIs between versions. Code that compiled in UE 5.3 might not in 5.8.
- **Compile times** — C++ compiles to a DLL that UE loads. [Live Coding](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-coding-in-unreal-engine) helps iterate faster. (Hot Reload was removed in 5.8.)
- **Disk space** — editor symbols for debugging take ~60 GB. Building UE from source takes ~200 GB.
