# Golang 数据结构与算法


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

```
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
