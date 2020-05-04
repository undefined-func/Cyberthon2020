# Baba-OAuth

## Score: 120

## Description
It was reported that an intern managed to use a discount coupon from the intern's boss. The discount coupon feature is implemented with OAuth. The intern only had his own credentials and the username of his boss. You will be using Baba's Oauth web application for this challenge. Connect to http://p7ju6oidw6ayykt9zeglwyxired60yct.ctf.sg:2416 to try it out.

Find out what the intern did to access the boss's discount coupon to retrieve the flag.

Please refer to the provided details below.

Intern's credentials: - username = intern@baba.com - password = internP@ssw0rd123

Boss's credentials: - username = internBoss@baba.com

List of all the scopes that the OAuth server accepts:  
Y29tLmN5YmVydGhvbi5MQHpAbUAtZGkkYzB1bnQ=  
Y29tLmN5YmVydGhvbi5ENkB5LWRpJGMwdW50  
Y29tLmN5YmVydGhvbi5QMDA5LWRpJGMwdW50  
Y29tLmN5YmVydGhvbi5CQDEwckAtZGkkYzB1bnQ=  
Y29tLmN5YmVydGhvbi5CQGJALWRpJGMwdW50  
Y29tLmN5YmVydGhvbi5DQHIwdTZ1eS1kaSRjMHVudA==  
Y29tLmN5YmVydGhvbi5CMXUzbUBydC1kaSRjMHVudA==  
Y29tLmN5YmVydGhvbi5EaTVoMG4zNXRiMzMtZGkkYzB1bnQ=  
Y29tLmN5YmVydGhvbi5BMWloQGhALWRpJGMwdW50   
Y29tLmN5YmVydGhvbi5CQDBUQDAtZGkkYzB1bnQ=  

\* The scopes are encoded such that it is safe to use in the URL.

## Solution
First, let's try to login with the intern's username and password.

We are then brought to the page below:
![auth-token-intern](https://raw.githubusercontent.com/undefined-func/Cyberthon2020/master/Finals/Web%20Services/Baba-OAuth/src/auth_code_intern.png)

Let's try to input the authorization code and a scope.

And then input the access token given.

We then reach this page:
![good-try](https://github.com/undefined-func/Cyberthon2020/blob/master/Finals/Web%20Services/Baba-OAuth/src/good_try.png)

By trying every scope in order, we find that this scope `Y29tLmN5YmVydGhvbi5CQGJALWRpJGMwdW50` gives a different page.
![not-flag](https://github.com/undefined-func/Cyberthon2020/blob/master/Finals/Web%20Services/Baba-OAuth/src/not_flag.png?raw=true)

We then remember that the discount coupon was obtained from the boss' account. We also realised that the username is passed in as plaintext in the URL on the second page.  
<pre><code>http://p7ju6oidw6ayykt9zeglwyxired60yct.ctf.sg:2416/cyberthon/oauth/authenticate?userToken=XeouB_vEhDTNOBPCSgmRqUsm2Zw%3D&bgRequest=-GFDotEniPlR-R0Kz8eZceqUv01Hb29kIGpvYiBpbnZlc3RpZ2F0aW5nIHRoaXMhIE5vdGhpbmcgdG8gc2VlIGhlcmUuIFRoaXMgaXMganVzdCBoZXJlIHRvIG1ha2UgdGhlIHVybCBsb29rIHVubmVjZXNzYXJpbHkgbG9uZy4gMjAyMC0wNS0wNFQxNzoxMzowNy44MTQyNTA%3D&<b>username=intern%40baba.com</b>
</code></pre>

We then change the username to `internBoss@baba.com` in the URL to get the authorization code for the boss and use the scope that produced a different output earlier (`Y29tLmN5YmVydGhvbi5CQGJALWRpJGMwdW50`).
![auth-token-boss](https://github.com/undefined-func/Cyberthon2020/blob/master/Finals/Web%20Services/Baba-OAuth/src/auth_token_boss.png)
![flag](https://github.com/undefined-func/Cyberthon2020/blob/master/Finals/Web%20Services/Baba-OAuth/src/flag.png)

## Flag
`Cyberthon{@1w@ys_v@1id@t3_t0k3ns}`
