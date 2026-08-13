2025-03-26
Tags:# [[Programming]] [[Software]] [[Python]]

A function that wraps another function. Commonly used to enhance/modify a function without changing the function itself.

example:

```python
def decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@decorator
def say_hello():
    print("Hello!")

say_hello()
```

Output:
```pgsql
Before function call  
Hello!  
After function call  
```

Real life use case:
- Logging 
- Authentication - check user's auth details before running function
- Caching - Store results of lengthy functions
- Timing Execution
- Retry Mechanism 
### Reference

ChatGPT Conversation