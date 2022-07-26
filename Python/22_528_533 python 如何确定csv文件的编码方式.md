https://krinkere.github.io/krinkersite/encoding_csv_file_python.html

https://www.jb51.net/article/211203.htm

使用chardet模块
```py
import chardet 
with open("tokyo_rain.csv", 'rb') as rawdata:
    result = chardet.detect(rawdata.read(10000))

# check what the character encoding might be
print(result)
```

output
```py
{'encoding': 'SHIFT_JIS', 'confidence': 0.99, 'language': 'Japanese'}
```
