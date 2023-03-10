<!--
AUTHORS:
Phuykong Meng
-->

# ISIP NEDC Python Style Guide

<!-- markdown="1" is required for GitHub Pages to render the TOC properly. -->

<details markdown="1">
    <summary>Table of Contents</summary>


</details>

## Acknowledgement

This style guide is heavily influenced by Google's Python Style Guide.

[Google's Python Style Guide](https://google.github.io/styleguide/pyguide.html)

<a id="s1-background"></a>
<a id="1-background"></a>

<a id="background"></a>
## 1 Background

Python is the main dynamic language used at NEDC. This style guide is a list
of *dos and don'ts* for Python programs.

This guide is meant for newer students who recently joined our group as it is
meant to serve as a handbook that allows you to reference it at any time.

As always, this stylistic choice is solely subjective and will vary between
companies, organization, and research groups. If this guide does not answer
any of your doubts or concerns, please talk to a **Senior** or **Dr. Joseph Picone**.

## 2 Template

Below are templates that you can use to save time. These templates are expected in all of the group's utility and classes.

The author is highly encouraged to follow other utilities/classes style and use his/her best judgement when it comes down to the specific detail implementation.

### 2.1 Utility

#### 2.1.1 Utility Comment Header

Raw Template:

```python
#!/usr/bin/env python
#
# file: path/to/utility/example.py
#
# revision history:
#
# yyyymmdd (first_name_initial last_name_initial): what did you change?
#
# Short description of the utility
#------------------------------------------------------------------------------

# import system modules
#

# import nedc_modules
#

#------------------------------------------------------------------------------
#
# global variables are listed here
#
#------------------------------------------------------------------------------

# set the filename using basename
#
__FILE__ = os.path.basename(__file__)

# define the location of the help files
#
HELP_FILE = \
    "path/to/utility/example.help"

USAGE_FILE = \
    "path/to/utility/example.usage"

# define local constants
#
DEF_EXAMPLE = "example"

# define the program options:
#  note that you cannot separate them by spaces
#
ARG_EXAMPLE = "--example_argument"
ARG_ABRV_EXAMPLE = "-e"

# define default argument values
#
DEF_EXAMPLE = int(1)

# define the required number of arguments
#
NUM_ARGS = 0

#------------------------------------------------------------------------------
#
# functions are listed here
#
#------------------------------------------------------------------------------

# declare a global debug object so we can use it in functions
#
dbgl = ndt.Dbgl()

```

Example:

```python
#!/usr/bin/env python
#
# file: $NEDC_NFC/util/python/nedc_convert_awstats/nedc_convert_awstats.py
#
# revision history:
#
# 20211024 (JP): refactored the code
# 20211024 (PM): initial version
#
# This is a Python script that converts data from a csv file generated by
# netdata to a JSON format that can be plotted by chart.js on the neuronix
# dashboard: http://www.isip.piconepress.com/projects/neuronix.
#------------------------------------------------------------------------------

# import system modules
#
import csv
import datetime as dt
import json
import os
import sys

# import nedc_modules
#
import nedc_cmdl_parser as ncp
import nedc_debug_tools as ndt
import nedc_file_tools as nft

#------------------------------------------------------------------------------
#
# global variables are listed here
#
#------------------------------------------------------------------------------

# set the filename using basename
#
__FILE__ = os.path.basename(__file__)

# define the location of the help files
#
HELP_FILE = \
    "$NEDC_NFC/util/python/nedc_convert_awstats/nedc_convert_awstats.help"

USAGE_FILE = \
    "$NEDC_NFC/util/python/nedc_convert_awstats/nedc_convert_awstats.usage"

# define local constants
#
DEF_AWSTATS_HEADER = "AWSTATS DATA FILE"
DEF_CSV_FORMAT = "# Date,Visits"
DEF_DATE_FORMAT = "%Y%m%d"
DEF_TXT_FORMAT = "# Date: Visits"
DEF_VISITOR_DELIMITER = "# Date,Pages,Hits,Bandwidth,Visits"

# define the program options:
#  note that you cannot separate them by spaces
#
ARG_INCR = "--increment"
ARG_ABRV_INCR = "-i"

ARG_NDAYS = "--num_days"
ARG_ABRV_NDAYS = "-n"

ARG_OTYPE = "--otype"
ARG_ABRV_OTYPE = "-o"

# define default argument values
#
DEF_INCR = int(1)
DEF_NDAYS = int(365)
DEF_OTYPE = DEF_JSON

# define the required number of arguments
#
NUM_ARGS = 0

#------------------------------------------------------------------------------
#
# functions are listed here
#
#------------------------------------------------------------------------------

# declare a global debug object so we can use it in functions
#
dbgl = ndt.Dbgl()
```

#### 2.1.2 Function Header Definer

Raw Template:
```python
# function: name_of_function
#
# argument:
#   argument1: description of argument1
#
# return: the return type
#
# short description of the function
#
def name_of_function(argument1):
    # code
    pass

```

Example:
```python
# function: nedc_is_awstats
#
# argument:
#   fname: path to awstats file
#
# return: True if file is an awstats file
#
# this function checks the beginning of the file, and decides
# if the file is an awstats file based on its header
#
def nedc_is_awstats(fname):
    # code
```

#### 2.1.3 Error Message

Raw Template:
```python
print("Error: %s (line: %s) %s: description of error (%s)" %
              (__FILE__, ndt.__LINE__, ndt.__NAME__, error))
```

Example:

```python
print("Error: %s (line: %s) %s: error opening file (%s)" %
              (__FILE__, ndt.__LINE__, ndt.__NAME__, fname))
```




















### 2.2 Class

### 2.3 Help File

### 2.4 Usage File

### 2.5 Makefile



## 3 Python Language Rules

### 4.1 Imports

*   Use `import x` for importing packages and modules.
*   Use `from x import y` where `x` is the package prefix and `y` is the module
    name with no prefix.
*   Use `from x import y as z` if two modules named `y` are to be imported, if
    `y` conflicts with a top-level name defined in the current module, or if `y`
    is an inconveniently long name.
*   Use `import y as z` only when `z` is a standard abbreviation (e.g., `np` for
    `numpy`).

For example the module `sound.effects.echo` may be imported as follows:

```python
from sound.effects import echo
...
echo.EchoFilter(input, output, delay=0.7, atten=4)
```

Do not use relative names in imports. Even if the module is in the same package,
use the full package name. This helps prevent unintentionally importing a
package twice.

### 4.2 Packages

Import each module using the full pathname location of the module.

All new code should import each module by its full package name.

Imports should be as follows:

```python
Yes:
  # Reference absl.flags in code with the complete name (verbose).
  import absl.flags
  from doctor.who import jodie

  _FOO = absl.flags.DEFINE_string(...)
```

```python
Yes:
  # Reference flags in code with just the module name (common).
  from absl import flags
  from doctor.who import jodie

  _FOO = flags.DEFINE_string(...)
```

*(assume this file lives in `doctor/who/` where `jodie.py` also exists)*

```python
No:
  # Unclear what module the author wanted and what will be imported.  The actual
  # import behavior depends on external factors controlling sys.path.
  # Which possible jodie module did the author intend to import?
  import jodie
```

The directory the main binary is located in should not be assumed to be in
`sys.path` despite that happening in some environments. This being the case,
code should assume that `import jodie` refers to a third party or top level
package named `jodie`, not a local `jodie.py`.

##### 4.2.1 Exemptions

Exemptions from this rule:

*  NEDC Internal Classes
```python
import nedc_cmdl_parser as ncp
import nedc_debug_tools as ndt
import nedc_file_tools as nft
# etc..
```
### 4.3 Comprehensions & Generator Expressions

List, Dict, and Set comprehensions as well as generator expressions provide a concise and efficient way to create container types and iterators without resorting to the use of traditional loops, `map()`, `filter()`, or `lambda`.

Okay to use for simple cases. Each portion must fit on one line: mapping
expression, `for` clause, filter expression. Multiple `for` clauses or filter expressions are not permitted. Use loops instead when things get more complicated.

```python
Yes:
  result = [mapping_expr for value in iterable if filter_expr]

  result = [{'key': value} for value in iterable
            if a_long_filter_expression(value)]

  result = [complicated_transform(x)
            for x in iterable if predicate(x)]

  descriptive_name = [
      transform({'key': key, 'value': value}, color='black')
      for key, value in generate_iterable(some_input)
      if complicated_condition_is_met(key, value)
  ]

  result = []
  for x in range(10):
      for y in range(5):
          if x * y > 10:
              result.append((x, y))

  return {x: complicated_transform(x)
          for x in long_generator_function(parameter)
          if x is not None}

  squares_generator = (x**2 for x in range(10))

  unique_names = {user.name for user in users if user is not None}

  eat(jelly_bean for jelly_bean in jelly_beans
      if jelly_bean.color == 'black')
```

```python
No:
  result = [complicated_transform(
                x, some_argument=x+1)
            for x in iterable if predicate(x)]

  result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]

  return ((x, y, z)
          for x in range(5)
          for y in range(5)
          if x != y
          for z in range(5)
          if y != z)
```

### 4.4 Lambda Functions

Okay to use them for one-liners. If the code inside the lambda function is
longer than 60-80 chars, it's probably better to define it as a regular
nested function.

### 4.5 Conditional Expressions

Conditional expressions (sometimes called a “ternary operator”) are mechanisms that provide a shorter syntax for if statements. For example: `x = 1 if cond else 2`.

Okay to use for simple cases. Each portion must fit on one line:
true-expression, if-expression, else-expression. Use a complete if statement
when things get more complicated.

```python
Yes:
    one_line = 'yes' if predicate(value) else 'no'

    slightly_split = ('yes' if predicate(value)
                      else 'no, nein, nyet')

    the_longest_ternary_style_that_can_be_done = (
        'yes, true, affirmative, confirmed, correct'
        if predicate(value)
        else 'no, false, negative, nay')
```

```python
No:
    bad_line_breaking = ('yes' if predicate(value) else
                         'no')

    portion_too_long = ('yes'
                        if some_long_module.some_long_predicate_function(
                            really_long_variable_name)
                        else 'no, false, negative, nay')
```

### 4.6 Default Argument Values

You can specify values for variables at the end of a function’s parameter list, e.g., def foo(a, b = 0): . If foo is called with only one argument, b is set to 0. If it is called with two arguments, b has the value of the second argument.

Often you have a function that uses lots of default values, but on rare occasions you want to override the defaults. Default argument values provide an easy way to do this, without having to define lots of functions for the rare exceptions. As Python does not support overloaded methods/functions, default arguments are an easy way of “faking” the overloading behavior.

Do not use mutable objects as default values in the function or method
definition.

```python
Yes: def foo(a, b = None):
         if b is None:
             b = []

Yes: def foo(a, b: Optional[Sequence] = None):
         if b is None:
             b = []

Yes: def foo(a, b: Sequence = ()):  # Empty tuple OK since tuples are immutable.
         ...
```

```python
from foo import bar
example = bar.class_1()

No:  def foo(a, b = []):
         ...
No:  def foo(a, b = time.time()):  # The time the module was loaded???
         ...
No:  def foo(a, b = example.value):  # sys.argv has not yet been parsed...
         ...
No:  def foo(a, b: Mapping = {}):  # Could still get passed to unchecked code.
         ...
```

### 4.7 True/False Evaluations

Python evaluates certain values as `False` when in a boolean context. A quick "rule of thumb" is that all "empty" values are considered false, so `0, None, [], {}, ''` all evaluate as false in a boolean context.

Conditions using Python booleans are easier to read and less error-prone. In most cases, they're also faster.

Use the "implicit" false if possible, e.g., `if foo:` rather than `if foo != []:`. There are a few caveats that you should keep in mind though:

-   Always use `if foo is None:` (or `is not None`) to check for a `None` value. E.g., when testing whether a variable or argument that defaults to `None` was set to some other value. The other value might be a value that's false in a boolean context!

-   Never compare a boolean variable to `False` using `==`. Use `if not x:` instead. If you need to distinguish `False` from `None` then chain the
expressions, such as `if not x and x is not None:`.

-   For sequences (strings, lists, tuples), use the fact that empty sequences are false, so `if seq:` and `if not seq:` are preferable to `if len(seq):` and `if not len(seq):` respectively.

-   When handling integers, implicit false may involve more risk than benefit (i.e., accidentally handling `None` as 0). You may compare a value which is known to be an integer (and is not the result of `len()`) against theinteger 0.

    ```python
    Yes: if not users:
             print('no users')

         if i % 10 == 0:
             self.handle_multiple_of_ten()

         def f(x=None):
             if x is None:
                 x = []
    ```

    ```python
    No:  if len(users) == 0:
             print('no users')

         if not i % 10:
             self.handle_multiple_of_ten()

         def f(x = None):
             x = x or []
    ```

-   Note that `'0'` (i.e., `0` as string) evaluates to true.

## 4 Python Style Rules

### 4.1 Semicolons

Do not terminate your lines with semicolons, and do not use semicolons to put two
statements on the same line.

### 4.2 Line length

Maximum line length is *80 characters*.

Explicit exceptions to the 80 character limit:
-   Long import statements.
-   URLs, pathnames, or long flags in comments.
-   Long string module level constants not containing whitespace that would be
    inconvenient to split across lines such as URLs or pathnames.

You can use explicit backslash line continuation for line continuation.

Make use of Python's
[implicit line joining inside parentheses, brackets and braces](http://docs.python.org/reference/lexical_analysis.html#implicit-line-joining).
If necessary, you can add an extra pair of parentheses around an expression.

```python
Yes: foo_bar(self, width, height, color = 'black', design = None,
            x = 'foo', emphasis = None, highlight = 0)

     if (width == 0 and height == 0 and
         color == 'red' and emphasis == 'strong'):

     a = '1' + '2' + '3' + \
         '4' + '5'
```
Within comments, put long URLs on their own line if necessary.

```python
Yes:  # See details at
      # http://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
```

```python
No:  # See details at
     # http://www.example.com/us/developer/documentation/api/content/\
     # v2.0/csv_file_name_extension_full_specification.html
```

Authors are encouraged to manually break the line up per the notes above when it is sensible.

### 4.3 Parentheses

**Use** parentheses sparingly.

However, do **USE** parentheses heavily for mathematical equations to
explicitly show order of operations.

It is fine, though not required, to use parentheses around tuples. Do not use
them in return statements or conditional statements unless using parentheses for
implied line continuation or to indicate a tuple.

```python
Yes: if foo:
         bar()
     while x:
         x = bar()
     if x and y:
         bar()
     if not x:
         bar()
     # For a 1 item tuple the ()s are more visually obvious than the comma.
     onesie = (foo,)
     return foo
     return spam, beans
     return (spam, beans)
     for (x, y) in dict.items(): ...
```

```python
No:  if (x):
         bar()
     if not(x):
         bar()
     return (foo)
```

### 4.4 Indentation

Indent your code blocks with *4 spaces*.

Never use tabs. Implied line continuation should align wrapped elements
vertically (see [line length examples](#4.2-Line-length)), or use a hanging
4-space indent. Closing (round, square or curly) brackets can be placed at the
end of the expression, or on separate lines, but then should be indented the
same as the line with the corresponding opening bracket.

```python
Yes:   # Aligned with opening delimiter.
       foo = long_function_name(var_one, var_two,
                                var_three, var_four)
       meal = (spam,
               beans)

       # Aligned with opening delimiter in a dictionary.
       foo = {
           'long_dictionary_key': value1 +
                                  value2,
           ...
       }

       # 4-space hanging indent; nothing on first line.
       foo = long_function_name(
           var_one, var_two, var_three,
           var_four)
       meal = (
           spam,
           beans)

       # 4-space hanging indent; nothing on first line,
       # closing parenthesis on a new line.
       foo = long_function_name(
           var_one, var_two, var_three,
           var_four
       )
       meal = (
           spam,
           beans,
       )

       # 4-space hanging indent in a dictionary.
       foo = {
           'long_dictionary_key':
               long_dictionary_value,
           ...
       }
```

```python
No:    # Stuff on first line forbidden.
       foo = long_function_name(var_one, var_two,
           var_three, var_four)
       meal = (spam,
           beans)

       # 2-space hanging indent forbidden.
       foo = long_function_name(
         var_one, var_two, var_three,
         var_four)

       # No hanging indent in a dictionary.
       foo = {
           'long_dictionary_key':
           long_dictionary_value,
           ...
       }
```
#### 4.4.1 Trailing commas in sequences of items?

Trailing commas in sequences of items are recommended only when the closing
container token `]`, `)`, or `}` does not appear on the same line as the final
element. The presence of a trailing comma is also used as a hint to our Python
code auto-formatter [YAPF](https://pypi.org/project/yapf/) to direct it to auto-format the container
of items to one item per line when the `,` after the final element is present.

```python
Yes:   golomb3 = [0, 1, 3]
Yes:   golomb4 = [
           0,
           1,
           4,
           6,
       ]
```

```python
No:    golomb4 = [
           0,
           1,
           4,
           6
       ]
```

### 4.6 Whitespace

Follow standard typographic rules for the use of spaces around punctuation.

No whitespace inside parentheses, brackets or braces.

```python
Yes: spam(ham[1], {'eggs': 2}, [])
```

```python
No:  spam( ham[ 1 ], { 'eggs': 2 }, [ ] )
```

No whitespace before a comma, semicolon, or colon. Do use whitespace after a
comma, semicolon, or colon, except at the end of the line.

```python
Yes: if x == 4:
         print(x, y)
     x, y = y, x
```

```python
No:  if x == 4 :
         print(x , y)
     x , y = y , x
```

No whitespace before the open paren/bracket that starts an argument list,
indexing or slicing.

```python
Yes: spam(1)
```

```python
No:  spam (1)
```

```python
Yes: dict['key'] = list[index]
```

```python
No:  dict ['key'] = list [index]
```

No trailing whitespace.

Surround binary operators with a single space on either side for assignment
(`=`), comparisons (`==, <, >, !=, <>, <=, >=, in, not in, is, is not`), and
Booleans (`and, or, not`). Use your better judgment for the insertion of spaces
around arithmetic operators (`+`, `-`, `*`, `/`, `//`, `%`, `**`, `@`).

```python
Yes: x == 1
```

```python
No:  x<1
```

Never use spaces around `=` when passing keyword arguments or defining a default
parameter value, with one exception:
[when a type annotation is present](#typing-default-values), *do* use spaces
around the `=` for the default parameter value.

```python
Yes: def complex(real, imag=0.0): return Magic(r=real, i=imag)
Yes: def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
```

```python
No:  def complex(real, imag = 0.0): return Magic(r = real, i = imag)
No:  def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
```

Don't use spaces to vertically align tokens on consecutive lines, since it
becomes a maintenance burden (applies to `:`, `#`, `=`, etc.):

```python
Yes:
  foo = 1000
  long_name = 2

  dictionary = {
      'foo': 1,
      'long_name': 2,
  }
```

```python
No:
  foo       = 1000
  long_name = 2

  dictionary = {
      'foo'      : 1,
      'long_name': 2,
  }
```

### 4.7 Shebang Line

At the top of your program always include a shebang line. It is usually:
`#!/usr/bin/env python`

This line is used by the kernel to find the Python interpreter, but is ignored by Python when importing modules.

### 4.8 Comments and Docstrings

Be sure to use the right style for module, function, method docstrings and
inline comments.

#### 4.8.1 Docstrings

Python uses *docstrings* to document code. A docstring is a string that is the first statement in a package, module, class or function. These strings can be extracted automatically through the `__doc__` member of the object and are used by `pydoc`. Always use the three double-quote `"""` format for docstrings (per [PEP 257](https://www.google.com/url?sa=D&q=http://www.python.org/dev/peps/pep-0257/)).

#### 4.8.2 Functions

Certain aspects of a function should be documented in special sections, listed below. Each section begins with a heading line, which ends with a colon. All sections other than the heading should maintain a hanging indent of two or four spaces (be consistent within a file). **Always** have an extra empty line of comment between the comment line and the function.

<a id="doc-function-args"></a>
[*Args:*](#doc-function-args)
:   List each parameter by name. A description should follow the name, and be separated by a colon followed by either a space or newline. If the
description is too long to fit on a single 80-character line, use a hanging
indent of 2 or 4 spaces more than the parameter name (be consistent with the rest of the docstrings in the file).

<a id="doc-function-returns"></a>
[*Returns:* (or *Yields:* for generators)](#doc-function-returns)
:   Describe the type and semantics of the return value. If the function only
    returns None, this section is not required.

```python
Yes:

# function: this_is_a_function
#
# argument:
#   argument1: description of argument 1
#   argument2: description of argument 2
#
# return: description of the return time
#
# short description of the function
#
def this_is_a_function(argument1 , argument2)

    # code

    # exit gracefully
    #
    return True
#
# end of function

# function: this_is_a_function
#
# argument:
#   this_is_a_very_long_argument_name: a long description of this
#                                      very long argument name
#   argument2: description of argument 2
#
# return: description of the return time
#
# short description of the function
#
def this_is_a_function(this_is_a_very_long_argument_name,
                       argument2)
    # code

    # exit gracefully
    #
    return True
#
# end of function
```

<a id="class-docs"></a>
#### 4.8.4 Classes and Methods

Classes and Methods should be very similar to Functions.

```
Differences between a Function and a Method:

Note: This may vary between people and companies but in this NEDC,
      this is our distinction.

FUNCTION: A standalone function that **does NOT exist** within a class
METHOD  : A function that **exist** within a class.
```

```python
Yes:

# class: SampleClass
#
# a short description of the class
#
class SampleClass:

    # method: SampleClass::constructor
    #
    # arguments:
    #  argument1: a short description of argument1
    #
    # return: the return type
    #
    def __init__(self, argument1 = False):
        self.argument1 = argument1
        self.eggs = 0
    #
    # end of method

    # method: SampleClass::public_method
    #
    # arguments:
    #  argument: a short description of argument
    #
    # return: the return type
    #
    # a short description of the method
    #
    def public_method(self, argument):

        # exit gracefully
        #
        return True
    #
    # end of method
#
# end of class
```

#### 4.8.5 Punctuation, Spelling, and Grammar

Pay attention to punctuation, spelling, and grammar; it is easier to read
well-written comments than badly written ones.

Comments should be as readable as narrative text, with proper capitalization and
punctuation. In many cases, complete sentences are more readable than sentence
fragments. Shorter comments, such as comments at the end of a line of code, can
sometimes be less formal, but you should be consistent with your style.

Although it can be frustrating to have a code reviewer point out that you are
using a comma when you should be using a semicolon, it is very important that
source code maintain a high level of clarity and readability. Proper
punctuation, spelling, and grammar help with that goal.


#### 4.8.6 Endings

You may have noticed throughout the commenting sections that there were comments at the ending of the method, function and the class.

```python
#
# exit gracefully

#
# end of function

#
# end of method

#
# end of class
```

Always include them when you are writing your utility or class as it is part of the group's style and also makes it easier to navigate through the code with a text editor (Ex: Emac) that doesn't have features like many modern IDE (Ex: Vscode, Pycharm).

### 4.9 Strings

Use an
[f-string](https://docs.python.org/3/reference/lexical_analysis.html#f-strings),
the `%` operator, or the `format` method for formatting strings, even when the
parameters are all strings. Use your best judgment to decide between string
formatting options. A single join with `+` is okay but do not format with `+`.

```python
Yes: x = f'name: {name}; score: {n}'
     x = '%s, %s!' % (imperative, expletive)
     x = '{}, {}'.format(first, second)
     x = a + b
```

```python
No: x = first + ', ' + second
    x = 'name: ' + name + '; score: ' + str(n)
```

Avoid using the `+` and `+=` operators to accumulate a string within a loop. In some conditions, accumulating a string with addition can lead to quadratic rather than linear running time. Although common accumulations of this sort may be optimized on CPython, that is an implementation detail. The conditions under which an optimization applies are not easy to predict and may change. Instead, add each substring to a list and `''.join` the list after the loop terminates, or write each substring to an `io.StringIO` buffer. These techniques consistently have amortized-linear run time complexity.

```python
Yes: items = ["start"]
     for last_name, first_name in employee_list:
         items.append('%s, %s' % (last_name, first_name))
     items.append("end")
     employee_table = ''.join(items)
```

```python
No: employee_table = 'start'
    for last_name, first_name in employee_list:
        employee_table += '%s, %s' % (last_name, first_name)
    employee_table += 'end'
```

Be consistent with your choice of string quote character within a file. Pick `'`
or `"` and stick with it. It is okay to use the other quote character on a
string to avoid the need to backslash-escape quote characters within the string.

```python
Yes:
  Python('Why are you hiding your eyes?')
  Gollum("I'm scared of lint errors.")
  Narrator('"Good!" thought a happy Python reviewer.')
```

```python
No:
  Python("Why are you hiding your eyes?")
  Gollum('The lint. It burns. It burns us.')
  Gollum("Always the great lint. Watching. Watching.")
```

Prefer `"""` for multi-line strings rather than `'''`. Projects may choose to
use `'''` for all non-docstring multi-line strings if and only if they also use
`'` for regular strings. Docstrings must use `"""` regardless.

Multi-line strings do not flow with the indentation of the rest of the program.

```python
  No:
  long_string = """This is pretty ugly.
Don't do this.
"""
```

```python
  Yes:
  long_string = """This is fine if your use case can accept
      extraneous leading spaces."""
```

```python
  Yes:
  long_string = ("And this is fine if you cannot accept\n" +
                 "extraneous leading spaces.")
```

```python
  Yes:
  long_string = ("And this too is fine if you cannot accept\n"
                 "extraneous leading spaces.")
```

```python
  Yes:
  import textwrap

  long_string = textwrap.dedent("""\
      This is also fine, because textwrap.dedent()
      will collapse common leading spaces in each line.""")
```

#### 4.9.1 Error Messages

Use the error message [template](####error_message_template) from above to print your error message then exit out of your program.

### 4.10 Files, Sockets, and similar Stateful Resources

Explicitly close files and sockets when done with them. This rule naturally
extends to closeable resources that internally use sockets, such as database connections, and also other resources that need to be closed down in a similar fashion.

Leaving files, sockets or other such stateful objects open unnecessarily has
many downsides:

-   They may consume limited system resources, such as file descriptors. Code
    that deals with many such objects may exhaust those resources unnecessarily
    if they're not returned to the system promptly after use.
-   Holding files open may prevent other actions such as moving or deleting
    them, or unmounting a filesystem.
-   Files and sockets that are shared throughout a program may inadvertently be
    read from or written to after logically being closed. If they are actually
    closed, attempts to read or write from them will raise exceptions, making
    the problem known sooner.


Relying on finalizers to do automatic cleanup that has observable side effects
has been rediscovered over and over again to lead to major problems, across many
decades and multiple languages.


The preferred way to manage files and similar resources is using the
[`with` statement](http://docs.python.org/reference/compound_stmts.html#the-with-statement):

```python
with open("hello.txt") as hello_file:
    for line in hello_file:
        print(line)
```

### 4.11 Statements

Generally only one statement per line.

However, you may put the result of a test on the same line as the test only if
the entire statement fits on one line. In particular, you can never do so with
`try`/`except` since the `try` and `except` can't both fit on the same line, and
you can only do so with an `if` if there is no `else`.

```python
Yes:

  if foo: bar(foo)
```

```python
No:

  if foo: bar(foo)
  else:   baz(foo)

  try:               bar(foo)
  except ValueError: baz(foo)

  try:
      bar(foo)
  except ValueError: baz(foo)
```

### 4.12 Naming

`module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`,
`function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`,
`function_parameter_name`, `local_var_name`, `query_proper_noun_for_thing`,
`send_acronym_via_https`.

Function names, variable names, and filenames should be descriptive; avoid
abbreviation. In particular, do not use abbreviations that are ambiguous or
unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word.

Always use a `.py` filename extension. Never use dashes.

#### 4.12.1 Names to Avoid

-   single character names, except for specifically allowed cases:

    -   counters or iterators (e.g. `i`, `j`, `k`, `v`, et al.)
    -   `e` as an exception identifier in `try/except` statements.
    -   `f` as a file handle in `with` statements

    Please be mindful not to abuse single-character naming. Generally speaking,
    descriptiveness should be proportional to the name's scope of visibility.
    For example, `i` might be a fine name for 5-line code block but within
    multiple nested scopes, it is likely too vague.

-   dashes (`-`) in any package/module name

-   `__double_leading_and_trailing_underscore__` names (reserved by Python)

-   offensive terms

-   names that needlessly include the type of the variable (for example:
    `id_to_name_dict`)

#### 4.12.2 Mathematical Notation

For mathematically heavy code, short variable names that would otherwise violate the style guide are preferred when they match established notation in a reference paper or algorithm. When doing so, reference the source of all naming conventions in a comment or docstring or, if the source is not accessible, clearly document the naming conventions. Prefer PEP8-compliant descriptive_names for public APIs, which are much more likely to be encountered out of context.

### 4.13 Main

If a file is meant to be used as an executable, its main functionality should be in a `main()` function, and your code should always check `if __name__ == '__main__'` before executing your main program, so that it is not executed when the module is imported.

Use:
```python
def main(argv):
    ...

# begin gracefully
#
if __name__ == '__main__':
    main(sys.argv[0:])
#
# end of file
```

### 4.14 Function length

Prefer small and focused functions.

We recognize that long functions are sometimes appropriate, so no hard limit is
placed on function length. If a function exceeds about 40 lines, think about
whether it can be broken up without harming the structure of the program.

Even if your long function works perfectly now, someone modifying it in a few
months may add new behavior. This could result in bugs that are hard to find.
Keeping your functions short and simple makes it easier for other people to read
and modify your code.

You could find long and complicated functions when working with
some
code. Do not be intimidated by modifying existing code: if working with such a
function proves to be difficult, you find that errors are hard to debug, or you
want to use a piece of it in several different contexts, consider breaking up
the function into smaller and more manageable pieces.

### 4.15 Type Annotations

#### 4.15.1 Default Values

As per [PEP-008](https://www.python.org/dev/peps/pep-0008/#other-recommendations), use spaces around the `=` *only* for arguments that have both a type annotation and a default value.

```python
Yes:
def func(a = 0):
  ...
```

```python
No:
def func(a=0):
  ...
```

## 5 Parting Words

*BE CONSISTENT*.

If you're editing code, take a few minutes to look at the code around you and determine its style. If they use spaces around all their arithmetic operators, you should too. If their comments have little boxes of hash marks around them, make your comments have little boxes of hash marks around them too.

The point of having style guidelines is to have a common vocabulary of coding so people can concentrate on what you're saying rather than on how you're saying it. We present global style rules here so people know the vocabulary, but local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Avoid this.