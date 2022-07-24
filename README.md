SM3的长度扩展攻击

实验原理

任意M1，已知其长度len1与对应的hash值，可以构造合法的消息M = M2||padding||M3，其中M2、M3为任意消息，且可以满足SM3（M1||padding||M3）=SM3（M）

文件说明

my_sm3.py 参照https://www.cnblogs.com/wcwnina/p/13604915.html编写过程中使用的指定iv的sm3简单实现；

sm3_len_ext_attack.py 实现初始消息为“Hello SDU CST!20220718”、附加消息为“202000210008”的长度扩展攻击。
