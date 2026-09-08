## LeetCode Problem 295. Find Medium from Data Stream
## 問題
[問題](https://leetcode.com/problems/find-median-from-data-stream/)
## 解法
```
class MedianFinder:

    def __init__(self):
        self.low = [] #max heap
        self.high = [] #min heap

    def addNum(self, num: int) -> None:
        heapq.heappush(self.low, -num)
        n = -heapq.heappop(self.low)
        heapq.heappush(self.high, n)
        if len(self.high) > len(self.low):
            n = -heapq.heappop(self.high)
            heapq.heappush(self.low, n)

    def findMedian(self) -> float:
        if len(self.low) > len(self.high):
            return -self.low[0]
        else:
            return (-self.low[0] + self.high[0]) / 2

# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```
