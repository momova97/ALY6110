select c.category_name, count(oi.order_item_quantity) as order_count
<br/>
from order_items oi
<br/>
inner join products p on oi.order_item_product_id = p.product_id
<br/>
inner join categories c on c.category_id = p.product_category_id
<br/>
group by c.category_name
<br/>
order by order_count desc
<br/>
limit 10;
