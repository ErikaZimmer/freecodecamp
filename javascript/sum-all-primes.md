# Sum All Primes
## Task
A prime number is a whole number greater than 1 with exactly two divisors: 1 and itself. For example, 2 is a prime number because it is only divisible by 1 and 2. In contrast, 4 is not prime since it is divisible by 1, 2 and 4.

Rewrite sumPrimes so it returns the sum of all prime numbers that are less than or equal to num.

## Tests
- sumPrimes(10) should return a number.
- sumPrimes(10) should return 17.
- sumPrimes(977) should return 73156.

## Challenge Seed
```
function sumPrimes(num) {
  return num;
}

sumPrimes(10);
```
## Solution
```
function sumPrimes(num) {
  var total = 0, divisores = 0;
  for (var x = 1; x <= num; x++){
    for (var y = 1; y <= x; y++){
      if (x % y ==0 ){
        divisores++; 
      }
      }
      if (divisores <= 2){
        total += x;
    }
    divisores = 0
  }

  return total-1;
}

sumPrimes(10);
```
