select count(*)url from tokenized_access_logs where url like '%\/product\/%' group by url order by count(*) desc;
