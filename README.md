# Funcy SQF

## Download

[For Linux](https://github.com/xetra11/Funcy-SQF/releases/download/v1.1.0/funcy)

[For Windows (untested)](https://github.com/xetra11/Funcy-SQF/releases/download/v1.1.0/funcy.fy)

**You need to have Python 3 installed for `funcy` to work**


## Description
I made this tool to get rid of the tedious job of defining functions and adding them to the CfgFunctions.hpp file.
This tool was made for CoopR-Mod. Its use-case is to be integrated into workflows via build-scripts, key-bindings (like Emacs or IntelliJ, etc.) for instance in Emacs or IntelliJ. I bound it to a key in my Spacemacs (Emacs on steroids) and find it very convenient.

## How to use
Place `funcy` in your mod directory where your `addons` folder is located. Funcy needs to know where your `addons` directory is and looks for it where it (the tool) is being executed. When executing `funcy` you have to provide specific parameters. `funcy --help` will give you a description how to use the tool.

## CLI Doc
```
usage: Funcy v1.1.0 [-h] [-v] [-t] [-d] [-o] tag addon name [category]

Creates SQF functions

positional arguments:
  tag              the tag of your mod
  addon            the addon the function should be created for
  name             name of the function (without fn prefix)
  category         the category where the function is defined

optional arguments:
  -h, --help       show this help message and exit
  -v, --verbose    prints log messages to follow the process
  -t, --template   uses a template for creating function files
  -d, --dry-run    performs a dry run without changing any files
  -o, --overwrite  overwrites existing function entry and file

When using Funcy without the template flag (-t) the created function will be
blank. To use a global template for all functions create a file called
'template.fy' in the directory Funcy is in. When creating a function Funcy will
take the content of this template file for all created functions. If you want to
have a different template per category then put a 'template.fy' file into the
specific directory ie. /addons/core/functions/template.py
```

### Prerequisites
As prerequisite for `funcy` to work you need to have a mod/addon folder structure in terms of **Folder Path** which is described here: https://community.bistudio.com/wiki/Arma_3_Functions_Library (scroll down to the _Folder Path_ section)
It describes a way to declare functions in the `CfgFunctions.hpp` file like this:

```
class CfgFunctions
{
	class myTag
	{
		class myCategory
		{
			file = "myPath";
			class myFunction {};
		};
	};
};
```
Please stick to this if you are using `funcy` because the other "ways" of declaring functions is not yet implemented but will come for sure if requests are made for it.

## Example Usage
Let's say you have the following mod structure: `.../mymod/addons/core/helper/`. So you have in your mod an addon folder called `core` with all of your core functions/features in it. In there you separate your functions into subfolders or categories. Your `CfgFunctions.hpp` file however resides in the addon folder `core`. Now you want to add a new function to the `helper` category/subfolder. To do so place execute `funcy` from the `mymod` folder. The `funcy` tool itself can be anywhere on your system but it has to be executed from where it can find the `addons` folder of your mod. To add a new function type the following:

```funcy mymod core myNewFunction helper```

Funcy now creates a new function file called `fn_myNewFunction.sqf` in the category/subfolder `helper` which itself is in the addon folder `core`. Additionally `funcy` adds an entry to `.../mymod/addons/core/CfgFunctions.hpp`.

## Advanced Usage

### Overwrite functions
If `funcy` detects that the function you want to add is already existing either as function file (.sqf) or is declared in the `CfgFunctions.hpp` config it will abort the operation to avoid accidental overwrites or duplicates. If you still want to overwrite the function you can add the `-o` or `--overwrite` option. `funcy` will then overwrite the function.

### Dry-Run
If you are unsure what `funcy` does to your `CfgFunctions.hpp` file or your mod directory but you still want to see how `funcy`'s CLI works you can use the `-d` or `--dry-run` option. This will log all the stuff that happens **without** changing anything. Use in combination with `-v` or `--verbose` to understand more about `funcy`'s process.




