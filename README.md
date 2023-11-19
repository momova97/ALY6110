SELECT COUNT(*) AS count,<br/>
       url<br/>
FROM tokenized_access_logs<br/>
WHERE url LIKE '%/product/%'<br/>
GROUP BY url<br/>
ORDER BY count DESC;<br/>
