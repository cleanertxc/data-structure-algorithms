# Description
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial)

# Note
- s could be empty and contains only lowercase letters a-z.
- p could be empty and contains only lowercase letters a-z, and characters like . or *.

# Example
Example 1:

Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
Example 2:

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
Example 3:

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
Example 4:

Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
Example 5:

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false

# Solution(DP)
```java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] memo =new boolean[s.length()+1][p.length()+1];
        for(int i=s.length();i>=0;i--){
            for(int j=p.length();j>=0;j--){
                if(j==p.length()){
                    memo[i][j]=i==s.length();
                }else{
                    char c=p.charAt(j);
                    if(j+1<p.length()&&p.charAt(j+1)=='*'){
                        memo[i][j]=memo[i][j+2]||(i!=s.length()&&match(s.charAt(i),c)&&memo[i+1][j]);
                        
                    }else{
                        memo[i][j]=i!=s.length()&&match(s.charAt(i),c)&&memo[i+1][j+1];
                    }
                }
            }
        }
        return memo[0][0];
    }
    
    private boolean match(char c,char p){
        return p=='.'?true:p==c;
    }
}
```
