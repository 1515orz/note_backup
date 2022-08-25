# 变量（variables）

## 属性
`变量在会话中被保存,在关闭时被释放`
* 使用 SET 语句定义他们
* 使用@符号作为前缀

**SET @invoices_count = 0**

## 本地变量(local variable)
* 当我们完成任务后,本地变量就会被清除
* 使用**DECLARE**对变量进行声明
`DELCARE variable_name TYPE() DEFAULT []`

_EXP_
BEGIN
	DECLARE risk_factor DECIMAL(9,2) DEFAULT 0;
    DECLARE invoices_total DECIMAL(9,2);
    DECLARE invoices_count INT;
    
    SELECT COUNT(*), SUM(invoice_total)
    INTO invoices_count, invoices_total
    FROM invoices;
    
    SET risk_factor = invoices_total/ invoices_count * 5;
    
    SELECT risk_factor;
