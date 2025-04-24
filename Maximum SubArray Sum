class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # curr_sum = maxi = nums[0]

        # for num in nums[1:]:
        #     curr_sum = max(num,curr_sum+num)
        #     maxi = max(maxi,curr_sum)
        # return maxi  
        maxSum = nums[0]
        current = 0 
        for n in nums:
            if current < 0:
                current = 0
            current += n
            maxSum = max(maxSum , current)
        return maxSum
