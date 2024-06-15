### Title: # Sqlmap Tutorial in Depth | How to Use Sqlmap | SQL Injection With Sqlmap
Tags: #sql #sqli #sql-tools #sqlmap
Author: 
Reference: https://www.youtube.com/watch?v=QsMkQMKsIII

#### Notes
**Summary**: In depth tutorial on sqlmap
**Notes**:
- Techniques:
	  1. Boolean-based blind
	  2. Time based blind
	  3. Error based
	  4. Union query based
	  5. Stack queries
- Crawl  =>`--crawl <depth>` example `crawl 3`
- Batch =>By default ans will be selected. `sqlmap -u http://vuln.com/ --crawl 3 --batch`
- Techniques => for specific techniques. 
  <mark class="hltr-pink">exmaple.sh</mark>
```sh
sqlmap -u http://vuln.com/ --crawl 3 --technique="U"
```  
- Threads => nothing to talk about it.
- Risk => risk 3 can update the main database so use it cautiously. `--risk 3`
- Level => different level of testing. like on parameter then cookie then other places `--level <>`
- Verbosity `-v <number>`
	  0: Show only Python tracebacks, error and critical messages.
	  1: Show also information and warning messages.
	  2: Show also debug messages.
	  3: Show also payloads injected.
	  4: Show also HTTP requests.
	  5: Show also HTTP responses' headers.
	  6: Show also HTTP responses' page content.
- information gather
```sh
--current-user
--current-db
--hostname
--dbs => all database information
```
  - Working with database
	  - `-D <database> --tables` list all table of the given database
	  - `-D <database> -T <table> --dump` => dump all the data of that table
	  - `--columns ` get all the column of the given table
	  - `--dump-all` dumps all the data of a database
- `--output-dir="<path>"` save output in the directory
- `--headers="<>:<>"` add headers in the request.
- `--user-agent="<>"` give a user-agent like `chrome` or something like that. Watch the http::user-agent tutorial from mdn.
- `--mobile` provides mobile agents.
- `--list-tamper` list of tamper for firewall bypass
- `--tampar="<tamper-name>"`
- POST requests=>
	- `--forms` to find vulnerable forms
	- `--data` send data in post requests
- Proxy =>
	- `--proxy="127.0.0.8080"` 
	- reverse proxy
		```sh
		sqlmap -r <file-name> --batch
		```
		`<file-name>` is saved request file.
- 
```sh
--cookie => can give cookies from the actual request
--flush-session => session is cleared so that can try diff payloasd
--comment => find hidden comment

```
