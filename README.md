# MitM
A GAP package for annotating functions with their expected output filters.

##What it can do
This package is a library that can be used to automatically determine the
output types of functions containing calls to the 'Objectify'-function. it
currently returns output in about 50% of the cases in the library.

Additionally there is a prototype-implementation for annotating constructors
to created objects. This is however quite rudimentary and one should rather
use the version available on the 'PrintConstructors'-branch on the 'gap'-fork
of LiftnLearn.

###How it works
The findObjectify-files are responsible for finding all Objectify-calls in
a given set of files/functions. It returns an object that collects relevant
information per set of declaration and implementation files.

Based on this object the produceDeclaration files then produces a declaration-
file that is wrapping the respective functions and passes the detected output-
filters in the arguments of the declaration. These are currently not used.

##What it can't do
It can't determine the output type of Objectify-calls whose results
depend on values that are only determined on runtime.

It currently also cannot handle if there are multiple Objectify-calls
within one and the same function, i.e. when they are occuring within
conditional statements.

In any of those cases it will return an IsObject-filter for the function.
There is currently no distinction between recognizing IsObject as the
actual result filter of a function and returning IsObject due to a lack
of better information.

There is also no useful output for global functions installed using
InstallGlobalFunctions (it is always the
empty list printed).

##Bugs
No bugs are currently known.

##How to use
At first the package should be loaded into a running GAP-session.

    LoadPackage("MitM");

One can then pass the names of a .gi and respective .gd file to
the declareOperationsCaller-function as implemented in lib/produceDeclaration.gd
and an output-path for the resulting header-file.

For example:
    declareOperationsCaller("json_output/grp.gd.json", "json_output/grp.gi.json", "declarationsForGroups.gd");

The function however expects that the GAP-files have already been precompiled
to the JSON-format using the JSON-compiler.
