# pool 是 go的线程池.

## 使用方法如下:

```go
package main

import (
	"github.com/jiangzhengqiao/logger"
	"github.com/jiangzhengqiao/pool"
)

func main() {
	logger.Info("开始执行。")

	for {
		p := pool.New(1000)               // 开启1000个线程
		for i := 0; i < 1000000000; i++ { // 执行这么多个任务
			p.Add(1)
			go test(p)
		}
		p.Wait() // 等待线程结束
	}
}

func test(p *pool.Pool) {
	defer p.Done()
	logger.Info("开始执行线程。")
}


```
