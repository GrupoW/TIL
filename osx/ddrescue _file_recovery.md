##How to recover files from a damage disk using ddrescue

copy the following script and give proper permisions:

```bash
#!/bin/bash
echo "copying from $1"

find "$1" -type f -print0 | while read -d $'\0' -r file ; do
    echo Processing ${file#$1}
    target="$2""${file#$1}"
    echo $target
    if (test -f "$target") then
        echo File Exists:  "$target"
    else
        echo copying to "$target"
        targetDir=`dirname "$target"`
        
        if [ ! -d "$targetDir" ]; then
            echo creating directory: $targetDir
            mkdir -p "$targetDir"
        fi

        ddrescue -e0 -r0 -v -n "$file" "$target"
        if ([ $? -ne 0 ]) then
            echo Copy failed, deleting "$target"
            rm -f "$target"
        fi
    fi
done
```

### usage 

```
$ ./copy_files_from "/source/example" /target/example
```
@reference: [force copying a corrupted home directory](http://unix.stackexchange.com/questions/29728/force-copying-a-corrupted-home-directory)