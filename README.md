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

	 
Q.2(415) Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

class Solution {
    public String addStrings(String num1, String num2) {
        int carry = 0;
        int len1 = num1.length() - 1;
        int len2 = num2.length() - 1;String word="";
       // StringBuilder sb = new StringBuilder();
        while (len1 >= 0 || len2 >= 0) {
           int a = len1 < 0 ? 0 : num1.charAt(len1) - '0';
            int b = len2 < 0 ? 0 : num2.charAt(len2) - '0';
           
            int sum = a + b + carry;
            int num = sum % 10;
            carry = sum / 10;
            //sb.append(num);
            word=String.valueOf(num)+word;
            len1--;
            len2--;
        }
        if (carry == 1) {
           // sb.append("1");
            word="1"+word;
        }
      //  sb.reverse();
       // return sb.toString();
        return word;
    }
}



Q.3(450)  Given a word, you need to judge whether the usage of capitals in it is right or not.We define the usage of capitals in a word to be
right when one of the following cases holds:
All letters in this word are capitals, like "USA".All letters in this word are not capitals, like "leetcode".Only the first letter in this word is 
capital, like "Google".Otherwise, we define that this word doesn't use capitals in a right way.


class Solution {
    public boolean detectCapitalUse(String word) {
        int c=0,d=0; boolean z=true; boolean y=false;
        for(int i=0;i<word.length();i++)
        {
           char ch= word.charAt(i);
            int x=(int)ch;
            if(x>=65 && x<=90)
                c++;
            char ch1=word.charAt(0);
            int b=(int)ch1;
            if(b>=65 && b<=90)
            d=1;
        }
        if(c==1 && d==1 || c==word.length() ||c==0)                                           //if one character is in upper case then it must be first character
       // if(c==1 && Character.isUpperCase(word.charAt(0)) || c==word.length() ||c==0)
            return z;
        else
            return y;
        
    }
}
