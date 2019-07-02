## Get longest line from file

run the following line:

```
awk 'length > max_length { max_length = length; longest_line = $0 } END { print longest_line }' file
```
