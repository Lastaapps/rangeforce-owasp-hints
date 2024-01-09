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


