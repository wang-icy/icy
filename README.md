# icy
Linux脚本
#!/bin/

ls -i | cat -n

echo "---------------------------------"
read -p "请输入你要删除的文件编号: "  chos

#### 判定 chos 的合法性  #########
max=`ls -i | cat -n | wc -l`
min=1
for f in $chos
do
  if [[ $f =~ [^0-9] ]] || [ $f -lt  1 ] || [ $f -gt  $max  ]
  then
    echo "发现不合法编号，请重新输入"
    exit 1
  fi
done
#############################

for i in `echo $chos`
do
  inum="$inum `ls -i | cat -n | sed -n "$i"p | awk '{print $2}'`"
done

for a in  `echo $inum`
do
   find . -inum $a -ok rm -rf  {} \;
done
