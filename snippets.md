# 片段

> 各种有用的 Bash 风格命令，可随时复制、粘贴。
> [Awesome OS X Command Line](https://github.com/nusr/awesome-macos-command-line-zh) 的一部分。

- [片段](#%E7%89%87%E6%AE%B5)
  - [文本操作](#%E6%96%87%E6%9C%AC%E6%93%8D%E4%BD%9C)
    - [从文本中提取唯一单词](#%E4%BB%8E%E6%96%87%E6%9C%AC%E4%B8%AD%E6%8F%90%E5%8F%96%E5%94%AF%E4%B8%80%E5%8D%95%E8%AF%8D)

## 文本操作

### 从文本中提取唯一单词

```bash
grep -o -E '\w+' <file> | sort -u -f
```
