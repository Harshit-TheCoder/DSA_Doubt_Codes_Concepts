### An Odd Number has divisors all of which are odd.

### To break a number in 'k' parts of different powers of 2, i.e, num = 2^a + 2^b + 2^c + .... k times EXACTLY,
    it is possible only if number of set bits in num <= k <= num

### In terms of bits, a number num always lies between [ b^k , b^(k+1) -1 ]
    Eg, if base is 4 then [4^0, 4^(0+1) - 1] -> 0 - 3
                          [4^1, 4^(1+1) - 1] -> 4 - 15
                          [4^2, 4^(2+1) - 1] -> 16 - 63 and so on

### XOR Basis Trick (Short Form)
    Purpose
    Represent all subset XORs compactly.
    Answer queries like max subset XOR, kth subset XOR, representability.
    Rules
    Insert Rule:
        For each number, reduce it with current basis (XOR out higher bits).
        If it becomes 0 → skip (dependent).
        Else put it in the basis at its MSB position.
        ✅ Reason: Ensures basis is linearly independent, like Gaussian elimination.
    Max XOR Rule:
        Start ans = 0.
        From high → low bits: if ans ^ basis[i] > ans, then do ans ^= basis[i].
        ✅ Reason: Always try to add higher-bit vectors if they increase the number.
    Representability Rule:
        To check if x is possible, reduce x using basis.
        If x ends as 0 → yes, else no.
        ✅ Reason: If x lies in the span of basis, it can be formed.
    Count Rule:
        If basis size = k, then number of distinct subset XORs = 2^k.
        ✅ Reason: Each basis element can be included or not, independently.
    Complexity
    Build basis: O(n · log(maxA))
    (Each number reduced by up to log(maxA) bits).
    Max XOR query: O(log(maxA))
    Representability check: O(log(maxA))
    Distinct count: just O(1) (2^k).

    for(int num: nums){
        for(int i=31;i>=0;i--){
            if((num & (1 << i)) == 0) continue;
            if(basis[i] == 0){
                basis[i] = num;
                break;
            }
            num ^= basis[i];
        }
    }

    int ans = 0;
    for(int i=31;i>=0;i--) ans = Math.max(ans, ans^basis[i]);

### If there are two arrays and an inuequality given or some relation to relate two arrays
     always combine the two arrays together using the inequality

### Difference Array Concept
    For range updates, we can use difference arrays to precalculate the range in O(n) time.
    int diff[] = new int[n]
    diff[l] += 1, diff[r+1] -= -1

### Remove some occurences of one character to make string palindrome
    i = 0, j= n-1
    See if s[i] == s[j] do i++; j--;
    else removal of either s[i] or s[j] will make string palidrome else string cannot be palindrome.
    string 0...i-1 and j+1 .... n-1 is already palindrome, 
    between i and j ignore wherever s[i] == s[j]. 
    if s[i] != s[j] and both are not character to be removed then return false.
    else simulate removing the character using two pointers till i<=j.

### Jump Array Concept
    In an array, [a1, a2, a3, a4, .... an] you have two operations,
    1. move ahead to a strictly smaller element 
    2. move behind to a strictly greater element
    calculate prefix max, suffix min array, 
    now for each element, 
    start from i=n-2 to i = 0.
    1. p[i] > s[i + 1] then let x = p[i], y = s[i+1] then it is always possible i -> x -> y -> (i+1) then ans[i] = ans[i+1]
    2. p[i] <= s[i + 1] then no valid jump is possible so ans[i] = p[i]

### Decrease Array Concept
    let a = [a1, a2, a3, ......, an], you have to choose two ai , aj,  i not = j and decrease both 1 and ultimately see if array can be 0.
    here two conditions are,
    1. Array sum must be even because everytime we are decreasing sum by 2.
    2. Also the largest element M must be M <= S - M where S is sum because to make M 0 we need atleast M 1's among other elements

### If we are given 3 binary strings and we have to arrange them in a way such that we get maximum binary number,
    Always remember for 2 strings s and t, iff s + t > t + s,
    Do brute force for 3 strings and do above operation for all 6 permutations.

### Find number of rectangles in binary matrix
    Start from top to bottom.
    At each level count height of histograms and count the rectangles using monotonic stack

### If there is a question, which has an array [ (l1, r1), (l2, r2) .... (ln ,rn) ] that is dealing with segments, always try focussing on intersection of segments and make use of difference array or difference map to handle segments effectively

### If we have to deal with trailing zeroes in a number, always think in power of 2's and 5's because number of trailing zeroes = Math.min(count(2), count(5)). If we have to multiply a given number of any number k <= m to maximise trailing zeroes, find out number of 2's and 5's in that number and multiply both that count(2) = count(5) equal in input number. then multiply by 10 till k*10 > m and then multiply m/k to maximize input.

### to make [p,q,r,s,t,u,v,w] -> [a,a,a,a,a,a,a,a] by adding remainder of number % 10, 
	0 -> 0
	1 -> 1,        2,4,8,6 now cycle
	2 ->           2,4,8,6 now cycle
	3 -> 3,6,      2,4,8,6 now cycle
	4 -> 4,8,6,    2,4,8,6 now cycle
	5 -> 5,0
	6 -> 6,        2,4,8,6 now cycle
	7 -> 7,4,8,6,  2,4,8,6 now cycle
	8 -> 8,6       2,4,8,6 now cycle
	9 -> 9,8,6     2,4,8,6 now cycle
	to make them equal for each number,  suppose a = p + residual(p%10) + n*20,   (p + residual(p%10)) for all numbers must give same remainder that set carrying all remainders must hae size 1.

### Apply Binary Search on Answer whenever you see "Minimize/Maximize X parameter" and "Search space is sorted" . Apply Binary Search on Search Space of X and try to calculate X value in helper function, and compare it with mid, always ask "Can given task be completed with given mid that satisfies X"

### Whenever an inequality is given, always look HOW TO SIMPLIFY THE GIVEN INEQUALITY?

### If there is 2D Matrix question, and you have to make use of Manhattan distance between two points, ALWAYS REMEMBER MANHATTAN DISTANCE BETWEEN ANY PAIR OF POINTS IS ALWAYS INDEPENDANT OF MANHATTAN DISTANCE BETWEEN OTHER PAIR OF POINTS. ALWAYS SEPARATE COORDINDATES TO X AND Y AND HANDLE DISTANCE OF X AND Y SEPARATELY.

### Always remember, if an array is given consisting of houses and gaps and you have to shift the house 1 unit left or right at a time to ultimately obtain largest gap and return minimum moves, ALWAYS REMEMBER MIDDLE HOUSE WILL NEVER MOVE.

### If we have to apply DP ON DIVISORS OF A NUMBER , ALWAYS REMEMBER FINDING DIVISORS OF ALL NUMBERS UPTO N COSTS ONLY O(NLOGN) , USE THIS WHILE DESIGNING DP TRANSITIONS

### WHENEVER AN ALGERBRAIC EQUATION RELATING ARRAY ELEMENTS WITH THEIR INDICES IS GIVEN, ALWAYS SIMPLIFY THAT GIVEN EQUATION
	
    

    
    


