hadoop fs -ls /user/hive/warehouse/original_access_logsCREATE EXTERNAL TABLE intermediate_access_logs (<br/>
    ip STRING,<br/>
    date STRING,<br/>
    method STRING,<br/>
    url STRING,<br/>
    http_version STRING,<br/>
    code1 STRING,<br/>
    code2 STRING,<br/>
    dash STRING,<br/>
    user_agent STRING)<br/>
ROW FORMAT SERDE 'org.apache.hadoop.hive.contrib.serde2.RegexSerDe'<br/>
WITH SERDEPROPERTIES (<br/>
    'input.regex' = '([^ ]*) - - \\[([^\\]]*)\\] “([^ ]*) ([^ ]*) ([^ ]*)” (\\d*) (\\d*) “([^”]*)” “([^”]*)”',<br/>
    'output.format.string' = "%1$s %2$s %3$s %4$s %5$s %6$s %7$s %8$s %9$s")<br/>
LOCATION '/user/hive/warehouse/original_access_logs';<br/>
<br/>
CREATE EXTERNAL TABLE tokenized_access_logs (<br/>
    ip STRING,<br/>
    date STRING,<br/>
    method STRING,<br/>
    url STRING,<br/>
    http_version STRING,<br/>
    code1 STRING,<br/>
    code2 STRING,<br/>
    dash STRING,<br/>
    user_agent STRING)<br/>
ROW FORMAT DELIMITED <br/>
FIELDS TERMINATED BY ','<br/>
LOCATION '/user/hive/warehouse/tokenized_access_logs';<br/>
<br/>
ADD JAR {{lib_dir}}/hive-contrib.jar;<br/>
<br/>
INSERT OVERWRITE TABLE tokenized_access_logs <br/>
SELECT * FROM intermediate_access_logs;<br/>
