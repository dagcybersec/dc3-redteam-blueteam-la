## Commands Used (Blue Team)

### View Apache Logs

cat /var/log/apache2/access.log

### Filter Suspicious Requests

cat /var/log/apache2/access.log | grep "cmd="

### Detect SQL Injection Patterns

cat /var/log/apache2/access.log | grep "list[fullordering]"

### Identify Automated Tools (sqlmap)

cat /var/log/apache2/access.log | grep "sqlmap"

### Check HTTP 500 Errors

cat /var/log/apache2/access.log | grep "500"

cat /var/log/apache2/access.log | grep "cmd="
