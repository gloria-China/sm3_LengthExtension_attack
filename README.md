用长度扩展攻击寻找sm3的碰撞。  
完成人：本人。  
原理：已知SM3是MD结构的，且为大端存储，有SM3(IV, salt+data+padding+append) = SM3(SM3(IV, salt+data), append)构成了碰撞。  
思路：SM3(IV, salt+data+padding+append)：c为原始消息salt+data，c_2是扩展的消息append。我们取m=Fill(c)是被填充至512bit的消息,salt+data+padding+append=m+c_2，加密后得到h_3；  
     SM3(SM3(IV, salt+data), append)：SM3(IV, salt+data)作为新加密的IV，append作为新消息，将这两个进行加密得到h_2。  
     若h_2=h_3，则找到碰撞。  
问题：结果不对。       
  
运行效果：  
[07/30/22]seed@VM:~$ ./sm3.py  
SM3(c_2,SM3(IV,c)):  7380166f4914b2b9172442d7da8a0600a96f30bc163138aae38dee4db0fb0e4e  
SM3(c+padding+c_2,IV):  b47645341de94064e70aa34b0102a9bfb9ce4ee25f4e67639c67adf3d82d1234  
Fales!  
![image]([https://github.com/gloria-China/sm3_LengthExtension_attack/blob/main/images/sm3.jpg])

