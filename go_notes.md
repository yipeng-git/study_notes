# go 里的坑

## sync.Map

-   sync.Map 线程安全，非常棒。但是不支持获取长度。获取长度要遍历一遍自己计数。
-   就算 sync.Map 自身是线程安全的，替换引用的时候也不安全，所以无法整体更新。
-   sync.Map 存的是 interface{}，导致取的时候很难知道存的是什么类型，经常有类型转换错误。

## 普通 map 用 WaitGroup

-   多读少改的时候：读的时候 wg.Wait()，写的时候 wg.Aad(1) 写 wg.Done()。

## for _, entry := range

-   这里看似遍历的时候 entry 都被重新赋值了，但其实没有，如果存 &entry 那存的元素都一样。

