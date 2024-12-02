# CTF Challenge: Vault Door 3 

## Table of Content

- commands-executed:   simple reverse engineering
- flag : picoctf{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}


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
Enter 32 bit stringABCDEFGHIJKLMNOPQRSTUVWXYZ123456
Output:
ABCDEFGHPONMLKJI5R3T1VYXWZU2S4Q6

=== Code Execution Successful ===


jU5t_a_sna_3lpm18g947_u_4_m9r54f
```
1 - 8 as it is 	
jU5t_a_s
9-16 reversed : 
jU5t_a_s1mpl3_an
17 - second last character
18 remains 18 
jU5t_a_s1mpl3_an4g
19  -- 29 
20 as it is 
jU5t_a_s1mpl3_an4gr4
21 --- last sixth
22 --- remains as it is. 
jU5t_a_s1mpl3_an4gr4m_
 23 --- 25 
jU5t_a_s1mpl3_an4gr4m_4
24 --- remains 24. 
jU5t_a_s1mpl3_an4gr4m_4_
25 --- 23 
jU5t_a_s1mpl3_an4gr4m_4_u
26 -- remains as it is. 
jU5t_a_s1mpl3_an4gr4m_4_u_
27 -- 21
jU5t_a_s1mpl3_an4gr4m_4_u_7
28 -- as it is 
jU5t_a_s1mpl3_an4gr4m_4_u_79
29 --- 19
jU5t_a_s1mpl3_an4gr4m_4_u_799
30 -- as it is 
jU5t_a_s1mpl3_an4gr4m_4_u_7995
31 --- 17 
jU5t_a_s1mpl3_an4gr4m_4_u_79958
32 - same 
jU5t_a_s1mpl3_an4gr4m_4_u_79958f
```										

- we follow these very changes and can reverse the output.
- we know final string must be jU5t_a_sna_3lpm18g947_u_4_m9r54f
-After all the changes we get

==picoctf{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}==
 
#### Output:

Enter 32 bit stringABCDEFGHIJKLMNOPQRSTUVWXYZ123456
Output:
ABCDEFGHPONMLKJI5R3T1VYXWZU2S4Q6
