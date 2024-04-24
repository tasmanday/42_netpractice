# 42_netpractice

------------------------------------------
calculating number of subnets and range of ip addresses from subnet mask
<br><br><br>
to calculate the number of subnets and range of ip addresses from subnet mask first you need to convert the non-255 bytes of the subnet mask to binary.
this can be done by repeatedly dividing by 2 and keeping track of the remainder as shown below.
converting 192 to binary:

|	| remainder |
|:----:|:----:|
| 192 ÷ 2 = 96 | 0 |
| 96 ÷ 2 = 48 | 0 |
| 48 ÷ 2 = 24 | 0 |
| 24 ÷ 2 = 12 | 0 |
| 12 ÷ 2 = 6 | 0 |
| 6 ÷ 2 = 3 | 0 |
| 3 ÷ 2 = 1 | 1 |
| 1 ÷ 2 = 0 | 1 |

the binary number is the remainders read in reverse order (from last to first).
so 192 in binary is 11000000.

this binary number is then used to calculate the number of subnets and range of ip addresses.
the formula to calculate the number of subnets is:

**Number of subnets = 2<sup>n</sup>**

where *n* is the number of bits used for subnetting.

the formula to calculate the number of ip addresses per subnet is:

**Number of ip addresses = 2<sup>m</sup>**

where *m* is the number of host bits.

so for 255.255.255.192 (or in binary: 11111111.11111111.11111111.11000000)
the number of subnets would be 2<sup>2</sup> = 4 and the number of ip addresses per subnet would be 2<sup>6</sup> = 64.
the range of ip addresses for the 4 subnets would be:
- 255.255.255.0 - 255.255.255.63
- 255.255.255.64 - 255.255.255.127
- 255.255.255.128 - 255.255.255.191
- 255.255.255.192 - 255.255.255.255

the first and last addresses from each subnet are reserved for the network and broadcast address respectively.

slash notation is also based on the binary subnet masks.
it shows the number of bits in the ip address that represent the network address (1's at the start).

**decimal 255.255.255.192 = binary 11111111.11111111.11111111.11000000 = slash /26**

------------------------------------------
level 1
<br><br><br>
interface A1:

subnet mask is 255.255.255.0 so the first 3 bytes of the ip need to match interface B1's ip (104.98.23.12).
this means ip address can be any in the range 104.98.23.0 - 104.98.23.255 except the following 3:
- 104.98.23.0 - the first number represents the network and cannot be used by a host.
- 104.98.23.255 - the last number represents the broadcast address and cannot be used by a host.
- 104.98.23.12 - this ip address is already being used by interface B1.

interface D1:

subnet mask is 255.255.0.0 so the first 2 bytes of the ip need to match interface C1's ip (211.191.239.75).
this means ip address can be any in the range 211.191.0.0 - 211.191.255.255 except the following 3:
- 211.191.0.0 - represents the network.
- 211.191.255.255 - represents the broadcast address.
- 211.191.239.75 - this ip address is already being used by interface C1.

------------------------------------------
level 2
<br><br><br>
interface A1:

subnet mask 255.255.255.224 = 11111111.11111111.11111111.11100000 = /27
using the formuli above we know that there are 8 subnets with 32 addresses each.
we can work out that the range of ip addresses for this subnet are **192.168.59.191 - 192.168.59.223**
the ip address for interface A1 can be any of the addresses in this range except for:
- 192.168.59.191 - host.
- 192.168.59.223 - broadcast.
- 192.168.59.222 - taken by interface B1.