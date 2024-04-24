# 42_netpractice

------------------------------------------
calculating number of subnets and range of ip addresses from subnet mask


to calculate the number of subnets and range of ip addresses from subnet mask first you need to convert the non-255 bytes of the subnet mask to binary.
this can be done by repeatedly dividing by 2 and keeping track of the remainder as shown below.
converting 224 to binary:

|	| remainder |
|:----:|:----:|
| 224 ÷ 2 = 112 | 0 |
| 112 ÷ 2 = 56 | 0 |
| 56 ÷ 2 = 28 | 0 |
| 28 ÷ 2 = 14 | 0 |
| 14 ÷ 2 = 7 | 0 |
| 7 ÷ 2 = 3 | 1 |
| 3 ÷ 2 = 1 | 1 |
| 1 ÷ 2 = 0 | 1 |

the binary number is the remainders read in reverse order (from last to first).
so 224 in binary is 11100000.

this binary number is then used to calculate the number of subnets and range of ip addresses.
the formula to calculate the number of subnets is:
**Number of subnets=2<sup>n</sup>**
where *n* is the number of bits used for subnetting.

------------------------------------------
level 1


interface A1:

subnet mask is 255.255.255.0 so the first 3 bytes of the ip need to match interface B1's ip (104.98.23.12).
this means ip address can be any in the range 104.98.23.0 - 104.98.23.255 except the following 3:
104.98.23.0 - the first number represents the network and cannot be used by a host.
104.98.23.255 - the last number represents the broadcast address and cannot be used by a host.
104.98.23.12 - this ip address is already being used by interface B1.

interface D1:

subnet mask is 255.255.0.0 so the first 2 bytes of the ip need to match interface C1's ip (211.191.239.75).
this means ip address can be any in the range 211.191.0.0 - 211.191.255.255 except the following 3:
211.191.0.0 - represents the network.
211.191.255.255 - represents the broadcast address.
211.191.239.75 - this ip address is already being used by interface C1.

------------------------------------------
level 2
