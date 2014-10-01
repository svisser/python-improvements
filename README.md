Improvements for Python projects
================================

This is a list of common improvements for your Python code. These are not
necessarily mistakes but they can improve the quality of your code.

* The string `sys.version` is sometimes used to determine version of the
Python interpreter (such as `sys.version[0] > "2"` to run code only for Python 3+).
However, this is a string and there is no guarantee across Python implementations
that the Python version is at the beginning of the string. Instead you should
use the tuple `sys.version_info`. For example: `sys.version_info[0] > 3`. As of
Python 2.7 you can also access the numbers using names, such as `sys.version_info.major`
for the major Python version (i.e., `sys.version_info[0]` is the same as `sys.version_info.major`).
