### 9. Palindrome Number

```ts
function isPalindrome(x: number): boolean {
    if(x<0) return false 
    const arrayofx = x.toString().split('');
    const lenghtOfArrayofX = arrayofx.length;
    for (let i = 0 ; i< lenghtOfArrayofX;i++) {
        const left = arrayofx[i];
        const right = arrayofx[(lenghtOfArrayofX - 1)- i]
        if(left !== right) return false
    }
    return true
};
```

### 1464. Maximum Product of Two Elements in an Array

```ts
function maxProduct(nums: number[]): number {
    const numLength = nums.length;
    const possiblePair = [];
    let max = 0;

    for(let i = 0 ; i<numLength;i++) {
        const num = nums[i]
        for(let j= i+1; j<numLength;j++) {
            possiblePair.push([num , nums[j]])
        }
    }

    for(let pp of possiblePair) {
        const left = pp[0] 
        const right = pp[1]
        const productValue = (left-1)*(right-1)
        if(max<productValue) {
            max = productValue
        }
    }
    return max;
};
```

```ts
function maxProduct(nums: number[]): number { 
    if(nums.length<2) return 0;
    nums.sort((a : number , b: number) => b - a);
    return (nums[0] - 1) * (nums[1] -1);
}
```

### 3731. Find Missing Elements

```ts
function findMissingElements(nums: number[]): number[] {
    if(nums.length < 1 ) return [];

    let min = nums[0];
    let max = 0;
    const elementPresenSet = new Set();
    const missingNumber = [];

    for(let i = 0 ;i < nums.length; i++) {
        const num = nums[i];
        elementPresenSet.add(num)
        if(max < num ) max = num;
        if(num < min) min = num
    }
    
    for(let i = min; i < max; i++ ) {
        if(!elementPresenSet.has(i)) {
            missingNumber.push(i)
        }
    }
    return missingNumber
    
};
```

### 58. Length of Last Word

```ts
function lengthOfLastWord(s: string): number {
    const words = s.replace(/\s+/g , " ").split(' ');
    console.log(words);
    const lastWord = words[words.length - 1] ? words[words.length - 1] : words[words.length - 2];
    return lastWord.length;
    
};
```

### 263. Ugly Number

```ts
function isUgly(n: number): boolean {
    if(n <1) return false;
    let num = n;
    while(num >= 2) {
        if(num%2 === 0) num /= 2;
        else if(num%3 === 0) num /= 3;
        else if(num%5 === 0) num /= 5;
        else return false;
    }
    return true;
    
};
```

### 509. Fibonacci Number

```ts
function fib(n: number): number {
    if(n===0) return 0;
    if(n===1) return 1;
    return fib(n -1) + fib(n-2);
};
```

### 344. Reverse String

```ts
function reverseString(s: string[]): void {
    if(s.length < 1) return ;
    let left = 0 ; 
    let right = s.length -1;
    
   while(left < right) {
        const val =  s[left];
        s[left] = s[right];
        s[right] = val
        left++;
        right --;
   }
};
```

### 3760. Maximum Substrings With Distinct Start

```ts
function maxDistinct(s: string): number {
    return new Set(s.split('')).size
};
```

### 3069. Distribute Elements Into Two Arrays I

```ts
function resultArray(nums: number[]): number[] {
    const arr1 = [];
    const arr2 = [];
    for(let i = 0; i<nums.length; i++) {
        const num = nums[i];
        let arr1LastNum = arr1[arr1.length - 1]
        let arr2LastNum = arr2[arr2.length - 1]
        if(arr1LastNum === undefined) {
            arr1.push(num);
            continue;
        }

        if(arr2LastNum === undefined) {
            arr2.push(num);
            continue;
        }

        if(arr1LastNum > arr2LastNum) arr1.push(num);
        else arr2.push(num);
    }

    return [...arr1 , ...arr2]
};
```

### 3718. Smallest Missing Multiple of K

```ts
function missingMultiple(nums: number[], k: number): number {
    const number = new Set(nums);
    for(let i= 1 ; i<=nums.length;i++) {
        const reqNum = k*i;
        if(!number.has(reqNum)) return reqNum;
    }
    return k * (nums.length + 1)
};
```

### 258. Add Digits

```ts
function addDigits(num: number): number {
    if(num<10) return num;
    return addDigits(num.toString().split('').reduce((a,b) => Number(a)+Number(b) , 0))
};
```



### 48. Rotate Image

```ts
function rotate(matrix: number[][]): void {
    const rotatedMatrix = [];

    for (let i = 0; i < matrix.length; i++) {
        const row = [];
        for (let j = 0; j < matrix.length; j++) {
            row.push(matrix[j][i])
        }
        rotatedMatrix.push(row.reverse())
    }

    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix.length; j++) {
            matrix[i][j] = rotatedMatrix[i][j]
        }
    }
};
```

### 383. Ransom Note

```ts
function canConstruct(ransomNote: string, magazine: string): boolean {
    const magazineCharCount = new Map();

    for(let i = 0 ; i< magazine.length; i++) {
        if(magazineCharCount.has(magazine[i])) {
            magazineCharCount.set(magazine[i] , magazineCharCount.get(magazine[i]) + 1);
        } else {
            magazineCharCount.set(magazine[i] , 1)
        }
    }

    for(let i = 0 ; i< ransomNote.length; i++) {
        if(magazineCharCount.has(ransomNote[i]) && magazineCharCount.get(ransomNote[i]) > 0 ) {
            magazineCharCount.set(ransomNote[i] , magazineCharCount.get(ransomNote[i]) - 1);
        }else {
            return false;
        }

    }
    return true;
};
```

### 27. Remove Element

```ts
function removeElement(nums: number[], val: number): number {
    let k = 0;

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== val) {
            nums[k] = nums[i];
            k++;
        }
    }

    return k;
}
```

### 3895. Count Digit Appearances

```ts
function countDigitOccurrences(nums: number[], digit: number): number {
    let digitCount = 0;
    const digitStr = digit.toString();
    for(let char of nums.join('')) {
        if(char === digitStr) digitCount++;
    }
    return digitCount;
};
```

### 26. Remove Duplicates from Sorted Array

```ts
function removeDuplicates(nums: number[]): number {
    let filledIndex = 1;

    for (let i = 1; i < nums.length; i++) {
        if (nums[i] !== nums[filledIndex - 1]) {
            nums[filledIndex] = nums[i];
            filledIndex++;
        }
    }

    return filledIndex;
}
```

### 179. Largest Number

```ts
function largestNumber(nums: number[]): string {
    const largestValue = nums.sort((a, b) => {
        const ab = a.toString() + b.toString();
        const ba = b.toString() + a.toString();

        return ba.localeCompare(ab);
    }).join('');
    return largestValue[0] !== '0' ? largestValue : '0'

};
```

### 3875. Construct Uniform Parity Array I

```ts
function uniformArray(nums1: number[]): boolean {
    const num2Even = [];
    const num2Odd = [];
    for (let i = 0; i < nums1.length; i++) {
        const num = nums1[i];
        if (num % 2 === 0) {
            num2Even.push(num);
            for (let j = 0; j < nums1.length; j++) {

                if (i === j) continue;

                if ((num - nums1[j]) % 2 !== 0) {
                    num2Odd.push(num - nums1[j])
                    break;
                };
            }

        }
        else {
            num2Odd.push(num);
            for (let j = 0; j < nums1.length; j++) {
                if (i === j) continue;
                if ((num - nums1[j]) % 2 === 0) { num2Even.push(num - nums1[j]); break }
            }
        }
    }
    return nums1.length === num2Even.length || nums1.length === num2Odd.length ? true : false

};
```

### 13. Roman to Integer

```ts
function romanToInt(s: string): number {
    let num = 0;
    const romanRepresentation = {
        "I": 1,
        "V": 5,
        "X": 10,
        "L": 50,
        "C": 100,
        "D": 500,
        "M": 1000
    }

    for (let i = s.length - 1; i >= 0; i--) {
        if (romanRepresentation[s[i]] < romanRepresentation[s[i + 1]]) {
            num = num - romanRepresentation[s[i]];
        } else {
            num = num + romanRepresentation[s[i]];
        }
    }

    return num;
};
```

### 3903. Smallest Stable Index I

```ts
function firstStableIndex(nums: number[], k: number): number {
    let max = -Infinity;

    for(let i = 0 ; i< nums.length ; i++) {
        if(nums[i] > max) max = nums[i];
        let min = Math.min(...nums.slice(i))

        if((max - min) <= k) return i;
    }
    return -1;
};
```

### 3904. Smallest Stable Index II

```ts
function firstStableIndex(nums: number[], k: number): number {
    let max = -Infinity;
    let min = Math.min(...nums);

    if(nums.length === 1 && nums[0] ===0) return 0; 

    for(let i = 0 ; i<nums.length; i++) {
        if(max < nums[i]) max = nums[i];
        if(nums[i] === min) min = null;
        if(!((max - k) <= nums[i])) continue;
        if(!min) min = Math.min(...nums.slice(i));
        if((max - min ) <= k) return i;
    }
    return -1;
};
```

### 342. Power of Four

```ts
function isPowerOfFour(n: number): boolean {
    if (n <= 0) return false;

    while (n % 4 === 0) {
        n /= 4;
    }

    return n === 1;
}
```

### 75. Sort Colors

```ts
/**
 Do not return anything, modify nums in-place instead.
 */
function sortColors(nums: number[]): void {
    if(nums.length <= 1) return;
    const obj = {
        0 : 0,
        1 : 0 ,
        2 : 0
    }
    for(let i= 0 ; i<nums.length; i++){
        obj[nums[i]] = obj[nums[i]] + 1
    }
    
    const keys = Object.keys(obj).filter((key) => obj[key] >= 1);
    let sort = 0;

    for(let i= nums.length; i>0; i--){
        if( ((nums.length) - (obj[keys[keys.length-1]] + sort )) === i) {
            sort = sort + obj[keys[keys.length-1]];
            keys.pop();
            }
                nums[i - 1] = Number(keys[keys.length-1]);


    }

};
```


### 3870. Count Commas in Range

```ts
function countCommas(n: number): number {
    if(n<999) return 0;
    return n-999;
};
```

### 3871. Count Commas in Range II

```ts
function countCommas(n: number): number {
    if (n < 999) return 0;
    let commaCount = 0;

    if (n >= 999999999999999) {
        commaCount = commaCount + 5 * (n - 999999999999999);
        n = 999999999999999;
    }


    if (n >= 999999999999) {
        commaCount = commaCount + 4 * (n - 999999999999);
        n = 999999999999;
    }

    if (n >= 999999999) {
        commaCount = commaCount + 3 * (n - 999999999);
        n = 999999999;
    }

    if (n >= 999999) {
        commaCount = commaCount + 2 * (n - 999999);
        n = 999999;
    }

    if (n >= 999) {
        commaCount = commaCount + 1 * (n - 999);
        n = 999;
    }

    return commaCount;
};
```

### 231. Power of Two

```ts
function isPowerOfTwo(n: number): boolean {
    if(n <= 0) return false;
    if(n=== 1) return true;
    
    for(let i = 1; i<n; i++) {
        if(Math.pow(2 , i) === n) return true;
        if(Math.pow(2 , i) > n) return false;
    }    
};
```

### 17. Letter Combinations of a Phone Number

```ts
function letterCombinations(digits: string): string[] {
    const phone_board = {
        1: [], 2: ['a', 'b', 'c'], 3: ['d', 'e', 'f'],
        4: ['g', 'h', 'i'], 5: ['j', 'k', 'l'], 6: ['m', 'n', 'o'],
        7: ['p', 'q', 'r', 's'], 8: ['t', 'u', 'v'], 9: ['w', 'x', 'y', 'z']
    }

    let prevComb = [""];

    for(let i = 0 ; i<digits.length;i++) {
        const currentComb = [];
        for(let char of phone_board[digits[i]]) {
            for(let cc of prevComb) {
                currentComb.push(cc+char)
            }
        }
        prevComb = currentComb;
    }
    return prevComb;
};
```

### 155. Min Stack

```ts
class MinStack {
    _min = Infinity;

    stack: { val: number, min: number }[];

    constructor() {
        this.stack = [];
    }

    push(value: number): void {
        this._min = Math.min(this._min, value);
        this.stack.push({ val: value, min: this._min });
    }

    pop(): void {
        if (this.isEmpty()) {
            return;
        }
        this.stack.pop();
        if(this.isEmpty()) this._min = Infinity;
        else this._min = this.getMin();
    }

    top(): number {
        if (this.isEmpty()) return;
        return this.stack[this.stack.length - 1].val;
    }

    getMin(): number {
        if (this.isEmpty()) return;
        return this.stack[this.stack.length - 1].min;
    }

    isEmpty(): boolean {
        return this.stack.length === 0;
    }
}


/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(value)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```

### 69. Sqrt(x)

```ts
function mySqrt(x: number): number {
    if (x === 0) return 0;
    if (x <= 3) return 1;

    let num = 1;

    for (let i = 2; i <= x; i++) {
        // If (x / i) / i is less than 1, it means i * i > x
        if (((x / i) / i) < 1) {
            return num; // Return the last valid 'i' stored in num
        }
        
        num = i; // Update the closest valid integer square root
    }
    
    return num;
}
```

### 819. Most Common Word

```ts
function mostCommonWord(paragraph: string, banned: string[]): string {
    const wordWithOccurancesount = new Map();

    const bannedWord = new Set(banned);

    for (let w of paragraph.split(/[,.!?;'\s]+/)) {
        let word = w.toLowerCase();
        if (bannedWord.has(word) || !word) continue;
        if (wordWithOccurancesount.has(word)) {
            wordWithOccurancesount.set(word, wordWithOccurancesount.get(word) + 1);
        } else {
            wordWithOccurancesount.set(word, 1);
        }
    }
    return [...wordWithOccurancesount.entries()].sort((a, b) => b[1] - a[1])[0][0];
};
```

### 2396. Strictly Palindromic Number

```ts
function isStrictlyPalindromic(n: number): boolean {
    for(let i = 2; i<=(n - 2); i++) {
        if(n.toString(i) !== n.toString(i).split('').reverse().join('')) {
            return false;
        }
    }    
    return true;
};
```

### 3498. Reverse Degree of a String

```ts 
function reverseDegree(s: string): number {
    let sum = 0;
    for (let i = 0 ; i<s.length; i++) {
        sum += (123 - s[i].charCodeAt(0)) * (i + 1);
    }
    return sum;
};
```

### 2610. Convert an Array Into a 2D Array With Conditions

## solution 1 

```ts
function findMatrix(nums: number[]): number[][] {

    const matrixTrack = new Map();
    let matrix = [];
    for (let i = 0; i < nums.length; i++) {
        if (matrixTrack.has(nums[i])) {
            matrixTrack.set(nums[i], matrixTrack.get(nums[i]) + 1);
        } else {
            matrixTrack.set(nums[i], 0);
        }
        matrix[matrixTrack.get(nums[i])] =
            matrix[matrixTrack.get(nums[i])] ?
                [...matrix[matrixTrack.get(nums[i])], nums[i]] :
                [nums[i]];

    }
    return matrix;
};
```

## solution 2

```ts
function findMatrix(nums: number[]): number[][] {

    const matrixTrack = new Map();
    let obj = {};
    for (let i = 0; i < nums.length; i++) {
        if (matrixTrack.has(nums[i])) {
            matrixTrack.set(nums[i], matrixTrack.get(nums[i]) + 1);
        } else {
            matrixTrack.set(nums[i], 0);
        }

        if (obj[matrixTrack.get(nums[i])]) {
            obj[matrixTrack.get(nums[i])].push(nums[i]);
        } else {
            obj[matrixTrack.get(nums[i])] = [nums[i]];
        }

    }
    return Object.values(obj);
};
```

### 1561. Maximum Number of Coins You Can Get

```ts
function maxCoins(piles: number[]): number {
    let max = (piles.length) - 2; 
    let sumOfCoins = 0;
    piles.sort((a : number , b: number) => a - b);
    for(let i = 0 ; i<(piles.length /3); i++) {
        sumOfCoins += piles[max];
        max -=2;
    };
    return sumOfCoins;    
};
```