##### heapq 库
- 这个模块提供了堆队列算法的实现，也称为优先队列算法。
- 适用于**需要高效地处理最小/最大元素的场景**，例如任务调度、数据流中的滑动窗口等。它提供了一种轻量级的实现方式来处理堆队列，可以在一些特定场景中提供性能优势。
```python 
# heapq : 堆模块，构建最小堆 (如果要构建最大堆，对入堆元素取负即可)
import heapq

# 创建
heapq.heapify(heap) # 构建/调整一个堆

# 操作
heapq.heappop(heap) # 返回最小数
heapq.heappush(heap, item) # 向堆内压入一个元素
heapq.heappushpop(heap, item) # 向堆内压入一个元素后返回最小数
heapq.heapreplace(heap, item) # 删除堆中最小元素并加入一个元素

# 结果
heapq.nlargest(n, iterable, key) # 返回最大的n个数的列表
heapq.nsmallest(n, iterable, key) # 返回最小的n个数的列表

# 其他
heapq.merge(*iterables) # 合并多个有序列表，并返回有序列表的迭代器(即需要手动list())
```
##### 示例
```python
import heapq

def heap_sort(arr):
    heap = arr[:]
    heapq.heapify(heap)  # 将列表转化为堆

    sorted_list = []
    while heap:
        sorted_list.append(heapq.heappop(heap))  # 弹出堆中最小元素

    return sorted_list

if __name__ == "__main__":
    input_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
    sorted_list = heap_sort(input_list)
    print("Original List:", input_list)
    print("Sorted List:", sorted_list)

# 在这个案例中，我们定义了一个 heap_sort 函数，它接受一个列表作为输入，并使用 heapq 模块中的函数将输入列表转化为堆（最小堆）
# 然后，我们循环地从堆中弹出最小元素，直到堆为空，这样就得到了一个按照升序排列的有序列表。

```