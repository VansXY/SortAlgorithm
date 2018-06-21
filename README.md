# SortAlgorithm
排序算法集合

## 冒泡排序
> 思想
其思想是通过无序区中相邻记录关键字间的比较和位置的交换,使关键字最小的记录如气泡一般逐渐往上“漂浮”直至“水面”。 冒泡排序的复杂度，在最好情况下，即正序有序，则只需要比较n次。故，为O(n) ，最坏情况下，即逆序有序，则需要比较(n-1)+(n-2)+……+1，故，为O(n²)。

> 代码实现
```
// 冒泡排序(i控制趟树，j控制每趟的次数)
    NSMutableArray *array = [NSMutableArray arrayWithArray:@[@1, @3, @2, @9, @6, @19, @7]];
    for (int i = 0; i < array.count - 1; i++) {
        for (int j = 0; j < array.count - 1 - i; j++) {
            if (array[j] > array[j+1]) {
                int temp = [array[j] intValue];
                array[j] = array[j + 1];
                array[j+1] = [NSNumber numberWithInteger:temp];
            }
        }
    }
    NSLog(@"%@", array);
```

#### 优化
```
NSMutableArray *array = [NSMutableArray arrayWithArray:@[@1, @3, @2, @9, @6, @19, @7]];
    int k = 0;
    BOOL isSort = YES;
    for (int i = 0; i < array.count - 1 && isSort; i++) {
        k++;
        isSort = NO;
        for (int j = 0; j < array.count - i - 1; j++) {
            if (array[j] > array[j+1]) {
                
                int temp = [array[j] intValue];
                array[j] = array[j + 1];
                array[j+1] = [NSNumber numberWithInteger:temp];
                isSort = YES;
            }
        }
        NSLog(@"k = %d", k);
        NSLog(@"%@\n", array);
    }
```

## 插入排序
> 思想
每次只处理一个元素，从后往前查找，找到该元素合适的插入位置，最好的情况下，即正序有序(从小到大)，这样只需要比较n次，不需要移动。因此时间复杂度为O(n) ，最坏的情况下，即逆序有序，这样每一个元素就需要比较n次，共有n个元素，因此实际复杂度为O(n²) 。

> 代码实现
```
int k = 0;
    NSMutableArray *array = [NSMutableArray arrayWithArray:@[@1, @3, @2, @9, @6, @19, @7]];
    for (int i = 0; i < array.count; i++) {
        k++;
        for (int j = i; j > 0; j--) {
            if (array[j-1] > array[j]) {
                int temp = [array[j] intValue];
                array[j] = array[j - 1];
                array[j - 1] = [NSNumber numberWithInteger:temp];
            }
            
        }
        NSLog(@"k = %d", k);
        NSLog(@"%@\n", array);
    }
```

## 鸡尾酒排序
> 思想 
如果觉得冒泡已经够用了，那么就不用再继续往下看了，如果觉得这个还能再继续优化，那么，双向循环排序了解一下，简称鸡尾酒排序

> 代码实现
```
NSMutableArray *array = [NSMutableArray arrayWithArray:@[@1, @3, @2, @9, @6, @19, @7]];
    int k = 0;
    BOOL isSort = YES;
    // 因为是双向比较，所以比较次数为原来数组的1/2次即可。
    for (int i = 0; i < array.count - 1 && isSort; i++) {
        k++;
        isSort = NO;
        // 从前到后的排序 (升序)
        for (int j = 0; j < array.count - i - 1; j++) {
            // 如果前面大于后面，则进行交换
            if (array[j] > array[j+1]) {
                int temp = [array[j] intValue];
                array[j] = array[j + 1];
                array[j+1] = [NSNumber numberWithInteger:temp];
                isSort = YES;
            }
        }
        
        // 从后到前的排序（降序）
        for (int k = (int)array.count - i - 1; k > i; k--) {
            // 如果前面大于后面，则进行交换
            if (array[k - 1] > array[k]) {
                int temp = [array[k] intValue];
                array[k] = array[k - 1];
                array[k - 1] = [NSNumber numberWithInteger:temp];
                isSort = YES;
            }
        }
        NSLog(@"k = %d", k);
        NSLog(@"%@\n", array);
    }
```

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
