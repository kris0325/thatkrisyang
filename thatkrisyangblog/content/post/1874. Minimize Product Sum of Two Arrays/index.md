--- 
title:  1874. Minimize Product Sum of Two Arrays
description:  1874.2個數組的最小乘積和

slug:  1874. Minimize Product Sum of Two Arrays

date: 2024-08-02

image: 1874.png

categories:

- Leetcode
tags:
- Greedy
- Medium
- Google
- Amazon
- TikTok
weight: 1 # You can add weight to some posts to override the default sorting (date descending)

---

```
The product sum of two equal-length arrays a and b is 
equal to the sum of a[i] * b[i] for all 0 <= i < a.length (0-indexed).

For example, if a = [1,2,3,4] and b = [5,2,3,1], the product sum would be 1*5 + 2*2 + 3*3 + 4*1 = 22.
Given two arrays nums1 and nums2 of length n, return the minimum product sum 
if you are allowed to rearrange the order of the elements in nums1.

Example 1:

Input: nums1 = [5,3,4,2], nums2 = [4,2,2,5]
Output: 40
Explanation: We can rearrange nums1 to become [3,5,4,2]. The product sum of [3,5,4,2] and [4,2,2,5] is 3*4 + 5*2 + 4*2 + 2*5 = 40.
Example 2:

Input: nums1 = [2,1,4,5,7], nums2 = [3,2,4,8,6]
Output: 65
Explanation: We can rearrange nums1 to become [5,7,4,1,2]. The product sum of [5,7,4,1,2] and [3,2,4,8,6] is 5*3 + 7*2 + 4*4 + 1*8 + 2*6 = 65.
Constraints:

n == nums1.length == nums2.length
1 <= n <= 105
1 <= nums1[i], nums2[i] <= 100

https://medium.com/@k.manu00005/google-amazon-1874-minimize-product-sum-of-two-arrays-291cb5daacc0

```

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.PriorityQueue;

public class Solution {
  //greedy question : greedy + 相向雙指針
  // 局部最優：最小數*最大數 乘積最小，推導全劇最優
  // TC:O(n*logn)
  // SC:O(1)
  public int minProductSum(int[] nums1, int[] nums2) {
    int sum = 0;
    //升序排序
    Arrays.sort(nums1);
    Arrays.sort(nums2);
    int i = 0;
    int j = nums2.length - 1;
    while (i <= nums1.length - 1 && j >= 0) {
      sum += nums1[i] * nums2[j];
      i++;
      j--;
    }
    return sum;
  }
}


public class Solution2 {
  //greedy question : greedy + 優先級隊列最大堆
  // 局部最優：最小數*最大數 乘積最小，推導全劇最優
  // TC:O(n*logn)
  // SC:O(m)
  public int minProductSum(int[] nums1, int[] nums2) {
    int sum = 0;
    //升序排序
    Arrays.sort(nums1);
    //使用nums2構造最大堆優先級隊列, 實際上相當於對nums2升序排序
    PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());
    for (int i: nums2){
        priorityQueue.add(i);
    }
    int i = 0;
    while (i <= nums1.length - 1 && !priorityQueue.isEmpty()) {
      sum += nums1[i] * priorityQueue.poll();
      i++;
    }
    return sum;
  }
}
```

```
title:  MinimizeProductSum
description: 1874. Minimize Product Sum of Two Arrays的變種， 給定一個數組,相鄰元素的最小乘積和

给定一个整数数组 arr,要实现以下数学公式,并使结果sum最小:

sum = arr[0] * arr[1] + arr[1] * arr[2] + ... + arr[n-3] * arr[n-2] + arr[n-2] * arr[n-1]

其中n是数组长度。

Input:  arr = [1, 10, 2, 7, 10, 6, 6]
Output: 127 
Explanation:

One of the optimal rearrangements is arr = [10, 1, 7, 6, 6, 2, 10], producing the result 10 * 1 + 1 * 7 + 7 * 6 + 6 * 6 + 6 * 2 + 2 * 10 = 127.
Constraints:
1 ≤ n ≤ 2 * 10^5
1 ≤ arr[i] ≤ 10^5
```

```java
import java.util.Arrays;

public class Solution {
    //greedy question : greedy + 雙指針
    // 局部最優：最小數*最大數 乘積最小，推導全劇最優
    public int findMinimumSum(int[] arr) {
        int n = arr.length;
        //升序排序
        Arrays.sort(arr);
        long sum = 0;
        //相向雙指針遍歷, 首尾分別取 最小值*最大值， 注意：由於是相鄰乘積，所以start需要遍歷到n-1,end需要遍歷到1
        int start = 0;
        int end = n - 1;
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                //偶數start++
                sum += (long) arr[start++] * arr[end];
            } else {
                //偶數end--
                sum += (long) arr[start] * arr[end--];
            }
        }
        return sum;
    }
}

//變種：如果是每兩個數乘積的最小和
// 给定一个整数数组 arr, 要实现以下数学公式, 并使结果sum最小:
//sum =arr[0]*arr[1]+arr[2]*arr[3]+...+arr[n-4]*arr[n-3]+arr[n-2]*arr[n-1]

//其中n是数组长度。(n為偶數長度)

public class Solution {
    //greedy question : greedy + 雙指針
    // 局部最優：最小數*最大數 乘積最小，推導全劇最優
    public int findMinimumSum(int[] arr) {
        int n = arr.length;
        //升序排序
        Arrays.sort(arr);
        long sum = 0;
        //相向雙指針遍歷, 首尾分別取 最小值*最大值， 注意：每兩個數乘積和最小值，所以start只需要相向遍歷到和end相遇即可
        int start = 0;
        int end = n - 1;
        while (start < end) {
            sum += (long) arr[star] * arr[end];
            start++;
            end--;
        }
        return sum;
    }
}
```