## Ramdom  lines from file


Get 10 random lines from a 1000 lines file 

```
awk -v n=1000 -v p=10 '
  BEGIN {srand()}
  rand() * n-- < p {p--; print}' < file
```
