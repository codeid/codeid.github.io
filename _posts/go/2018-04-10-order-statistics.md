---
layout: post
title: k th num
---


## divide ##

分治法中的分，下面代码是单链分区

```golang
func partition(arr []int, p int, q int) int {
	//use arr[p] as key first
	pivotIndex := p
	pivot := arr[pivotIndex]
	arr[0], arr[pivotIndex] = arr[pivotIndex], arr[0]

	i := p
	for j := p + 1; j <= q; j++ {
		if arr[j] < pivot {
			i++
			arr[i], arr[j] = arr[j], arr[i]
		}
	}

	//swap pivot to arr[i]
	arr[0], arr[i] = arr[i], arr[0]
	return i
}
```

pivotIndex := p 即每次选第一个作为划分点，修改为pivotIndex := randomInt(p, q)后使用随机元素做划分点


## select ##

```golang
func randSelect(arr []int, p int, q int, i int) int {
	//i>=1
	if p == q {
		return arr[p]
	}

	r := randPartition(arr, p, q)
	k := r - p + 1 //第k个，以1开始

	if i == k {
		return arr[r]
	}

	if i < k {
		return randSelect(arr, p, r-1, i)
	} else {
		return randSelect(arr, r+1, q, i-k)
	}
}
```
