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


Q.4(459)    Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.


class Solution {
    public boolean repeatedSubstringPattern(String s) {
        boolean z=true;int c=1;
        String str="";String str1="";
        for(int i=0;i<s.length()-c;i++)
        {
         if(s.charAt(i)!=s.charAt(i+c))                         //finding the index from which repetition of substring start
         {
             c=c+1;
             i=0;
         }
        }
        str=s.substring(0,c);
        if(2*c>s.length())
        {
        str1=s.substring(c);
        }
        else
            str1=s.substring(c,2*c); 
            if(str1.equals(str) && str.equals(s.substring(s.length()-c)))         //Condition to check whether that substring sequence repeat or not
                return true;
        else 
            return false;
    }
}


M2.    
char[] chars = s.toCharArray();
int n = chars.length;

for (int size = 1; size <= n / 2; size++) {
  if (n % size != 0)                                      //finding all substring possible length which can repeat
  {                                
	continue;
  }
  boolean found = true;
  for (int i = 0, j = i + size; j < n; ++i, ++j) {          //Checking whether above length of string is repeating or not
	if (chars[i] != chars[j]) {
	  found = false;
	  break;
	}
  }
  if (found) {
	return true;
  }
}
return false;

Q.5(168) Given a positive integer, return its corresponding column title as appear in an Excel sheet.

class Solution {
    public String convertToTitle(int n) 
    {String str="";int rem=0;
       for(int i=n;i>0;i=(i-1)/26)
       {
           rem=(i-1)%26+1;                        //otherwise instead of returning 26 it was returning zero
           str=(char)(rem+64)+str;
       }
            
        
        return str;
    }
}


Q.6(171)  Given a column title as appear in an Excel sheet, return its corresponding column number.

class Solution {
    public int titleToNumber(String s) {
        int x=0,sum=0,c=1,y=0;String str="";
        for(int i=s.length()-1;i>=0;i--)
        {
           x=(int)(s.charAt(i));
            y=x-64;
               sum=sum+y*c;
            c=c*26;
        }
        return sum;
    }
}


Q.7(223). Find the total area covered by two rectilinear rectangles in a 2D plane.
         Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.
	 
	 class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int area=0,area1=0,c1=0,c2=0;
        int len1=C-A;
        int breadth1=D-B;
        int len2=G-E;
        int breadth2=H-F;
        if((E>=A && E<=C)||(G>=A && G<=C)||(E<=A)&&(G>=C))        //condition only to reduce the no of iteration
        {
       for(int i=A;i<=C;i++)                                       //To find the common x axis length
       {
           for(int j=E;j<=G;j++)
           {
               if(i==j)
                   c1++;
           }
       }
        }
        if((F>=B && F<=D)||(H>=B && H<=D)||(F<=B)&&(H>=D))                //condition only to reduce the no of iteration
        {
        for(int i=B;i<=D;i++)                                       //to find common y axis length
       {
           for(int j=F;j<=H;j++)
           {
               if(i==j)
                   c2++;
           }
       }
        }
        if(c1>0 && c2>0)
        area1=(c1-1)*(c2-1);
        else
            area1=c1*c2;
        
        area=len1*breadth1+len2*breadth2-area1;                   //total area equal to area of first rectangle plus area of second rectangle minus area of common portion
        return area;
    }
}


M2.
public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        int overlap = 0;
        
		// two window does not overlaps if ones start is greater thatn the others end 
        if(!(C < E || A > G || D < F || B > H)){ 
            int h = Math.min(D, H) -Math.max(B,F);
            int l = Math.min(C, G) -Math.max(A,E);  
            overlap = h*l;
        }
	// area 1 + area2 - common area
        return (C-A) *(D -B) + (G -E)*(H -F) - overlap;
    }


Q.8(557).Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

class Solution {
    public String reverseWords(String s) {
        String strarr[]=s.split(" ");
        String str1="";
        for (int i=0;i<strarr.length;i++)
        {
            String str="";
            for(int j=strarr[i].length()-1;j>=0;j--)
            {
                str=str+strarr[i].charAt(j);                       //reversing particular word
            }
         str1=str1+" "+str;                                    //concatination of reverses word with whitespace
        }
        return str1.trim();
    }
}
