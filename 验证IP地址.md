# 验证IP地址

https://leetcode.cn/problems/validate-ip-address/solution/by-jiang-hui-4-qtsa/

```java
class Solution {
    public String validIPAddress(String queryIP) {
        if(queryIP.indexOf('.')>=0) return v4(queryIP)?"IPv4":"Neither";
        if(queryIP.indexOf(':')>=0) return v6(queryIP)?"IPv6":"Neither";
        else{
            return "Neither";
        }
    }

    private boolean v4(String queryIP){
        String[] array=queryIP.split("\\.",-1);
        if(array.length!=4) return false;
        for(String s: array){
            if(s.length()==0||s.length()>3) return false;
            if(s.charAt(0)=='0'&&s.length()!=1) return false;

            int ans=0;
            for(int i=0;i<s.length();i++){
                char c=s.charAt(i);
                if(!Character.isDigit(c)) return false;
                ans=ans*10+(c-'0');
            }

            if(ans>255) return false;
        }
        return true;
    }

    private boolean v6(String queryIP){
        String[] array=queryIP.split(":",-1);
        if(array.length!=8) return false;
        for(String  s:array){
            if(s.length()==0||s.length()>4) return false;
            for (int i=0;i<s.length();i++) {
                char c=s.charAt(i);
                if (!Character.isDigit(c) && !(Character.toLowerCase(c) >= 'a') || !(Character.toLowerCase(c) <= 'f')) return false;
            }
        }
        return true;
    }
}
