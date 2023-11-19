SELECT product_id, product_name, revenue<br/>
FROM (<br/>
    SELECT p.product_id,<br/>
           p.product_name,<br/>
           SUM(oi.order_item_subtotal) AS revenue,<br/>
           RANK() OVER (ORDER BY SUM(oi.order_item_subtotal) DESC) AS revenue_rank<br/>
    FROM order_items oi<br/>
    JOIN products p ON oi.order_item_product_id = p.product_id<br/>
    GROUP BY p.product_id, p.product_name<br/>
) AS ranked_products<br/>
WHERE revenue_rank = 5;<br/>
