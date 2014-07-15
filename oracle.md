# Oracle

ssh to EC2 instance using key [substitute proper DNS name]

    ssh -i foo.pem ubuntu@ec2-107-20-85-48.compute-1.amazonaws.com

Quick checklist

    ssh in
    screen
    change hostname (see below)
    restart Oracle (if necessary) (see below)
    sudo su oracle
    check tns listener (see below)

sudo change user

    sudo su oracle
    sudo su ubuntu

Oracle shell

    sqlplus 

log in as root

    sqlplus / as sysdba

log in as user

    sqlplus user/pwd

Oracle tns listener status. (Should *not* show no services running. Check 'hostname')

    lsnrctl status
    ifconfig

machine hostname

    hostname

change machine hostname (using info from ifconfig)

    sudo hostname ip-10-83-115-117

restart oracle (rather than directly invoke /etc/init.d/oracledb script) Need to restart after changing hostname.

    sudo service oracledb restart
    
Oracle jdbc url

    jdbc:oracle:thin:@[HOST][:PORT]:SID
    
You can find the SID/SERVICE name in your tnsnames.ora file

schema is case sensitive

Drop/reload .sql file

    sudo su oracle
    cd ~
    scp -i ~/.ssh/foo.pem nuge_cre.sql ubuntu@ec2-50-19-196-92.compute-1.amazonaws.com:/home/ubuntu/nuge_cre.sql
    sqlplus / as sysdba
    @/home/oracle/foo_main.sql  
    sqlplus <%=revelytix-aws-oracle-db.user%>/<%=revelytix-aws-oracle-db.pwd%>
    select count(table_name) from user_tables;    
