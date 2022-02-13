# Logstash
logstash for PLURA


## RUN

### 1.1 run in foreground

    /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/70-postfix-plura.conf 

### 1.2 run in background

    nohup /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/70-postfix-plura.conf > /var/log/plura/app-postfix-nohup.log 2>&1 &


## 2.1 test_db

### sample code

    INSERT INTO employees(emp_no, birth_date, first_name, last_name, gender, hire_date) VALUES(120022, '1964-12-31', 'eliot', 'PLURA', 'M', '1984-12-31');
    
    INSERT INTO dept_manager(emp_no, dept_no, from_date, to_date) VALUES(120022, 'd009', '1984-12-31', '1988-10-17');
