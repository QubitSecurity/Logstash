# Logstash
logstash for PLURA

## 1. Install Logstash

### 1.1 Install OpenJDK 11.x

    yum -y install java-11-openjdk java-11-openjdk-devel
    
    cat > /etc/profile.d/java11.sh <<EOF
    export JAVA_HOME=$(dirname $(dirname $(readlink $(readlink $(which javac)))))
    export PATH=\$PATH:\$JAVA_HOME/bin
    EOF
    
    source /etc/profile.d/java11.sh
    
    java --version
    
    alternatives --config java
    
### 1.2 Install Logstash

    cat > /etc/yum.repos.d/elasticsearch.repo <<EOF
    [elasticsearch-7.x]
    name=Elasticsearch repository for 7.x packages
    baseurl=https://artifacts.elastic.co/packages/7.x/yum
    gpgcheck=1
    gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
    enabled=1
    autorefresh=1
    type=rpm-md
    EOF

    yum -y install logstash

## 2. RUN Logstash

### 2.1 run in foreground

    /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/70-postfix-plura.conf 

### 2.2 run in background

    nohup /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/70-postfix-plura.conf > /var/log/plura/app-postfix-nohup.log 2>&1 &

## 3. Testing configuration
 
    /usr/share/logstash/bin/logstash --config.test_and_exit -f /etc/logstash/conf.d/70-postfix-plura.conf
    
    /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/70-postfix-plura.conf --path.settings /etc/logstash/

## 4. Example

### 4.1 sample code with test_db
#### https://github.com/datacharmer/test_db

    INSERT INTO employees(emp_no, birth_date, first_name, last_name, gender, hire_date) VALUES(120022, '1964-12-31', 'eliot', 'PLURA', 'M', '1984-12-31');
    
    INSERT INTO dept_manager(emp_no, dept_no, from_date, to_date) VALUES(120022, 'd009', '1984-12-31', '1988-10-17');


## X. Reference
##### https://logz.io/blog/debug-logstash/
##### https://www.elastic.co/guide/en/logstash/current/running-logstash-command-line.html#command-line-flags
##### https://github.com/logstash-plugins/logstash-patterns-core/tree/main/patterns/ecs-v1

##### https://grokdebug.herokuapp.com/
##### https://jsoneditoronline.org/
