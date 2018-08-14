-- All tables
SELECT *
FROM sys.tables
ORDER BY --NAME, 
CREATE_DATE DESC
GO

-- All procedures
SELECT *
FROM sys.procedures
ORDER BY --NAME, 
CREATE_DATE DESC
GO

-- Find column name in all the tables
SELECT c.NAME AS 'ColumnName', t.NAME AS 'TableName'
FROM sys.columns c
JOIN sys.tables t ON c.object_id = t.object_id
WHERE c.NAME LIKE '%Text%'
ORDER BY TableName, ColumnName;
GO

-- Find specific word in the SPs
SELECT DISTINCT P.[name], M.[definition]
FROM sys.procedures P
JOIN sys.sql_modules M ON M.[object_id] = P.[object_id]
WHERE M.[definition] LIKE '%Text%' ESCAPE '#'
GO

-- Find in all SP, functions
SELECT  so.name, sc.text 
FROM sysobjects so 
JOIN syscomments sc ON sc.id = so.id
WHERE UPPER(sc.text) LIKE '%Text%'
GO

-- Find view names in the SPs
SELECT DISTINCT P.[name], M.[definition],  V.[name]
FROM sys.procedures P
JOIN sys.sql_modules M ON M.[object_id] = P.[object_id]
JOIN (SELECT [name] FROM sys.views) V ON  M.[definition] LIKE '%' + V.[name] + '%'
GO

-- Get foreign keys
EXEC sp_fkeys sector
GO

-- Table contains zero rows
SELECT t.NAME AS TableName, p.rows AS RowCounts
FROM sys.tables t
INNER JOIN sys.partitions p ON t.object_id = p.OBJECT_ID
WHERE  t.is_ms_shipped = 0
	AND p.rows = 0
	-- AND t.NAME NOT LIKE '%wbs%'
GROUP BY t.NAME, p.Rows
ORDER BY p.rows, t.NAME
GO

SELECT t1.NAME, t1.NAME foundin, t1.type_desc
FROM sys.objects t1
LEFT OUTER JOIN sys.sql_modules sm
INNER JOIN sys.objects t2 ON t2.object_id = sm.object_id ON sm.DEFINITION LIKE '%' + t1.NAME + '%' WHERE t1.type = 'U'
	AND t2.NAME IS NULL
ORDER BY t1.NAME, t1.type_desc, foundin
GO

SP_DEPENDS 'TestTable'
GO

-- Get numbers from 1 to 2048
SELECT DISTINCT number FROM master..spt_values WHERE number > 0 ORDER BY number
GO
