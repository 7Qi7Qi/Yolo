# 常用函数列表

## 数学函数



## 三角函数







## 字符串处理

### regexp_replace

1. 用途：正则匹配替换
2. 语法：``REGEXP_REPLACE (source_string, pattern [, replace_string [, position [, occurrence, [match_parameter] ] ] ])``

```sql
select no, regexp_replace( classification_name, '（\w+）', '\1', 'g' )  from erp_project_file_model_list
```





------



[参考来源]: https://blog.csdn.net/sun5769675/article/details/50628979	"postgresql常用"