sqoop import-all-tables \ 
-m {{cluster_data.worker_node_hostname.length}} \
 --connect jdbc:mysql://{{cluster_data.manager_
node_hostname}}:3306/retail_db \
 --username=retail_dba \
 --password=cloudera \
 --compression-codec=snappy \
 --as-parquetfile \
 --warehouse-dir=/user/hive/warehouse \
 --hive-import
