## 0.1 **在LR字符串中交换相邻字符**

在一个由 `'L'` , `'R'` 和 `'X'` 三个字符组成的字符串（例如`"RXXLRXRXL"`）中进行移动操作。一次移动操作指用一个 `"LX"` 替换一个 `"XL"`，或者用一个 `"XR"` 替换一个 `"RX"`。现给定起始字符串 `start` 和结束字符串 `result`，请编写代码，当且仅当存在一系列移动操作使得 `start` 可以转换成 `result` 时， 返回 `True`。

**思路**
- L、R的相对位置关系不会发生变化
- L只能向左移动，因此对应位置字符的下标大小有规律；R同理

---

![[Pasted image 20250428132950.png]]

要求：时间复杂度O（n），空间复杂度O（1）

### 0.1.1 思路1：二分查找
**关键：需要想到——若重复的数字为a，则从a开始到最大数字，小于等于a的数字数量会大于a**
因此使用二分查找即可实现，时间复杂度为O（nlogn）

### 0.1.2 思路2：**环形链表解**

![[Pasted image 20250428141240.png]]

---

## 0.2 **螺旋矩阵**

给你一个 `m` 行 `n` 列的矩阵 `matrix` ，请按照 **顺时针螺旋顺序** ，返回矩阵中的所有元素。

思路：
每个方向给定一个位置指定指针，在遍历到该位置后切换方向并调整

```C++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int left = 0;
        int right = matrix[0].size();
        int up = 1;
        int down = matrix.size();
        int i = 0;
        int j = 0;
        int des = 0;
        vector<int> res;

        while(left <= right && up <= down){
            if(des == 0){
                while(j < right){
                    res.push_back(matrix[i][j]);
                    j++;
                }
                right--;
                j--;
                i++;
                des = 1;
            }
            else if(des == 1){
                while(i < down){
                    res.push_back(matrix[i][j]);
                    i++;
                }
                down--;
                i--;
                j--;
                des = 2;
            }
            else if(des == 2){
                while(j >= left){
                    res.push_back(matrix[i][j]);
                    j--;
                }
                left++;
                j++;
                i--;
                des = 3;
            }
            else if(des == 3){
                while(i >= up){
                    res.push_back(matrix[i][j]);
                    i--;
                }
                up++;
                i++;
                j++;
                des = 0;
            }
        }
        return res;
    }
};
```

---

