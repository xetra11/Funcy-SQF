# Funcy SQF
## Description
I made this tool to get rid of the tedious job of defining functions and adding them to the CfgFunctions.hpp file.
This tool was made for CoopR-Mod but I think it might be useful for others as well. The idea is to bind this tool to a workflow keybinding
for instance in Emacs or IntelliJ. I bound it to a key in my Spacemacs (Emacs on steroids) and find it very convenient.
## How to use
Place `funcy` in your mod directory where your `addons` folder is located. Funcy needs to know where your `addons` directory is and looks for it where it (the tool) is being executed. When executing `funcy` you have to provide specific parameters. `funcy --help` will give you a description how to use the tool.
### Example
Let's say you have a folder structure like this `/addons/core/functions/`. In the `functions` all you functins are in. Your `CfgFunctions.hpp` however is within `/addons/core/CfgFunctions.hpp`. This is the structure I use and for what `funcy` was build for. You can have different styles of defining functions in the `CfgFunctions.hpp` but only with one `funcy` is working at the moment.

```
class CfgFunctions {
    class yourmod {
        class yourmod_core_functions {
            file = "x\coopr\addons\core\functions";
            class foo {};
            class bar {};
            class test {};
        }
    }
}
```

This part `class yourmod_core_functions` in the CfgFunctions file is mandatory to be defined exactly this way. In ArmA 3 it does not matter how you describe this class definition.

If the above is setup exactly this way `funcy` is ready to use. Just give it the following parameters: `funcy yourmod core functions myNewFunction`. funcy should then create a new function called `class myNewFunction {}` in your CfgFunctions config file and create a new file called `fn_myNewFunction.sqf` in your `/addons/core/functions` directory.





