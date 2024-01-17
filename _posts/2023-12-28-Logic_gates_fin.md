---
title: Password Combiner
comments: true
description: My part of the project. It combines two passwords into one with logic gates
type: post
courses: { compsci: {week: 16} }
---

<body>
<!-- Collapsible button -->
<button type="button" class="collapsible">How the code works:</button>

<!-- Collapsible content with a textarea -->
<div class="content collapsible-content">
    <textarea placeholder="text">It takes in both passwords as ascii and then converts to unicode until finally going to binary. After combining the passwords, any unreadable ascii characters are removed based on the binary output of the logic gate and are filtered out before finally being displayed back as a single password. The shortest password is taken to avoid having to pad the end with zeros.</textarea>
</div>

<button type="button" class="collapsible">How to use the program:</button>

<!-- Collapsible content with a textarea -->
<div class="content collapsible-content">
    <textarea placeholder="text">Using this code is really quite simple and easy! First, enter in both passwords and then select the button for the logic gate you want to use to combine the two. There are images to guide you just in case you forget.</textarea>
</div>

<button type="button" class="collapsible">How code uses binary logic:</button>

<!-- Collapsible content with a textarea -->
<div class="content collapsible-content">
    <textarea placeholder="text">Code uses logic gates to combine the passwords at the binary level.</textarea>
</div>

<!-- JavaScript for collapsible functionality -->
<script>
    var coll = document.getElementsByClassName("collapsible");
    var i;
    for (i = 0; i < coll.length; i++) {
        coll[i].addEventListener("click", function() {
            this.classList.toggle("active");
            var content = this.nextElementSibling;
            if (content.style.display === "block") {
                content.style.display = "none";
            } else {
                content.style.display = "block";
            }
        });
    }
</script>
</body>
<style>
    #container {
        width: 800px;
        height: 400px;
        position: relative;
        background: #006400;
    }
    .animate {
        position: relative;
    }
    #animate1 {
        float: left;
        color: black;
    }
    #animate2 {
        float: right;
        color: black;
    }
    #animate3 {
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
    }
    #box {
        width: 200px;
        height: 100px;
        position: absolute;
        background: #8B0000;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        color: black;
        text-align: center;
    }
    /* Style the button that is used to open and close the collapsible content */
    .collapsible {
        background-color: #8B0000;
        color: white;
        cursor: pointer;
        padding: 18px;
        width: 100%;
        border: none;
        text-align: left;
        outline: none;
        font-size: 15px;
    }
    /* Add a background color to the button if it is clicked on (add the .active class with JS), and when you move the mouse over it (hover) */
    .active, .collapsible:hover {
        background-color: #006400;
        transition-delay: 0.01s;
    }
    /* Style the collapsible content. Note: hidden by default */
    .content {
        padding: 0 18px;
        display: none;
        overflow: hidden;
        background-color: #f1f1f1;
    }
    /* Style the textarea inside the collapsible content */
    .collapsible-content textarea {
        width: 100%;
        height: 100px;
        box-sizing: border-box;
        margin-top: 10px;
    }
</style>
<!-- Setting up the form for data entry -->
<form onsubmit="combinePasswords(event)">
    <label for="password1">Enter your first password</label><br>
    <input type="text" id="password1" name="password1"><br>
    <label for="password2">Enter your second password</label><br>
    <input type="text" id="password2" name="password2"><br>
    <input type="radio" id="and" name="gate" value="and">
    <label for="and">And Gate</label><br>
    <img src="https://media.discordapp.net/attachments/1138198617463730330/1181468296747429999/AND.webp?ex=65812b18&is=656eb618&hm=6d0583021058c70d1864ffdcdfb6ca25ba957fa269f64532f7b8b1d10ddc04f3&=&format=webp" alt="AND Gate" width="400" height="200"><br>
    <input type="radio" id="or" name="gate" value="or"><br>
    <label for="or">Or Gate</label><br>
    <img src="https://media.discordapp.net/attachments/1138198617463730330/1181468333263044680/OR.webp?ex=65812b21&is=656eb621&hm=98f9ec24a67731715b3a0126dda747165b4481f8c8013fedbedf55f531963ffd&=&format=webp" alt="OR Gate" width="400" height="200">
    <input type="submit" value="Submit">
</form>
<h2 id="combined"></h2>

<p><button onclick="move()">Start Animation</button></p>

<div id="container">
    <div id="animate1" class="animate">Password 1 goes here</div>
    <div id="animate2" class="animate">Password 2 goes here</div>
    <div>
        <p id="box">Logic gate goes here</p>
    </div>
    <div id="animate3" class="animate">Combined password goes here</div>
</div>

<script>
    function combinePasswords(event) {
        // Prevents from refreshing which would refresh the display for combined password
        event.preventDefault();
        //getting elements
        var password1= document.getElementById("password1").value;
        var password2 = document.getElementById("password2").value;
        var gateType = document.querySelector('input[name="gate"]:checked').value;
        // turns into binary using function
        var binary1 = textToBinary(password1);
        var binary2 = textToBinary(password2);
        var combined;
        //combines with and gate
        if (gateType == "and") {
            var combined = andGate(binary1, binary2);
        }
        else if (gateType == "or") {
            var combined = orGate(binary1, binary2);
        }
        console.log("First password: " + binary1);
        console.log("Second password: " + binary2);
        // displays
        document.getElementById("combined").innerHTML = "Combined password: " + binaryToText(combined);

        //animation code starts here
        document.getElementById("animate1").innerHTML = binary1;
        document.getElementById("animate2").innerHTML = binary2;
        document.getElementById("animate3").innerHTML = combined;
        document.getElementById("box").innerHTML = gateType + " gate";
    }
    function move() {
        //https://www.w3schools.com/js/js_htmldom_animate.asp
        let id = null;
        const element1 = document.getElementById("animate1");
        const element2 = document.getElementById("animate2");
        const element3 = document.getElementById("animate3");
        element1.style.visibility = "visible";
        element2.style.visibility = "visible";
        element3.style.visibility = "hidden";   
        let pos1 = 0;
        let pos2 = 0;
        clearInterval(id);
        id = setInterval(frame, 5);
        function frame() {
            if (pos1 == 200 || pos2 == 200) {
                clearInterval(id);
                document.getElementById("animate1").style.visibility = "hidden";
                document.getElementById("animate2").style.visibility = "hidden";
                element3.style.visibility = "visible";
            }
            else {
                pos1++;
                pos2++;
                //moves diagonal towards bottom right
                element1.style.top = pos1 + "px"; 
                element1.style.left = pos1 + "px";
                //moves diagonal towards bottom left
                element2.style.top = pos2 + "px";
                element2.style.right = pos2 + "px";
            }
        }
    }
    
    //https://stackoverflow.com/questions/14430633/how-to-convert-text-to-binary-code-in-javascript
    function textToBinary(text) {
        var binary = ""; 
        // for every character in the text
        for (var i = 0; i < text.length; i++) {
            var charBinary = "";
            // concat the binary version into the var "binary"
            //charCodeAt(0) retrieves the unicode character code of the character at i
            //.toString(2) converts unicode to binary
            charBinary += text[i].charCodeAt(0).toString(2);
            // pad with leading zeros
            while (charBinary.length < 8) {
                charBinary = "0" + charBinary;
            }
            // concat and adding necessary space
            binary += charBinary;
        }
        return binary.trim();
    }
    function binaryToText(binary) {
        var text = "";
        // Split the binary string into 8-bit chunks
        var binaryChunks = binary.match(/.{1,8}/g);
        // Convert each 8-bit chunk to decimal and then to ASCII
        for (var i = 0; i < binaryChunks.length; i++) {
            var decimalValue = parseInt(binaryChunks[i], 2);
            // Check if the ASCII character is printable
            if (decimalValue >= 32 && decimalValue <= 126) {
                text += String.fromCharCode(decimalValue);
            }
        }
        return text;
    }
    function andGate(binary1, binary2) {
        var result = "";
        var shorter = 0;
        // takes the longer one
        if (binary1.length >= binary2) {
            shorter = binary2;
        }
        else{
            shorter = binary1;
        }
        for (var i = 0; i < shorter.length; i++) {
            //if both 1 then return 1
            if(binary1[i] == "1" && binary2[i] == "1") {
                result += "1";
            }
            //otherwise return 0
            else{
                result += "0";
            }
        }
        return result;
    }
    function orGate(binary1, binary2) {
        var result = "";
        var shorter = 0;
        // takes the longer one
        if (binary1.length >= binary2) {
            shorter = binary2;
        }
        else{
            shorter = binary1;
        }
        for (var i = 0; i < shorter.length; i++) {
            //if both 1 then return 1
            if(binary1[i] == "1" || binary2[i] == "1") {
                result += "1";
            }
            //otherwise return 0
            else{
                result += "0";
            }
        }
        return result;
    }

</script>