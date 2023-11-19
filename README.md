-- top 10 revenue generating products<br/>
SELECT p.product_id,<br/>
       p.product_name,<br/>
       r.revenue<br/>
FROM products p<br/>
INNER JOIN (<br/>
    SELECT oi.order_item_product_id,<br/>
           SUM(CAST(oi.order_item_subtotal AS FLOAT)) AS revenue<br/>
    FROM order_items oi<br/>
    INNER JOIN orders o ON oi.order_item_order_id = o.order_id<br/>
    WHERE o.order_status <> 'CANCELED'<br/>
      AND o.order_status <> 'SUSPECTED_FRAUD'<br/>
    GROUP BY oi.order_item_product_id<br/>
) r ON p.product_id = r.order_item_product_id<br/>
ORDER BY r.revenue DESC<br/>
LIMIT 10;
