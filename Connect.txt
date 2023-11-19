Hi There
sqoop import-all-tables \
-m [number_of_worker_nodes] \
--connect jdbc:mysql://[manager_node_hostname]:3306/retail_db \
--username=retail_dba \
--password=cloudera \
--compression-codec=snappy \
--as-parquetfile \
--warehouse-dir=/user/hive/warehouse \
--hive-import
