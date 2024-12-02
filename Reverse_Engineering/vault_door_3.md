# CTF Challenge: Vault Door 3 

## Table of Content

- commands-executed:   
- flag : 


### Chain of thought / Learning:
- all i have is a java file with the code: 
```java
  import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18g947_u_4_m9r54f");
    }
}
```
-the function checkPassword performs a very simple function, it takes the input string , rearranges the letter according to the loops and then returns the output. 
- It'll take forever to figure out what each loop does , so my plan of action is , write a c code for this same program
```c
// Online C compiler to run C program online
#include <stdio.h>

int main() {
    char buffer[32],password[32]; 
    int i;
    printf("Enter 32 bit string");
    for(i=0;i<32;i++)
    {
        scanf("%c",&password[i]);
    }
    
    
    
    
    for (i=0; i<8; i++) {
            buffer[i] = password[i];
        }
        for (; i<16; i++) {
            buffer[i] = password[23-i];
        }
        for (; i<32; i+=2) {
            buffer[i] = password[46-i];
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password[i];
        }
        
    printf("Output:\n");
    for(i=0;i<32;i++)
    {
        printf("%c",buffer[i]);
    }
    return 0;
}
```
-This code will do the same thing to the input as the java while, so now we can provide this with a test input , figure out how the characters and rearranged and work our way backwards to figure out the original input. 
```console
O/P OF C CODE :
Enter 32 bit stringABCDEFGHIJKLMNOPQRSTUVWXYZ123456
Output:
ABCDEFGHPONMLKJI5R3T1VYXWZU2S4Q6
```
Characters 1-8 (ABCDEFGH) remain unchanged in both strings.
Characters 9-16 (IJKLMNOP) are reversed to PONMLKJI in the output.
I (9) → P (9)
J (10) → O (10)
K (11) → N (11)
L (12) → M (12)
M (13) → L (13)
N (14) → K (14)
O (15) → J (15)
P (16) → I (16)
Character 17 (Q) is replaced by 5.
Q (17) → 5 (17)
Character 18 (R) is replaced by R.
No change (R (18) → R (18))
Character 19 (S) is replaced by 3.
S (19) → 3 (19)
Character 20 (T) is replaced by T.
No change (T (20) → T (20))
Character 21 (U) is replaced by 1.
U (21) → 1 (21)
Characters 22-26 (VWXYZ) are reversed to VYXWZ.
V (22) → V (22)
W (23) → Y (23)
X (24) → X (24)
Y (25) → W (25)
Z (26) → Z (26)
Character 27 (1) is replaced by U.
1 (27) → U (27)
Character 28 (2) is replaced by 2.
No change (2 (28) → 2 (28))
Character 29 (3) is replaced by S.
3 (29) → S (29)
Character 30 (4) is replaced by 4.
No change (4 (30) → 4 (30))
Character 31 (5) is replaced by Q.
5 (31) → Q (31)
Character 32 (6) is replaced by 6.
No change (6 (32) → 6 (32))

- we follow these very changes and can reverse the output.
- we know final string must be jU5t_a_sna_3lpm18g947_u_4_m9r54f
-
jU5t_a_sna_3lpm18g947_u_4_m9r54f




 
#### Output:
