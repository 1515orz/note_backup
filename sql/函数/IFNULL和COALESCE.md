IFNULL
EXP:
SELECT 
	order_id,
	IFNULL(shipper_id,'Not assigned')
FROM orders 
如果shipper_id是NULL ,则返回'Not assigned'

COALESCE
EXP:
SELECT 
	order_id,
	COALESCE(shipper_id,comments,'Not assigned') AS shipper
FROM orders 
区别:
IFNULL 可以将NULL内容替换为其他内容,
COALESCE 可以提供一堆值,这个函数会返回这堆值中的第一个非空值 例:(shipper_id,comments,'Not assigned'....)