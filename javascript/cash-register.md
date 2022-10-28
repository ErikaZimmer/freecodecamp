# Cash Register
## Task
Design a cash register drawer function checkCashRegister() that accepts purchase price as the first argument (price), payment as the second argument (cash), and cash-in-drawer (cid) as the third argument.

cid is a 2D array listing available currency.

The checkCashRegister() function should always return an object with a status key and a change key.

Return {status: "INSUFFICIENT_FUNDS", change: []} if cash-in-drawer is less than the change due, or if you cannot return the exact change.

Return {status: "CLOSED", change: [...]} with cash-in-drawer as the value for the key change if it is equal to the change due.

Otherwise, return {status: "OPEN", change: [...]}, with the change due in coins and bills, sorted in highest to lowest order, as the value of the change key.

| Currency Unit	| Amount|
|--|--|
| Penny	| $0.01 (PENNY)|
| Nickel	| $0.05 (NICKEL)|
| Dime	| $0.1 (DIME)|
| Quarter	| $0.25 (QUARTER)|
| Dollar	| $1 (ONE)|
| Five Dollars	| $5 (FIVE)|
| Ten Dollars	| $10 (TEN)|
| Twenty Dollars	| $20 (TWENTY)|
| One-hundred Dollars	$100 (ONE HUNDRED)|

See below for an example of a cash-in-drawer array:

[
  ["PENNY", 1.01],
  ["NICKEL", 2.05],
  ["DIME", 3.1],
  ["QUARTER", 4.25],
  ["ONE", 90],
  ["FIVE", 55],
  ["TEN", 20],
  ["TWENTY", 60],
  ["ONE HUNDRED", 100]
]

## Tests
- checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]) should return an object.
- checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]) should return {status: "OPEN", change: [["QUARTER", 0.5]]}.
- checkCashRegister(3.26, 100, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]) should return {status: "OPEN", change: [["TWENTY", 60], ["TEN", 20], ["FIVE", 15], ["ONE", 1], ["QUARTER", 0.5], ["DIME", 0.2], ["PENNY", 0.04]]}.
- checkCashRegister(19.5, 20, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) should return {status: "INSUFFICIENT_FUNDS", change: []}.
- checkCashRegister(19.5, 20, [["PENNY", 0.01], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 1], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) should return {status: "INSUFFICIENT_FUNDS", change: []}.
- checkCashRegister(19.5, 20, [["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]) should return {status: "CLOSED", change: [["PENNY", 0.5], ["NICKEL", 0], ["DIME", 0], ["QUARTER", 0], ["ONE", 0], ["FIVE", 0], ["TEN", 0], ["TWENTY", 0], ["ONE HUNDRED", 0]]}.

## Challenge Seed
```
function checkCashRegister(price, cash, cid) {
  let change;
  return change;
}

checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);
```
## Solution
```
function checkCashRegister(price, cash, cid) {
  var cashRegister = [
    ["PENNY",	0.01],
    ["NICKEL", 0.05],
    ["DIME", 0.1],
    ["QUARTER", 0.25],
    ["ONE", 1],
    ["FIVE", 5],
    ["TEN", 10],
    ["TWENTY", 20],
    ["ONE HUNDRED", 100]
  ];
  var returnCash = cash - price;
  var returnRegister = {status: null, change: []};
  var totalRegister = 0, resto = 0, cashValue = 0;
  for (var x = 0; x < cid.length; x++){
    totalRegister += cid[x][1];
  }
  if (totalRegister == returnCash){
    returnRegister.status = 'CLOSED';
    returnRegister.change = cid;
    return returnRegister;
  }
  if(totalRegister < returnCash){
    returnRegister.status = 'INSUFFICIENT_FUNDS';
    return returnRegister;
  } 
  for (var x = cid.length-1; x>-1 ; x--){
    resto = Math.floor(returnCash / cashRegister[x][1]);
    cashValue = cashRegister[x][1]*Math.round(resto);
    if (returnCash > 0 && returnCash <1){
      returnCash = Number(returnCash).toFixed(2);
    }
    if (resto >= 1 && cid[x][1]>0){
      if(cid[x][1]>=cashValue){
        returnCash -= cashValue;
        returnRegister.change.push([cid[x][0],cashValue])
      } else { 
        var valorInicial = cid[x][1];
        var control = 0;
        while(valorInicial !== 0){
          control += 1;
          valorInicial -= cashRegister[x][1];
          returnCash -= cashRegister[x][1];
        } 
        returnRegister.change.push([cid[x][0],cashRegister[x][1]*control])
      }
    }  
    if (returnCash === 0){
      returnRegister.status = 'OPEN';
      return returnRegister;
    }
    if (x === 0 && returnCash > 0) {
      returnRegister.status = 'INSUFFICIENT_FUNDS';
      returnRegister.change = [];
      return returnRegister;
    }
  }
}


checkCashRegister(3.26, 100, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]])
```
