## Using the “rename” command

The rename syntax looks like this:

```bash
rename (option) 's/oldname/newname/' file1.ext file24.ext
```

The letter “s” stands for “substitute,” and it’s the main part of the regular expression. Single quotes around it are obligatory. Available options are:

    -v (verbose: prints the list of renamed files along with their new names)
    -n (“no action:” a test mode or simulation which only shows the files that will be changed without touching them)
    -f (a forced overwrite of the original files)

The rename command also accepts wildcards to rename multiple files of the same type, and it works on file extensions as well. For example, this would change all files with the extension .jpeg to .jpg:

```bash
rename 's/.jpeg/.jpg/' *
```

The wildcard symbol (*) means that all files in the folder will be affected.

**sufix example**

```bash
rename -n 's/.png/_xs.png/' *
```

@reference: [How to Rename Files in Linux](https://www.maketecheasier.com/rename-files-in-linux/)
