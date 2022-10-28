# Missing letters
## Task
Find the missing letter in the passed letter range and return it.

If all letters are present in the range, return undefined.

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
function fearNotLetter(str) {
  var letters = "abcdefghijklmnopqrstuvwxyz";
  var start = letters.indexOf(str[0]);
  letters = letters.slice(start, start+str.length);
  if (str === letters){
    return undefined;
  } else {
    for (var x = 0; x < str.length; x++){
      if(str[x] !== letters[x]){
        return letters[x];
      }
    }
  }
}

fearNotLetter("stvwx");
```
