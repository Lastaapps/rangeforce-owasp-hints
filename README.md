# OWASP Range force hints
The hints are provided with no warranty. Also don't fire any issues, they will be ignored,
just ask you friends.

## 1: Broken Access Control
### Path Traversal
- Go to the website.
- Locate the page, where files are loaded by their name (look into the URL).
- Try to load `secret.txt` (it wound work).
- You can see it's located in the articles folder.
- How can you go to the parent directory on Unix system?

### Direct Request
- Look through the webpage if there is something similar.
- Find the last financial report.
- There is no webpage for the new one, but the file may be still there.
- Open the report PDF.
- Search for date close to the one 

### Sensitive File in Web Root
- Open the webpage in browser first and look around.
- It's good to try to load an existing page with curl first.
- You can see that user agent is not accepted, try copying the agent from you browser.
- Not you can see that the login page is shown instead of your page.
- Think what may cause it.
- Yes, cookies again!
- You want to use `gobuster dir` mode (for directory search).
- Look into manual `gobuster dir --help` and set URL, word list, cookie (from browser) and User-Agent header.
- `gobuster` still complains, what a shame. Look in the manual.
- The option you need is `--exclude-length`.
- Look into the previous `gobuster` output.
- You found the file, just access it in the browser now.


## 2: Cryptographic Failures
### Use of Weak Hash
- Open the PhpMyAdmin and look through the database.
- Look for the table with user password hashes.
- No need to crack the MD5 hash.
- Try using web pages for cracking with hashes ready.
- I used [crackstation.net](https://crackstation.net) worked for me just fine.

### Hard-Coded Cryptographic Key
- Look through the code (backend) to find a secret.
- Try to understand how authentication works.
- Would be pity if you managed to seal your own credentials with a different role.
- Now open the website and find when are the credentials sent (Firefox recommended).
- They are sent on the resolve button press.
- We need to get `npm` working.
- Clone the project from Github. Go into the backend folder.
- Install hapi and iron - `npm install hapi iron`.
- Place your code into `server.js`. This way you don't have to deal with `npm`.
- Place the code right under the `init()` function declaration.
- You want to take code from the `auth.js`, both the `servet_key` and part of `authenticate` function.
- Run `npm start` and print the output with `console.log()`.
- Edit the request (Firefox only) or use curl with the new access token.

### PRNG Predictable Seed
- Sign up on the website.
- Find an interesting article describing how login works (and copy the code).
- You have to find correct session cookie.
- Write a simple python script that tries all the times from now in the **past**.
- You can use python requests library to do the request, check for status code 200.
- It should take about 20s to find the right session cookie.

