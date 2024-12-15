## Template  

```
  while lo <= hi:
    mid = lo + (hi - lo) / 2 
     # find the smallest lo such that nums[lo:] >= target，condition can be anything
    if nums[mid] >= target:
      hi = mid - 1 
    else:
      lo = mid + 1    
  return lo
```

---
## Explanation  
This Binary Search code is designed to find the leftmost element which meets our requirements.
