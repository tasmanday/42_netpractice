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

where *n* is the number of bits used for subnetting (1s in binary subnet mask).

the formula to calculate the number of ip addresses per subnet is:

**Number of ip addresses = 2<sup>m</sup>**

where *m* is the number of host bits (0s in binary subnet mask).

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

interface B1:

the subnet mask must match that of interface A1 as there is no router.
- subnet mask should be **255.255.255.224 or /27**.

interface C1 & D1

subnet mask 255.255.255.252 = 11111111.11111111.11111111.11111100 = /30
this mask has 64 subnets with 4 addresses each.
again the first and last addesses of each subnet are the host and broadcast addresses.
this leaves the middle 2 host addresses per subnet.
the original ip addresses in these boxes seem like they would work but 127.0.0.0 adresses are reserved for loopback and IPC on the local host.

------------------------------------------
level 3
<br><br><br>
interface A1:

the subnet mask for all interfaces need to match the given unchangable mask of interface C1.
- 255.255.255.128 or /25.

interface B1:

the subnet mask for all interfaces need to match the given unchangable mask of interface C1.
- 255.255.255.128 or /25.
the ip address range for based on the subnet mask and the given unchangable ip address at interface A1 is **104.198.180.0 - 104.198.180.127**.
the ip address for interface B1 must be:
- within that range.
- not the host or broadcast addresses.
- not the same as the addresses at A1 and C1.

interface C1:
the ip address range for based on the subnet mask and the given unchangable ip address at interface A1 is **104.198.180.0 - 104.198.180.127**.
the ip address for interface C1 must be:
- within that range.
- not the host or broadcast addresses.
- not the same as the addresses at A1 and B1.

------------------------------------------
level 4
<br><br><br>
the subnet masks for interface A1, interface B1, & interface R1 must all be the same and must be able to support 3 host addresses.
the ip addresses for interface B1, & interface R1 must be in the same subnet range as the given A1 ip (122.130.111.132).

------------------------------------------
level 5
<br><br><br>
interface A1:

the subnet mask for interface A1 must match that of interface R1 and the ip address must be in the same subnet ip range.
this ip range is 50.24.79.0 - 50.24.79.127 but the first and last addresses are reserved and 50.24.79.126 is already taken by interface R1.
- the possible acceptable host addresses for interface A1 are 50.24.79.1 - 50.24.79.125.
- the subnet mask is 255.255.255.128

Host A Routes:

since there is only one route that host A canb send it's packets the destination can be default.
the next hop is the ip address of the next router (or internet) interface to which the interface of the current machine must send its packets.
for host A the next router interface is interface R1.
- destination is 'default'
- next hop is 50.24.79.126

interface B1:

the subnet mask for interface B1 must match that of interface R2 and the ip address must be in the same subnet ip range.
