# 加解密

[在线加解密](https://www.qqxiuzi.cn/bianma/base64.htm)

<span style="color:red">可以直接看最后，如何调用.net内置的方法</span>

**一、编码规则
**   Base64编码的思想是是采用64个基本的ASCII码字符对数据进行重新编码。它将需要编码的数据拆分成字节数组。以3个字节为一组。按顺序排列24 位数据，再把这24位数据分成4组，即每组6位。再在每组的的最高位前补两个0凑足一个字节。这样就把一个3字节为一组的数据重新编码成了4个字节。当所要编码的数据的字节数不是3的整倍数，也就是说在分组时最后一组不够3个字节。这时在最后一组填充1到2个0字节。并在最后编码完成后在结尾添加1到2个 “=”。

例：将对ABC进行BASE64编码：

> 
> 1、首先取ABC对应的ASCII码值。A（65）B（66）C（67）；
> 2、再取二进制值A（01000001）B（01000010）C（01000011）；
>  3、然后把这三个字节的二进制码接起来（010000010100001001000011）；
> 4、 再以6位为单位分成4个数据块,并在最高位填充两个0后形成4个字节的编码后的值，（00010000）（00010100）（00001001）（00000011），其中蓝色部分为真实数据；
>  5、再把这四个字节数据转化成10进制数得（16）（20）（9）（3）；
>  6、最后根据BASE64给出的64个基本字符表，查出对应的ASCII码字符（Q）（U）（J）（D），这里的值实际就是数据在字符表中的索引。

注：BASE64字符表：ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/

**二、解码规则
**   解码过程就是把4个字节再还原成3个字节再根据不同的数据形式把字节数组重新整理成数据。

**三、C#中的实现**

**编码类：**

```csharp
/// <summary>
/// Base64编码类。
/// 将byte[]类型转换成Base64编码的string类型。
/// </summary>
public class Base64Encoder
{
    byte[] source;
    int length, length2;
    int blockCount;
    int paddingCount;
    public static Base64Encoder Encoder = new Base64Encoder();

    public Base64Encoder()
    {
    }

    private void init(byte[] input)
    {
        source = input;
        length = input.Length;
        if ((length % 3) == 0)
        {
            paddingCount = 0;
            blockCount = length / 3;
        }
        else
        {
            paddingCount = 3 - (length % 3);
            blockCount = (length + paddingCount) / 3;
        }
        length2 = length + paddingCount;
    }

    public string GetEncoded(byte[] input)
    {
        //初始化
        init(input);

        byte[] source2;
        source2 = new byte[length2];

        for (int x = 0; x < length2; x++)
        {
            if (x < length)
            {
                source2[x] = source[x];
            }
            else
            {
                source2[x] = 0;
            }
        }

        byte b1, b2, b3;
        byte temp, temp1, temp2, temp3, temp4;
        byte[] buffer = new byte[blockCount * 4];
        char[] result = new char[blockCount * 4];
        for (int x = 0; x < blockCount; x++)
        {
            b1 = source2[x * 3];
            b2 = source2[x * 3 + 1];
            b3 = source2[x * 3 + 2];

            temp1 = (byte)((b1 & 252) >> 2);

            temp = (byte)((b1 & 3) << 4);
            temp2 = (byte)((b2 & 240) >> 4);
            temp2 += temp;

            temp = (byte)((b2 & 15) << 2);
            temp3 = (byte)((b3 & 192) >> 6);
            temp3 += temp;

            temp4 = (byte)(b3 & 63);

            buffer[x * 4] = temp1;
            buffer[x * 4 + 1] = temp2;
            buffer[x * 4 + 2] = temp3;
            buffer[x * 4 + 3] = temp4;

        }

        for (int x = 0; x < blockCount * 4; x++)
        {
            result[x] = sixbit2char(buffer[x]);
        }


        switch (paddingCount)
        {
            case 0: break;
            case 1: result[blockCount * 4 - 1] = '='; break;
            case 2: result[blockCount * 4 - 1] = '=';
                result[blockCount * 4 - 2] = '=';
                break;
            default: break;
        }
        return new string(result);
    }
    private char sixbit2char(byte b)
    {
        char[] lookupTable = new char[64]{
            'A','B','C','D','E','F','G','H','I','J','K','L','M',
            'N','O','P','Q','R','S','T','U','V','W','X','Y','Z',
            'a','b','c','d','e','f','g','h','i','j','k','l','m',
            'n','o','p','q','r','s','t','u','v','w','x','y','z',
            '0','1','2','3','4','5','6','7','8','9','+','/'};

        if ((b >= 0) && (b <= 63))
        {
            return lookupTable[(int)b];
        }
        else
        {
            return ' ';
        }
    }
}
```

**解码类：**

```csharp
/// <summary>
/// Base64解码类
/// 将Base64编码的string类型转换成byte[]类型
/// </summary>
public class Base64Decoder
{
    char[] source;
    int length, length2, length3;
    int blockCount;
    int paddingCount;
    public static Base64Decoder Decoder = new Base64Decoder();

    public Base64Decoder()
    {
    }

    private void init(char[] input)
    {
        int temp = 0;
        source = input;
        length = input.Length;

        for (int x = 0; x < 2; x++)
        {
            if (input[length - x - 1] == '=')
                temp++;
        }
        paddingCount = temp;

        blockCount = length / 4;
        length2 = blockCount * 3;
    }

    public byte[] GetDecoded(string strInput)
    {
        //初始化
        init(strInput.ToCharArray());

        byte[] buffer = new byte[length];
        byte[] buffer2 = new byte[length2];

        for (int x = 0; x < length; x++)
        {
            buffer[x] = char2sixbit(source[x]);
        }

        byte b, b1, b2, b3;
        byte temp1, temp2, temp3, temp4;

        for (int x = 0; x < blockCount; x++)
        {
            temp1 = buffer[x * 4];
            temp2 = buffer[x * 4 + 1];
            temp3 = buffer[x * 4 + 2];
            temp4 = buffer[x * 4 + 3];

            b = (byte)(temp1 << 2);
            b1 = (byte)((temp2 & 48) >> 4);
            b1 += b;

            b = (byte)((temp2 & 15) << 4);
            b2 = (byte)((temp3 & 60) >> 2);
            b2 += b;

            b = (byte)((temp3 & 3) << 6);
            b3 = temp4;
            b3 += b;

            buffer2[x * 3] = b1;
            buffer2[x * 3 + 1] = b2;
            buffer2[x * 3 + 2] = b3;
        }

        length3 = length2 - paddingCount;
        byte[] result = new byte[length3];

        for (int x = 0; x < length3; x++)
        {
            result[x] = buffer2[x];
        }

        return result;
    }

    private byte char2sixbit(char c)
    {
        char[] lookupTable = new char[64]{  
            'A','B','C','D','E','F','G','H','I','J','K','L','M','N',
            'O','P','Q','R','S','T','U','V','W','X','Y', 'Z',
            'a','b','c','d','e','f','g','h','i','j','k','l','m','n',
            'o','p','q','r','s','t','u','v','w','x','y','z',
            '0','1','2','3','4','5','6','7','8','9','+','/'};
        if (c == '=')
            return 0;
        else
        {
            for (int x = 0; x < 64; x++)
            {
                if (lookupTable[x] == c)
                    return (byte)x;
            }

            return 0;
        }

    }
}
//解码类结束
```

提示：

上面的代码只是说明base64编码的原理，以便用更多语言重写。但.net里面可以使用更简单的方法：

编码：

```csharp
byte[] bytes=Encoding.Default.GetBytes("要转换的字符串");



Convert.ToBase64String(bytes);
```

解码：

```csharp
//"ztKwrsTj"是“我爱你”的base64编码



byte[] outputb = Convert.FromBase64String("ztKwrsTj");



string orgStr= Encoding.Default.GetString(outputb);
```

 