# KMP Algorithm
### Prefix Function: max string with the both prefix and suffix of string S,but not S

> E.g:
> prefix(abacab) = "ab"
> prefix(ab) = ""

### what if we want to finad all prefix fn of S?

> well if s1 = max prefix(S)
  then s2 = prefix(s1) => prefix(prefix(S))

### KMP algo:

given S =>  calculate p[i] = prefix(S[0...i-1]) 

> S =    a  b  b a  a  b  b  a  b 
                                   
> p = -1  0  0  0  1  1  2  3  4  2 

if we want to calculate p[i](added x) = then we will iterate overall the prefixFun(pf) of p[i-1] until we find next position of that pf is x


```
class KMP:
    def partial(self, pattern):
        ret = [0]
        for i in range(1, len(pattern)):
            j = ret[i - 1]
            while j > 0 and pattern[j] != pattern[i]:
                j = ret[j - 1]
            ret.append(j + 1 if pattern[j] == pattern[i] else j)
        return ret

    def search(self, T, P):
        partial, ret, j = self.partial(P), [], 0
        
        for i in range(len(T)):
            while j > 0 and T[i] != P[j]:
                j = partial[j - 1]
            if T[i] == P[j]: j += 1
            if j == len(P): 
                ret.append(i - (j - 1))
                j = partial[j - 1]
            
        return ret
```
Ref: https://gist.github.com/m00nlight/daa6786cc503fde12a77