# Coroutines

https://ru.stackoverflow.com/questions/496002/%D0%A1%D0%BE%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D1%8B-%D0%BA%D0%BE%D1%80%D1%83%D1%82%D0%B8%D0%BD%D1%8B-coroutine-%D1%87%D1%82%D0%BE-%D1%8D%D1%82%D0%BE

 - instead of callback
```await``` is this:
```cpp
handle = get_coroutine_handle();
async_write(buffer, [=]{ resume(handle); });
yield;
```
```cpp
// Использование коллбеков              |  // Использование сопрограмм
                                        |  
Socket src, dst;                        |  void copy(Socket src, Socket dst) {
byte buffer[1024];                      |    byte buffer[1024];
void copy() {                           |    for (;;) {
  async_read(src, buffer, on_read);     |      int n = await 
}                                       |      if (n <= 0) 
void on_read(int n) {                   |      await async_write(dst, buffer, n);
  if (n <= 0) return;                   |    }
  async_write(dst, buffer, n, copy);    |  }
}                                       |
```

- Generator
```cpp
generator<int> fib() {
  int a = 0, b = 1;
  for (;;) {
    yield a;
    a = a + b;
    yield b;
    b = a + b;
  }
}

int main() {
  generator<int> g = fib();
  // печатаем первые 5
  for (int i = 0; i != 5; ++i) {
    g.next();
    print(g.value());
  }
}
```


# Types

https://stackoverflow.com/questions/28977302/how-do-stackless-coroutines-differ-from-stackful-coroutines

- Stackfull (can yield from the nested stackframe - creating is close to a thread)
- Stackless (cannot yield from the nested stackframe - cheaper to call)

---
status: #⚙️ 
tags: 
related: 
