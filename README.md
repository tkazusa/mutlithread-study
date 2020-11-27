# Python でのシングルプロセス＆マルチスレッドにてシステムリソースをうまく使うための勉強

## まずはきちんと計測することを覚える
- real: 実際にかかった時間
- user: カーネルの外の処理でかかった時間
- sys: カーネル内の特定の処理でかかった時間
 sys + user の時間を足し合わせれば、自分のプログラムの実行時間。 real が大きい場合、IO待ちにある可能性が高い
 
 ```Python
 import time

class Timer(object):
    def __init__(self, verbose=False):
        self.verbose = verbose

    def __enter__(self):
        self.start = time.time()
        return self

    def __exit__(self, *args):
        self.end = time.time()
        self.secs = self.end - self.start
        self.msecs = self.secs * 1000  # millisecs
        if self.verbose:
            print 'elapsed time: %f ms' % self.msecs
```


## Threading
[Pythonで学ぶ 基礎からのプログラミング入門 第32回 マルチスレッド処理を理解しよう(前編)](https://news.livedoor.com/article/detail/11028734/)
[マルチスレッドで走るPythonプログラムをプロファイルするには？](https://tech-blog.link-u.co.jp/2019/03/22/profiling-multi-threaded-python/)
