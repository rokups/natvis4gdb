natvis4gdb
==========

![image](https://user-images.githubusercontent.com/19151258/61788416-b0329b00-ae1a-11e9-9230-0ff36e002420.png)

natvis4gdb is a single script natvis implementation for GDB debugger.

Natvis Documentation: https://docs.microsoft.com/en-us/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015#BKMK_Using_Natvis_files

## Supported features

  * `<Type>` element with partial matching of template types.
  * `<DisplayString>` with optional `Condition` attribute and expression evaluation within `{}`.
  * Access to template parameters inside expressions through `$T1..N` variable.
  * Format specifiers for expression evaluation:
    * sb
    * d
  * `<ArrayItems><Size/><ValuePointer/></ArrayItems>` elements.
  
  Features unsupported at this time will be silently ignored by the script.

## Usage

Enable script by editing `~/.gdbinit` and add following:
```
python
sys.path.insert(0, '/path/to/natvis4gdb')
import natvis4gdb
natvis4gdb.register()
end
```
Load natvis files by executing command `add-natvis /path/to/your.natvis`

## Debugging

1. Modify your `~/.gdbinit` file and add following
```
python
sys.path.insert(0, '/path/to/natvis4gdb')
sys.path.insert(0, os.getenv('HOME') + '/.local/lib/python3.7/site-packages')
import natvis4gdb
natvis4gdb.register(True)
end
```
2. Also install required python library like `pip install --user pydevd-pycharm`.
3. Create `Python Remote Debug` configuration in PyCharm and set it to connect to port 41879.
4. Start remote debugging session in PyCharm.
5. Run C++ application that will be inspecting some variables.
6. Inspect some variables in your C++ application and breakpoints in PyCharm should trigger.

Parts and ideas salvaged from https://github.com/asarium/gdb-natvis
