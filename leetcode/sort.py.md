```python
class solution:

    def bubble_sort(self, arr):

        for i in range(len(arr)):

            for j in range(len(arr)-i-1):

                if arr[j] > arr[j+1]:

                    arr[j], arr[j+1] = arr[j+1], arr[j]

        return arr

    def select_sort(self, arr):

        for i in range(len(arr)):

            min_idx = i

            for j in range(i+1, len(arr)):

                if arr[min_idx] > arr[j]:

                    min_idx = j

            arr[i], arr[min_idx] = arr[min_idx], arr[i]

        return arr

    def insert_sort(self, arr):

        for i in range(1, len(arr)):

            for j in range(i):

                if arr[j] > arr[i]:

                    arr[i], arr[j] = arr[j], arr[i]

        return arr

    def quick_sort(self, arr):

        if len(arr) <= 1:

            return arr

        else:

            return self.quick_sort([x for x in arr if x < arr[len(arr)//2]]) + [arr[len(arr)//2]] + self.quick_sort([x for x in arr if x > arr[len(arr)//2]])

    def merge_sort(self, arr):

        def arr_sort(arr1, arr2):

            result = []

            i, j = 0, 0

            while i <= len(arr1)-1 and j <= len(arr2)-1:

                    if arr1[i] <= arr2[j]:

                        result.append(arr1[i])

                        i += 1

                    else:

                        result.append(arr2[j])

                        j += 1

            if i != len(arr1):

                result += arr1[i:]

            else:

                result += arr2[j:]

            return result

  

        def split(arr):

            if len(arr) <= 1:

                return arr

            else:

                return arr_sort(split(arr[:len(arr)//2]), split(arr[len(arr)//2:]))

        return split(arr)

    def heap_sort(self, arr):

        def heapify(arr, n, i):

            largest = i

            left = 2 * i + 1

            right = 2 * i + 2

            if left < n and arr[left] > arr[largest]:

                largest = left

            if right < n and arr[right] > arr[largest]:

                largest = right

            if largest != i:

                arr[i], arr[largest] = arr[largest], arr[i]

                heapify(arr, n, largest)

        def hp_sort(arr):

            n = len(arr)

            # 构建最大堆

            for i in range(n//2 -1, -1, -1):

                heapify(arr, n, i)

            # 逐个提取元素

            for i in range(n-1, 0, -1):

                arr[i], arr[0] = arr[0], arr[i]

                heapify(arr, i, 0)

            return arr

        return hp_sort(arr)

  

if __name__ == "__main__":

    so = solution()

    arr = [1, 234, 1231, 2842, 1293192, 274, 237, 0, 273, 12312313, -1]

    print(so.heap_sort(arr))
```