- asymmetric form of encryption.
- you have a private key which is to be kept a secret
- a public key which is to be given to anyone you want to be in contact with , basically they can decrypt your message or encrypt their mssg
- to send to you. 
https://www.youtube.com/watch?v=wXB-V_Keiu8
- you cant encrypt a lot of info with rsa , only data that is less than rsa key size , usually 256 bytes.
- 91 hr clock example , anything raised to power 5 if again is raised to 29 you get the original result on the clock
- m^(ed) mod n = answer
- multiplicaton is easy , but prime factorisation is hard.

- generate one prime number over 150 dig long , second prime number of same length and multiply , this would give 300 dig+ number say N
- p1 * p2 is hidden , N is shared , it would take years to find p1 and p2.
- euler's phi function , basically say for a number it returns number of numbers that are less than or equal to 8 that share a factor not greater than 1 with N
- example phi(8) = 4 as : 1,2,3,4,5,6,7,8 ; only 1,3,5,7 share a factor with 8 that is not greater than 1.
- phi is easiest to calc for a prime number andd phi(prime_number) = prime_number-1 ; say 7 : 1,2,3,4,5,6 i.e 7-1 i.e 6.
- phi(a*b) = phi(a)*phi(b)
- using this for n:
- phi(n) = phi(p1) * phi(p2) , now p1,p2 are primes therefore :
- phi(n) = p1-1 * p2-1
**euler's theorem**
