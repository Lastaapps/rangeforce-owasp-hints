# OWASP Range force hints

The hints are provided with no warranty, they will not be updated (by me) and
may top working after some time. Also, don't fire any issues, they will be
ignored, just ask your classmates. I don't have to care anymore. Don't forget
to star if you found this useful. PR with updates may be accepted (hints only,
not complete solutions).

Before you start do as many other modules. These OWASP challenges require good
previous knowledge of both "hacking" and Unix/Linux. This hints also expect
that you have at least basic knowledge/experience.

Good luck and have fun.



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
- Clone the project from GitHub. Go into the backend folder.
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



## 3: Injection

### Command Injection
- See prerequisites first. This one is really trivial.
- On Unix systems `;` can be used to separate commands.
- See `ping` man page and command usage. What is always the last part of the command?
- `destination` is the last parameter - the place to do the injection.
- Command to create files on Linux is `touch`.

### Template Injection
- Open the web and locate field that returns/processes something.
- It's the shipping field.
- Try editing the URL part with the search query. Input some random data and
  see the error message. Try to guess the language the server is written in.
- Web seems to be written using Python.
- One of the most common Python template library is Jinja2.
- Search on the web for Jinja2 template injection.
- [Possible solution, not the best
  one](https://kleiber.me/blog/2021/10/31/python-flask-jinja2-ssti-example/).

### Second-Order SQL Injection
- See prerequisites first.
- Try to play with `;` while creating account and login in.
- You can discover that SQL injection is hidden inside the `username` field.
- Construct the `union select` query showing the data.
- What is a possible name of table with data about *users*? What can be the
  column name for *password*s?
- It depends on the order and number of columns selected.



## 4: Insecure Design

### Unrestricted File Upload
- You can upload any files.
- We can make a guess that the website is written in PHP.
- Try uploading some PHP web shell (find some on the internet) and view the uploaded file.

### Exposed Credentials
- Use Firefox of Burp, we need to edit requests.
- See how does request done by the spellchecker look like.
- Let's try querying different collection.
- You can delete some query parameters.

### HTTP Request Smuggling
- Read on the net what it actually is.
- [Blog](https://regilero.github.io/english/security/2019/10/17/security_apache_traffic_server_http_smuggling/).
- There are 3+ ways to exploit this.
- The guest book is the only way to get data back.
- Use Burp. You may need to disable `Content-length` auto update at some point
  (depends on the approach).
- The second request should be POST request into the guestbook.
- Send the request few times and see the quest book if you caught something.



## 5: Security Misconfiguration

### Debug Mode
- Search for `Flusk debug mode RCE`.
- Enjoy your Python shell, it's not hard to create a file now.

### Directory Listing
- I expect you know what directory listing is.
- Look through both the `/api` and `/backend` files, one of them is the one.

### XML External Entities
- Exactly the same as the prerequisite.



## 6: Vulnerable and Outdated Components

### Vulnerable Component
- Run `nmap -sV --script=vulners.nse target`.
- Find exploit on port 80 with RCE.
- Use `msfconsole` to exploit it.

### Backdoored Component
- The backend server may be outdated.
- Look at the PHP version used.
- Find how to exploit the specific PHP version on internet (GitHub).

### Log4Shell
- See the prerequisite first.
- You will need to install `maven` to compile `rogue-jndi`.
- I used `msfconsole` to deliver malicious payload, search online. It should
  work also without, I guess.
- The home page is not vulnerable, you have to use another.



## 7: Identification and Authentication Failures

### Missing Authentication for Critical Function
- Just list then all, they don't check it even though they proclaim it.

### Brute Forcing
- Start with creating your own account.
- Is the password the only thing you can brute force?
- You can either write a simple python script, or use generate wordlist with
  numbers and use hydra.
- Make sure you are using right words/spelling and port.

### Session Fixation
- Image the server admin clicks on every link you send him.
- Image you are totally stupid developer.
- Image you decide that URL params can override your cookies.
- Image letting admin log with your session cookie.
- Image setting cookie with `NAME=value`.



## 8: Software and Data Integrity Failures

### Remote File Inclusion
- The page loads whatever URL you give it.
- If the file is PHP, it even gets executed.
- Would be pity if you crafted a file that executes some command when loaded by
  PHP.
- You can share it with `puthon -m http.server 80`

### Insecure Deserialization
- First try to find what is the difference between dark and light mode
  requests.
- Yes, a new cookie appeared.
- Try to guess/discover the language the server is written in.
- The language is Python.
- Try to find what is the most popular Python object serialization library.
- It's pickle. Try to find online how to abuse it.
- You want to abuse the `__reduce__` function.

### Code Download Without Integrity Check
- You can easily see how can the management download the unsecure code.
- The router is secure, no change of succeeding there.
- Is there a way how you would become 192.168.6.2?
- Did you ever hear of ARP?
- The answer is ARP spoofing. Set you ip address and use `aprspoof` command.
- Run your own https file server (search on web).



## 9: Security Logging and Monitoring Failures

### Sensitive Information in Log File
- See blue button page.
- This is really trivial path traversal.

### Log Forging
- You can guess the first part.
- Use `host=server` to view all the relevant logs.
- Copy one result from Spunk and edit it little.

### Sensitive Information in Log File
- ../../../../../
- Use gobuster in the dir or fuzz mode.
- The file extension is `.log`.



## 10: Server-Side Request Forgery

### Server-Side Request Forgery
- Just write a simple script in python/script, that sends the same request as
  the web page.
- The script can be just simple for loop with curl inside.
- You want to access `http://localhost:{port_number}`.
- Try ports in range 1-100.

### AWS Metadata SSRF
- Do the prerequisite first (and keep it opened).
- See where you can enter some kind of URL.
- Maybe the web hooks module could be exploited.

### SSRF Insecure Allowlist Bypass
- You were given another domain - try visiting it.
- Register your own domain.
- It would be beneficial for the domain to point to `localhost` (`127.0.0.1`).
- If you managed to register there a subdomain of `commensuratetechnology.com`,
  you would bypass the checks.
- The domain google.com and GOOGLE.COM

