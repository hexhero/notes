# AES 加密

## 环境安装

```
pip uninstall crypto
pip uninstall pycryptodome
pip install pycryptodome
```

## CBC 加密 (需偏移量)

```py
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
import base64
import binascii

# 数据类
class MData():
    def __init__(self, data = b"",characterSet='utf-8'):
        # data肯定为bytes
        self.data = data
        self.characterSet = characterSet
    
    def readFile(self, filename):
        with open(filename,'r') as f:
            self.data = f.read()
            return self.data
    
    def saveData(self,FileName):
        with open(FileName,'wb') as f:
            f.write(self.data)

    def fromString(self,data):
        self.data = data.encode(self.characterSet)
        return self.data

    def fromBase64(self,data):
        self.data = base64.b64decode(data.encode(self.characterSet))
        return self.data

    def fromHexStr(self,data):
        self.data = binascii.a2b_hex(data)
        return self.data

    def toString(self):
        return self.data.decode(self.characterSet)

    def toBase64(self):
        return base64.b64encode(self.data).decode()

    def toHexStr(self):
        return binascii.b2a_hex(self.data).decode()

    def toBytes(self):
        return self.data

    def __str__(self):
        try:
            return self.toString()
        except Exception:
            return self.toBase64()


### 封装类
class AEScryptor():
    def __init__(self,key,mode,iv = '',paddingMode= "NoPadding",characterSet ="utf-8"):
        '''
        构建一个AES对象
        key: 秘钥，字节型数据
        mode: 使用模式，只提供两种，AES.MODE_CBC, AES.MODE_ECB
        iv： iv偏移量，字节型数据
        paddingMode: 填充模式，默认为NoPadding, 可选NoPadding，ZeroPadding，PKCS5Padding，PKCS7Padding
        characterSet: 字符集编码
        '''
        self.key = self._pad(key)
        self.mode = mode
        self.iv = iv
        self.characterSet = characterSet
        self.paddingMode = paddingMode
        self.data = ""    

    def _pad(self, data):
        return pad(data, AES.block_size, style='pkcs7')
    
    def __ZeroPadding(self,data):
        data += b'\x00'
        while len(data) % 16 != 0:
            data += b'\x00'
        return data

    def __StripZeroPadding(self,data):
        data = data[:-1]
        while len(data) % 16 != 0:
            data = data.rstrip(b'\x00')
            if data[-1] != b"\x00":
                break
        return data

    def __PKCS5_7Padding(self,data):
        needSize = 16-len(data) % 16
        if needSize == 0:
            needSize = 16
        return data + needSize.to_bytes(1,'little')*needSize

    def __StripPKCS5_7Padding(self,data):
        paddingSize = data[-1]
        return data.rstrip(paddingSize.to_bytes(1,'little'))

    def __paddingData(self,data):
        if self.paddingMode == "NoPadding":
            if len(data) % 16 == 0:
                return data
            else:
                return self.__ZeroPadding(data)
        elif self.paddingMode == "ZeroPadding":
            return self.__ZeroPadding(data)
        elif self.paddingMode == "PKCS5Padding" or self.paddingMode == "PKCS7Padding":
            return self.__PKCS5_7Padding(data)
        else:
            print("不支持Padding")

    def __stripPaddingData(self,data):
        if self.paddingMode == "NoPadding":
            return self.__StripZeroPadding(data)
        elif self.paddingMode == "ZeroPadding":
            return self.__StripZeroPadding(data)

        elif self.paddingMode == "PKCS5Padding" or self.paddingMode == "PKCS7Padding":
            return self.__StripPKCS5_7Padding(data)
        else:
            print("不支持Padding")

    def setCharacterSet(self,characterSet):
        '''
        设置字符集编码
        characterSet: 字符集编码
        '''
        self.characterSet = characterSet

    def setPaddingMode(self,mode):
        '''
        设置填充模式
        mode: 可选NoPadding，ZeroPadding，PKCS5Padding，PKCS7Padding
        '''
        self.paddingMode = mode

    def decryptFromBase64(self,entext):
        '''
        从base64编码字符串编码进行AES解密
        entext: 数据类型str
        '''
        mData = MData(characterSet=self.characterSet)
        self.data = mData.fromBase64(entext)
        return self.__decrypt()

    def decryptFromHexStr(self,entext):
        '''
        从hexstr编码字符串编码进行AES解密
        entext: 数据类型str
        '''
        mData = MData(characterSet=self.characterSet)
        self.data = mData.fromHexStr(entext)
        return self.__decrypt()

    def decryptFromString(self,entext):
        '''
        从字符串进行AES解密
        entext: 数据类型str
        '''
        mData = MData(characterSet=self.characterSet)
        self.data = mData.fromString(entext)
        return self.__decrypt()

    def decryptFromBytes(self,entext):
        '''
        从二进制进行AES解密
        entext: 数据类型bytes
        '''
        self.data = entext
        return self.__decrypt()

    def encryptFromString(self,data):
        '''
        对字符串进行AES加密
        data: 待加密字符串，数据类型为str
        '''
        self.data = data.encode(self.characterSet)
        return self.__encrypt()

    def __encrypt(self):
        if self.mode == AES.MODE_CBC:
            aes = AES.new(self.key,self.mode,self.iv) 
        elif self.mode == AES.MODE_ECB:
            aes = AES.new(self.key,self.mode) 
        else:
            print("不支持这种模式")  
            return           

        data = self.__paddingData(self.data)
        enData = aes.encrypt(data)
        return MData(enData)

    def __decrypt(self):
        if self.mode == AES.MODE_CBC:
            aes = AES.new(self.key,self.mode,self.iv) 
        elif self.mode == AES.MODE_ECB:
            aes = AES.new(self.key,self.mode) 
        else:
            print("不支持这种模式")  
            return           
        data = aes.decrypt(self.data)
        mData = MData(self.__stripPaddingData(data),characterSet=self.characterSet)
        return mData



def decode(key, iv, data):
    aes = AEScryptor(key,AES.MODE_CBC,iv,paddingMode= "ZeroPadding",characterSet='utf-8')
    rData = aes.decryptFromBase64(data)
    return rData

def encode(key, iv, data):
    aes = AEScryptor(key,AES.MODE_CBC,iv,paddingMode= "ZeroPadding",characterSet='utf-8')
    rData = aes.encryptFromString(data)
    return rData

import sys, getopt

if __name__ == '__main__':
    key = b'13224'
    iv =  b"1912003030020218"
    m = MData();
    
    # 加密或解密文件
    opts, args = getopt.getopt(sys.argv[1:], 'k:e:d:',['key=','encode=','decode='])
    for opt, arg in opts:
        if opt in ['-k', '--key']:
            key = arg.encode('utf-8')
        if opt in ['-e', '--encode']:
            data = m.readFile(arg)
            res = encode(key, data)
            print(res)
        if opt in ['-d','--decode']:
            data = m.readFile(arg)
            res = decode(key, data)
            print(res)
```