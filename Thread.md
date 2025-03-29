2025-03-26
Tags:# [[Programming]] [[Software]]

Threads allow programs to run multiple tasks at the same time. Example: Downloading a file while you are interacting with the user UI.


```python
import threading

def print_numbers():
    for i in range(5):
        print(i)

# Create and start a thread
thread = threading.Thread(target=print_numbers)
thread.start()

print("Main program continues running...")
```



### Reference

ChatGPT conversation