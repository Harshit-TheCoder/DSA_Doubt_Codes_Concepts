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

### If there are two arrays and an inuequality given or some relation to relate two arrays, always combine the two arrays
     together using the inequality

### SOS DP ARRAY 
    


