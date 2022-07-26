# 加载表格

```processing
 table = loadTable("data/new.csv", "header");
 print(table.lastRowIndex());
```

header可选，可以把第一行“排除”掉，让index=0是第二行。
如果没有，index=0是第一行。


# 获取某一格的内容：
![[src/img/Pasted image 20220313150108.png]]
例如要读取这样的表格。（注意这张图的id有误，因为是我手动复制粘贴的）。
## 先获取Row
- 【获取row】`table.getRow(id)` 会返回一行，是个对象实例。
- 【获取row里的col】`row.getString("col-header")` 
- 同理还有   `row.getInt(row, column)`,`row.getFloat(row, column)`

```processing
 TableRow row = table.getRow(1);
 String content = row.getString("newName");
 print(content);

```

# 写入
# 创建新的一行
因为行会追随header产生对应的col。
所以set的时候会制定具体在哪个col位置写入内容。
```processing
TableRow newRow = table.addRow();  //创建
newRow.setString("newName", "Lion"); //写入
```

## 创建新的一列
```processing
table.addColumn("name");
table.addColumn("type");
```
## 技巧-设定id
```processing
  TableRow newRow = table.addRow();
  newRow.setInt("id", table.lastRowIndex());
```

## 保存
要保存才会生效。
```processing
  saveTable(table, "data/new.csv");
```

# 查找row
```processing
  TableRow result = table.findRow("被查找的关键词", "columnName"); //会返回一个row
```
