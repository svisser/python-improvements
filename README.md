Improvements for Python projects
================================

This is a list of common improvements for your Python code.

These are not necessarily mistakes but they can improve the quality of your code.

**Use sys.version_info instead of sys.version**:
The string `sys.version` is sometimes used to determine version of the
Python interpreter (such as `sys.version[0] > "2"` to run code only for Python 3+).
However, this is a string and there is no guarantee across Python implementations
that the Python version is at the beginning of the string. Instead you should
use the tuple `sys.version_info`. For example: `sys.version_info[0] > 3`. As of
Python 2.7 you can also access the numbers using names, such as `sys.version_info.major`
for the major Python version (i.e., `sys.version_info[0]` is the same as `sys.version_info.major`).

**Ignoring potential future Python versions**:
As part of porting a codebase from Python 2 to a Python 2/3 compatible codebase
some people forget that there most likely will be a Python 4. This means checking
for `if sys.version_info[0] == 3` works for now but will fail to work in Python 4.
The code that you're executing for Python 3 would need to be executed for
Python 4 as well (as Python 4 won't break backwards compatibility with 3). The
Unicode / bytes separation still applies and therefore the code would need to
be `if sys.version_info[0] >= 3: ... else: ...`. If Python 4 does introduce
any specific changes then things can be changed at that time - but without
further changes the Python 3 code would apply.

**Ensure file handles are closed in setup.py**:
In `setup.py` you may wish to read the contents of other files, such as
the README or CHANGELOG, and pass them to `setup()` without explicitly closing
the file yourself. Although running the `setup.py` file will be a short-lived
process, best practises should apply here as well so it's better to close
the file yourself:

    with open(...) as f:
        readme = f.read()
