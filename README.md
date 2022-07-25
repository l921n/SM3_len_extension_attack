# SM3的长度扩展攻击

## 实验原理

任意M1，已知其长度len1与对应的hash值，可以构造合法的消息M = M2||padding||M3，其中M2、M3为任意消息，且可以满足SM3（M1||padding||M3）=SM3（M）

## 文件说明

my_sm3.py 参照https://www.cnblogs.com/wcwnina/p/13604915.html 编写过程中使用的指定iv的sm3简单实现；

sm3_len_ext_attack.py 实现初始消息为“Hello SDU CST!20220718”、附加消息为“202000210008”的长度扩展攻击。

## 实现细节

### my_sm3.py 

1）定义rotl函数，实现SM3过程中循环左移操作；

2）将常数T_j内容存储在列表中；

3）依次完成SM3中FF函数 sm3_ff_j 、GG函数 sm3_gg_j 、置换函数 sm3_p_0 与 sm3_p_1 、压缩函数 sm3_cf 定义；

4）编写可以实现自定义初始变量的SM3函数：

    传入列表类参数 msg 与 指定初始变量 new_v，首先确定 msg 长度，实现消息填充：在 msg 末端添 1，添 k 个 0 至满足 len(msg) + 1 + k (mod 64) = 56，最后填充比特长度，此处利用struct模块中pack函数实现['>q'表示大端模式long long类型]
    
    实现迭代压缩时，由于伪造消息只需要对附加的消息进行加密，因此加密次数要比之前少一次，从消息的第64字节开始加密，即可得到hash值。
    
    最后完成格式化输出 result 即可完成 hash 。
    
### sm3_len_ext_attack.py

1）
