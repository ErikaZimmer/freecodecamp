# Palindrome Checker
## Task
Return true if the given string is a palindrome. Otherwise, return false.

A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing.

Note: You'll need to remove all non-alphanumeric characters (punctuation, spaces and symbols) and turn everything into the same case (lower or upper case) in order to check for palindromes.

We'll pass strings with varying formats, such as racecar, RaceCar, and race CAR among others.

We'll also pass strings with special symbols, such as 2A3*3a2, 2A3 3a2, and 2_A3*3#A2.

## Tests
- fearNotLetter("abce") should return the string d.
- fearNotLetter("abcdefghjklmno") should return the string i.
- fearNotLetter("stvwx") should return the string u.
- fearNotLetter("bcdf") should return the string e.
- fearNotLetter("abcdefghijklmnopqrstuvwxyz") should return undefined.

## Challenge Seed
```
function fearNotLetter(str) {
  return str;
}

fearNotLetter("abce");
```
## Solution
```
function palindrome(str) {
  
  var oldString = str.toLowerCase().replace(/[^\w\s]|_/g,"").replace(/\s+/g,"");
  var newStr= oldString.split("").reverse().join("");
  
  var control = 0;
  for (var x = 0; x < oldString.length ; x++){
    if (oldString[x] === newStr[x]){
      control += 1;
    }
  }

  if (control === oldString.length){
    return true;
  } else {
    return false;
  }
}

palindrome("1 eye for of 1 eye."); 
```
