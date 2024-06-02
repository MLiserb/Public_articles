This will generate and search for 5 random strings. (seq 1 5) 
<br>(seq 1 20): 20 random strings will be generated

```sc
for i in $(seq 1 5) 
do
    DIGITS=$((10 + RANDOM % 10))
    RANDOM_STRING=$(openssl rand -hex $DIGITS)
    echo "Generated Random String: $RANDOM_STRING"
    open -a "Brave Browser" "https://www.google.com/search?q=$RANDOM_STRING"
    sleep 2
done
```


