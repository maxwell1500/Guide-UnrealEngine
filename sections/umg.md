## 🧩 UMG

UMG (Unreal Motion Graphics) is UE's visual UI authoring tool. It provides a node-based system for designing UI elements connected to C++ code.

You can read more about from the [docs](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-ui-designer-for-unreal-engine/).

There is also a video about [UMG Widgets with C++ by Lively Geek](https://www.youtube.com/watch?v=T7v3UnL6PNU).

### UMG with C++

To control Blueprint-created widgets from C++ in Unreal Engine, you can use the `BindWidget` meta property. This powerful feature allows you to establish a connection between widgets created in the Unreal Motion Graphics (UMG) editor and corresponding C++ variables.

By applying the `BindWidget` meta property to a C++ variable, you can establish the link between the widget and the variable, giving you direct access to the widget's properties and functionalities within your C++ code.

Here's an example that demonstrates how to use `BindWidget`:

```cpp
UPROPERTY(meta=(BindWidget)) // Binding via UMG editor
UTextBlock* PlayerDisplayNameText;
```

In this example, the `PlayerDisplayNameText` variable is declared as a `UTextBlock*` type, representing a text widget. The `meta=(BindWidget)` property indicates that this variable is bound to a widget created in the UMG editor.

Now you can access and control `PlayerDisplayNameText` directly from C++ — change its text, color, visibility, or bind events to it.

Here's an example showcasing the usage of the widget:

```cpp
#include "MainMenu.h"

void UMainMenu::NativeConstruct()
{
    if (PlayerDisplayNameText == nullptr)
        return;

    PlayerDisplayNameText->OnClicked.AddDynamic(this, &UMainMenu::UpdatePlayerDisplayName);
}

void UMainMenu::UpdatePlayerDisplayName()
{
    if (PlayerDisplayNameText == nullptr)
        return;

    const FString& NewDisplayName = TEXT("John Doe");
    PlayerDisplayNameText->SetText(FText::FromString(NewDisplayName));
}
```

In this example, assume we have a custom player character class called `AMyPlayerCharacter`. The `UpdatePlayerDisplayName()` function receives a `NewDisplayName` as a parameter, which represents the updated display name for the player.

Inside the function, we check if the `PlayerDisplayNameText` widget is valid. If it is, we use the `SetText()` function to update the text displayed by the widget. In this case, we convert the `NewDisplayName` string to an FText object using `FText::FromString` before assigning it to the `PlayerDisplayNameText` widget.

You can read more about binding widgets with C++ from the [article by BenUI](https://benui.ca/unreal/ui-bindwidget/).

### UI Tweening Library

[BenUI](https://benui.ca/) has also created a free helpful plugin, which helps you animate UMG in C++. Plugin can be install from github[^5]. [Link to repository](https://github.com/benui-dev/UE-BUITween).

Here's an example from UI Tweening Library:

```cpp
UBUITween::Create( SomeWidget, 0.2f )
	.FromTranslation( FVector2D( -100, 0 ) )
	.FromOpacity( 0.2f )
	.ToTranslation( FVector2D( 20, 10 ) )
	.ToOpacity( 1.0f )
	.Begin();
```
