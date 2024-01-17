---
title: Password Combiner
comments: true
description: My part of the project. It combines two passwords into one with logic gates
type: post
courses: { compsci: {week: 13} }
---

<form onsubmit="combinePasswords(event)">
    <label for="password1">Enter your first password</label><br>
    <input type="text" id="password1" name="password1"><br>
    <label for="password2">Enter your second password</label><br>
    <input type="text" id="password2" name="password2"><br>
    <input type="submit" value="Submit">
</form>
<p id="combined"></p>

<script>
    function combinePasswords(event) {
        event.preventDefault();
        var password1= document.getElementById("password1").value;
        var password2 = document.getElementById("password2").value;
        document.getElementById("combined").innerHTML = "Combined password: " + password1 + password2;
    }
</script>