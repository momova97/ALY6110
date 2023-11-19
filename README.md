sudo -u hdfs hadoop fs -mkdir /user/hive/warehouse/original_access_logs <br/>
sudo -u hdfs hadoop fs -copyFromLocal /opt/examples/log_files/access.log.2 /user/hive/warehouse/original_access_logs
