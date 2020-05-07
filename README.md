# Golang 数据结构与算法

###7大排序
```Golang
func quick_sort(nums []int, l, r int) {
	if l >= r {
		return
	}
	nums[r], nums[(l+r)>>1] = nums[(l+r)>>1], nums[r]
	i := l - 1
	for j := l; j < r; j++ {
		if nums[j] < nums[r] {
			i++
			nums[i], nums[j] = nums[j], nums[i]
		}
	}
	i++
	nums[i], nums[r] = nums[r], nums[i]
	quick_sort(nums, l, i-1)
	quick_sort(nums, i+1, r)
}
```

```Golang
func merge_sort(nums []int, l, r int) {
	if l >= r {
		return
	}
	mid := (l + r) >> 1
	merge_sort(nums, l, mid)
	merge_sort(nums, mid+1, r)
	i, j := l, mid+1
	tmp := []int{}
	for i <= mid || j <= r {
		if i > mid || (j <= r && nums[j] < nums[i]) {
			tmp = append(tmp, nums[j])
			j++
		} else {
			tmp = append(tmp, nums[i])
			i++
		}
	}
	copy(nums[l:r+1], tmp)
}
```

```Golang
func heap_sort(nums []int) {
	lens := len(nums) - 1
	for i := lens << 1; i >= 0; i-- {//建堆O(n)
		down(nums, i, lens)
	}
	for j := lens; j >= 1; j-- {
		nums[0], nums[j] = nums[j], nums[0]
		lens--
		down(nums, 0, lens)
	}
}
func down(nums []int, i, lens int) {//O(logn)
	max := i
	if i<<1+1 <= lens && nums[i<<1+1] > nums[max] {
		max = i<<1 + 1
	}
	if i<<1+2 <= lens && nums[i<<1+2] > nums[max] {
		max = i<<1 + 2
	}
	if i != max {
		nums[i], nums[max] = nums[max], nums[i]
		down(nums, max, lens)
	}
}
```

```Golang
func select_sort(nums []int) {
	for i := 0; i < len(nums)-1; i++ {
		pos := i
		for j := i + 1; j < len(nums); j++ {
			if nums[j] < nums[pos] {
				pos = j
			}
		}
		nums[i], nums[pos] = nums[pos], nums[i]
	}
}
```

```Golang
func insert_sort(nums []int) {
	for i := 1; i < len(nums); i++ {
		tmp := nums[i]
		j := i - 1
		for j >= 0 && nums[j] > tmp {
			nums[j+1] = nums[j] //向后移动1位
			j--                 //向前扫描
		}
		nums[j+1] = tmp //添加到小于它的数的右边
	}
}
```


```Golang
func bubble_sort(nums []int) {
	for i := 0; i < len(nums); i++ {
		for j := 0; j < len(nums)-i-1; j++ { //最后剩一个数不需比较-1
			if nums[j] > nums[j+1] {
				nums[j], nums[j+1] = nums[j+1], nums[j]
			}
		}
	}
}
```


```Golang
func count_sort(nums []int) {
	cnt := [100001]int{}
	for i := 0; i < len(nums); i++ {
		cnt[nums[i]+50000] ++ //防止负数导致数组越界
	}
	for i, idx := 0, 0; i < 100001; i++ {
		for cnt[i] > 0 {
			nums[idx] = i - 50000
			idx++
			cnt[i] --
		}
	}
}
```
