用长度扩展攻击寻找sm3的碰撞。  
完成人：本人。  
原理：已知SM3是MD结构的，且为大端存储，有SM3(IV, salt+data+padding+append) = SM3(SM3(IV, salt+data), append)构成了碰撞。  
思路：SM3(IV, salt+data+padding+append)：c为原始消息salt+data= “abc”，c_2是扩展的消息append= “defj”。我们取m=Fill(c)是被填充至512bit的消息,c_3=salt+data+padding+append=m+c_2，将c_3作为新的消息填充后，经过扩展、压缩得到h_3；  
     SM3(SM3(IV, salt+data), append)：SM3(IV, salt+data)作为新加密的IV，append作为新消息进行哈希，需注意，我们在对append填充时，后缀长度应为m+c_2的长度大小，填充后长度为512bit的倍数。  
     若h_2=h_3，则找到碰撞。  
     
  
运行效果：  
SM3(c_2,SM3(IV,c)):  7380166f4914b2b9172442d7da8a0600a96f30bc163138aae38dee4db0fb0e4e  
SM3(c+padding+c_2,IV):  7380166f4914b2b9172442d7da8a0600a96f30bc163138aae38dee4db0fb0e4e  
Success!  
 
![image]([https://github.com/gloria-China/sm3_LengthExtension_attack/blob/main/images/sm3.jpg])

