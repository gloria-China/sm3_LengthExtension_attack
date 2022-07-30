用长度扩展攻击寻找sm3的碰撞。\\
完成人：本人。\\
原理：已知SM3是MD结构的，且为大端存储，有SM3(IV, salt+data+padding+append) = SM3(SM3(IV, salt+data), append)构成了碰撞。
问题：SM3(IV, salt+data+padding+append)：c为原始消息salt+data，c_2是扩展的消息append。我们取m=Fill(c)是被填充至512bit的消息,salt+data+padding+append=m+c_2，加密后得到h_3；
     SM3(SM3(IV, salt+data), append)：SM3(IV, salt+data)作为新加密的IV，append作为新消息，将这两个进行加密得到h_2。
     若h_2=h_3，则找到碰撞。
     


