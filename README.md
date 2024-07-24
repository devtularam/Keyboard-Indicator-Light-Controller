# Keyboard Light Control

This C# console application controls the keyboard lights (Num Lock, Caps Lock, and Scroll Lock) by toggling them in a sequential manner, 
creating a signal light effect. The lights turn on sequentially, then turn off sequentially, 
and this process repeats until the user stops the program by pressing any key.

## Features

- Toggle Num Lock, Caps Lock, and Scroll Lock lights in sequence.
- Lights turn on sequentially, then turn off sequentially.
- Continuous looping until the user interrupts by pressing any key.

## Requirements

- Windows operating system (required for the `user32.dll` library functions).
- .NET Framework or .NET Core SDK installed.

## Usage

1. Clone the repository:

    ```sh
    git clone https://github.com/devtularam/Keyboard-Indicator-Light-Controller.git
    ```

2. Open the project in your favorite C# IDE (e.g., Visual Studio, Visual Studio Code).

3. Build the project.

4. Run the executable. The keyboard lights will start toggling in sequence.

5. Press any key to stop the program.

## Code Overview

The main functionality is implemented in the `Program.cs` file. Here's an overview of the key components:

### Constants

- `VK_NUMLOCK`, `VK_CAPITAL`, `VK_SCROLL`: Virtual key codes for Num Lock, Caps Lock, and Scroll Lock keys.
- `KEYEVENTF_EXTENDEDKEY`, `KEYEVENTF_KEYUP`: Flags used to simulate key press and release events.

### External Functions

- `GetKeyState`: Retrieves the state of the specified key.
- `keybd_event`: Synthesizes a keystroke, used to simulate key presses and releases.

### Main Method

The `Main` method starts a thread that continuously toggles the keyboard lights in sequence until a key is pressed to stop the program.

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Press any key to stop...");

    bool stop = false;
    Thread signalThread = new Thread(() =>
    {
        while (!stop)
        {
            // Turn on lights sequentially
            TurnOnLight(VK_NUMLOCK);
            Thread.Sleep(500);
            TurnOnLight(VK_CAPITAL);
            Thread.Sleep(500);
            TurnOnLight(VK_SCROLL);
            Thread.Sleep(500);

            // Turn off lights sequentially
            TurnOffLight(VK_NUMLOCK);
            Thread.Sleep(500);
            TurnOffLight(VK_CAPITAL);
            Thread.Sleep(500);
            TurnOffLight(VK_SCROLL);
            Thread.Sleep(500);
        }
    });

    signalThread.Start();
    Console.ReadKey();
    stop = true;
    signalThread.Join();
}
```

### Helper Methods

- `TurnOnLight(int keyCode)`: Turns on the specified key light if it is not already on.
- `TurnOffLight(int keyCode)`: Turns off the specified key light if it is not already off.
- `IsLightOn(int keyCode)`: Checks if the specified key light is currently on.
-  `Thread.Sleep(500)` : You can adjust the time turning Off and On


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Contact

For any questions or suggestions, please contact [tularamkathariya3@gmail.com](mailto:tularamkathariya3@gmail.com).
