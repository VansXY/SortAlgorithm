# SortAlgorithm
排序算法集合

## 冒泡排序
> 思想

> 代码实现


## 插入排序
> 思想

> 代码实现

## 快排
> 思想
- 在数组中随机取一个值作为标兵
- 对标兵左、右的区间进行划分(将比标兵大的数放在标兵的右面，比标兵小的数放在标兵的左面，如果倒序就反过来)
- 重复如上两个过程，直到选取了所有的标兵并划分(此时每个标兵决定的区间中只有一个值，故有序)

> 代码实现
```
- (void)quickSortArray:(NSMutableArray *)array leftIndex:(NSInteger)leftIndex rightIndex:(NSInteger)rightIndex {
    
    if (leftIndex >= rightIndex) {
        return;
    }
    
    NSInteger i = leftIndex;
    NSInteger j = rightIndex;
    NSInteger key = [array[i] integerValue];
    
    while (i < j) {
        while (i < j && [array[j] integerValue] >= key) {
            j--;
        }
        array[i] = array[j];
        
        while (i < j && [array[i] integerValue] <= key) {
            i++;
        }
        array[j] = array[i];
    }
    array[i] = @(key);
    
    [self quickSortArray:array leftIndex:leftIndex rightIndex:i - 1];
    [self quickSortArray:array leftIndex:i + 1 rightIndex:rightIndex];
}
```
