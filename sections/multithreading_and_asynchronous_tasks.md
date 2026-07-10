## 🧠 Multithreading and Asynchronous Tasks

A game engine runs on a game loop — a while loop that processes input, updates logic, and renders frames. Simple and predictable. But it doesn't use your CPU efficiently. That's where threads come in.

UE dedicates separate threads for audio, [rendering](https://dev.epicgames.com/documentation/en-us/unreal-engine/threaded-rendering-in-unreal-engine/), and stats, but most gameplay code (EventTicks, Blueprints) still runs on the **game thread**. Expensive Blueprint logic will tank your framerate because it's all on one thread. Threading lets you offload that work.

> [!WARNING]
> Threading adds complexity. You'll deal with [race conditions](https://en.wikipedia.org/wiki/Race_condition) (two threads fighting over the same data), [deadlocks](https://www.youtube.com/watch?v=oEbXlSH8hyE), and subtle bugs that are hard to reproduce. Only thread work that actually needs it.

**Resources:**
- [Game Loop Patterns (Robert Nystrom)](https://gameprogrammingpatterns.com/game-loop.html)
- [Ayliroé's UE Multithreading Guide](https://docs.google.com/document/d/1uw9Dfui5ZepSrBpMc1DrxFOeRFnDu8ubzFse8Mr_s7E/)
- [Multithreading in Blueprint (Project Ispheria)](https://www.youtube.com/watch?v=0Yyh3oQgonI)

### Runnables

`FRunnable` is a class which runs on a dedicated, newly created thread. Which you have full control over it.

They will automatically stop once their work is completed, and are generally useful for big computations that require a nearly continuously running thread.

Here's an example:

```cpp
// .h
#pragma once

#include "CoreMinimal.h"
#include "HAL/Runnable.h"

class FMyThread : public FRunnable
{
public:
    FMyThread( /*Parameters*/ )
    {
        bIsRunning = true;
        Thread = FRunnableThread::Create(this, TEXT("MyThread"));
    };

    virtual ~FMyThread()
    {
    	if (Thread)
    	{
            bool bShouldWait = false; // Will forcefully terminate the thread.
    		Thread->Kill(bShouldWait);
    		delete Thread;
    	}
    }

public:
    bool Init() override;
    uint32 Run() override;
    void Exit() override;
    void Stop() override;

private:
    FRunnableThread* Thread;
    bool bIsRunning;
};
```

```cpp
// .cpp
#include "FMyThread.h"

bool FMyThread::Init()
{
    /* Should the thread start? */
    return true;
}

uint32 FMyThread::Run()
{
    while (bIsRunning)
    {
        /* Work on a dedicated thread */
    }

    return 0;
}

void FMyThread::Exit()
{
    /* Post-Run code, threaded */
}

void FMyThread::Stop()
{
    bIsRunning = false;
}
```

When you want to start your thread, include its header and call its constructor (keep the pointer at hand!):

```cpp
auto* Thread = new FMyThread( /*Parameters*/ );
```

### Tasks

[TaskGraph](https://dev.epicgames.com/documentation/en-us/unreal-engine/tasks-systems-in-unreal-engine/), is a job manager that tries to balance out workload along multiple preexisting threads. This is ideal to send packages of small operations, as it abstracts away from you the complexity of managing threads, and also supports defining dependencies between Tasks.

Queuing Tasks will not cause performance concerns due to the threads being already running, but the system may also be less reactive as it has to find slots to fit the work in inside a limited pool, and sending long Tasks should be avoided to not clog-up threads. It may also sometimes decide to run Tasks directly in the game thread, depending on the setup.

#### AsyncTask

If you want to run a small async operation without creating a dedicated class or starting a new thread and do not need the control logic for pausing or callbacks, you can put it inside an `AsyncTask` running on the TaskGraph:

```cpp
AsyncTask(ENamedThreads::AnyHiPriThreadNormalTask, [this] ()
{
    /* Work on the TaskGraph */
    Caller->FunctionToThread(); // Function call captured using [this]
});
```

If you don't know about **lambda**, then highly recommend reading about it on this [section](./README_CPP.md#-lambda).

#### ParallelFor

A [fancier](https://isaratech.com/ue4-improving-speed-with-parallelfor/) version of `AsyncTask` that splits a for loop into multiple Tasks running in the TaskGraph.

```cpp
ParallelFor(Array.Num(), [&](int32 i)
{
    // Run Array.Num() operations, with current index i
    /* Work on the TaskGraph (order of execution is variable!) */
    ++Array[i];
});
```

There’s no guarantee about the order or the thread safety of the operation within, so you might want to use mutexes or atomics with it. MSVC has [an analogous](https://learn.microsoft.com/en-us/cpp/preprocessor/loop?view=msvc-170) #pragma loop(hint_parallel(n)). Practically speaking, the contents of your loop must be significant to really benefit from this approach.

#### FNonAbandonableTask

A way to declare your own AsyncTasks, in a format that sits inbetween FRunnable and lambda-like AsyncTasks. You can implement your own code in a standalone class to be more reusable, which will run on the TaskGraph instead of inside a dedicated thread, but missing some of FRunnable’s initializing and stopping logic.

```cpp
#pragma once

#include "CoreMinimal.h"
#include "Async/AsyncWork.h"

class FMyTask : public FNonAbandonableTask
{
    friend class FAutoDeleteAsyncTask<FMyTask>;

    FMyTask( /*Parameters*/ )
    {
        /* Constructor */
    }

    void DoWork()
    {
        /* Work on the TaskGraph */
    }

    FORCEINLINE TStatId GetStatId() const
    {
        // Probably declares the Task to the TaskGraph
        RETURN_QUICK_DECLARE_CYCLE_STAT(FMyTask, STATGROUP_ThreadPoolAsyncTasks);
    }
};
```

Start your custom Task like such:

```cpp
auto* MyTask = new FAsyncTask<FMyTask>( /*Parameters*/ );
MyTask->StartBackgroundTask();
```

---

As said before, Ayliroé wrote an awesome documentation on Unreal's multithreading and asynchronous tasks system, which you can read either from [Google Docs](https://docs.google.com/document/d/1uw9Dfui5ZepSrBpMc1DrxFOeRFnDu8ubzFse8Mr_s7E/) or from [Forum Post](https://forums.unrealengine.com/t/multithreading-and-performance-in-unreal/1216417/1).
