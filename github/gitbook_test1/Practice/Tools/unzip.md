# ubuntu下各种压缩和解压命令

## 1、‘.tar'文件

* 仅打包并非压缩

```
tar -cvf  filename（压缩到当前文件夹）
```

```
tar -cvf fileName.tar DirName（压缩到指定文件夹）
```

* 解压

```
tar -xvf filename.tar（解压到当前文件夹）
```

## 2、'.gz'文件

* 压缩

```
gzip FileName       # 压缩，只能压缩文件
```

* 解压

```
gunzip FileName.gz  # 解压1
```

```
gzip -d FileName.gz # 解压2
```

## 3、'.tar.gz'、'.tgz'文件

* 压缩

```
# .tar.gz 和 .tgz
tar -zcvf FileName.tar.gz DirName       # 将DirName和其下所有文件（夹）压缩
```

* 解压

```
# .tar.gz 和 .tgz
tar -zxvf FileName.tar.gz               # 解压
tar -C DesDirName -zxvf FileName.tar.gz # 解压到目标路径
```

## 4、'.zip'文件

* 压缩

```
zip FileName.zip DirName    # 将DirName本身压缩
zip -r FileName.zip DirName # 压缩，递归处理，将指定目录下的所有文件和子目录一并压缩
```

* 解压

```
unzip FileName.zip          # 解压
```

## 5、'.rar'文件

* 需要下载
* 压缩

```
rar a FileName.rar DirName # 压缩
```

* 解压

```
rar x FileName.rar      # 解压
```

## 6、’.xz‘文件

* 压缩

```
xz -z filename
```

* 解压

```
xz -d filename.xz
```

## 7、'.tar.xz'文件

* 压缩

```
未知
```

* 解压

```
tar xvJf filename.tar.xz
```



## 8、’.bz2‘文件

* 压缩

```
.bzip2 -d FileName.bz2   #方式1
```

```
.bunzip2 FileName.bz2	#方式2
```

* 解压

```
bzip2 -z FileName
```

## 9、通用方法

* 安装

```
sudo apt-get install unar
```

* 压缩

```
unar file.zip
```

* 解压

```
unar file.zip -o FileName  #指定解压路径
```









