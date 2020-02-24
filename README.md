# Global Hot Key Core
Provides an easy way to setup system-wide hot keys and react on their events. Works well in both, WPF and WebForms applications without any need to use Windows API.
This fork added .NET Core 3.1+ support.

# Installation

Th package is available through the NuGet by running the command

```
PM> Install-Package GlobalHotKeyCore
```

# Usage

An example below demonstrates how to register system-wide hotkey Ctrl+Alt+F5 and handle it:
```csharp
// Include required namespaces.
using System.Windows.Input;
using GlobalHotKey;

// Create the hotkey manager.
hotKeyManager = new HotKeyManager();

// Register Ctrl+Alt+F5 hotkey. Save this variable somewhere for the further unregistering.
var hotKey = hotKeyManager.Register(Key.F5, ModifierKeys.Control | ModifierKeys.Alt);

// Handle hotkey presses.
hotKeyManager.KeyPressed += HotKeyManagerPressed;

private void HotKeyManagerPressed(object sender, KeyPressedEventArgs e)
{
    if (e.HotKey.Key == Key.F5)
        MessageBox.Show("Hot key pressed!");
}

// Unregister Ctrl+Alt+F5 hotkey.
hotKeyManager.Unregister(hotKey);

// Dispose the hotkey manager.
hotKeyManager.Dispose();
```

`HotKeyManager` class registers and unregisters system-wide hotkeys, handles them, and raises an event on hotkeys pressing. `KeyPressedEventArgs` class contains information about pressed hotkey and keys modifiers.
Note, that it is not necessary to unregister all hotkeys manually before closing application, because `Dispose()` does it. Make sure that it is called.
