This will generate and search for 5 random strings. (seq 1 5) 
<br>(seq 1 20): 20 random strings will be generated.

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

I decided to use "Brave Browser" but we also can use "Google Chrome".

### Explanation:

- **Loop**: `for i in $(seq 1 5)` runs the loop 20 times.
- **Generate Random Number of Digits**: `DIGITS=$((10 + RANDOM % 10))` generates a random number between 10 and 19.
- **Generate Random String**: `RANDOM_STRING=$(openssl rand -hex $DIGITS)` generates a random hexadecimal string with the specified number of digits.
- **Echo the Random String**: `echo "Generated Random String: $RANDOM_STRING"` prints the generated random string.
- **Open Brave Browser and Search**: `open -a "Brave Browser" "https://www.google.com/search?q=$RANDOM_STRING"` opens Brave and performs a Google search with the random string.
- **Pause**: `sleep 2` pauses the script for 2 seconds before the next iteration.

This script should work as intended on a Unix-based system (like macOS) where the `open` command is available. If you have any more questions or need further adjustments, feel free to ask!

