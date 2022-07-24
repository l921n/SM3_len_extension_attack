SM3的长度扩展攻击

实验原理

任意M1，已知其长度len1与对应的hash值，可以构造合法的消息M = M2||padding||M3，其中M2、M3为任意消息，且可以满足SM3（M1||padding||M3）=SM3（M）
