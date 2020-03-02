# 0회차 스터디
`2020. 02. 22`

## Theme
Implementation

## Problem 1
### [valid palindrome](https://leetcode.com/problems/valid-palindrome/)
#### 찬용님
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
const alphbet = {
    'a': true,
    b: true,
    c: true,
    d: true,
    e: true,
    f: true,
    g: true,
    h: true,
    i: true,
    j: true,
    k: true,
    l: true,
    m: true,
    n: true,
    o: true,
    p: true,
    q: true,
    r: true,
    s: true,
    t: true,
    u: true,
    v: true,
    w: true,
    x: true,
    y: true,
    z: true,
    0: true,
    1: true,
    2: true,
    3: true,
    4: true,
    5: true,
    6: true,
    7: true,
    8: true,
    9: true,
}

var isPalindrome = function(s) {
  s = s.toLowerCase()
    .split('')
    .filter(c => alphbet[c])

  for (let i = 0, end = Number.parseInt(s.length/ 2) ;i < end; ++i) {
     const [f, l] = [s[i], s[s.length - i - 1]];
      console.log(f, l);
     if (f != l) return false;
  }
    return true;
};
```
> 정규식을 필요하면 찾자는 생각이라서 알고리즘 풀떄는 이런케이스는 외워두는게 필요할거 같네요

#### 보곤님
```javascript
const isPalindrome = s => {
    if (s.length === 0) return true;
    const lowerCaseS = s.toLowerCase();
    const filteredS = lowerCaseS.match(/\w/g);
    if (filteredS === null || filteredS === undefined) return true
    const length = filteredS.length;

    let reversedS = '', originalS = '';

    for (let i = 0; i < length; i++) {
      reversedS = filteredS[i] + reversedS;
      originalS = originalS + filteredS[i]
    }

    return reversedS === originalS
};
```
> Palindrome 문제를 푼 경험이 도움되었다.

## Problem 2
### [construct the rectangle](https://leetcode.com/problems/construct-the-rectangle/)
#### 찬용님
```javascript
/**
 * from 22
 * @param {number} area
 * @return {number[]}
 */
var constructRectangle = function(area) {
    /*
     * sameArea
     * W <= L
     * MIN(L - W)
     */
    let a = Math.sqrt(area);

    if (Number.isInteger(a)) return [a, a];
    else a = Number.parseInt(a);

    do {
        if (a == 1) return [area, 1];
        else if (area % a == 0) return [area / a, a];
    } while(--a)

};
```
> 에라토스테네스의 채가 떠올라서 이용해서 짧게 풀을 수 있었던거 같습니다. 

#### 보곤님
```javascript
var constructRectangle = function(area) {
    let w, l, quo, rest, gap = area, result = [];

    for (let i = 1; i <= area; i++) {
      quo = area / i;
      rest = area % i;
      if (rest === 0) {
        l = i;
        w = quo;
        if (l >= w) {
          if (l-w < gap) {

          gap = l-w;
        result.push(l,w)
          }
        }
      }
    };

    return result
};
```
> 약수를 구하는 방법이 키포인트였음. 특정한 공식이 있을거라고 예상하고 생각하다가 시간을 많이 소모함. 몫과 나머지로 문제 해결.

## Problem 3
### [longest substring](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
#### 찬용님
```javascript
/**
  from 52 + 10
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  let memo = {}
  let num = s[0] == s[1] ? 1 : 2;
  let ans = ''
  let temp = ''

  if (s.length == 0) return 0;
  if (s.length == 1) return 1;

    memo[s[0]] = true

  for (let i = 0, j = 1 ; j < s.length; j++) {
     let [f, l] = [s[i], s[j]]

     if (memo[l]) {
         while(i != j) {
             if (f == l) break;

             memo[f] = false;
             f = s[++i];
         }

         ++i;
     }

      memo[l] = true;
      num = eval(j - i + 1, num)
  }

    return num
};

const eval = (ans, temp) => ans > temp ? ans : temp;
```
> 제출하고보니 예전에 풀었던 문제였는데 예외 케이스를 고려하지않고 우선 풀어서 좀 예외케이스 부터 생각해보고 풀어야겠네요

#### 보곤님
```javascript
var lengthOfLongestSubstring = function(s) {
    if (!s) return 0;
    let longestWord = '';
    let uniqueWord = '';
    const length = s.length;
    for (let i = 0; i < length; i++) {
        if (longestWord.indexOf(s[i]) > -1) {
            longestWord = longestWord.slice(longestWord.indexOf(s[i])+1);
            longestWord += s[i];
        } else {
            longestWord += s[i]
        }

        if (longestWord.length > uniqueWord.length) {
            uniqueWord = longestWord;
        }

    }
    return uniqueWord.length
};
```
> 최근에 풀었던 문제라서 다시 검토함.
