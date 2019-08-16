---
layout: post
title: Joblib사용시 Lock이 필요할때
date: 2019-08-16
comments: true
external-url: https://stackoverflow.com/questions/35394373/processpoolexecutor-and-lock-in-python
categories: Python
---

> joblib에서 lock걸때 

https://stackoverflow.com/questions/35394373/processpoolexecutor-and-lock-in-python

joblib에서 loky를 backend로 사용하는 경우 concurrent.futures.ProcessPoolExecutor를 사용하는데,
multiprocessing.Lock을 그냥 쓰면 안된다.

아래는 위 stackoverflow에서 가져온 샘플 코드

```python
import multiprocessing
from concurrent.futures import ProcessPoolExecutor

import time

def f(i, lock):
    with lock:
        print(i, 'hello')
        time.sleep(1)
        print(i, 'world')

def main():
    pool = ProcessPoolExecutor()
    m = multiprocessing.Manager()
    lock = m.Lock()
    futures = [pool.submit(f, num, lock) for num in range(3)]
    for future in futures:
        future.result()


if __name__ == '__main__':
    main()
```