public class minDistBtw3Equalelmts {

    //BruteFore - O(n3), O(1)
    public static int BruteForce(int nums[]) {
        int n = nums.length;
        int minDist = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] == nums[j] && nums[j] == nums[k]) {
                        int currDist = Math.abs(i - j) + Math.abs(j - k) + Math.abs(k - i);
                        minDist = Math.min(minDist, currDist);
                    }
                }
            }
        }
        return (minDist == Integer.MAX_VALUE) ? -1 : minDist;
    }

    public static void main(String args[]) {
        int nums[] = { 1, 1, 2, 3, 2, 1, 2 };
        System.out.println(BruteForce(nums));
    }
}
