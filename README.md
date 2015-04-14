# gEDA-gschem-sym
This repository contains a collection of symbol definitions for the [gEDA Schematic][1] software.
The definition in this repository has been created along the way where no suitable sym definitions has been found for my own schematics.


### Usage

To use this symbold library in a project, checkout the repository to some place and then edit (or create) the **```gafrc```** file that
should be located in the home folder, ie: **```/home/<user>/.gEDA```**


An add the following

```
(component-library-search "/<full-path-to>/gEDA-gschem-sym/")
```


### pre-commit hook
A trivial pre-commit hook that runs __gsymcheck__ to detect any error in the sym definitions before the actual commit.

```bash
#!/bin/bash
   
# check sym(s) from error
for symfile in $(git diff --name-only HEAD | grep ".sym"); do
   gsymcheck -vv $symfile
   status=$?
   if [ $status -gt 1 ]; then
      echo "Error(s) in $symfile, please correct"
      exit $status
   fi
done
exit 0
```


[1]: http://wiki.geda-project.org/
