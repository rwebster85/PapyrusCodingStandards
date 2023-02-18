# Papyrus Coding Standards Guide

## Overview

This specification defines a consistent standard for writing scripts in the Papyrus scripting language for The Elder Scrolls V: Skyrim and Fallout 4.

## 1. Script Example

The following is a short example that encompasses most of the rules set out in this document:

```papyrus
scriptname SomeScriptName extends Quest

ObjectReference property SomeObjectRef auto

int property some_int = 20 autoreadonly

bool some_bool = true

ObjectReference function SampleFunction(string asStringParam, Form akFormToUse = none)
    if (akFormToUse)
        if (asStringParam == "some value")
            ObjectReference new_ref = SomeObjectRef.PlaceAtMe(akFormToUse)
            return new_ref
        endif
    endif

    return none
endfunction

int[] function ArrayFunction()
    int[] some_array = new int[10]
    int foo = 1

    while (some_array.length > foo)
        ; do stuff
    endwhile

    return some_array
endfunction

string function YetAnother(Weapon[] akWeaponArray)
    if (akWeaponArray.length == 5)
        return "5"
    else
        return "foo"
    endif
endfunction

state MyState
    ObjectReference function SampleFunction(string asStringParam, Form akFormToUse = none)
        return none
    endfunction
endstate
```

## 2. General

### 2.1 Files

All files should have the script declaration as the first line, and end with a single empty line.

All script names should be in PascalCase, althought scripts can be prefixed with a unique identifier if necessary to improve compatibility. For example, `_RW_ScriptName`.

### 2.2 Lines

There is a recommended limit of 120 characters per line.

Blank lines may be added to improve readability, unless where explicitly forbidden.

Blank lines must have no whitespace. Lines with comments or code must not have trailing whitespace.

### 2.3 Indentation

Code must use an indent of 4 spaces for each indent level, and must not use tabs for indenting.

### 2.4 Keywords and Types

All papyrus [keywords](https://www.creationkit.com/index.php?title=Keyword_Reference), including functions, control statements, and events, must be in lower case. All object types must be in PascalCase.

### 2.5 Property/Variable Naming Convention

Variable names should be meaningful and descriptive, with the exception of variables controlling the iteration of `while` statements, where the variable will often be named `i` or `j`, for example.

Properties and variables for objects should be written in `PascalCase`. For all other types they should be written in `snake_case`. For example:

```papyrus
ObjectReference SomeRef
Spell Property MySpell auto

int some_int
float my_float
```

If it is preferred to use a different casing standard, then that standard must be consistent across all scripts in the project.

## 3. Script Headers

A script header can contain many blocks. Each block must be seperated by a single blank line. Each block MUST be in the order listed below, although blocks that are not relevant may be omitted.

* Script declaration
* Imports
* Properties
* Script variables

## 4. Functions and Events

### 4.1 Function and Event Names

Functions and events must be declared after all script header blocks. When present, any initialising functions or events must be placed before any other functions/events.

Function/event names should be written in PascalCase and should be meaningful.

```papyrus

; bad
string function n()
    return name
endfunction

; good
string function GetName()
    return name
endfunction
```

### 4.2 Function and Event Arguments

Arguments should follow the Bethesda nomenclature for function arguments:

a : Argument :: b : Bool :: f : Float :: i : Int :: s : String :: k : Form/Alias :: u : Unsigned

For example, an integer argument name would being with 'ai'.

Argument lists may be split across multiple lines using a space (or multiple spaces for alignment) followed by a backslash. Where a function declaration has been split across multiple lines, for readability the opening and closing parenthesis should be on their own lines and not indented. For example:

```papyrus
Furniture function ThisIsALongFunctionDeclaration \
(                                                 \
    ObjectReference akObjectRef1,                 \
    ObjectReference akObjectRef2,                 \
    bool abSomeBoolValue = true,                  \
    int aiSomeInt = 10                              \
)
    ; function body
endfunction
```

## 5. Control structures

* There must be one space after the control structure keyword
* The control expression must be inside parenthesis
* There must not be a space after the opening parenthesis
* There must not be a space before the closing parenthesis
* The structure body must be indented once
* The body must be on the next line after the preceeding statement

### 5.1 `if`, `else`, `elseif`

An if structure looks like the following. Note the placement of parentheses and spaces.

```papyrus
if (expression1)
    ; if body
elseif (expression2)
    ; elseif body
else
    ; else body
endif
```

Expressions in parenthesis may be split across multiple lines using a space (or multiple spaces for alignment) followed by a backslash. Where expressions have been split across multiple lines, the comparison operator (`&&` for instance) must be on the proceeding line, and the closing parenthesis should be on its own line and not indented. For example:

```papyrus
if ( \
    expression1 \
    && expression2 \
)
    ; if body
elseif (expression3)
    ; elseif body
endif
```

### 5.2 `while`, `endwhile`

A while statement looks like the following. Note the placement of parentheses and spaces.

```papyrus
int i = 0
while (i < 5)
    ; do stuff
    i += 1
endwhile
```

Expressions in parenthesis may be split across multiple lines using a space (or multiple spaces for alignment) followed by a backslash. Where expressions have been split across multiple lines, the comparison operator (`&&` for instance) must be on the proceeding line, and the closing parenthesis should be on its own line and not indented. For example:

```papyrus
int i = 0
while ( \
    i < 5 \
    && expression1 \
)
    ; do stuff
    i += 1
endwhile
```

## 6. States

State names should be in PascalCase. If a script contains an `auto` state, that state must preceed any other states in that script. An example of a script with states:

```papyrus
scriptname StateExampleScript extends Actor

auto state DefaultStart
    function SomeFunction(float afSomeNumber)
        ; function body
    endfunction
endstate

state AnotherState
    function SomeFunction(float afSomeNumber)
        ; override here
    endfunction
endstate
```
