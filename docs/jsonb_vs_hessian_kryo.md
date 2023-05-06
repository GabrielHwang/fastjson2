# Int32整数处理
* 这三种协议都采用了整数压缩的算法，kryo的压缩效果最好，实际使用中大小会比较接近。 
* jsonb和hessian的大小是一样的。
* jsonb在size为1的期间[-6, 47]的二进制的值和数值一致，是为调试时的可读性更好考虑。

|     | jsonb                                       | hessian                                   | kryo                                              | 
|-----|---------------------------------------------|-------------------------------------------|---------------------------------------------------|
| 1   | [-16, 47]                                   | [-16, 47]                                 | [-64, 63]                                         |
| 2   | [-2048, -17] <br/>[48, 2047]                     | [-2048, -17] <br/>[48, 2047]                   | [-8192, -65] <br/>[64, 8191]                           |
| 3   | [-262144, -2049] <br/>[2048, 262143]             | [-262144, -2049] <br/>[2048, 262143]           | [-1048576, -8193] <br/>[8192, 1048575]                 |
| 4   |                                             |                                           | [-134217728, -1048577] <br/>[1048576, 134217727]       |
| 5   | [-2147483648, -262145] <br/>[262144, 2147483647] | [-2147483648, -262145]<br/> [262144, 2147483647] | [-2147483648, -134217729] <br/>[134217727, 2147483647] |


