# 片段

> 各种有用的 Bash 风格命令，可随时复制、粘贴。
> [Awesome OS X Command Line](https://github.com/nusr/awesome-macos-command-line-zh) 的一部分。

- [片段](#%E7%89%87%E6%AE%B5)
  - [文本操作](#%E6%96%87%E6%9C%AC%E6%93%8D%E4%BD%9C)
    - [从文本中提取唯一单词](#%E4%BB%8E%E6%96%87%E6%9C%AC%E4%B8%AD%E6%8F%90%E5%8F%96%E5%94%AF%E4%B8%80%E5%8D%95%E8%AF%8D)
  - [License](#license)

## 文本操作

### 从文本中提取唯一单词

```bash
grep -o -E '\w+' <file> | sort -u -f
```

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
