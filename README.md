Q.1 Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.

An interleaving of two strings s and t is a configuration where they are divided into non-empty substrings such that:

class Solution {
    public boolean isInterleave(String s1, String s2, String s3)
    {
      int m = s1.length(), n = s2.length();
	if (m + n != s3.length()) return false;

	// initializaion
	boolean[][] dp = new boolean[m + 1][n + 1];
	dp[0][0] = true;

	// function
	for (int i = 0; i <= m; i++) {
		for (int j = 0; j <= n; j++) {
			if (i > 0 && s1.charAt(i - 1) == s3.charAt(i + j - 1)) {
				dp[i][j] |= dp[i - 1][j];
			}
			if (j > 0 && s2.charAt(j - 1) == s3.charAt(i + j - 1)) {
				dp[i][j] |= dp[i][j - 1];
			}
		}
	}

	return dp[m][n];
}
}
