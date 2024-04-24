# 42_netpractice

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
