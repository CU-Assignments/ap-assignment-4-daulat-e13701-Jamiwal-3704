[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/o-KsyuFI)
# AP-ASSIGNMENT-4-DAULAT-E13701
Sorting and Searching
https://leetcode.com/problems/merge-sorted-array/

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1; 
        int j = n - 1; 
        int k = m + n - 1; 

        while (j >= 0) {
            if (i >= 0 && nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }
    }
};
```
![image](https://github.com/user-attachments/assets/8e4834b6-55b9-4a1b-bc26-756b0fcf2c7f)

https://leetcode.com/problems/first-bad-version/
```
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int left = 1;
        int right = n;

        while (left < right) {
            int mid = left + (right - left) / 2; 

            if (isBadVersion(mid)) {
                right = mid; 
            } else {
                left = mid + 1; 
            }
        }

        return left; 
    }
};
```
![image](https://github.com/user-attachments/assets/307cb9aa-33a7-4089-92d9-0541aa2df5a7)

https://leetcode.com/problems/sort-colors/

```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;
        int mid = 0;
        int high = nums.size() - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
               swap(nums[low], nums[mid]);
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else { // nums[mid] == 2
               swap(nums[mid], nums[high]);
                high--;
            }
        }
    }
};
```
![image](https://github.com/user-attachments/assets/04b8e9c7-56b7-47fb-87f7-5ecc16f9041b)

https://leetcode.com/problems/top-k-frequent-elements/

```
class Solution {
public:
    std::vector<int> topKFrequent(std::vector<int>& nums, int k) {
        // 1. Count the frequency of each element
        std::unordered_map<int, int> frequencyMap;
        for (int num : nums) {
            frequencyMap[num]++;
        }

        // 2. Create a min-heap (priority queue)
        std::priority_queue<std::pair<int, int>,
                            std::vector<std::pair<int, int>>,
                            std::greater<std::pair<int, int>>> minHeap;

        // 3. Populate the min-heap
        for (auto const& [num, frequency] : frequencyMap) {
            minHeap.push({frequency, num}); // Push {frequency, num}

            if (minHeap.size() > k) {
                minHeap.pop(); // Keep only the top k frequent elements
            }
        }

        // 4. Extract the top k elements from the min-heap
        std::vector<int> result;
        while (!minHeap.empty()) {
            result.push_back(minHeap.top().second); // Get the number (second element of pair)
            minHeap.pop();
        }

        // 5. Reverse the result to get the elements in descending order of frequency
        std::reverse(result.begin(), result.end());

        return result;
    }
};
```
![image](https://github.com/user-attachments/assets/b05e99ee-1bc0-4f4e-b18d-505612471d36)

https://leetcode.com/problems/kth-largest-element-in-an-array/
```
class Solution {
public:
    int findKthLargest(std::vector<int>& nums, int k) {
        std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap; // Min-heap

        for (int num : nums) {
            minHeap.push(num);
            if (minHeap.size() > k) {
                minHeap.pop();
            }
        }

        return minHeap.top();
    }
};
```
![image](https://github.com/user-attachments/assets/35985fed-c3cf-4f10-8ac7-2757fe52c67a)

https://leetcode.com/problems/find-peak-element/

```
class Solution {
public:
    int findPeakElement(std::vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] < nums[mid + 1]) {
                // Peak is to the right
                left = mid + 1;
            } else {
                // Peak is at mid or to the left
                right = mid;
            }
        }

        return left; // left == right, which is the peak index
    }
};
```
![image](https://github.com/user-attachments/assets/e4142c93-b075-4742-bb1e-b0a5d9b2aaef)

https://leetcode.com/problems/search-for-a-range/

```
class Solution {
public:
    std::vector<std::vector<int>> merge(std::vector<std::vector<int>>& intervals) {
        if (intervals.empty()) {
            return {};
        }

        // Sort intervals based on start times
        std::sort(intervals.begin(), intervals.end(), [](const std::vector<int>& a, const std::vector<int>& b) {
            return a[0] < b[0];
        });

        std::vector<std::vector<int>> merged;
        merged.push_back(intervals[0]);

        for (int i = 1; i < intervals.size(); ++i) {
            std::vector<int>& currentInterval = intervals[i];
            std::vector<int>& lastMergedInterval = merged.back();

            if (currentInterval[0] <= lastMergedInterval[1]) {
                // Overlapping intervals
                lastMergedInterval[1] = std::max(lastMergedInterval[1], currentInterval[1]);
            } else {
                // Non-overlapping intervals
                merged.push_back(currentInterval);
            }
        }

        return merged;
    }
};
```
![image](https://github.com/user-attachments/assets/bcff2638-d815-48e4-8666-576771804296)

https://leetcode.com/problems/merge-intervals/

```
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int s=0;
        int e=nums.size()-1;
        while(s<=e){
            int mid=s+(e-s)/2;
            if(nums[mid]==target){
                return mid;
            }
            if(nums[s]<=nums[mid]){
                if(nums[s]<=target&&target<=nums[mid]){
                    e=mid-1;
                }
                else{
                    s=mid+1;
                }
            }
            else{
            
                if(nums[mid]<=target&&target<=nums[e]){
                    s=mid+1;
                }
                else{
                    e=mid-1;
                }
            }
        }
        return -1;
    }
};
```
![image](https://github.com/user-attachments/assets/83a5c7e1-9c20-49f6-af94-92d804365f5e)

https://leetcode.com/problems/search-in-rotated-sorted-array/

```
class Solution {
public:
    bool searchMatrix(std::vector<std::vector<int>>& matrix, int target) {
        if (matrix.empty() || matrix[0].empty()) {
            return false;
        }

        int rows = matrix.size();
        int cols = matrix[0].size();

        int row = 0;
        int col = cols - 1; // Start from the top-right corner

        while (row < rows && col >= 0) {
            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] < target) {
                // Target is greater, move down to the next row
                row++;
            } else {
                // Target is smaller, move left to the previous column
                col--;
            }
        }

        return false; // Target not found
    }
};
```
![image](https://github.com/user-attachments/assets/3ac1efc1-8e9c-4ac2-8a41-3bf73b2dd828)

https://leetcode.com/problems/search-a-2d-matrix-ii/

```
class Solution {
public:
    int kthSmallest(std::vector<std::vector<int>>& matrix, int k) {
        int n = matrix.size();
        std::priority_queue<int> maxHeap; // Max-heap to store k smallest elements

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                maxHeap.push(matrix[i][j]);
                if (maxHeap.size() > k) {
                    maxHeap.pop();
                }
            }
        }

        return maxHeap.top();
    }
};
```
![image](https://github.com/user-attachments/assets/13087e85-ed47-4630-b2dc-6722e26b24fa)

https://leetcode.com/problems/wiggle-sort-2/
```
class Solution {
public:
    double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
        int m = nums1.size();
        int n = nums2.size();

        if (m > n) {
            // Ensure nums1 is the smaller array to optimize binary search
            return findMedianSortedArrays(nums2, nums1);
        }

        int low = 0;
        int high = m;
        int half = (m + n + 1) / 2; // Calculate half point

        while (low <= high) {
            int partitionX = (low + high) / 2;
            int partitionY = half - partitionX;

            int maxLeftX = (partitionX == 0) ? INT_MIN : nums1[partitionX - 1];
            int minRightX = (partitionX == m) ? INT_MAX : nums1[partitionX];

            int maxLeftY = (partitionY == 0) ? INT_MIN : nums2[partitionY - 1];
            int minRightY = (partitionY == n) ? INT_MAX : nums2[partitionY];

            if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
                // Found the correct partition
                if ((m + n) % 2 == 0) {
                    // Even number of elements
                    return (std::max(maxLeftX, maxLeftY) + std::min(minRightX, minRightY)) / 2.0;
                } else {
                    // Odd number of elements
                    return std::max(maxLeftX, maxLeftY);
                }
            } else if (maxLeftX > minRightY) {
                // Move partitionX to the left
                high = partitionX - 1;
            } else {
                // Move partitionX to the right
                low = partitionX + 1;
            }
        }

        return 0.0; // Should not reach here
    }
};
```
![image](https://github.com/user-attachments/assets/fec64b1f-d4cf-4154-9fbf-22adabfa4d7d)

