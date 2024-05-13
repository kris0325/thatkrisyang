--- 
title: 15. 3Sum
description: 15. 3Sum

slug: 15. 3Sum

date: 2024-05-12
image: 15.png
categories:
    - leetcode
tags:
    - hashtable
    - two-pointers
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/3sum/description/>


```
3Sum
Category	Difficulty	Likes	Dislikes
algorithms	Medium (34.46%)	30399	2815
Tags
array | two-pointers

Companies
adobe | amazon | bloomberg | facebook | microsoft

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
 

Constraints:

3 <= nums.length <= 3000
-105 <= nums[i] <= 105
```

```
/* 思路：solution1雙指針法 
        Notice that the solution set must not contain duplicate triplets.需要去重複,雙指針法比哈希表算法更簡單
 
       1.排序
       2.i去重複 i> 0 && nums[i] == nums[i-1],(三元數組內部元素可以重複，所以需要用後一個數與前一個數進行比較，
          並且從第二個數i=1開始，比如case[-1,-1,0], 所以不能使用條件nums[i] == nums[i+1]判斷，或漏掉，
          也就是說三元數組不能重複，但三元數組內部元素可以重複)
       3. i遍歷數組， 每次循環left= i+1; right = nums.length()-1,
       4. when( left < right), 
          nums[i] + nums[j] + nums[k] < 0 , 將left指針右移，
          nums[i] + nums[j] + nums[k] > 0 , 將right指針左移， 
       5. 直到找到三元數組，滿足 nums[i] + nums[j] + nums[k] == 0，
       6. 然後left | right 去重複  
            nums[left] == nums[left+1], left++;
            nums[right] == nums[right-1], right--;

    
       solution2 哈希表法

**/
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution1 {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            //剪枝， 排序後，第一個數大於零，則無法滿足條件，可以直接return
            if (nums[i] > 0) {
                return result;
            }
            // nums[i]去重
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = nums.length - 1;
            while (right > left) {
                if (nums[i] + nums[left] + nums[right] < 0) {
                    left++;
                } else if (nums[i] + nums[left] + nums[right] > 0) {
                    right--;
                } else if (nums[i] + nums[left] + nums[right] == 0) {
                    //收集滿足條件的三元數組
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    // left指針去重複
                    while (right > left && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    // right右指針去重複
                    while (right > left &&  nums[right] == nums[right - 1]) {
                        right--;
                    }
                    left++;
                    right--;
                }
            }
        }
        return result;
    }
}



class Solution2 {
    public List<List<Integer>> threeSum(int[] nums) {
	List<List<Integer>> result = new ArrayList<>();
	Arrays.sort(nums);

	for (int i = 0; i < nums.length; i++) {
		// 如果第一个元素大于零，不可能凑成三元组
		if (nums[i] > 0) {
			return result;
		}
		// 三元组元素a去重
		if (i > 0 && nums[i] == nums[i - 1]) {
			continue;
		}

		HashSet<Integer> set = new HashSet<>();
		for (int j = i + 1; j < nums.length; j++) {
			// 三元组元素b去重

            /**
            注意:元素b取去重時，需要考慮只有當當前元素nums[j]，
                與之前第一個元素nums[j-1]，之前第2個元素都相同時，
               也就是前三個元素都相同時，才需要考慮去重跳過。
               否則，只考慮 nums[j] == nums[j - 1]，會出現過度去重，漏掉正確答案。
               根本原因在於,三元組數組之間不能重複，但時單個三元組內部元素可以重複。

               例如：    
            /**
             * if (j > i + 2 && nums[j] == nums[j - 1]) {
			 	continue;
			   }
             * 
             * Wrong Answer:
              Input
                    nums =
                        [-2,0,1,1,2]

                    Output
                        [[-2,2,0]]

                    Expected
                        [[-2,0,2],[-2,1,1]]
            */ 

			if (j > i + 2 && nums[j] == nums[j - 1]&& nums[j - 1] == nums[j - 2] ) {
				continue;
			}

			int c = -nums[i] - nums[j];
			if (set.contains(c)) {
				result.add(Arrays.asList(nums[i], nums[j], c));
				set.remove(c); // 三元组元素c去重
			} else {
				set.add(nums[j]);
			}
		}
	}
	return result;
    }
}

// @lc code=end
```