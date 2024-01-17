---
toc: true
comments: true
layout: post
title: Bank Account Simulator
description: A cool bank account simulator that makes use of if and else statements paired with try and catch statements
type: hacks
courses: { compsci: {week: 4} }
---

<!-- 
Errors I encountered:
1. I was using a finally statement after the try catch statement to add to the total amount, without realizing that 'finally' made it so that any input would be added even if it was invalid
2. On line 59, I wrote 'document.getElementbyId' instead of 'document.getElementById' (capitalization error). Funnily enough, the catch statement actually displayed the error ('document.getElementbyId is not a function')and helped me fix it!
 -->

<p>Please deposit an amount between 1-1000 dollars</p>

<!-- Code to create the deposit button -->
<input id="demo" type="text">
<button type="button" onclick="deposit()">Deposit</button>
<p id="message"></p>

<!-- Withdrawal button -->
<p>Please withdrawal an amount less than what you have in your bank account<p>
<input id="demo1" type="text">
<button type="button" onclick="withdrawal()">Withdrawal</button>
<p id="message1"></p>
<!-- Displays the total amount of dollars in bank account -->
<p>Total: <span id="total">0</span> dollars</p>

<script>
//Sets amount in bank account to 0
var totalAmount = 0;

function deposit() {
  //Sets error display to empty
  const message = document.getElementById("message");
  message.innerHTML = "";
  let x = document.getElementById("demo").value;
  //Checks if the input is valid
  try { 
    if(x.trim() == "")  throw "empty";
    if(isNaN(x)) throw "not a number";
    x = Number(x);
    if(x > 1000)  throw "too much";
    if(x < 1)   throw "too little";

    //Updates if input is valid
    totalAmount += x;
    document.getElementById("total").textContent = totalAmount;
  }
  //If input is not valid, display the error
  catch(err) {
    message.innerHTML = "Deposit is " + err;
  }
}

function withdrawal() {
    //Sets error display to empty
  const message = document.getElementById("message1");
  message.innerHTML = "";
  let y = document.getElementById("demo1").value;
  //Checks if the input is valid
  try { 
    if(y.trim() == "")  throw "empty";
    if(isNaN(y)) throw "not a number";
    y = Number(y);
    if(y > totalAmount)  throw "too much";
    if(y < 1)   throw "too little";

    //Updates if input is valid
    totalAmount -= y;
    document.getElementById("total").textContent = totalAmount;
  }
  //If input is not valid, display the error
  catch(err) {
    message.innerHTML = "Withdrawal is " + err;
  }
}
</script>