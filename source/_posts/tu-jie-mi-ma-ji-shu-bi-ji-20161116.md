---
title: 图解密码技术 读书笔记
date: 2016-11-17 15:56:05
tags: [笔记, cryptography]
---
---
本书分为三个部分：
第一部分：密码
+ 对称密码
+ 分组密码
+ 公钥密码
+ 混合密码系统

第二部分：认证
+ 单项散列函数
+ 消息认证码
+ 数字签名
+ 证书

第三部分：密钥、随机数与应用技术
+ 密钥
+ 随机数
+ PGP
+ SSL/TLS
+ 密码技术与现实社会

---
密码角色：

|名称|说明|
|---|---|
|Alice |一般角色|
|Bob |一般角色 |
|Eve |窃听者，可窃听通信内容 |
|Mallory |主动攻击者，可妨碍通信、伪造消息等 |
|Trent |可信任第三方 |
|Victor |验证者 |

名词：
加密：cryptography
加密：encrypt
解密：decrypt
明文：plaintext
密文：ciphertext
机密性：confidentiality
密码破译：cryptanalysis
破译者：cryptanalyst
算法：algorithm
密钥:key
密钥空间：keyspace
对称密码：symmetric cryptography,其它别名 **公共密钥密码**(common-key cryptography),**传统密码**(conventional cryptography)，**私钥密码**（secret-key cryptography）,**共享密钥密码**(shared-key cryptography)
非对称密码：asymmetric cryptography,又称为公钥密码(public-key cryptography)
混合密码系统:hybrid cryptosystem,将对称密码和公钥密码结合起来的密码系统

单向散列函数(one-way hash function):计算hash，用于保护数据的完整性（integrity）
散列值(hash)又称为哈希值、密码校验和(cryptography checksum)、指纹(fingerprint)、消息摘要(message digest).

消息认证码（message authentication code）:通过消息认证码不仅可以确认消息是否被篡改，而且能确认消息是否来自期待的通信对象。也就是说，消息认证码不仅能保证完整性，还能提供认证(authentication)机制。

数字签名（digital signature）：能够确保完整性、提供认证并防止否认的密码技术。
伪装(spoofing)
否认（repudiation）
验证（verify）

伪随机数生成器(Pseudo Random Number Generator, PRNG)：模拟产生随机数的算法

隐写术（steganography）:它不是让消息内容变得无法解读，而是能够隐藏消息本身。

###  密码与信息安全常识
+ 不要使用保密的密码算法
+ 使用低强度的密码比不进行任何加密更危险
+ 任何密码总有一天都会被破解
+ 密码只是信息安全的一部分

试图通过密码算法本身进行保密来确保安全性的行为，一般称为**隐蔽式安全性**(security by obsecurity)，这种行为是危险且愚蠢的。

严格来说，绝对不会被破解的密码算法是存在的，这种算法成为**一次一密**(one-time pad)，但它不是一种现实可用的密码。

要保证良好的安全性，就需要理解“系统”这一概念的本质。复杂的系统就像一根由无数环节相连组成的链条，如果用力拉，就会从其中最脆弱的环节处断开。因此系统的强度取决于其中最脆弱的环节的强度。

------
凯撒密码(Caesar cipher)



















