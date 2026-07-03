## 1.两数之和

go:

```go
func twoSum(nums []int, target int) []int {
    hashTable := map[int]int{}
    for i,x := range nums{
        if p,ok := hashTable[target - x]; ok {
            return []int{p,i}
        }
        hashTable[x] = i
    }
    return nil
}
```

python:

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable = dict()
        for i,num in enumerate(nums):
            if target - num in hashtable:
                return [hashtable[target - num],i]
            hashtable[nums[i]] = i
        return []
```

## 2.字母异位词分组

go:

```go
func groupAnagrams(strs []string) [][]string {
    mp := map[[26]int][]string{}
    for _,str := range strs{
        cnt := [26]int{}
        for _,b := range str{
            cnt[b - 'a'] ++
        }
        mp[cnt] = append(mp[cnt],str)
    }
    ans := make([][]string,0,len(mp))
    for _,v := range mp{
        ans = append(ans,v)
    }
    return ans
}
```

python:

```py
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        mp = collections.defaultdict(list)

        for str in strs:
            counts = [0] * 26
            for ch in str:
                counts[ord(ch) - ord('a')] += 1
            mp[tuple(counts)].append(str)
        
        return list(mp.values())
```

## 3.最长连续序列

go:

```go
func longestConsecutive(nums []int) int {
    numSet := map[int]bool{}
    for _,num := range nums{
        numSet[num] = true
    }
    longestStreak := 0
    for num := range numSet{
        if !numSet[num - 1]{
            currentStreak := 1
            currentNum := num
            for numSet[currentNum + 1]{
                currentNum ++
                currentStreak ++
            }
            if longestStreak < currentStreak{
                longestStreak = currentStreak
            }
        }
    }
    return longestStreak
}
```

python:

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        longest_streak = 0
        num_set = set(nums)
        for num in num_set :
            if num - 1 not in num_set:
                current_num = num
                current_streak = 1
                while current_num + 1 in num_set:
                    current_num += 1
                    current_streak += 1
                longest_streak = max(longest_streak,current_streak)
        return longest_streak
```

## 4.移动零

go:

```go
func moveZeroes(nums []int)  {
    left,right,n := 0,0,len(nums)
    for right < n{
        if nums[right] != 0{
            nums[left],nums[right] = nums[right],nums[left]
            left ++
        }
        right ++
    }
}
```

python:

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        n = len(nums)
        left = right = 0
        while right < n:
            if nums[right] != 0:
                nums[left],nums[right] = nums[right],nums[left]
                left += 1
            right += 1
```

## 5.盛最多水的容器

go:

```go
func maxArea(height []int) (ans int) {
   l,r := 0,len(height) - 1
   ans = 0
    for l < r{
        area := (r - l) * min(height[l],height[r])
        ans = max(area,ans)
        if (height[l] <= height[r]){
            l ++
        }else{
            r --
        }
    }
    return ans
}
```



python:

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l,r = 0,len(height) - 1
        ans = 0
        while l < r:
            area = min(height[l],height[r]) * (r - l)
            ans = max(ans,area)
            if height[l] <= height[r]:
                l += 1
            else:
                r -= 1
        return ans
```

## 6.三数之和

go:

```go
func threeSum(nums []int) (ans [][]int) {
    slices.Sort(nums)
    n := len(nums)
    for i,x := range nums[:n-2]{
        
        if i > 0 && x == nums[i - 1]{
            continue
        }
        if x + nums[i + 1] + nums[i + 2] > 0{
            break
        }
        if x + nums[n - 1] + nums[n - 2] < 0{
            continue
        }

        l := i + 1
        r := n - 1
        for l < r{
            s := x + nums[l] + nums[r]
            if s > 0{
                r --
            }else if s < 0{
                l ++
            }else{
                ans = append(ans,[]int{x,nums[l],nums[r]})
                for l ++; l < r && nums[l] == nums[l - 1];l ++{

                }
                for r --; l < r && nums[r] == nums[r + 1];r --{

                }
            }
        }
    }
    return ans
}
```

python:

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        ans = []
        nums.sort()
        n = len(nums)
        for i in range(n - 2):
            x = nums[i]
            if i > 0 and x == nums[i - 1]:
                continue
            if x + nums[i + 1] + nums[i + 2] > 0:
                break
            if x + nums[-1] + nums[-2] < 0:
                continue
            l = i + 1
            r = n - 1
            while l < r:
                s = x + nums[l] + nums[r]
                if s > 0:
                    r -= 1
                elif s < 0:
                    l += 1
                else:
                    ans.append([x,nums[l],nums[r]])
                    l += 1
                    while l < r and nums[l] == nums[l - 1]:
                        l += 1
                    r -= 1
                    while l < r and nums[r] == nums[r + 1]:
                        r -= 1
        return ans
```

## 7.接雨水

go:

```go
func trap(height []int) (ans int) {
    ans = 0
    st := []int{}
    for i,h := range height{
        for len(st) > 0 && height[st[len(st) - 1]] <= h{
            bottomH := height[st[len(st) - 1]]
            st = st[:len(st) - 1]
            if len(st) == 0{
                break
            }
            left := st[len(st) - 1]
            dh := min(height[left],h) - bottomH
            ans += dh * (i - left - 1)
        }
        st = append(st,i)
    }
    return ans
}
```

python:

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        st = []
        ans = 0
        for i,h in enumerate(height):
            while st and height[st[-1]] <= h:
                bottom_h = height[st.pop()]
                if not st:
                    break
                left = st[-1]
                dh = min(height[left],h) - bottom_h
                ans += dh * (i - left - 1)
            st.append(i)
        return ans
```

## 8.无重复字符的最长字串

go:

```go
func lengthOfLongestSubstring(s string) (ans int) {
    cnt := [128]int{}
    left := 0
    for right,c := range s{
        cnt[c] ++
        for cnt[c] > 1{
            cnt[s[left]] --
            left ++
        }
        ans = max(ans,right - left + 1)
    }
    return ans
}
```

python:

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        ans = left = 0
        cnt = defaultdict(int)
        for right,c in enumerate(s):
            cnt[c] += 1
            while cnt[c] > 1:
                cnt[s[left]] -= 1
                left += 1
            ans = max(ans,right - left + 1)
        return ans
```

## 9.找到字符串中所有字母异位词

go:

```go
func findAnagrams(s, p string) (ans []int) {
    // 统计 p 的每种字母的出现次数
    cnt := [26]int{}
    for _, c := range p {
        cnt[c-'a']++
    }

    left := 0
    for right, c := range s {
        c -= 'a'
        cnt[c]-- // 右端点字母进入窗口
        for cnt[c] < 0 { // 字母 c 太多了
            cnt[s[left]-'a']++ // 左端点字母离开窗口
            left++
        }
        if right-left+1 == len(p) { // t 和 p 的每种字母的出现次数都相同（证明见上）
            ans = append(ans, left) // t 左端点下标加入答案
        }
    }
    return
}

```

python:

```python
# 请选择 Python3 提交代码，而不是 Python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        cnt = Counter(p)  # 统计 p 的每种字母的出现次数
        ans = []

        left = 0
        for right, c in enumerate(s):
            cnt[c] -= 1  # 右端点字母进入窗口
            while cnt[c] < 0:  # 字母 c 太多了
                cnt[s[left]] += 1  # 左端点字母离开窗口
                left += 1
            if right - left + 1 == len(p):  # t 和 p 的每种字母的出现次数都相同（证明见上）
                ans.append(left)  # t 左端点下标加入答案

        return ans

```

## 10.和为k的子数组

go:

```go
func subarraySum(nums []int, k int) (ans int) {
    cnt := make(map[int]int,len(nums) + 1)
    cnt[0] = 1
    s := 0
    for _,x := range nums{
        s += x
        ans += cnt[s - k]
        cnt[s] ++
    }
    return 
}
```

python:

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        cnt = defaultdict(int)
        cnt[0] = 1  # s[0]=0 单独统计
        ans = s = 0
        for x in nums:
            s += x
            ans += cnt[s - k]
            cnt[s] += 1
        return ans
```

## 11.滑动窗口最大值

go:

```go
func maxSlidingWindow(nums []int, k int) []int {
    ans := make([]int, len(nums)-k+1) // 窗口个数
    q := []int{}

    for i, x := range nums {
        // 1. 右边入
        for len(q) > 0 && nums[q[len(q)-1]] <= x {
            q = q[:len(q)-1] // 维护 q 的单调性
        }
        q = append(q, i) // 注意保存的是下标，这样下面可以判断队首是否离开窗口

        // 2. 左边出
        left := i - k + 1 // 窗口左端点
        if q[0] < left {  // 队首离开窗口
            q = q[1:] // Go 的切片是 O(1) 的
        }

        // 3. 在窗口左端点处记录答案
        if left >= 0 {
            // 由于队首到队尾单调递减，所以窗口最大值就在队首
            ans[left] = nums[q[0]]
        }
    }

    return ans
}

```

python:

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        ans = [0] * (len(nums) - k + 1)  # 窗口个数
        q = deque()  # 双端队列

        for i, x in enumerate(nums):
            # 1. 右边入
            while q and nums[q[-1]] <= x:
                q.pop()  # 维护 q 的单调性
            q.append(i)  # 注意保存的是下标，这样下面可以判断队首是否离开窗口

            # 2. 左边出
            left = i - k + 1  # 窗口左端点
            if q[0] < left:  # 队首离开窗口
                q.popleft()

            # 3. 在窗口左端点处记录答案
            if left >= 0:
                # 由于队首到队尾单调递减，所以窗口最大值就在队首
                ans[left] = nums[q[0]]

        return ans

```

## 12.最小覆盖子串

go:

```go
func isCovered(cntS, cntT []int) bool {
    for i := 'A'; i <= 'Z'; i++ {
        if cntS[i] < cntT[i] {
            return false
        }
    }
    for i := 'a'; i <= 'z'; i++ {
        if cntS[i] < cntT[i] {
            return false
        }
    }
    return true
}

func minWindow(s, t string) string {
    var cntS, cntT [128]int
    for _, c := range t {
        cntT[c]++
    }

    ansLeft, ansRight := -1, len(s)
    left := 0

    for right, c := range s { // 移动子串右端点
        cntS[c]++ // 右端点字母移入子串
        for isCovered(cntS[:], cntT[:]) { // 涵盖
            if right-left < ansRight-ansLeft { // 找到更短的子串
                ansLeft, ansRight = left, right // 记录此时的左右端点
            }
            cntS[s[left]]-- // 左端点字母移出子串
            left++
        }
    }

    if ansLeft < 0 {
        return ""
    }
    return s[ansLeft : ansRight+1]
}
```

python:

```python
# 请选择 Python3 提交代码，而不是 Python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        cnt_s = Counter()  # s 子串字母的出现次数
        cnt_t = Counter(t)  # t 中字母的出现次数

        ans_left, ans_right = -1, len(s)
        left = 0

        for right, c in enumerate(s):  # 移动子串右端点
            cnt_s[c] += 1  # 右端点字母移入子串
            while cnt_s >= cnt_t:  # 涵盖
                if right - left < ans_right - ans_left:  # 找到更短的子串
                    ans_left, ans_right = left, right  # 记录此时的左右端点
                cnt_s[s[left]] -= 1  # 左端点字母移出子串
                left += 1

        return "" if ans_left < 0 else s[ans_left: ans_right + 1]

```

## 13.最大子数组和

go:

```go
func maxSubArray(nums []int) int {
    ans := math.MinInt // 注意答案可以是负数，不能初始化成 0
    f := 0
    for _, x := range nums {
        f = max(f, 0) + x
        ans = max(ans, f)
    }
    return ans
}
```

python:

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        ans = -inf
        f = 0
        for x in nums:
            f = max(f,0) + x
            ans = max(ans,f)
        return ans
```

## 14.合并区间

go:

```go
func merge(intervals [][]int) (ans [][]int) {
    slices.SortFunc(intervals, func(p, q []int) int { return p[0] - q[0] }) // 按照左端点从小到大排序

    for _, p := range intervals {
        m := len(ans)
        if m > 0 && p[0] <= ans[m-1][1] { // 左端点在合并区间内，可以合并
            ans[m-1][1] = max(ans[m-1][1], p[1]) // 更新合并区间的右端点
        } else { // 不相交，无法合并
            ans = append(ans, p) // 新的合并区间
        }
    }
    return
}
```

python:

```##python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda p: p[0])  # 按照左端点从小到大排序

        ans = []
        for p in intervals:
            if ans and p[0] <= ans[-1][1]:  # 左端点在合并区间内，可以合并
                ans[-1][1] = max(ans[-1][1], p[1])  # 更新合并区间的右端点
            else:  # 不相交，无法合并
                ans.append(p)  # 新的合并区间
        return ans
```

## 15.轮转数组

go

```go
func rotate(nums []int, k int) {
    k %= len(nums) // 轮转 k 次等于轮转 k % n 次
    slices.Reverse(nums)
    slices.Reverse(nums[:k])
    slices.Reverse(nums[k:])
}
```

python

```python
# 注：请勿使用切片，会产生额外空间
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        def reverse(i: int, j: int) -> None:
            while i < j:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
                j -= 1

        n = len(nums)
        k %= n  # 轮转 k 次等于轮转 k % n 次
        reverse(0, n - 1)
        reverse(0, k - 1)
        reverse(k, n - 1)
```

## 16.除了自身以外数组的乘积

go

```go
func productExceptSelf(nums []int) []int {
    n := len(nums)
    suf := make([]int,n)
    suf[n - 1] = 1
    for i := n - 2;i >= 0;i --{
        suf[i] = suf[i + 1]*nums[i + 1]
    }
    pre := 1
    for i,x := range nums{
        suf[i] *= pre
        pre *= x
    }
    return suf
}
```

python

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        suf = [1] * n
        for i in range (n - 2,-1,-1):
            suf[i] = suf[i + 1] * nums[i + 1]
        
        pre = 1
        for i,x in enumerate(nums):
            suf[i] *= pre
            pre *= x
        return suf
```

## 17.缺失的第一个正数

go

```go
func firstMissingPositive(nums []int) int {
    n := len(nums)
    for i := range n {
        // 如果当前学生的学号在 [1,n] 中，但（真身）没有坐在正确的座位上
        for 1 <= nums[i] && nums[i] <= n && nums[nums[i]-1] != nums[i] {
            // 那么就交换 nums[i] 和 nums[j]，其中 j 是 i 的学号
            j := nums[i] - 1 // 减一是因为数组下标从 0 开始
            nums[i], nums[j] = nums[j], nums[i]
        }
    }

    // 找第一个学号与座位编号不匹配的学生
    for i := range n {
        if nums[i] != i+1 {
            return i + 1
        }
    }

    // 所有学生都坐在正确的座位上
    return n + 1
}
```

python

```python
class Solution:
    def firstMissingPositive(self, nums: list[int]) -> int:
        n = len(nums)
        for i in range(n):
            # 如果当前学生的学号在 [1,n] 中，但（真身）没有坐在正确的座位上
            while 1 <= nums[i] <= n and nums[nums[i] - 1] != nums[i]:
                # 那么就交换 nums[i] 和 nums[j]，其中 j 是 i 的学号
                j = nums[i] - 1  # 减一是因为数组下标从 0 开始
                nums[i], nums[j] = nums[j], nums[i]

        # 找第一个学号与座位编号不匹配的学生
        for i in range(n):
            if nums[i] != i + 1:
                return i + 1

        # 所有学生都坐在正确的座位上
        return n + 1
```

## 18.矩阵置零

python

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        m, n = len(matrix), len(matrix[0])
        first_row_has_zero = 0 in matrix[0]

        for i in range(1, m):
            for j in range(n):
                if matrix[i][j] == 0:
                    matrix[i][0] = matrix[0][j] = 0

        for i in range(1, m):
            # 倒着遍历，避免提前把 matrix[i][0] 改成 0，误认为这一行要全部变成 0
            for j in range(n - 1, -1, -1):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0

        if first_row_has_zero:
            for j in range(n):
                matrix[0][j] = 0
```

go

```go
func setZeroes(matrix [][]int) {
    m, n := len(matrix), len(matrix[0])
    firstRowHasZero := slices.Contains(matrix[0], 0)

    for i := 1; i < m; i++ {
        for j, x := range matrix[i] {
            if x == 0 {
                matrix[i][0] = 0
                matrix[0][j] = 0
            }
        }
    }

    for i := 1; i < m; i++ {
        // 倒着遍历，避免提前把 matrix[i][0] 改成 0，误认为这一行要全部变成 0
        for j := n - 1; j >= 0; j-- {
            if matrix[i][0] == 0 || matrix[0][j] == 0 {
                matrix[i][j] = 0
            }
        }
    }

    if firstRowHasZero {
        clear(matrix[0])
    }
}
```

## 19.螺旋矩阵

go

```go
var dirs = [4][2]int{{0, 1}, {1, 0}, {0, -1}, {-1, 0}} // 右下左上

func spiralOrder(matrix [][]int) []int {
    m, n := len(matrix), len(matrix[0])
    ans := make([]int, 0, m*n)
    i, j := 0, -1 // 从 (0, -1) 开始
    for di := 0; len(ans) < cap(ans); di = (di + 1) % 4 {
        for range n { // 走 n 步（注意 n 会减少）
            i += dirs[di][0]
            j += dirs[di][1] // 先走一步
            ans = append(ans, matrix[i][j]) // 再加入答案
        }
        m, n = n, m-1 // 减少后面的循环次数
    }
    return ans
}
```

python

```python
DIRS = (0, 1), (1, 0), (0, -1), (-1, 0)  # 右下左上

class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        m, n = len(matrix), len(matrix[0])
        size = m * n
        ans = []
        i, j, di = 0, -1, 0  # 从 (0, -1) 开始
        while len(ans) < size:
            dx, dy = DIRS[di]
            for _ in range(n):  # 走 n 步（注意 n 会减少）
                i += dx
                j += dy  # 先走一步
                ans.append(matrix[i][j])  # 再加入答案
            di = (di + 1) % 4  # 右转 90°
            m, n = n, m - 1  # 减少后面的循环次数（步数）
        return ans
```

## 20.旋转图像

go

```go
func rotate(matrix [][]int) {
    n := len(matrix)
    // 第一步：转置
    for i := range n {
        for j := range i { // 遍历对角线下方元素
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        }
    }

    // 第二步：行翻转
    for _, row := range matrix {
        slices.Reverse(row)
    }
}
```

python

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        n = len(matrix)
        # 第一步：转置
        for i in range(n):
            for j in range(i):  # 遍历对角线下方元素
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # 第二步：行翻转
        for row in matrix:
            row.reverse()
```

## 21.搜索二维矩阵

go

```
func searchMatrix(matrix [][]int, target int) bool {
    m, n := len(matrix), len(matrix[0])
    i, j := 0, n-1 // 从右上角开始
    for i < m && j >= 0 { // 还有剩余元素
        if matrix[i][j] == target {
            return true // 找到 target
        }
        if matrix[i][j] < target {
            i++ // 这一行剩余元素全部小于 target，排除
        } else {
            j-- // 这一列剩余元素全部大于 target，排除
        }
    }
    return false
}
```

python

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])
        i, j = 0, n - 1  # 从右上角开始
        while i < m and j >= 0:  # 还有剩余元素
            if matrix[i][j] == target:
                return True  # 找到 target
            if matrix[i][j] < target:
                i += 1  # 这一行剩余元素全部小于 target，排除
            else:
                j -= 1  # 这一列剩余元素全部大于 target，排除
        return False
```

## 22.相交链表

go

```
func getIntersectionNode(headA, headB *ListNode) *ListNode {
    p, q := headA, headB
    for p != q {
        if p != nil {
            p = p.Next
        } else {
            p = headB
        }
        if q != nil {
            q = q.Next
        } else {
            q = headA
        }
    }
    return p
}
```

python

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        p, q = headA, headB
        while p is not q:
            p = p.next if p else headB
            q = q.next if q else headA
        return p
```

## 23.反转链表

go

```go
func reverseList(head *ListNode) *ListNode {
    var pre, cur *ListNode = nil, head
    for cur != nil {
        nxt := cur.Next
        cur.Next = pre // 把 cur 插在 pre 链表的前面（头插法）
        pre = cur
        cur = nxt
    }
    return pre
}
```

python

```
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        pre = None
        cur = head
        while cur:
            nxt = cur.next
            cur.next = pre  # 把 cur 插在 pre 链表的前面（头插法）
            pre = cur
            cur = nxt
        return pre
```

## 24.回文链表

go

```
// 876. 链表的中间结点
func middleNode(head *ListNode) *ListNode {
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    return slow
}

// 206. 反转链表
func reverseList(head *ListNode) *ListNode {
    var pre, cur *ListNode = nil, head
    for cur != nil {
        nxt := cur.Next
        cur.Next = pre
        pre = cur
        cur = nxt
    }
    return pre
}

func isPalindrome(head *ListNode) bool {
    mid := middleNode(head)
    head2 := reverseList(mid)
    for head2 != nil {
        if head.Val != head2.Val { // 不是回文链表
            return false
        }
        head = head.Next
        head2 = head2.Next
    }
    return true
}
```

python

```
class Solution:
    # 876. 链表的中间结点
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow

    # 206. 反转链表
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        pre, cur = None, head
        while cur:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        return pre

    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        mid = self.middleNode(head)
        head2 = self.reverseList(mid)
        while head2:
            if head.val != head2.val:  # 不是回文链表
                return False
            head = head.next
            head2 = head2.next
        return True
```



## 25.环形链表

go

```
func hasCycle(head *ListNode) bool {
    slow, fast := head, head // 乌龟和兔子同时从起点出发
    for fast != nil && fast.Next != nil {
        slow = slow.Next // 乌龟走一步
        fast = fast.Next.Next // 兔子走两步
        if fast == slow { // 兔子追上乌龟（套圈），说明有环
            return true
        }
    }
    return false // 访问到了链表末尾，无环
}
```

python

```
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = fast = head  # 乌龟和兔子同时从起点出发
        while fast and fast.next:
            slow = slow.next  # 乌龟走一步
            fast = fast.next.next  # 兔子走两步
            if fast is slow:  # 兔子追上乌龟（套圈），说明有环
                return True
        return False  # 访问到了链表末尾，无环
```

## 26.环形链表2

go

```
func detectCycle(head *ListNode) *ListNode {
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if fast == slow { // 相遇
            for slow != head { // 再走 a 步
                slow = slow.Next
                head = head.Next
            }
            return slow
        }
    }
    return nil
}
```

python

```
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if fast is slow:  # 相遇
                while slow is not head:  # 再走 a 步
                    slow = slow.next
                    head = head.next
                return slow
        return None
```

## 27.合并两个有序列表

go

```
func mergeTwoLists(list1, list2 *ListNode) *ListNode {
    dummy := ListNode{} // 用哨兵节点简化代码逻辑
    cur := &dummy // cur 指向新链表的末尾
    for list1 != nil && list2 != nil {
        if list1.Val < list2.Val {
            cur.Next = list1 // 把 list1 加到新链表中
            list1 = list1.Next
        } else { // 注：相等的情况加哪个节点都是可以的
            cur.Next = list2 // 把 list2 加到新链表中
            list2 = list2.Next
        }
        cur = cur.Next
    }
    // 拼接剩余链表
    if list1 != nil {
        cur.Next = list1
    } else {
        cur.Next = list2
    }
    return dummy.Next
}
```

python

```
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        cur = dummy = ListNode()  # 用哨兵节点简化代码逻辑
        while list1 and list2:
            if list1.val < list2.val:
                cur.next = list1  # 把 list1 加到新链表中
                list1 = list1.next
            else:  # 注：相等的情况加哪个节点都是可以的
                cur.next = list2  # 把 list2 加到新链表中
                list2 = list2.next
            cur = cur.next
        cur.next = list1 or list2  # 拼接剩余链表
        return dummy.next
```



## 28.两数相加

go

```
// l1 和 l2 为当前遍历的节点，carry 为进位
func addTwo(l1 *ListNode, l2 *ListNode, carry int) *ListNode {
    if l1 == nil && l2 == nil && carry == 0 { // 递归边界
        return nil
    }

    s := carry
    if l1 != nil {
        s += l1.Val // 累加进位与节点值
        l1 = l1.Next
    }
    if l2 != nil {
        s += l2.Val
        l2 = l2.Next
    }

    // s 除以 10 的余数为当前节点值，商为进位
    return &ListNode{s % 10, addTwo(l1, l2, s/10)}
}

func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    return addTwo(l1, l2, 0)
}
```

python

```
class Solution:
    # l1 和 l2 为当前遍历的节点，carry 为进位
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode], carry=0) -> Optional[ListNode]:
        if l1 is None and l2 is None and carry == 0:  # 递归边界
            return None

        s = carry
        if l1:
            s += l1.val  # 累加进位与节点值
            l1 = l1.next
        if l2:
            s += l2.val
            l2 = l2.next

        # s 除以 10 的余数为当前节点值，商为进位
        return ListNode(s % 10, self.addTwoNumbers(l1, l2, s // 10))
```

## 29.删除链表的倒数第N个结点

go

```
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    // 由于可能会删除链表头部，用哨兵节点简化代码
    dummy := &ListNode{Next: head}
    left, right := dummy, dummy
    for ; n > 0; n-- {
        right = right.Next // 右指针先向右走 n 步
    }
    for right.Next != nil {
        left = left.Next
        right = right.Next // 左右指针一起走
    }
    left.Next = left.Next.Next // 左指针的下一个节点就是倒数第 n 个节点
    return dummy.Next
}
```

python

```
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        # 由于可能会删除链表头部，用哨兵节点简化代码
        left = right = dummy = ListNode(next=head)
        for _ in range(n):
            right = right.next  # 右指针先向右走 n 步
        while right.next:
            left = left.next
            right = right.next  # 左右指针一起走
        left.next = left.next.next  # 左指针的下一个节点就是倒数第 n 个节点
        return dummy.next
```

## 30.两两交换链表中的结点

go

```
func swapPairs(head *ListNode) *ListNode {
    dummy := &ListNode{Next: head} // 用哨兵节点简化代码逻辑
    node0 := dummy
    node1 := head
    for node1 != nil && node1.Next != nil { // 至少有两个节点
        node2 := node1.Next
        node3 := node2.Next

        node0.Next = node2 // 0 -> 2
        node2.Next = node1 // 2 -> 1
        node1.Next = node3 // 1 -> 3

        node0 = node1 // 下一轮交换，0 是 1
        node1 = node3 // 下一轮交换，1 是 3
    }
    return dummy.Next // 返回新链表的头节点
}
```

python

```
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node0 = dummy = ListNode(next=head)  # 用哨兵节点简化代码逻辑
        node1 = head
        while node1 and node1.next:  # 至少有两个节点
            node2 = node1.next
            node3 = node2.next

            node0.next = node2  # 0 -> 2
            node2.next = node1  # 2 -> 1
            node1.next = node3  # 1 -> 3

            node0 = node1  # 下一轮交换，0 是 1
            node1 = node3  # 下一轮交换，1 是 3
        return dummy.next  # 返回新链表的头节点
```

## 31.K个一组翻转链表

go

```
func reverseKGroup(head *ListNode, k int) *ListNode {
    // 统计节点个数
    n := 0
    for cur := head; cur != nil; cur = cur.Next {
        n++
    }

    dummy := &ListNode{Next: head}
    p0 := dummy
    var pre *ListNode
    cur := p0.Next

    // k 个一组处理
    for ; n >= k; n -= k {
        for i := 0; i < k; i++ {
            nxt := cur.Next
            cur.Next = pre // 每次循环只修改一个 Next，方便大家理解
            pre = cur
            cur = nxt
        }

        // 见视频
        nxt := p0.Next
        p0.Next.Next = cur
        p0.Next = pre
        p0 = nxt
    }
    return dummy.Next
}
```

python

```
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        # 统计节点个数
        n = 0
        cur = head
        while cur:
            n += 1
            cur = cur.next

        p0 = dummy = ListNode(next=head)
        pre = None
        cur = head

        # k 个一组处理
        while n >= k:
            n -= k
            for _ in range(k):  # 同 92 题
                nxt = cur.next
                cur.next = pre  # 每次循环只修改一个 next，方便大家理解
                pre = cur
                cur = nxt

            # 见视频
            nxt = p0.next
            nxt.next = cur
            p0.next = pre
            p0 = nxt
        return dummy.next
```

## 32.随机链表的复制

go

```
func copyRandomList(head *Node) *Node {
    // 复制每个节点，把新节点直接插到原节点的后面
    for cur := head; cur != nil; cur = cur.Next.Next {
        cur.Next = &Node{Val: cur.Val, Next: cur.Next}
    }

    // 遍历交错链表中的原链表节点
    for cur := head; cur != nil; cur = cur.Next.Next {
        if cur.Random != nil {
            // 要复制的 random 是 cur.Random 的下一个节点
            cur.Next.Random = cur.Random.Next
        }
    }

    // 把交错链表分离成两个链表
    dummy := Node{}
    tail := &dummy
    for cur := head; cur != nil; cur, tail = cur.Next, tail.Next {
        clone := cur.Next     // 新节点
        tail.Next = clone     // 把新节点插在 tail 的后面，构建新的链表
        cur.Next = clone.Next // 恢复原节点的 next
    }

    return dummy.Next
}
```

python

```
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        # 复制每个节点，把新节点直接插到原节点的后面
        cur = head
        while cur:
            cur.next = Node(cur.val, cur.next)
            cur = cur.next.next

        # 遍历交错链表中的原链表节点
        cur = head
        while cur:
            if cur.random:
                # 要复制的 random 是 cur.random 的下一个节点
                cur.next.random = cur.random.next
            cur = cur.next.next

        # 删除交错链表中的原链表节点，剩下的节点即为新链表
        cur = dummy = Node(0, head)
        while cur.next:
            # 删除原链表的节点，即当前节点的下一个节点
            # 如果要恢复原链表，见另一份代码【Python3 写法二】
            cur.next = cur.next.next
            cur = cur.next

        return dummy.next
```

## 33.排序链表

go

```
// 876. 链表的中间结点（快慢指针）
func middleNode(head *ListNode) *ListNode {
    pre, slow, fast := head, head, head
    for fast != nil && fast.Next != nil {
        pre = slow // 记录 slow 的前一个节点
        slow = slow.Next
        fast = fast.Next.Next
    }
    pre.Next = nil  // 断开 slow 的前一个节点和 slow 的连接
    return slow
}

// 21. 合并两个有序链表（双指针）
func mergeTwoLists(list1, list2 *ListNode) *ListNode {
    dummy := ListNode{} // 用哨兵节点简化代码逻辑
    cur := &dummy // cur 指向新链表的末尾
    for list1 != nil && list2 != nil {
        if list1.Val < list2.Val {
            cur.Next = list1 // 把 list1 加到新链表中
            list1 = list1.Next
        } else { // 注：相等的情况加哪个节点都是可以的
            cur.Next = list2 // 把 list2 加到新链表中
            list2 = list2.Next
        }
        cur = cur.Next
    }
    // 拼接剩余链表
    if list1 != nil {
        cur.Next = list1
    } else {
        cur.Next = list2
    }
    return dummy.Next
}

func sortList(head *ListNode) *ListNode {
    // 如果链表为空或者只有一个节点，无需排序
    if head == nil || head.Next == nil {
        return head
    }
    // 找到中间节点 head2，并断开 head2 与其前一个节点的连接
    // 比如 head=[4,2,1,3]，那么 middleNode 调用结束后 head=[4,2] head2=[1,3]
    head2 := middleNode(head)
    // 分治
    head = sortList(head)
    head2 = sortList(head2)
    // 合并
    return mergeTwoLists(head, head2)
}
```

python

```
class Solution:
    # 876. 链表的中间结点（快慢指针）
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head
        while fast and fast.next:
            pre = slow  # 记录 slow 的前一个节点
            slow = slow.next
            fast = fast.next.next
        pre.next = None  # 断开 slow 的前一个节点和 slow 的连接
        return slow

    # 21. 合并两个有序链表（双指针）
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        cur = dummy = ListNode()  # 用哨兵节点简化代码逻辑
        while list1 and list2:
            if list1.val < list2.val:
                cur.next = list1  # 把 list1 加到新链表中
                list1 = list1.next
            else:  # 注：相等的情况加哪个节点都是可以的
                cur.next = list2  # 把 list2 加到新链表中
                list2 = list2.next
            cur = cur.next
        cur.next = list1 if list1 else list2  # 拼接剩余链表
        return dummy.next

    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 如果链表为空或者只有一个节点，无需排序
        if head is None or head.next is None:
            return head
        # 找到中间节点 head2，并断开 head2 与其前一个节点的连接
        # 比如 head=[4,2,1,3]，那么 middleNode 调用结束后 head=[4,2] head2=[1,3]
        head2 = self.middleNode(head)
        # 分治
        head = self.sortList(head)
        head2 = self.sortList(head2)
        # 合并
        return self.mergeTwoLists(head, head2)
```

## 34.合并K个升序链表

go

```
// 21. 合并两个有序链表
func mergeTwoLists(list1, list2 *ListNode) *ListNode {
    dummy := &ListNode{} // 用哨兵节点简化代码逻辑
    cur := dummy // cur 指向新链表的末尾
    for list1 != nil && list2 != nil {
        if list1.Val < list2.Val {
            cur.Next = list1 // 把 list1 加到新链表中
            list1 = list1.Next
        } else { // 注：相等的情况加哪个节点都是可以的
            cur.Next = list2 // 把 list2 加到新链表中
            list2 = list2.Next
        }
        cur = cur.Next
    }
    // 拼接剩余链表
    if list1 != nil {
        cur.Next = list1
    } else {
        cur.Next = list2
    }
    return dummy.Next
}

func mergeKLists(lists []*ListNode) *ListNode {
    m := len(lists)
    if m == 0 {
        return nil
    }
    for step := 1; step < m; step *= 2 {
        for i := 0; i < m-step; i += step * 2 {
            lists[i] = mergeTwoLists(lists[i], lists[i+step])
        }
    }
    return lists[0]
}
```

python

```
class Solution:
    # 21. 合并两个有序链表
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        cur = dummy = ListNode()  # 用哨兵节点简化代码逻辑
        while list1 and list2:
            if list1.val < list2.val:
                cur.next = list1  # 把 list1 加到新链表中
                list1 = list1.next
            else:  # 注：相等的情况加哪个节点都是可以的
                cur.next = list2  # 把 list2 加到新链表中
                list2 = list2.next
            cur = cur.next
        cur.next = list1 if list1 else list2  # 拼接剩余链表
        return dummy.next

    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        m = len(lists)
        if m == 0:
            return None
        step = 1
        while step < m:
            for i in range(0, m - step, step * 2):
                lists[i] = self.mergeTwoLists(lists[i], lists[i + step])
            step *= 2
        return lists[0]
```

## 35.LRU缓存

go

```
type Node struct {
    key, value int
    prev, next *Node
}

type LRUCache struct {
    capacity  int
    dummy     *Node // 哨兵节点
    keyToNode map[int]*Node
}

func Constructor(capacity int) LRUCache {
    dummy := &Node{}
    dummy.prev = dummy
    dummy.next = dummy
    return LRUCache{
        capacity:  capacity,
        dummy:     dummy,
        keyToNode: map[int]*Node{},
    }
}

// 删除一个节点（抽出一本书）
func (c *LRUCache) remove(x *Node) {
    x.prev.next = x.next
    x.next.prev = x.prev
}

// 在链表头添加一个节点（把一本书放到最上面）
func (c *LRUCache) pushFront(x *Node) {
    x.prev = c.dummy
    x.next = c.dummy.next
    x.prev.next = x
    x.next.prev = x
}

// 获取 key 对应的节点，同时把该节点移到链表头部
func (c *LRUCache) getNode(key int) *Node {
    node := c.keyToNode[key]
    if node == nil { // 没有这本书
        return nil
    }
    c.remove(node)    // 把这本书抽出来
    c.pushFront(node) // 放到最上面
    return node
}

func (c *LRUCache) Get(key int) int {
    node := c.getNode(key) // getNode 会把对应节点移到链表头部
    if node == nil {
        return -1
    }
    return node.value
}

func (c *LRUCache) Put(key, value int) {
    node := c.getNode(key) // getNode 会把对应节点移到链表头部
    if node != nil {       // 有这本书
        node.value = value // 更新 value
        return
    }
    node = &Node{key: key, value: value} // 新书
    c.keyToNode[key] = node
    c.pushFront(node) // 放到最上面
    if len(c.keyToNode) > c.capacity { // 书太多了
        backNode := c.dummy.prev
        delete(c.keyToNode, backNode.key)
        c.remove(backNode) // 去掉最后一本书
    }
}
```

python

```
class Node:
    # 提高访问属性的速度，并节省内存
    __slots__ = 'prev', 'next', 'key', 'value'

    def __init__(self, key=0, value=0):
        self.key = key
        self.value = value

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.dummy = Node()  # 哨兵节点
        self.dummy.prev = self.dummy
        self.dummy.next = self.dummy
        self.key_to_node = {}

    # 获取 key 对应的节点，同时把该节点移到链表头部
    def get_node(self, key: int) -> Optional[Node]:
        if key not in self.key_to_node:  # 没有这本书
            return None
        node = self.key_to_node[key]  # 有这本书
        self.remove(node)  # 把这本书抽出来
        self.push_front(node)  # 放到最上面
        return node

    def get(self, key: int) -> int:
        node = self.get_node(key)  # get_node 会把对应节点移到链表头部
        return node.value if node else -1

    def put(self, key: int, value: int) -> None:
        node = self.get_node(key)  # get_node 会把对应节点移到链表头部
        if node:  # 有这本书
            node.value = value  # 更新 value
            return
        self.key_to_node[key] = node = Node(key, value)  # 新书
        self.push_front(node)  # 放到最上面
        if len(self.key_to_node) > self.capacity:  # 书太多了
            back_node = self.dummy.prev
            del self.key_to_node[back_node.key]
            self.remove(back_node)  # 去掉最后一本书

    # 删除一个节点（抽出一本书）
    def remove(self, x: Node) -> None:
        x.prev.next = x.next
        x.next.prev = x.prev

    # 在链表头添加一个节点（把一本书放到最上面）
    def push_front(self, x: Node) -> None:
        x.prev = self.dummy
        x.next = self.dummy.next
        x.prev.next = x
        x.next.prev = x
```

## 36.二叉树的中序遍历

go

```
func inorderTraversal(root *TreeNode) (ans []int) {
    var dfs func(*TreeNode)
    dfs = func(node *TreeNode) {
        if node == nil {
            return
        }
        dfs(node.Left)              // 左
        ans = append(ans, node.Val) // 根（这行代码移到前面就是前序，移到后面就是后序）
        dfs(node.Right)             // 右
    }
    dfs(root)
    return
}
```

python

```
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        def dfs(node: Optional[TreeNode]) -> None:
            if node is None:
                return
            dfs(node.left)       # 左
            ans.append(node.val) # 根（这行代码移到前面就是前序，移到后面就是后序）
            dfs(node.right)      # 右

        ans = []
        dfs(root)
        return ans
```

## 37.二叉树的最大深度

go

```
func maxDepth(root *TreeNode) int {
    if root == nil{
        return 0
    }
    l_depth := maxDepth(root.Left)
    r_depth := maxDepth(root.Right)
    return max(l_depth,r_depth) + 1
}
```

python

```
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0
        l_depth = self.maxDepth(root.left)
        r_depth = self.maxDepth(root.right)
        return max(l_depth,r_depth) + 1
```

## 38.翻转二叉树

go

```
func invertTree(root *TreeNode) *TreeNode {
    if root == nil{
        return nil
    }
    left := invertTree(root.Left)
    right := invertTree(root.Right)
    root.Left = right
    root.Right = left
    return root
}
```

python

```
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root is None:
            return None
        left = self.invertTree(root.left)
        right = self.invertTree(root.right)
        root.left = right
        root.right = left
        return root
```

## 39.对称二叉树

go

```
func isSameTree(q *TreeNode,p *TreeNode) bool{
    if q == nil || p == nil{
        return p == q
    }
    return q.Val == p.Val && isSameTree(q.Left,p.Right) && isSameTree(q.Right,p.Left)
}
func isSymmetric(root *TreeNode) bool {
    return isSameTree(root.Left,root.Right)
}
```

python

```
class Solution:
    def isSameTree(self,q:Optional[TreeNode],p:Optional[TreeNode]) -> bool:
        if q is None or p is None:
            return q is p
        return q.val == p.val and self.isSameTree(q.left,p.right) and self.isSameTree(p.left,q.right)
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        return self.isSameTree(root.left,root.right)
```

## 40.二叉树的直径

go

```
func diameterOfBinaryTree(root *TreeNode) (ans int) {
    var dfs func(*TreeNode) int
    dfs = func(node *TreeNode) int {
        if node == nil {
            return 0
        }
        lLen := dfs(node.Left)
        rLen := dfs(node.Right)
        ans = max(ans, lLen+rLen) // 两条链拼成路径
        return max(lLen, rLen) + 1
    }

    dfs(root)
    return
}
```

python

```
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        ans = 0

        def dfs(node: Optional[TreeNode]) -> int:
            if node is None:
                return 0
            l_len = dfs(node.left)
            r_len = dfs(node.right)
            nonlocal ans
            ans = max(ans, l_len + r_len)  # 两条链拼成路径
            return max(l_len, r_len) + 1

        dfs(root)
        return ans
```

## 41.二叉树的层序遍历

go

```
func levelOrder(root *TreeNode) (ans [][]int) {
    if root == nil {
        return
    }
    q := []*TreeNode{root}
    for len(q) > 0 {
        n := len(q)
        vals := make([]int, n) // 预分配空间
        for i := range vals {
            node := q[0]
            q = q[1:]
            vals[i] = node.Val
            if node.Left != nil {
                q = append(q, node.Left)
            }
            if node.Right != nil {
                q = append(q, node.Right)
            }
        }
        ans = append(ans, vals)
    }
    return
}
```

python

```
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if root is None:
            return []
        ans = []
        q = deque([root])
        while q:
            vals = []
            for _ in range(len(q)):
                node = q.popleft()
                vals.append(node.val)
                if node.left:  q.append(node.left)
                if node.right: q.append(node.right)
            ans.append(vals)
        return ans
```

## 42.将有序数组转化为二叉搜索树

go

```
func sortedArrayToBST(nums []int) *TreeNode {
    if len(nums) == 0{
        return nil
    }
    m := len(nums) / 2
    left := sortedArrayToBST(nums[:m])
    right := sortedArrayToBST(nums[m + 1:])
    return &TreeNode{
        Val: nums[m],
        Left: left,
        Right: right,
    }
}
```

python

```
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        if len(nums) == 0:
            return None
        m = len(nums) // 2
        left = self.sortedArrayToBST(nums[:m])
        right = self.sortedArrayToBST(nums[m + 1:])
        return TreeNode(nums[m],left,right)
```

## 43.验证二叉搜索树

go

```
func dfs(root *TreeNode,left int,right int) bool {
    if root == nil{
        return true
    }
    x := root.Val
    return left < x && x < right && dfs(root.Left,left,x) && dfs(root.Right,x,right)
}
func isValidBST(root *TreeNode) bool {
    return dfs(root,math.MinInt,math.MaxInt)
}
```

python

```
class Solution:
    def isValidBST(self, root: Optional[TreeNode],left = -inf,right = inf) -> bool:
        if root is None:
            return True
        x = root.val
        return left < x < right and self.isValidBST(root.left,left,x) and self.isValidBST(root.right,x,right)
```

## 44.二叉搜索树中第K小的元素

go

```
func kthSmallest(root *TreeNode, k int) (ans int) {
    var dfs func(node *TreeNode)
    dfs = func(node *TreeNode){
        if node == nil || k < 0{
            return
        }
        dfs(node.Left)
        k -= 1
        if k == 0{
            ans = node.Val
        }
        dfs(node.Right)
    }
    dfs(root)
    return 
}
```

python

```
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        ans = 0
        def dfs(node: Optional[TreeNode]) -> None:
            nonlocal ans,k
            if node is None or k < 0:
                return 
            dfs(node.left)
            k -= 1
            if k == 0:
                ans = node.val
            dfs(node.right)
        dfs(root)
        return ans
```

## 45.二叉树的右视图

go

```
func rightSideView(root *TreeNode) (ans []int) {
    if root == nil{
        return 
    }
    cur := []*TreeNode{root}
    for len(cur) > 0{
        ans = append(ans,cur[len(cur) - 1].Val)
        nxt := []*TreeNode{}
        for _,node := range cur{
            if node.Left != nil{
                nxt = append(nxt,node.Left)
            }
            if node.Right != nil{
                nxt = append(nxt,node.Right)
            }
        }
        cur = nxt
    }
    return 
}
```

python

```
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if root is None:
            return []
        cur = [root]
        ans = []
        while cur:
            ans.append(cur[len(cur) - 1].val)
            nxt = []
            for i in range(len(cur)):
                if cur[i].left is not None:
                    nxt.append(cur[i].left)
                if cur[i].right is not None:
                    nxt.append(cur[i].right)
            cur = nxt
        return ans
```

## 46.二叉树展开为链表

go

```
func flatten(root *TreeNode) {
    var head *TreeNode

    var dfs func(*TreeNode)
    dfs = func(node *TreeNode) {
        if node == nil {
            return
        }
        // 右 - 左 - 根
        dfs(node.Right)
        dfs(node.Left)
        node.Left = nil
        node.Right = head // 头插法，相当于链表的 node.Next = head
        head = node       // 现在链表头节点是 node
    }

    dfs(root)
}
```

python

```
class Solution:
    head = None

    def flatten(self, root: Optional[TreeNode]) -> None:
        if root is None:
            return
        # 右 - 左 - 根
        self.flatten(root.right)
        self.flatten(root.left)
        root.left = None
        root.right = self.head  # 头插法，相当于链表的 root.next = head
        self.head = root  # 现在链表头节点是 root
```

## 47.从前序与中序遍历序列构造二叉树

go

```
func buildTree(preorder []int, inorder []int) *TreeNode {
    if len(preorder) == 0{
        return nil
    }
    leftSize := slices.Index(inorder,preorder[0])
    left := buildTree(preorder[1:1 + leftSize],inorder[:leftSize])
    right := buildTree(preorder[1 + leftSize:],inorder[1 + leftSize:])
    return &TreeNode{preorder[0],left,right}
}
```

python

```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder:
            return None
        left_size = inorder.index(preorder[0])
        left = self.buildTree(preorder[1:1 + left_size],inorder[:left_size])
        right = self.buildTree(preorder[1 + left_size:],inorder[left_size + 1:])
        return TreeNode(preorder[0],left,right)
```

## 48.路径总和3

go

```
func pathSum(root *TreeNode, targetSum int) (ans int) {
    // key：从根到 node 的节点值之和
    // value：节点值之和的出现次数
    // 注意在递归过程中，哈希表只保存根到 node 的路径的前缀的节点值之和
    cnt := map[int]int{0: 1}

    // s 表示从根到 node 的父节点的节点值之和（node 的节点值尚未计入）
    var dfs func(*TreeNode, int)
    dfs = func(node *TreeNode, s int) {
        if node == nil {
            return
        }

        s += node.Val
        // 把 node 当作路径的终点，统计有多少个起点
        ans += cnt[s-targetSum]

        cnt[s]++
        dfs(node.Left, s)
        dfs(node.Right, s)
        cnt[s]-- // 恢复现场（撤销 cnt[s]++）
    }

    dfs(root, 0)
    return ans
}
```

python

```
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        # key：从根到 node 的节点值之和
        # value：节点值之和的出现次数
        # 注意在递归过程中，哈希表只保存根到 node 的路径的前缀的节点值之和
        cnt = defaultdict(int)  
        cnt[0] = 1
        ans = 0

        # s 表示从根到 node 的父节点的节点值之和（node 的节点值尚未计入）
        def dfs(node: Optional[TreeNode], s: int) -> None:
            if node is None:
                return

            nonlocal ans
            s += node.val
            # 把 node 当作路径的终点，统计有多少个起点
            ans += cnt[s - targetSum]

            cnt[s] += 1
            dfs(node.left, s)
            dfs(node.right, s)
            cnt[s] -= 1  # 恢复现场（撤销 cnt[s] += 1）

        dfs(root, 0)
        return ans
```

## 49.二叉树的最近公共祖先

go

```
func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
    if root == nil || root == p || root == q {
        return root // 找到 p 或 q 就不往下递归了，原因见上面答疑
    }
    left := lowestCommonAncestor(root.Left, p, q)
    right := lowestCommonAncestor(root.Right, p, q)
    if left != nil && right != nil { // 左右都找到
        return root // 当前节点是最近公共祖先
    }
    // 如果只有左子树找到，就返回左子树的返回值
    // 如果只有右子树找到，就返回右子树的返回值
    // 如果左右子树都没有找到，就返回 nil（注意此时 right = nil）
    if left != nil {
        return left
    }
    return right
}
```

python

```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root in (None, p, q):  # 找到 p 或 q 就不往下递归了，原因见上面答疑
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right:  # 左右都找到
            return root  # 当前节点是最近公共祖先
        # 如果只有左子树找到，就返回左子树的返回值
        # 如果只有右子树找到，就返回右子树的返回值
        # 如果左右子树都没有找到，就返回 None（注意此时 right = None）
        return left or right
```

## 50.二叉树的最大路径和

go

```
func maxPathSum(root *TreeNode) int {
    ans := math.MinInt
    var dfs func(*TreeNode) int
    dfs = func(node *TreeNode) int {
        if node == nil {
            return 0 // 没有节点，和为 0
        }
        lVal := dfs(node.Left)  // 左子树最大链和
        rVal := dfs(node.Right) // 右子树最大链和
        ans = max(ans, lVal+rVal+node.Val) // 两条链拼成路径
        return max(max(lVal, rVal)+node.Val, 0) // 当前子树最大链和（注意这里和 0 取最大值了）
    }
    dfs(root)
    return ans
}
```

python

```
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        ans = -inf
        def dfs(node: Optional[TreeNode]) -> int:
            if node is None:
                return 0  # 没有节点，和为 0
            l_val = dfs(node.left)  # 左子树最大链和
            r_val = dfs(node.right)  # 右子树最大链和
            nonlocal ans
            ans = max(ans, l_val + r_val + node.val)  # 两条链拼成路径
            return max(max(l_val, r_val) + node.val, 0)  # 当前子树最大链和（注意这里和 0 取最大值了）
        dfs(root)
        return ans
```

## 51.岛屿数量

go

```
func numIslands(grid [][]byte) (ans int) {
    m, n := len(grid), len(grid[0])
    var dfs func(int, int)
    dfs = func(i, j int) {
        // 出界，或者不是 '1'，就不再往下递归
        if i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != '1' {
            return
        }
        grid[i][j] = '2' // 插旗！避免来回横跳无限递归
        dfs(i, j-1)      // 往左走
        dfs(i, j+1)      // 往右走
        dfs(i-1, j)      // 往上走
        dfs(i+1, j)      // 往下走
    }

    for i, row := range grid {
        for j, c := range row {
            if c == '1' { // 找到了一个新的岛
                dfs(i, j) // 把这个岛插满旗子，这样后面遍历到的 '1' 一定是新的岛
                ans++
            }
        }
    }
    return
}
```

python

```
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m,n = len(grid),len(grid[0])
        ans = 0
        def dfs(i: int,j: int) -> None:
            if i < 0 or i >= m or j < 0 or j >= n or grid[i][j] is not '1':
                return
            grid[i][j] = '2'
            dfs(i,j + 1)
            dfs(i,j - 1)
            dfs(i + 1,j)
            dfs(i - 1,j)
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    dfs(i,j)
                    ans += 1
        return ans 
```

## 52.腐烂的橘子

go

```
type pair struct{ x, y int }
var directions = []pair{{-1, 0}, {1, 0}, {0, -1}, {0, 1}} // 四方向

func orangesRotting(grid [][]int) int {
    m, n := len(grid), len(grid[0])
    fresh := 0
    q := []pair{}
    for i, row := range grid {
        for j, x := range row {
            if x == 1 {
                fresh++ // 统计新鲜橘子个数
            } else if x == 2 {
                q = append(q, pair{i, j}) // 一开始就腐烂的橘子
            }
        }
    }

    ans := 0
    for fresh > 0 && len(q) > 0 {
        ans++ // 经过一分钟
        tmp := q
        q = []pair{}
        for _, p := range tmp { // 已经腐烂的橘子
            for _, d := range directions { // 四方向
                i, j := p.x+d.x, p.y+d.y
                if 0 <= i && i < m && 0 <= j && j < n && grid[i][j] == 1 { // 新鲜橘子
                    fresh--
                    grid[i][j] = 2 // 变成腐烂橘子
                    q = append(q, pair{i, j})
                }
            }
        }
    }

    if fresh > 0 {
        return -1
    }
    return ans
}
```

python

```
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        fresh = 0
        q = []
        for i, row in enumerate(grid):
            for j, x in enumerate(row):
                if x == 1:
                    fresh += 1  # 统计新鲜橘子个数
                elif x == 2:
                    q.append((i, j))  # 一开始就腐烂的橘子

        ans = 0
        while q and fresh:
            ans += 1  # 经过一分钟
            tmp = q
            q = []
            for x, y in tmp:  # 已经腐烂的橘子
                for i, j in (x - 1, y), (x + 1, y), (x, y - 1), (x, y + 1):  # 四方向
                    if 0 <= i < m and 0 <= j < n and grid[i][j] == 1:  # 新鲜橘子
                        fresh -= 1
                        grid[i][j] = 2  # 变成腐烂橘子
                        q.append((i, j))

        return -1 if fresh else ans
```

## 53.课程表

go

```
func canFinish(numCourses int, prerequisites [][]int) bool {
    g := make([][]int, numCourses)
    for _, p := range prerequisites {
        g[p[1]] = append(g[p[1]], p[0])
    }

    colors := make([]int, numCourses)
    // 返回 true 表示找到了环
    var dfs func(int) bool
    dfs = func(x int) bool {
        colors[x] = 1 // x 正在访问中
        for _, y := range g[x] {
            // 情况一：colors[y] == 1，表示发生循环依赖，找到了环
            // 情况二：colors[y] == 0，没有访问过 y，继续递归 y 获取信息
            // 情况三：colors[y] == 2，重复访问 y 只会重蹈覆辙，和之前一样无法找到环，跳过
            if colors[y] == 1 || colors[y] == 0 && dfs(y) {
                return true // 找到了环
            }
        }
        colors[x] = 2 // x 完全访问完毕，从 x 出发无法找到环
        return false // 没有找到环
    }

    for i, c := range colors {
        if c == 0 && dfs(i) {
            return false // 有环
        }
    }
    return true // 没有环
}
```

python

```
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        g = [[] for _ in range(numCourses)]
        for a, b in prerequisites:
            g[b].append(a)

        colors = [0] * numCourses
        # 返回 True 表示找到了环
        def dfs(x: int) -> bool:
            colors[x] = 1  # x 正在访问中
            for y in g[x]:
                # 情况一：colors[y] == 1，表示发生循环依赖，找到了环
                # 情况二：colors[y] == 0，没有访问过 y，继续递归 y 获取信息
                # 情况三：colors[y] == 2，重复访问 y 只会重蹈覆辙，和之前一样无法找到环，跳过
                if colors[y] == 1 or colors[y] == 0 and dfs(y):
                    return True  # 找到了环
            colors[x] = 2  # x 完全访问完毕，从 x 出发无法找到环
            return False  # 没有找到环

        for i, c in enumerate(colors):
            if c == 0 and dfs(i):
                return False  # 有环
        return True  # 没有环
```

## 54.实现Trim

go

```
type Node struct {
    son [26]*Node
    end bool
}

type Trie struct {
    root *Node
}

func Constructor() Trie {
    return Trie{&Node{}}
}

func (t Trie) Insert(word string) {
    cur := t.root
    for _, c := range word {
        c -= 'a'
        if cur.son[c] == nil { // 无路可走？
            cur.son[c] = &Node{} // 那就造路！
        }
        cur = cur.son[c]
    }
    cur.end = true
}

func (t Trie) find(word string) int {
    cur := t.root
    for _, c := range word {
        c -= 'a'
        if cur.son[c] == nil { // 道不同，不相为谋
            return 0
        }
        cur = cur.son[c]
    }
    // 走过同样的路（2=完全匹配，1=前缀匹配）
    if cur.end {
        return 2
    }
    return 1
}

func (t Trie) Search(word string) bool {
    return t.find(word) == 2
}

func (t Trie) StartsWith(prefix string) bool {
    return t.find(prefix) != 0
}
```

python

```
class Node:
    __slots__ = 'son', 'end'

    def __init__(self):
        self.son = [None] * 26
        self.end = False

class Trie:
    def __init__(self):
        self.root = Node()

    def insert(self, word: str) -> None:
        cur = self.root
        for c in word:
            c = ord(c) - ord('a')
            if cur.son[c] is None:  # 无路可走？
                cur.son[c] = Node()  # 那就造路！
            cur = cur.son[c]
        cur.end = True

    def find(self, word: str) -> int:
        cur = self.root
        for c in word:
            c = ord(c) - ord('a')
            if cur.son[c] is None:  # 道不同，不相为谋
                return 0
            cur = cur.son[c]
        # 走过同样的路（2=完全匹配，1=前缀匹配）
        return 2 if cur.end else 1

    def search(self, word: str) -> bool:
        return self.find(word) == 2

    def startsWith(self, prefix: str) -> bool:
        return self.find(prefix) != 0
```

## 55.全排列

go

```
func permute(nums []int) (ans [][]int) {
    n := len(nums)
    path := make([]int, n)
    onPath := make([]bool, n)

    // 枚举 path[i] 填 nums 的哪个数
    var dfs func(int)
    dfs = func(i int) {
        if i == n {
            ans = append(ans, append([]int(nil), path...))
            return
        }
        for j, on := range onPath {
            if !on {
                path[i] = nums[j]
                onPath[j] = true
                dfs(i + 1)
                onPath[j] = false
            }
        }
    }

    dfs(0)
    return
}
```

python

```
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        path = [0] * n  # 所有排列的长度都是一样的 n
        on_path = [False] * n
        ans = []

        # 枚举 path[i] 填 nums 的哪个数
        def dfs(i: int) -> None:
            if i == n:
                ans.append(path.copy())  # 也可以写 path[:]
                return
            for j, on in enumerate(on_path):
                if not on:
                    path[i] = nums[j]  # 从没有选的数字中选一个
                    on_path[j] = True  # 已选上
                    dfs(i + 1)
                    on_path[j] = False  # 恢复现场
                    # 注意 path 无需恢复现场，因为排列长度固定，直接覆盖就行

        dfs(0)
        return ans
```



## 56.子集

go

```
func subsets(nums []int) [][]int {
    n := len(nums)
    ans := make([][]int, 0, 1<<n) // 预分配空间
    path := make([]int, 0, n) // 预分配空间

    // 选或不选：讨论 nums[i] 是否加入 path
    var dfs func(int)
    dfs = func(i int) {
        if i == n { // 子集构造完毕
            ans = append(ans, slices.Clone(path)) // 复制 path
            return
        }
        
        // 不选 nums[i]
        dfs(i + 1) // 考虑下一个数 nums[i+1] 选或不选
        
        // 选 nums[i]
        path = append(path, nums[i])
        dfs(i + 1) // 考虑下一个数 nums[i+1] 选或不选
        path = path[:len(path)-1] // 恢复现场，撤销 path = append(path, nums[i])
    }

    dfs(0)
    return ans
}
```

python

```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = []
        path = []

        # 选或不选：讨论 nums[i] 是否加入 path
        def dfs(i: int) -> None:
            if i == n:  # 子集构造完毕
                ans.append(path.copy())  # 复制 path，也可以写 path[:]
                return

            # 不选 nums[i]
            dfs(i + 1)  # 考虑下一个数 nums[i+1] 选或不选

            # 选 nums[i]
            path.append(nums[i])
            dfs(i + 1)  # 考虑下一个数 nums[i+1] 选或不选
            path.pop()  # 恢复现场，撤销 path.append(nums[i])

        dfs(0)
        return ans
```

## 57.电话号码的字母组合

go

```
var mapping = [...]string{"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"}

func letterCombinations(digits string) (ans []string) {
    n := len(digits)
    if n == 0 {
        return
    }

    path := make([]byte, n) // 注意 path 长度一开始就是 n，不是空列表

    var dfs func(int)
    dfs = func(i int) {
        if i == n {
            ans = append(ans, string(path))
            return
        }
        for _, c := range mapping[digits[i]-'0'] {
            path[i] = byte(c) // 直接覆盖
            dfs(i + 1)
        }
    }

    dfs(0)
    return
}
```

python

````
MAPPING = "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"

class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        n = len(digits)
        if n == 0:
            return []
  
        ans = []
        path = [''] * n  # 注意 path 长度一开始就是 n，不是空列表

        def dfs(i: int) -> None:
            if i == n:
                ans.append(''.join(path))
                return
            for c in MAPPING[int(digits[i])]:
                path[i] = c  # 直接覆盖
                dfs(i + 1)

        dfs(0)
        return ans
````

## 58.组合总和

go

```
func combinationSum(candidates []int, target int) (ans [][]int) {
    slices.Sort(candidates)
    path := []int{}
    var dfs func(int, int)
    dfs = func(i, left int) {
        if left == 0 {
            // 找到一个合法组合
            ans = append(ans, slices.Clone(path))
            return
        }

        if i == len(candidates) || left < candidates[i] {
            return
        }

        // 不选
        dfs(i+1, left)

        // 选
        path = append(path, candidates[i])
        dfs(i, left-candidates[i])
        path = path[:len(path)-1] // 恢复现场
    }
    dfs(0, target)
    return ans
}
```

python

```
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        ans = []
        path = []

        def dfs(i: int, left: int) -> None:
            if left == 0:
                # 找到一个合法组合
                ans.append(path.copy())
                return

            if i == len(candidates) or left < candidates[i]:
                return

            # 不选
            dfs(i + 1, left)

            # 选
            path.append(candidates[i])
            dfs(i, left - candidates[i])
            path.pop()  # 恢复现场

        dfs(0, target)
        return ans
```

## 59.括号生成

go

```
func generateParenthesis(n int) (ans []string) {
    path := make([]byte, n*2) // 所有括号长度都是一样的 2n

    // 目前填了 left 个左括号，right 个右括号
    var dfs func(int, int)
    dfs = func(left, right int) {
        if right == n { // 填完 2n 个括号
            ans = append(ans, string(path)) // 加入答案
            return
        }
        if left < n { // 可以填左括号
            path[left+right] = '(' // 直接覆盖
            dfs(left+1, right)
        }
        if right < left { // 可以填右括号
            path[left+right] = ')' // 直接覆盖
            dfs(left, right+1)
        }
    }

    dfs(0, 0) // 一开始没有填括号
    return
}
```

python

```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        ans = []
        path = [''] * (n * 2)  # 所有括号长度都是 2n

        # 目前填了 left 个左括号，right 个右括号
        def dfs(left: int, right: int) -> None:
            if right == n:  # 填完 2n 个括号
                ans.append(''.join(path))
                return
            if left < n:  # 可以填左括号
                path[left + right] = '('  # 直接覆盖
                dfs(left + 1, right)
            if right < left:  # 可以填右括号
                path[left + right] = ')'  # 直接覆盖
                dfs(left, right + 1)

        dfs(0, 0)  # 一开始没有填括号
        return ans
```

## 60.单词搜索

go

```
var dirs = []struct{ x, y int }{{0, -1}, {0, 1}, {-1, 0}, {1, 0}}

func exist(board [][]byte, word string) bool {
    cnt := map[byte]int{}
    for _, row := range board {
        for _, c := range row {
            cnt[c]++
        }
    }

    // 优化一
    w := []byte(word)
    wordCnt := map[byte]int{}
    for _, c := range w {
        wordCnt[c]++
        if wordCnt[c] > cnt[c] {
            return false
        }
    }

    // 优化二
    if cnt[w[len(w)-1]] < cnt[w[0]] {
        slices.Reverse(w)
    }

    m, n := len(board), len(board[0])
    var dfs func(int, int, int) bool
    dfs = func(i, j, k int) bool {
        if board[i][j] != w[k] { // 匹配失败
            return false
        }
        if k == len(w)-1 { // 匹配成功
            return true
        }
        board[i][j] = 0 // 标记访问过
        for _, d := range dirs {
            x, y := i+d.x, j+d.y // 相邻格子
            if 0 <= x && x < m && 0 <= y && y < n && dfs(x, y, k+1) {
                return true // 搜到了！
            }
        }
        board[i][j] = w[k] // 恢复现场
        return false // 没搜到
    }
    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            if dfs(i, j, 0) {
                return true // 搜到了！
            }
        }
    }
    return false // 没搜到
}
```

python

```
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        cnt = Counter(c for row in board for c in row)
        if not cnt >= Counter(word):  # 优化一
            return False
        if cnt[word[-1]] < cnt[word[0]]:  # 优化二
            word = word[::-1]

        m, n = len(board), len(board[0])
        def dfs(i: int, j: int, k: int) -> bool:
            if board[i][j] != word[k]:  # 匹配失败
                return False
            if k == len(word) - 1:  # 匹配成功！
                return True
            board[i][j] = ''  # 标记访问过
            for x, y in (i, j - 1), (i, j + 1), (i - 1, j), (i + 1, j):  # 相邻格子
                if 0 <= x < m and 0 <= y < n and dfs(x, y, k + 1):
                    return True  # 搜到了！
            board[i][j] = word[k]  # 恢复现场
            return False  # 没搜到
        return any(dfs(i, j, 0) for i in range(m) for j in range(n))
```

## 61.分割回文串

go

```
func isPalindrome(s string) bool {
    n := len(s)
    for i := range n / 2 {
        if s[i] != s[n-1-i] {
            return false
        }
    }
    return true
}

func partition(s string) (ans [][]string) {
    n := len(s)
    path := []string{}

    // 现在 s 未被分割的部分为 [start, n-1]
    // 当前位于下标 i，讨论是否在 i 和 i+1 之间切一刀
    var dfs func(int, int)
    dfs = func(i, start int) {
        if i == n { // s 分割完毕
            ans = append(ans, slices.Clone(path))
            return
        }

        // 不分割
        if i < n-1 { // i=n-1 时必须分割（这是最后一段），i<n-1 时才可以不分割
            dfs(i+1, start)
        }

        // 分割，那么得到子串 [start, i]
        substr := s[start : i+1]
        if isPalindrome(substr) { // 判断子串 substr 是不是回文串
            path = append(path, substr)
            // 现在 s 未被分割的部分为 [i+1, n-1]
            dfs(i+1, i+1)
            path = path[:len(path)-1] // 恢复现场
        }
    }

    dfs(0, 0)
    return
}
```

python

```
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        n = len(s)
        ans = []
        path = []

        # 现在 s 未被分割的部分为 [start, n-1]
        # 当前位于下标 i，讨论是否在 i 和 i+1 之间切一刀
        def dfs(i: int, start: int) -> None:
            if i == n:  # s 分割完毕
                ans.append(path.copy())  # 复制 path
                return

            # 不分割
            if i < n - 1:  # i=n-1 时必须分割（这是最后一段），i<n-1 时才可以不分割
                dfs(i + 1, start)

            # 分割，那么得到子串 [start, i]
            t = s[start: i + 1]
            if t == t[::-1]:  # 判断 t 是不是回文串
                path.append(t)
                # 现在 s 未被分割的部分为 [i+1, n-1]
                dfs(i + 1, i + 1)
                path.pop()  # 恢复现场

        dfs(0, 0)
        return ans
```

## 62.N皇后

go

```
func solveNQueens(n int) (ans [][]string) {
    queens := make([]int, n) // 皇后放在 (r,queens[r])
    col := make([]bool, n)
    diag1 := make([]bool, n*2-1)
    diag2 := make([]bool, n*2-1)
    var dfs func(int)
    dfs = func(r int) {
        if r == n {
            board := make([]string, n)
            for i, c := range queens {
                board[i] = strings.Repeat(".", c) + "Q" + strings.Repeat(".", n-1-c)
            }
            ans = append(ans, board)
            return
        }
        // 在 (r,c) 放皇后
        for c, ok := range col {
            rc := r - c + n - 1
            if !ok && !diag1[r+c] && !diag2[rc] { // 判断能否放皇后
                queens[r] = c // 直接覆盖，无需恢复现场
                col[c], diag1[r+c], diag2[rc] = true, true, true // 皇后占用了 c 列和两条斜线
                dfs(r + 1)
                col[c], diag1[r+c], diag2[rc] = false, false, false // 恢复现场
            }
        }
    }
    dfs(0)
    return
}
```

python

```
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        ans = []
        queens = [0] * n  # 皇后放在 (r,queens[r])
        col = [False] * n
        diag1 = [False] * (n * 2 - 1)
        diag2 = [False] * (n * 2 - 1)
        def dfs(r: int) -> None:
            if r == n:
                ans.append(['.' * c + 'Q' + '.' * (n - 1 - c) for c in queens])
                return
            # 在 (r,c) 放皇后
            for c, ok in enumerate(col):
                if not ok and not diag1[r + c] and not diag2[r - c]:  # 判断能否放皇后
                    queens[r] = c  # 直接覆盖，无需恢复现场
                    col[c] = diag1[r + c] = diag2[r - c] = True  # 皇后占用了 c 列和两条斜线
                    dfs(r + 1)
                    col[c] = diag1[r + c] = diag2[r - c] = False  # 恢复现场
        dfs(0)
        return ans
```

## 63.搜索插入位置

go

```
// 闭区间写法
func lowerBound(nums []int, target int) int {
    left, right := 0, len(nums)-1 // 闭区间 [left, right]
    for left <= right {           // 区间不为空
        // 循环不变量：
        // nums[left-1] < target
        // nums[right+1] >= target
        mid := left + (right-left)/2
        if nums[mid] < target {
            left = mid + 1 // 范围缩小到 [mid+1, right]
        } else {
            right = mid - 1 // 范围缩小到 [left, mid-1]
        }
    }
    return left
}
```

python

```
// 闭区间写法
func lowerBound(nums []int, target int) int {
    left, right := 0, len(nums)-1 // 闭区间 [left, right]
    for left <= right {           // 区间不为空
        // 循环不变量：
        // nums[left-1] < target
        // nums[right+1] >= target
        mid := left + (right-left)/2
        if nums[mid] < target {
            left = mid + 1 // 范围缩小到 [mid+1, right]
        } else {
            right = mid - 1 // 范围缩小到 [left, mid-1]
        }
    }
    return left
}
```

## 64.搜索二维矩阵

go

```
func searchMatrix(matrix [][]int, target int) bool {
    m, n := len(matrix), len(matrix[0])
    i, j := 0, n-1
    for i < m && j >= 0 { // 还有剩余元素
        if matrix[i][j] == target {
            return true // 找到 target
        }
        if matrix[i][j] < target {
            i++ // 这一行剩余元素全部小于 target，排除
        } else {
            j-- // 这一列剩余元素全部大于 target，排除
        }
    }
    return false
}
```

python

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])
        i, j = 0, n - 1
        while i < m and j >= 0:  # 还有剩余元素
            if matrix[i][j] == target:
                return True  # 找到 target
            if matrix[i][j] < target:
                i += 1  # 这一行剩余元素全部小于 target，排除
            else:
                j -= 1  # 这一列剩余元素全部大于 target，排除
        return False
```

## 65.在排序数组中查找元素的第一个和最后一个位置

go

```
// lowerBound 返回最小的满足 nums[i] >= target 的下标 i
// 如果数组为空，或者所有数都 < target，则返回 len(nums)
// 要求 nums 是非递减的，即 nums[i] <= nums[i + 1]
func lowerBound(nums []int, target int) int {
    left, right := 0, len(nums)-1 // 闭区间 [left, right]
    for left <= right { // 区间不为空
        // 循环不变量：
        // nums[left-1] < target
        // nums[right+1] >= target
        mid := left + (right-left)/2
        if nums[mid] >= target {
            right = mid - 1 // 范围缩小到 [left, mid-1]
        } else {
            left = mid + 1 // 范围缩小到 [mid+1, right]
        }
    }
    // 循环结束后 left = right+1
    // 此时 nums[left-1] < target 而 nums[left] = nums[right+1] >= target
    // 所以 left 就是第一个 >= target 的元素下标
    return left
}

func searchRange(nums []int, target int) []int {
    start := lowerBound(nums, target)
    if start == len(nums) || nums[start] != target {
        return []int{-1, -1} // nums 中没有 target
    }
    // 如果 start 存在，那么 end 必定存在
    end := lowerBound(nums, target+1) - 1
    return []int{start, end}
}
```

python

```
class Solution:
    # lower_bound 返回最小的满足 nums[i] >= target 的下标 i
    # 如果数组为空，或者所有数都 < target，则返回 len(nums)
    # 要求 nums 是非递减的，即 nums[i] <= nums[i + 1]
    def lower_bound(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1  # 闭区间 [left, right]
        while left <= right:  # 区间不为空
            # 循环不变量：
            # nums[left-1] < target
            # nums[right+1] >= target
            mid = (left + right) // 2
            if nums[mid] >= target:
                right = mid - 1  # 范围缩小到 [left, mid-1]
            else:
                left = mid + 1  # 范围缩小到 [mid+1, right]
        # 循环结束后 left = right+1
        # 此时 nums[left-1] < target 而 nums[left] = nums[right+1] >= target
        # 所以 left 就是第一个 >= target 的元素下标
        return left

    def searchRange(self, nums: List[int], target: int) -> List[int]:
        start = self.lower_bound(nums, target)
        if start == len(nums) or nums[start] != target:
            return [-1, -1]  # nums 中没有 target
        # 如果 start 存在，那么 end 必定存在
        end = self.lower_bound(nums, target + 1) - 1
        return [start, end]
```

## 66.搜索旋转排序数组

go

```
// 153. 寻找旋转排序数组中的最小值（返回的是下标）
func findMin(nums []int) int {
    left, right := -1, len(nums)-1 // 开区间 (-1, n-1)
    for left+1 < right { // 开区间不为空
        mid := left + (right-left)/2
        if nums[mid] < nums[len(nums)-1] {
            right = mid
        } else {
            left = mid
        }
    }
    return right
}

// 有序数组中找 target 的下标
func lowerBound(nums []int, left, right, target int) int {
    for left+1 < right { // 开区间不为空
        // 循环不变量：
        // nums[right] >= target
        // nums[left] < target
        mid := left + (right-left)/2
        if nums[mid] >= target {
            right = mid // 范围缩小到 (left, mid)
        } else {
            left = mid // 范围缩小到 (mid, right)
        }
    }
    if nums[right] != target {
        return -1
    }
    return right
}

func search(nums []int, target int) int {
    i := findMin(nums)
    if target > nums[len(nums)-1] { // target 只可能在第一段
        return lowerBound(nums, -1, i, target) // 开区间 (-1, i)
    }
    // target 只可能在第二段
    // 由于此时 target <= nums[n-1]，所以 lowerBound 中的循环结束后，right < n 一定成立，无需判断 right == n
    return lowerBound(nums, i-1, len(nums), target) // 开区间 (i-1, n)
}
```

python

```
class Solution:
    # 153. 寻找旋转排序数组中的最小值（返回的是下标）
    def findMin(self, nums: List[int]) -> int:
        left, right = -1, len(nums) - 1  # 开区间 (-1, n-1)
        while left + 1 < right:  # 开区间不为空
            mid = (left + right) // 2
            if nums[mid] < nums[-1]:
                right = mid
            else:
                left = mid
        return right

    # 有序数组中找 target 的下标
    def lower_bound(self, nums: List[int], left: int, right: int, target: int) -> int:
        while left + 1 < right:  # 开区间不为空
            mid = (left + right) // 2
            # 循环不变量：
            # nums[right] >= target
            # nums[left] < target
            if nums[mid] >= target:
                right = mid  # 范围缩小到 (left, mid)
            else:
                left = mid  # 范围缩小到 (mid, right)
        return right if nums[right] == target else -1

    def search(self, nums: List[int], target: int) -> int:
        i = self.findMin(nums)
        if target > nums[-1]:  # target 只可能在第一段
            return self.lower_bound(nums, -1, i, target)  # 开区间 (-1, i)
        # target 只可能在第二段
        # 由于此时 target <= nums[-1]，所以 lower_bound 中的循环结束后，right < n 一定成立，无需判断 right == n
        return self.lower_bound(nums, i - 1, len(nums), target)  # 开区间 (i-1, n)
```

## 67.寻找旋转排序数组中的最小值

go

```
func findMin(nums []int) int {
    left, right := -1, len(nums)-1 // 开区间 (-1, n-1)
    for left+1 < right { // 开区间不为空
        mid := left + (right-left)/2
        if nums[mid] < nums[len(nums)-1] {
            right = mid
        } else {
            left = mid
        }
    }
    return nums[right]
}
```

python

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left, right = -1, len(nums) - 1  # 开区间 (-1, n-1)
        while left + 1 < right:  # 开区间不为空
            mid = (left + right) // 2
            if nums[mid] < nums[-1]:
                right = mid
            else:
                left = mid
        return nums[right]
```

## 68.寻找两个正序数组的中位数

go

```
func findMedianSortedArrays(a, b []int) float64 {
    if len(a) > len(b) {
        a, b = b, a // 保证下面的 i 可以从 0 开始枚举
    }

    m, n := len(a), len(b)
    a = append([]int{math.MinInt}, append(a, math.MaxInt)...)
    b = append([]int{math.MinInt}, append(b, math.MaxInt)...)

    // 循环不变量：a[left] <= b[j+1]
    // 循环不变量：a[right] > b[j+1]
    left, right := 0, m+1
    for left+1 < right { // 开区间 (left, right) 不为空
        i := left + (right-left)/2
        j := (m+n+1)/2 - i
        if a[i] <= b[j+1] {
            left = i // 缩小二分区间为 (i, right)
        } else {
            right = i // 缩小二分区间为 (left, i)
        }
    }

    // 此时 left 等于 right-1
    // a[left] <= b[j+1] 且 a[right] > b[(j-1)+1] = b[j]，所以答案是 i=left
    i := left
    j := (m+n+1)/2 - i
    max1 := max(a[i], b[j])
    min2 := min(a[i+1], b[j+1])
    if (m+n)%2 > 0 {
        return float64(max1)
    }
    return float64(max1+min2) / 2
}
```

python

```
class Solution:
    def findMedianSortedArrays(self, a: List[int], b: List[int]) -> float:
        if len(a) > len(b):
            a, b = b, a

        m, n = len(a), len(b)
        a = [-inf] + a + [inf]
        b = [-inf] + b + [inf]

        # 循环不变量：a[left] <= b[j+1]
        # 循环不变量：a[right] > b[j+1]
        left, right = 0, m + 1
        while left + 1 < right:  # 开区间 (left, right) 不为空
            i = (left + right) // 2
            j = (m + n + 1) // 2 - i
            if a[i] <= b[j + 1]:
                left = i  # 缩小二分区间为 (i, right)
            else:
                right = i  # 缩小二分区间为 (left, i)

        # 此时 left 等于 right-1
        # a[left] <= b[j+1] 且 a[right] > b[(j-1)+1] = b[j]，所以答案是 i=left
        i = left
        j = (m + n + 1) // 2 - i
        max1 = max(a[i], b[j])
        min2 = min(a[i + 1], b[j + 1])
        return max1 if (m + n) % 2 else (max1 + min2) / 2
```

## 69.有效的括号

go

```
func isValid(s string) bool {
    if len(s)%2 != 0 { // s 长度必须是偶数
        return false
    }
    st := []rune{}
    for _, c := range s {
        switch c {
        case '(':
            st = append(st, ')') // 入栈对应的右括号
        case '[':
            st = append(st, ']')
        case '{':
            st = append(st, '}')
        default: // c 是右括号
            if len(st) == 0 || st[len(st)-1] != c {
                return false // 没有左括号，或者左括号类型不对
            }
            st = st[:len(st)-1] // 出栈
        }
    }
    return len(st) == 0 // 所有左括号必须匹配完毕
}
```

python

```
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2:  # s 长度必须是偶数
            return False
        st = []
        for c in s:
            if c == '(':
                st.append(')')  # 入栈对应的右括号
            elif c == '[':
                st.append(']')
            elif c == '{':
                st.append('}')
            elif not st or st.pop() != c:  # c 是右括号
                return False  # 没有左括号，或者左括号类型不对
        return not st  # 所有左括号必须匹配完毕
```

## 70.最小栈

go

```
type pair struct{ val, preMin int }

type MinStack []pair

func Constructor() MinStack {
    // 这里的 0 写成任意数都可以，反正用不到
    return MinStack{{0, math.MaxInt}} // 栈底哨兵
}

func (st *MinStack) Push(val int) {
    *st = append(*st, pair{val, min(st.GetMin(), val)})
}

func (st *MinStack) Pop() {
    *st = (*st)[:len(*st)-1]
}

func (st MinStack) Top() int {
    return st[len(st)-1].val
}

func (st MinStack) GetMin() int {
    return st[len(st)-1].preMin
}
```

python

```
class MinStack:
    def __init__(self):
        # 这里的 0 写成任意数都可以，反正用不到
        self.st = [(0, inf)]  # 栈底哨兵

    def push(self, val: int) -> None:
        self.st.append((val, min(self.st[-1][1], val)))

    def pop(self) -> None:
        self.st.pop()

    def top(self) -> int:
        return self.st[-1][0]

    def getMin(self) -> int:
        return self.st[-1][1]
```

## 71.字符串解码

go

```
func decodeString(s string) string {
    type pair struct {
        s string
        k int
    }
    stack := []pair{} // 用于模拟计算机的递归
    res := ""
    k := 0
    for _, c := range s {
        if unicode.IsLetter(c) {
            res += string(c)
        } else if unicode.IsDigit(c) {
            k = k*10 + int(c-'0')
        } else if c == '[' {
            // 模拟递归
            // 在递归之前，把当前递归函数中的局部变量 res 和 k 保存到栈中
            stack = append(stack, pair{res, k})
            // 递归，初始化 res 和 k
            res = ""
            k = 0
        } else { // ']'
            // 递归结束，从栈中恢复递归之前保存的局部变量
            p := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            // 此时 res 是下层递归的返回值，将其重复 p.k 次，拼接到递归前的 p.s 之后
            res = p.s + strings.Repeat(res, p.k)
        }
    }
    return res
}
```

python

```
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []  # 用于模拟计算机的递归
        res = ''
        k = 0
        for c in s:
            if c.isalpha():
                res += c
            elif c.isdigit():
                k = k * 10 + int(c)
            elif c == '[':
                # 模拟递归
                # 在递归之前，把当前递归函数中的局部变量 res 和 k 保存到栈中
                stack.append((res, k))
                # 递归，初始化 res 和 k
                res = ''
                k = 0
            else:  # ']'
                # 递归结束，从栈中恢复递归之前保存的局部变量
                pre_res, pre_k = stack.pop()
                # 此时 res 是下层递归的返回值，将其重复 pre_k 次，拼接到递归前的 pre_res 之后
                res = pre_res + res * pre_k
        return res
```

## 72.每日温度

go

```
func dailyTemperatures(temperatures []int) []int {
    ans := make([]int, len(temperatures))
    st := []int{} // todolist
    for i, t := range temperatures {
        for len(st) > 0 && t > temperatures[st[len(st)-1]] {
            j := st[len(st)-1]
            st = st[:len(st)-1]
            ans[j] = i - j
        }
        st = append(st, i)
    }
    return ans
}
```

python

```
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        n = len(temperatures)
        ans = [0] * n
        st = []  # todolist
        for i, t in enumerate(temperatures):
            while st and t > temperatures[st[-1]]:
                j = st.pop()
                ans[j] = i - j
            st.append(i)
        return ans
```

## 73.柱状图中最大的矩形

go

```
func largestRectangleArea(heights []int) (ans int) {
    heights = append(heights, -1) // 最后大火收汁，用 -1 把栈清空
    st := []int{-1} // 在栈中只有一个数的时候，栈顶的「下面那个数」是 -1，对应 left[i] = -1 的情况
    for right, h := range heights {
        for len(st) > 1 && heights[st[len(st)-1]] >= h {
            i := st[len(st)-1] // 矩形的高（的下标）
            st = st[:len(st)-1]
            left := st[len(st)-1] // 栈顶下面那个数就是 left
            ans = max(ans, heights[i]*(right-left-1))
        }
        st = append(st, right)
    }
    return
}
```

python

```
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        heights.append(-1)  # 最后大火收汁，用 -1 把栈清空
        st = [-1]  # 在栈中只有一个数的时候，栈顶的「下面那个数」是 -1，对应 left[i] = -1 的情况
        ans = 0
        for right, h in enumerate(heights):
            while len(st) > 1 and heights[st[-1]] >= h:
                i = st.pop()  # 矩形的高（的下标）
                left = st[-1]  # 栈顶下面那个数就是 left
                ans = max(ans, heights[i] * (right - left - 1))
            st.append(right)
        return ans
```

## 74.数组中的第K个最大元素

go

```
// 在子数组 [left, right] 中随机选择一个基准元素 pivot
// 根据 pivot 重新排列子数组 [left, right]
// 重新排列后，<= pivot 的元素都在 pivot 的左侧，>= pivot 的元素都在 pivot 的右侧
// 返回 pivot 在重新排列后的 nums 中的下标
// 特别地，如果子数组的所有元素都等于 pivot，我们会返回子数组的中心下标，避免退化
func partition(nums []int, left int, right int) int {
    // 1. 在子数组 [left, right] 中随机选择一个基准元素 pivot
    i := left + rand.Intn(right-left+1)
    pivot := nums[i]
    // 把 pivot 与子数组第一个元素交换，避免 pivot 干扰后续划分，从而简化实现逻辑
    nums[i], nums[left] = nums[left], nums[i]

    // 2. 相向双指针遍历子数组 [left + 1, right]
    // 循环不变量：在循环过程中，子数组的数据分布始终如下图
    // [ pivot | <=pivot | 尚未遍历 | >=pivot ]
    //   ^                 ^     ^         ^
    //   left              i     j         right

    i, j := left+1, right
    for {
        for i <= j && nums[i] < pivot {
            i++
        }
        // 此时 nums[i] >= pivot

        for i <= j && nums[j] > pivot {
            j--
        }
        // 此时 nums[j] <= pivot

        if i >= j {
            break
        }

        // 维持循环不变量
        nums[i], nums[j] = nums[j], nums[i]
        i++
        j--
    }

    // 循环结束后
    // [ pivot | <=pivot | >=pivot ]
    //   ^             ^   ^     ^
    //   left          j   i     right

    // 3. 把 pivot 与 nums[j] 交换，完成划分（partition）
    // 为什么与 j 交换？
    // 如果与 i 交换，可能会出现 i = right + 1 的情况，已经下标越界了，无法交换
    // 另一个原因是如果 nums[i] > pivot，交换会导致一个大于 pivot 的数出现在子数组最左边，不是有效划分
    // 与 j 交换，即使 j = left，交换也不会出错
    nums[left], nums[j] = nums[j], nums[left]

    // 交换后
    // [ <=pivot | pivot | >=pivot ]
    //               ^
    //               j

    // 返回 pivot 的下标
    return j
}

func findKthLargest(nums []int, k int) int {
    n := len(nums)
    targetIndex := n - k  // 第 k 大元素在升序数组中的下标是 n - k
    left, right := 0, n-1 // 闭区间
    for {
        i := partition(nums, left, right)
        if i == targetIndex {
            // 找到第 k 大元素
            return nums[i]
        }
        if i > targetIndex {
            // 第 k 大元素在 [left, i - 1] 中
            right = i - 1
        } else {
            // 第 k 大元素在 [i + 1, right] 中
            left = i + 1
        }
    }
}
```

python

```
class Solution:
    def partition(self, nums: List[int], left: int, right: int) -> int:
        """
        在子数组 [left, right] 中随机选择一个基准元素 pivot
        根据 pivot 重新排列子数组 [left, right]
        重新排列后，<= pivot 的元素都在 pivot 的左侧，>= pivot 的元素都在 pivot 的右侧
        返回 pivot 在重新排列后的 nums 中的下标
        特别地，如果子数组的所有元素都等于 pivot，我们会返回子数组的中心下标，避免退化
        """

        # 1. 在子数组 [left, right] 中随机选择一个基准元素 pivot
        i = randint(left, right)
        pivot = nums[i]
        # 把 pivot 与子数组第一个元素交换，避免 pivot 干扰后续划分，从而简化实现逻辑
        nums[i], nums[left] = nums[left], nums[i]

        # 2. 相向双指针遍历子数组 [left + 1, right]
        # 循环不变量：在循环过程中，子数组的数据分布始终如下图
        # [ pivot | <=pivot | 尚未遍历 | >=pivot ]
        #   ^                 ^     ^         ^
        #   left              i     j         right

        i, j = left + 1, right
        while True:
            while i <= j and nums[i] < pivot:
                i += 1
            # 此时 nums[i] >= pivot

            while i <= j and nums[j] > pivot:
                j -= 1
            # 此时 nums[j] <= pivot

            if i >= j:
                break

            # 维持循环不变量
            nums[i], nums[j] = nums[j], nums[i]
            i += 1
            j -= 1

        # 循环结束后
        # [ pivot | <=pivot | >=pivot ]
        #   ^             ^   ^     ^
        #   left          j   i     right

        # 3. 把 pivot 与 nums[j] 交换，完成划分（partition）
        # 为什么与 j 交换？
        # 如果与 i 交换，可能会出现 i = right + 1 的情况，已经下标越界了，无法交换
        # 另一个原因是如果 nums[i] > pivot，交换会导致一个大于 pivot 的数出现在子数组最左边，不是有效划分
        # 与 j 交换，即使 j = left，交换也不会出错
        nums[left], nums[j] = nums[j], nums[left]

        # 交换后
        # [ <=pivot | pivot | >=pivot ]
        #               ^
        #               j

        # 返回 pivot 的下标
        return j

    def findKthLargest(self, nums: list[int], k: int) -> int:
        n = len(nums)
        target_index = n - k  # 第 k 大元素在升序数组中的下标是 n - k
        left, right = 0, n - 1  # 闭区间
        while True:
            i = self.partition(nums, left, right)
            if i == target_index:
                # 找到第 k 大元素
                return nums[i]
            if i > target_index:
                # 第 k 大元素在 [left, i - 1] 中
                right = i - 1
            else:
                # 第 k 大元素在 [i + 1, right] 中
                left = i + 1
```

## 75.前k个高频元素

go

```
func topKFrequent(nums []int, k int) []int {
    // 第一步：统计每个元素的出现次数
    cnt := map[int]int{}
    maxCnt := 0
    for _, x := range nums {
        cnt[x]++
        maxCnt = max(maxCnt, cnt[x])
    }

    // 第二步：把出现次数相同的元素，放到同一个桶中
    buckets := make([][]int, maxCnt+1)
    for x, c := range cnt {
        buckets[c] = append(buckets[c], x)
    }

    // 第三步：倒序遍历 buckets，把出现次数前 k 大的元素加入答案
    ans := make([]int, 0, k) // 预分配空间
    // 注意题目保证答案唯一，一定会出现某次 append 后 len(ans) 恰好等于 k 的情况
    for i := maxCnt; len(ans) < k; i-- {
        ans = append(ans, buckets[i]...)
    }
    return ans
}
```

python

```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 第一步：统计每个元素的出现次数
        cnt = Counter(nums)
        max_cnt = max(cnt.values())

        # 第二步：把出现次数相同的元素，放到同一个桶中
        buckets = [[] for _ in range(max_cnt + 1)]  # 也可以用 defaultdict(list)
        for x, c in cnt.items():
            buckets[c].append(x)

        # 第三步：倒序遍历 buckets，把出现次数前 k 大的元素加入答案
        ans = []
        for bucket in reversed(buckets):
            ans += bucket
            # 注意题目保证答案唯一，一定会出现恰好等于 k 的情况
            if len(ans) == k:
                return ans
```

## 76.数据流的中位数

go

```
type MedianFinder struct {
    left  hp // 入堆的元素取相反数，变成最大堆
    right hp // 最小堆
}

func Constructor() (_ MedianFinder) { return }

func (mf *MedianFinder) AddNum(num int) {
    if mf.left.Len() == mf.right.Len() {
        heap.Push(&mf.right, num)
        heap.Push(&mf.left, -heap.Pop(&mf.right).(int))
    } else {
        heap.Push(&mf.left, -num)
        heap.Push(&mf.right, -heap.Pop(&mf.left).(int))
    }
}

func (mf *MedianFinder) FindMedian() float64 {
    if mf.left.Len() > mf.right.Len() {
        return float64(-mf.left.IntSlice[0])
    }
    return float64(mf.right.IntSlice[0]-mf.left.IntSlice[0]) / 2
}

type hp struct{ sort.IntSlice }

func (h *hp) Push(v any) { h.IntSlice = append(h.IntSlice, v.(int)) }
func (h *hp) Pop() any   { a := h.IntSlice; v := a[len(a)-1]; h.IntSlice = a[:len(a)-1]; return v }
```

python

```
class MedianFinder:
    def __init__(self):
        self.left = []  # 最大堆
        self.right = []  # 最小堆

    def addNum(self, num: int) -> None:
        if len(self.left) == len(self.right):
            heappush_max(self.left, heappushpop(self.right, num))
        else:
            heappush(self.right, heappushpop_max(self.left, num))

    def findMedian(self) -> float:
        if len(self.left) > len(self.right):
            return self.left[0]
        return (self.left[0] + self.right[0]) / 2
```

## 77.买卖股票的最佳时机

go

```
func maxProfit(prices []int) (ans int) {
    minPrice := prices[0]
    for _, p := range prices {
        ans = max(ans, p-minPrice)
        minPrice = min(minPrice, p)
    }
    return
}
```

python

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        ans = 0
        min_price = prices[0]
        for p in prices:
            ans = max(ans, p - min_price)
            min_price = min(min_price, p)
        return ans
```

## 78.跳跃游戏

go

```
func canJump(nums []int) bool {
    mx := 0
    for i, jump := range nums {
        if i > mx { // 无法到达 i
            return false
        }
        mx = max(mx, i+jump) // 从 i 最右可以跳到 i + jump
        if mx >= len(nums)-1 { // 可以跳到 n-1
            break
        }
    }
    return true
}
```

python

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        mx = 0
        for i, jump in enumerate(nums):
            if i > mx:  # 无法到达 i
                return False
            mx = max(mx, i + jump)  # 从 i 最右可以跳到 i + jump
            if mx >= len(nums) - 1:  # 可以跳到 n-1
                return True
```

## 79.跳跃游戏2

go

```
func jump(nums []int) (ans int) {
    curEnd := 0  // 已建造的桥的右端点
    nextEnd := 0 // 下一座桥的右端点的最大值
    for i, num := range nums[:len(nums)-1] {
        // 遍历的过程中，记录下一座桥的最远点
        nextEnd = max(nextEnd, i+num)
        if i == curEnd { // 无路可走，必须建桥
            curEnd = nextEnd // 建桥后，最远可以到达 nextEnd
            ans++
        }
    }
    return
}
```

python

```
class Solution:
    def jump(self, nums: List[int]) -> int:
        ans = 0
        cur_end = 0  # 已建造的桥的右端点
        next_end = 0  # 下一座桥的右端点的最大值
        for i in range(len(nums) - 1):
            # 遍历的过程中，记录下一座桥的最远点
            next_end = max(next_end, i + nums[i])
            if i == cur_end:  # 无路可走，必须建桥
                cur_end = next_end  # 建桥后，最远可以到达 next_end
                ans += 1
        return ans
```

## 80.划分字母区间

go

```
func partitionLabels(s string) (ans []int) {
    last := [26]int{}
    for i, c := range s {
        last[c-'a'] = i // 每个字母最后出现的下标
    }

    start, end := 0, 0
    for i, c := range s {
        end = max(end, last[c-'a']) // 更新当前区间右端点的最大值
        if end == i { // 当前区间合并完毕
            ans = append(ans, end-start+1) // 区间长度加入答案
            start = end + 1 // 下一个区间的左端点
        }
    }
    return
}
```

python

```
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        last = {c: i for i, c in enumerate(s)}  # 每个字母最后出现的下标
        ans = []
        start = end = 0
        for i, c in enumerate(s):
            end = max(end, last[c])  # 更新当前区间右端点的最大值
            if end == i:  # 当前区间合并完毕
                ans.append(end - start + 1)  # 区间长度加入答案
                start = end + 1  # 下一个区间的左端点
        return ans
```

## 81.爬楼梯

go

```
func climbStairs(n int) int {
    f0,f1 := 1,1
    for i := 2;i < n + 1;i ++{
        new_f := f0 + f1
        f0 = f1
        f1 = new_f
    }
    return f1
}
```

python

```
class Solution:
    def climbStairs(self, n: int) -> int:
        f0 = f1 = 1
        for _ in range(2, n + 1):
            new_f = f1 + f0
            f0 = f1
            f1 = new_f
        return f1
```

## 82.杨辉三角

go

```
func generate(numRows int) [][]int {
    c := make([][]int, numRows)
    for i := range c {
        c[i] = make([]int, i+1)
        c[i][0], c[i][i] = 1, 1
        for j := 1; j < i; j++ {
            // 左上方的数 + 正上方的数
            c[i][j] = c[i-1][j-1] + c[i-1][j]
        }
    }
    return c
}
```

python

```
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        c = [[1] * (i + 1) for i in range(numRows)]
        for i in range(2, numRows):
            for j in range(1, i):
                # 左上方的数 + 正上方的数
                c[i][j] = c[i - 1][j - 1] + c[i - 1][j]
        return c
```

## 83.打家劫舍

go

```
func rob(nums []int) int {
    f0, f1 := 0, 0
    for _, x := range nums {
        f0, f1 = f1, max(f1, f0+x)
    }
    return f1
}
```

python

```
class Solution:
    def rob(self, nums: List[int]) -> int:
        f0 = f1 = 0
        for x in nums:
            f0, f1 = f1, max(f1, f0 + x)
        return f1
```

## 84.完全平方数

go

```
const N = 10000
var f [N + 1]int

func init() {
    for i := 1; i <= N; i++ {
        f[i] = math.MaxInt
    }
    for i := 1; i*i <= N; i++ {
        for j := i * i; j <= N; j++ {
            f[j] = min(f[j], f[j-i*i]+1) // 不选 vs 选
        }
    }
}

func numSquares(n int) int {
    return f[n]
}
```

python

```
N = 10000
f = [0] + [inf] * N
for i in range(1, isqrt(N) + 1):
    for j in range(i * i, N + 1):
        f[j] = min(f[j], f[j - i * i] + 1)  # 不选 vs 选

class Solution:
    def numSquares(self, n: int) -> int:
        return f[n]
```

## 85.零钱兑换

go

```
func coinChange(coins []int, amount int) int {
    f := make([]int, amount+1)
    for i := range f {
        f[i] = math.MaxInt / 2
    }
    f[0] = 0
    for _, x := range coins {
        for c := x; c <= amount; c++ {
            f[c] = min(f[c], f[c-x]+1)
        }
    }
    ans := f[amount]
    if ans < math.MaxInt/2 {
        return ans
    }
    return -1
}
```

python

```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        f = [0] + [inf] * amount
        for x in coins:
            for c in range(x, amount + 1):
                f[c] = min(f[c], f[c - x] + 1)
        ans = f[amount]
        return ans if ans < inf else -1
```

## 86.单词拆分

go

```
func wordBreak(s string, wordDict []string) bool {
    maxLen := 0
    words := make(map[string]bool, len(wordDict))
    for _, w := range wordDict {
        words[w] = true
        maxLen = max(maxLen, len(w))
    }

    n := len(s)
    f := make([]bool, n+1)
    f[0] = true
    for i := 1; i <= n; i++ {
        for j := i - 1; j >= max(i-maxLen, 0); j-- {
            if f[j] && words[s[j:i]] {
                f[i] = true
                break
            }
        }
    }
    return f[n]
}
```

python

```
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        max_len = max(map(len, wordDict))  # 用于限制下面 j 的循环次数
        words = set(wordDict)  # 便于快速判断 s[j:i] in words

        n = len(s)
        f = [True] + [False] * n
        for i in range(1, n + 1):
            for j in range(i - 1, max(i - max_len - 1, -1), -1):
                if f[j] and s[j:i] in words:
                    f[i] = True
                    break
        return f[n]
```

## 87.最长递增子序列

go

```
func lengthOfLIS(nums []int) int {
    g := nums[:0] // 原地修改
    for _, x := range nums {
        j := sort.SearchInts(g, x)
        if j == len(g) { // >=x 的 g[j] 不存在
            g = append(g, x)
        } else {
            g[j] = x
        }
    }
    return len(g)
}
```

python

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        ng = 0  # g 的长度
        for x in nums:
            j = bisect_left(nums, x, 0, ng)
            nums[j] = x
            if j == ng:  # >=x 的 g[j] 不存在
                ng += 1 
        return ng
```

## 88.乘积最大子数组

go

```
func maxProduct(nums []int) int {
    ans := math.MinInt // 注意答案可能是负数
    fMax, fMin := 1, 1
    for _, x := range nums {
        fMax, fMin = max(fMax*x, fMin*x, x),
                     min(fMax*x, fMin*x, x)
        ans = max(ans, fMax)
    }
    return ans
}
```

python

```
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        ans = -inf  # 注意答案可能是负数
        f_max = f_min = 1
        for x in nums:
            f_max, f_min = max(f_max * x, f_min * x, x), \
                           min(f_max * x, f_min * x, x)
            ans = max(ans, f_max)
        return ans
```

## 89.分割等和子集

go

```
func canPartition(nums []int) bool {
    s := 0
    for _, x := range nums {
        s += x
    }
    if s%2 != 0 {
        return false
    }
    s /= 2 // 注意这里把 s 减半了

    f := make([]bool, s+1)
    f[0] = true
    s2 := 0
    for _, x := range nums {
        s2 = min(s2+x, s)
        for j := s2; j >= x; j-- {
            f[j] = f[j] || f[j-x]
        }
        if f[s] {
            return true
        }
    }
    return false
}
```

python

```
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        s = sum(nums)
        if s % 2:
            return False
        s //= 2  # 注意这里把 s 减半了

        f = [True] + [False] * s
        s2 = 0
        for i, x in enumerate(nums):
            s2 = min(s2 + x, s)
            for j in range(s2, x - 1, -1):
                f[j] = f[j] or f[j - x]
            if f[s]:
                return True
        return False
```

## 90.最长有效括号

go

```
func longestValidParentheses(s string) (ans int) {
	st := []int{-1} // 未配对括号的下标，其中栈底元素表示永远无法配对的括号下标

	for i, ch := range s {
		if ch == '(' {
			st = append(st, i) // 保存左括号的下标
		} else if len(st) > 1 {
			st = st[:len(st)-1] // 右括号与栈顶的左括号配对
			ans = max(ans, i-st[len(st)-1]) // 从 st[len(st)-1]+1 到 i 都已配对，长为 i - st[len(st)-1]
		} else { // s[i] 是永远无法配对的右括号
			st[0] = i // 替换栈底
		}
	}

	return
}
```

python

```
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        st = [-1]  # 未配对括号的下标，其中栈底元素表示永远无法配对的括号下标
        ans = 0

        for i, ch in enumerate(s):
            if ch == '(':
                st.append(i)  # 保存左括号的下标
            elif len(st) > 1:
                st.pop()  # 右括号与栈顶的左括号配对
                ans = max(ans, i - st[-1])  # 从 st[-1]+1 到 i 都已配对，长为 i - st[-1]
            else:  # s[i] 是永远无法配对的右括号
                st[0] = i  # 替换栈底

        return ans
```

## 91.不同路径

go

```
func uniquePaths(m, n int) int {
    f := make([]int, n+1)
    f[1] = 1
    for range m {
        for j := range n {
            f[j+1] += f[j]
        }
    }
    return f[n]
}
```

python

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        f = [0] * (n + 1)
        f[1] = 1
        for _ in range(m):
            for j in range(n):
                f[j + 1] += f[j]
        return f[n]
```

## 92.最小路径和

go

```
func minPathSum(grid [][]int) int {
    n := len(grid[0])
    f := make([]int, n+1)
    for j := range f {
        f[j] = math.MaxInt
    }
    f[1] = 0
    for _, row := range grid {
        for j, x := range row {
            f[j+1] = min(f[j], f[j+1]) + x
        }
    }
    return f[n]
}
```

python

```
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        f = [inf] * (len(grid[0]) + 1)
        f[1] = 0
        for row in grid:
            for j, x in enumerate(row):
                f[j + 1] = min(f[j], f[j + 1]) + x
        return f[-1]
```

## 93.最长回文串

go

```
func longestPalindrome(s string) string {
    n := len(s)
    ansLeft, ansRight := 0, 0

    // 奇回文串
    for i := range n {
        l, r := i, i
        for l >= 0 && r < n && s[l] == s[r] {
            l--
            r++
        }
        if r-l-1 > ansRight-ansLeft {
            ansLeft = l + 1
            ansRight = r // 左闭右开区间
        }
    }

    // 偶回文串
    for i := range n - 1 {
        l, r := i, i+1
        for l >= 0 && r < n && s[l] == s[r] {
            l--
            r++
        }
        if r-l-1 > ansRight-ansLeft {
            ansLeft = l + 1
            ansRight = r // 左闭右开区间
        }
    }

    return s[ansLeft:ansRight]
}
```

python

```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        ans_left = ans_right = 0

        # 奇回文串
        for i in range(n):
            l = r = i
            while l >= 0 and r < n and s[l] == s[r]:
                l -= 1
                r += 1
            # 循环结束后，s[l+1] 到 s[r-1] 是回文串
            if r - l - 1 > ans_right - ans_left:
                ans_left, ans_right = l + 1, r  # 左闭右开区间

        # 偶回文串
        for i in range(n - 1):
            l, r = i, i + 1
            while l >= 0 and r < n and s[l] == s[r]:
                l -= 1
                r += 1
            if r - l - 1 > ans_right - ans_left:
                ans_left, ans_right = l + 1, r  # 左闭右开区间

        return s[ans_left: ans_right]
```

## 94.最长公共子序列

go

```
func longestCommonSubsequence(s, t string) int {
    m := len(t)
    f := make([]int, m+1)
    for _, x := range s {
        pre := 0 // f[0]
        for j, y := range t {
            if x == y {
                f[j+1], pre = pre+1, f[j+1]
            } else {
                pre = f[j+1]
                f[j+1] = max(f[j+1], f[j])
            }
        }
    }
    return f[m]
}
```

python

```
class Solution:
    def longestCommonSubsequence(self, s: str, t: str) -> int:
        f = [0] * (len(t) + 1)
        for x in s:
            pre = 0  # f[0]
            for j, y in enumerate(t):
                tmp = f[j + 1]
                f[j + 1] = pre + 1 if x == y else max(f[j + 1], f[j])
                pre = tmp
        return f[-1]
```

## 95.编辑距离

go

```
func minDistance(s, t string) int {
    m := len(t)
    f := make([]int, m+1)
    for j := range m {
        f[j+1] = j + 1
    }
    for _, x := range s {
        pre := f[0]
        f[0]++ // f[0] = i + 1
        for j, y := range t {
            if x == y {
                f[j+1], pre = pre, f[j+1]
            } else {
                f[j+1], pre = min(f[j+1], f[j], pre)+1, f[j+1]
            }
        }
    }
    return f[m]
}
```

python

```
class Solution:
    def minDistance(self, s: str, t: str) -> int:
        f = list(range(len(t) + 1))
        for x in s:
            pre = f[0]
            f[0] += 1  # f[0] = i + 1
            for j, y in enumerate(t):
                tmp = f[j + 1]
                f[j + 1] = pre if x == y else min(f[j + 1], f[j], pre) + 1
                pre = tmp
        return f[-1]
```

## 96.只出现一次的数字

go

```
func singleNumber(nums []int) (ans int) {
    for _, x := range nums {
        ans ^= x
    }
    return
}
```

python

```
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return reduce(xor, nums)
```

## 97.多数元素

go

```
func majorityElement(nums []int) (ans int) {
    hp := 0
    for _, x := range nums {
        if hp == 0 { // x 是初始擂主，生命值为 1
            ans, hp = x, 1
        } else if x == ans { // 比武，同门加血，否则扣血
            hp++
        } else {
            hp--
        }
    }
    return
}
```

python

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        ans = hp = 0
        for x in nums:
            if hp == 0:  # x 是初始擂主，生命值为 1
                ans, hp = x, 1
            else:  # 比武，同门加血，否则扣血
                hp += 1 if x == ans else -1
        return ans
```

## 98.颜色分类

go

```
func sortColors(nums []int) {
    p0, p1 := 0, 0
    for i, x := range nums {
        nums[i] = 2
        if x <= 1 {
            nums[p1] = 1
            p1++
        }
        if x == 0 {
            nums[p0] = 0
            p0++
        }
    }
}
```

python

```
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        p0 = p1 = 0
        for i, x in enumerate(nums):
            nums[i] = 2
            if x <= 1:
                nums[p1] = 1
                p1 += 1
            if x == 0:
                nums[p0] = 0
                p0 += 1
```

## 99.下一个排列

go

```
func nextPermutation(nums []int) {
    n := len(nums)

    // 第一步：从右到左找到第一个小于 nums[i+1] 的数 nums[i]
    i := n - 2
    for i >= 0 && nums[i] >= nums[i+1] {
        i--
    }

    // 如果找到了，进入第二步；否则跳过第二步，反转整个数组
    if i >= 0 {
        // 第二步：从右到左找到 nums[i] 右边最小的大于 nums[i] 的数 nums[j]
        j := n - 1
        for nums[j] <= nums[i] {
            j--
        }
        // 交换 nums[i] 和 nums[j]
        nums[i], nums[j] = nums[j], nums[i]
    }

    // 第三步：反转 nums[i+1:]（如果上面跳过第二步，此时 i = -1）
    slices.Reverse(nums[i+1:])
}
```

python

```
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        n = len(nums)

        # 第一步：从右到左找到第一个小于 nums[i+1] 的数 nums[i]
        i = n - 2
        while i >= 0 and nums[i] >= nums[i + 1]:
            i -= 1

        # 如果找到了，进入第二步；否则跳过第二步，反转整个数组
        if i >= 0:
            # 第二步：从右到左找到 nums[i] 右边最小的大于 nums[i] 的数 nums[j]
            j = n - 1
            while nums[j] <= nums[i]:
                j -= 1
            # 交换 nums[i] 和 nums[j]
            nums[i], nums[j] = nums[j], nums[i]

        # 第三步：反转 nums[i+1:]（如果上面跳过第二步，此时 i = -1）
        # nums[i+1:] = nums[i+1:][::-1] 这样写也可以，但空间复杂度不是 O(1) 的
        left, right = i + 1, n - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
```

## 100.寻找重复数

go

```
// 代码逻辑同 142. 环形链表 II
func findDuplicate(nums []int) int {
    slow, fast := 0, 0 // 0 一定不在环上，适合作为起点
    for {
        slow = nums[slow]       // 等价于 slow = slow.next
        fast = nums[nums[fast]] // 等价于 fast = fast.next.next
        if fast == slow {       // 快慢指针移动到同一个节点
            break
        }
    }

    head := 0 // 再用一个指针，从起点出发
    for slow != head {
        slow = nums[slow]
        head = nums[head]
    }
    return slow // 入环口即重复元素
}
```

python

```
# 代码逻辑同 142. 环形链表 II
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        slow = fast = 0  # 0 一定不在环上，适合作为起点
        while True:
            slow = nums[slow]  # 等价于 slow = slow.next
            fast = nums[nums[fast]]  # 等价于 fast = fast.next.next
            if fast == slow:  # 快慢指针移动到同一个节点
                break

        head = 0  # 再用一个指针，从起点出发
        while slow != head:
            slow = nums[slow]
            head = nums[head]
        return slow  # 入环口即重复元素
```

