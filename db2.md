# DB2

Documentation
    https://aws.amazon.com/amis/ibm-db2-express-c-9-7-5-on-linux-64-bit-development-use-only
    https://www.assembla.com/spaces/revelytix-spyder/tickets/744

EC2 instance setup wizard

    Use large instance
    Specify DB2 security group
    create EBS volume (40GB) in *same availability zone* as instance)

Web config - setup AMI

    https://ec2-xx-xx-xx-xxx.compute-1.amazonaws.com/config
    upload foo.pem to authenticate
    use X.509 cert/key pair starting with cert-SRMZ...
    configure EBS volume - attach to existing EBS

DB2 Instance User

    username: <%=revelytix-aws-db2-instance.user%>
    group: <%=revelytix-aws-db2-instance.group%>
    password: <%=revelytix-aws-db2-instance.pwd%>
    
Fenced User

    username: <%=revelytix-aws-db2-fenced.user%>
    group: <%=revelytix-aws-db2-fenced.group%>
    pwd: <%=revelytix-aws-db2-fenced.pwd%>
    
DB name

    DB name: <%=revelytix-aws-db2-fenced.db-name%>
    
ssh to machine

    ssh -i foo.pem root@ec2-107-20-85-48.compute-1.amazonaws.com

db2 shell:

    cd /home/spyder/sqllib/bin/
    rcdb2 status|restart|stop|start
    su spyder
    ./db2
    db2 => create database foo
    db2 => connect to foo
    db2 => create schema goo create table person (name varchar(255), birthtime timestamp
    db2 => INSERT INTO "PERSON" ( "NAME", "BIRTHTIME" ) VALUES ( 'Billy', '2000-07-31-10.30.15.610208' )
    db2 => INSERT INTO "PERSON" ( "NAME", "BIRTHTIME" ) VALUES ( 'Joe', '2020-07-31-10.30.15.610208' )
    db2 => quit

    db2 => list tables for user
    db2 => list tables for schema SCHEMA_NAME

    db2 => describe table person
    db2 => drop table TABLE
    db2 => drop schema SCHEMA restrict

    create schema LSW01D create table WHDIAGNOSTIC_MCRVW (WHKEY INTEGER, DIAGNOSIS varchar(255))
    insert into "LSW01D"."WHDIAGNOSTIC_MCRVW" ("WHKEY", "DIAGNOSIS") VALUES (1, 'mumps')
    insert into "LSW01D"."WHDIAGNOSTIC_MCRVW" ("WHKEY", "DIAGNOSIS") VALUES (2, 'cold')

    select * from "LSW01D"."WHDIAGNOSTIC_MCRVW" 
    select * from "ICARUS"."LSW01D"."WHDIAGNOSTIC_MCRVW" 

    SELECT DISTINCT ('http://diagnostic/' || RTRIM(CAST("LSW01D"."WHDIAGNOSTIC_MCRVW".WHKEY AS CHAR(20)))) AS resourceid, "LSW01D"."WHDIAGNOSTIC_MCRVW".DIAGNOSIS AS object FROM "LSW01D"."WHDIAGNOSTIC_MCRVW"

