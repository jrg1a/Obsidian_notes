A buffer overflow is a type of software vulnerability that occurs when a program attempts to store data beyond the boundaries of a fixed-size buffer or an allocated memory space. This can lead to unexpected and potentially malicious behavior, as the extra data may overwrite adjacent memory locations, including crucial program data, control structures, or even executable code. Buffer overflows are a common security concern and can have serious consequences, including system crashes, data corruption, and potential exploitation by attackers.

Here are some key points to understand about buffer overflows:
1.  Buffer Size Mismatch: Buffer overflows typically occur when a program writes more data into a buffer than it can hold. This can happen due to incorrect calculations or assumptions about the buffer size, improper input validation, or lack of boundary checks during data copying or input processing.
2.  Memory Corruption: When a buffer overflow occurs, it can overwrite adjacent memory locations beyond the intended buffer boundaries. This can corrupt important program data, such as variables, function pointers, or return addresses on the stack. In some cases, the overwritten memory can contain malicious code injected by an attacker.
3.  Code Execution: One of the most severe consequences of a buffer overflow is the potential for arbitrary code execution. If an attacker can overwrite a function pointer or a return address with a malicious address, they can redirect the program's execution flow to their injected code, enabling them to execute arbitrary commands or launch further attacks.
4.  Security Implications: Buffer overflows are a significant security risk as they can be exploited to gain unauthorized access, execute malicious code, or perform privilege escalation. Attackers can leverage buffer overflows to bypass security mechanisms, inject malware, or launch denial-of-service attacks.
5.  Prevention and Mitigation: To prevent buffer overflows, secure coding practices are crucial. This includes proper input validation, bounds checking, and using secure string manipulation functions or libraries that handle buffer sizes automatically. Language-specific techniques such as safe string functions, bounds-checked arrays, or memory-safe languages can also help mitigate buffer overflow vulnerabilities.
6.  Vulnerability Discovery and Patching: Security researchers and developers use various techniques, such as code reviews, static analysis tools, and fuzz testing, to identify and fix buffer overflow vulnerabilities. Patches and updates should be promptly applied to address known vulnerabilities in software.

It is important to note that buffer overflows are preventable by following secure coding practices, implementing proper input validation, and utilizing appropriate defensive programming techniques. By understanding the risks associated with buffer overflows and adopting best practices, developers can significantly reduce the likelihood of such vulnerabilities in their software.

## What is a Buffer Overflow?
A buffer overflow occurs when a program tries to write more data into a buffer than it can hold, resulting in data spilling into adjacent memory locations. This can lead to memory corruption, crashes, or even remote code execution.

## Causes of Buffer Overflows
Buffer overflows can be caused by various factors, including:
-   Inadequate input validation and boundary checking.
-   Improper use of functions that manipulate strings or arrays.
-   Failure to account for buffer sizes and limitations.

## Consequences of Buffer Overflows
Buffer overflows can have severe consequences, including:
-   Corruption of data and variables in memory.
-   Alteration of program flow, leading to unexpected behavior or crashes.
-   Execution of arbitrary code, potentially allowing attackers to gain unauthorized access or control over a system.
-   Exploitation of other vulnerabilities or security weaknesses.

## Prevention and Mitigation
To prevent buffer overflows, it is important to follow secure coding practices:
-   Always validate and sanitize input data to ensure it fits within the expected buffer size.
-   Use secure string manipulation functions or libraries that handle buffer sizes automatically.
-   Perform boundary checks when copying or manipulating data.
-   Use compiler options or language features that enforce strict array bounds checking.
-   Regularly update and patch software to fix known vulnerabilities.

## Security Testing and Analysis
Developers and security professionals should conduct rigorous testing and analysis to identify and address buffer overflow vulnerabilities:
- Use static code analysis tools to identify potential buffer overflow risks during development.
- Perform fuzz testing and input validation testing to identify boundary and input-related issues.
- Conduct regular security audits and penetration testing to identify vulnerabilities in production systems.

## Importance of Secure Coding Practices
Buffer overflows are a significant security concern, but they can be prevented through secure coding practices and a strong understanding of programming language features and limitations. By adhering to best practices, developers can minimize the risk of buffer overflow vulnerabilities and enhance the security of their software systems.

## Code Examples
```Java
import java.util.Scanner; 

public class ChooseList {  
	static String[] buffer = { "apple","orange","pear","banana","tangerine"}; 
	 
	public static void main(String[] args) {  
		System.out.println("Chose something:");  
		for(int i = 0; i < buffer.length ; ++i) {  
			System.out.println((i + 1) + ". " + buffer[i]);  
		}  
		int choice = (new Scanner(System.in)).nextInt();
		
		System.out.println("Here you go: One "  
							+ buffer[choice-1] + " for you!");  
	}
}
```

```C
#include <stdio.h>  
#include <stdlib.h>  
int main() {  
	char* buffer[5] = { "apple","orange","pear","banana","tangerine"};  
	char answer[5];  
	int choice;  
	printf("Please make a choice:\n");  
	for(int i = 0 ; i < 5; ++i) {  
		printf("%d. ",i+1);  
		printf("%s\n", buffer[i]);  
	}  
	fgets(answer,5,stdin);  
	choice = atoi(answer);  
	printf("Here you go: One %s for you!\n",buffer[choice-1]);  
	return 0;
}
```

##### Questions:
- What happen if we give the input “42”?
- Why is the output different for Java and C?
- Can you explain exactly the output from the C program?

## Programs and Processes
The term “program” can refer to either:
- the source code
- the executable
While a process is a specific instance of the program which is executing. 

```C
if (request.getMethod().equals("POST")) {  
	if (request.getParameter("newforum") != null) {  
		System.err.println("Crating a new forum.");  
		Maybe<Stored<Forum>> forum = inforum.createForum((new Maybe<String> (request.getParameter("name"))).get(), con);  
		response.setStatus(HttpServletResponse.SC_MOVED_TEMPORARILY);  
		response.setHeader("Location", "/forum/" + forum.get().value.handle + "/");  
		baseRequest.setHandled(true);  
		return ;  
	}  
}
```
Programs can be created from source code in different ways:
- Compiled to machine code
- Compiled to virtual machine code (Java VM, · · · ).
- Scripts are executed by an interpreter.
- Executing a program causes a process to be started.
The operating system (OS) manages the different processes running. 
Each process has:
- a Process ID (which identifies the process)
- a (virutal) memory space
- a lot of other metadata (UID,PID,file descriptors,· · · )
How the memory space is managed is called the runtime  
environment, and depends on the compiler.
In particular, the OS does not know about:
- Variables
- Types
- Objects
- Scopes
- Functions
All these must be emulated using bits of memory and machine code.

Example:
- The binary 01100010 01100001 01101110 01101011 could be:
	- the string “bank”, or
	- the number “1650552427” (unsigned, 32 bits, big endian)
	- or a number of other things!

The memory space of a program typically contains:
- Execution instructions (an image of the program)
- The stack:
	- data needed function calls and local variables.
	- organised in “frames”.
- The heap which contains dynamically allocated data.
- But more complex languages may use additional space for organising garbage collection, green threads, etc.
- Processes make system calls to interact with the world beyond its memory space:
	- Read/write to files
	- Network access
	- Time functions
	- Inter-proccess communication
- The OS receives the call and executes the action on behalf of the process
- The system call interface is a security boundary.

## Tools
Tools used to execute buffer overflows:
- GNU/Linux (YMMV if you use other Unix derivatives)
- A C-compiler: ``gcc``
- A debugger: ``gdb``
- A dissembler: ``objdump -d``
- ``xxd``: convert back and forth between hex and bytes.
- Python
- ``pwntools``: A python library which makes everything easier. 
- ``strace``: Make a log of the system calls made by the process.

## Buffer Overflow: example
Lets start off with this code:
```C
#include <stdio.h>
int main(int argc, char* argv) {  
	char buffer[8];  
	int a = 3;  
	fgets(buffer, 256 , stdin);  
	printf("You entered: %s \n", buffer);  
	printf("and a = %i \n", a);  
}
```
And look at the basic problem with it:
![[Pasted image 20230523025228.png]]
In code:
```C
int main() {  
	char a[] = "short";  
	char b[] = "very long";  
	// Copy b into a  
	for (int i = 0 ; i < strlen(b) ; ++i)  
		a[i] = b[i];  
	printf("%s",a);  
}
```
The simplest mistake one can make in an unsafe language is reading  
outside the bounds of a buffer (array). Example: The “Heartbleed” bug in ``libssl`` was caused by not bounds checking the TLS heart-beat signal before responding.
For understanding how to buffer overflow, we need to look closer at the memory layout of a C program, and the call stack.
![[Pasted image 20230523025451.png]]
The primary purpose of the call stack is to store return addresses for function calls:
- When a function is called:
	- a return pointer is pushed on the stack. 
- When the function is done:
	- the return pointer is popped from the stack
	- and program flow is returned to the caller, following the return pointer. 
![[Pasted image 20230523025616.png]]

## Shell-Code
The easiest way to exploit a buffer overflow bug:
- Fill the buffer with attack code
- Overwrite the return pointer to point into the array.
The attack code often spawns a shell (**Shell code**), which gives the attacker RCE on the machine.

## NO-OP sled
A NO-OP sled, also known as a NOP sled or a NOP slide, is a sequence of NO-OP (No Operation) instructions inserted in a buffer or exploit payload. It is often used in buffer overflow exploits to increase the chances of successfully jumping to the injected malicious code.

The purpose of a NO-OP sled is to provide a landing zone for the exploit code. When a buffer overflow occurs and the program's instruction pointer is overwritten, the execution flow can potentially land anywhere within the sled. Since NO-OP instructions have no effect on the program's state, they effectively act as a slide, allowing the execution flow to "slide" down the sled until it reaches the actual malicious code.

The length of the NO-OP sled is typically chosen to be long enough to accommodate variations in the exact location where the execution flow lands. By making the sled sufficiently large, the chances of hitting the exploit code are increased, even if the exact starting point is slightly off.

The NO-OP sled technique is particularly useful in scenarios where the exact memory location of the exploit code is unknown or hard to predict. It provides a level of flexibility and robustness to the exploit, increasing the chances of a successful attack.

However, it's worth noting that modern systems and defenses have become more sophisticated, making the use of NO-OP sleds less effective. Various mitigation techniques, such as address space layout randomization (ASLR), can make it harder to reliably land on the sled or exploit code. Security-conscious programming practices and regular software updates are crucial to minimizing the risk of buffer overflows and related vulnerabilities.

##### Difficulty:
- Attacker does not know the address of the buffer.
- Solution for an attacker:
	- Fill most of the buffer with NO-OPs (a NO-OP sled) and put shell-cpde at the end of the buffer
- If the attacker guesses any address in the NOP part, execution slides to the shell-code
- ![[Pasted image 20230523030338.png]]

## Return Oriented Programming
Return Oriented Programming (ROP) is an exploit technique using preexisting code in the program or libraries instead of uploaded shell code. It exploits to bypass security measures like data execution prevention (DEP) and address space layout randomization (ASLR). It is a powerful method that allows an attacker to execute arbitrary code by utilizing existing snippets of code called "gadgets" within the targeted program.

In a typical buffer overflow attack, the attacker overwrites the return address on the call stack to redirect the program's control flow to a malicious payload. However, with modern security mechanisms like DEP enabled, executing arbitrary code from injected shell-code or the stack itself is prevented. This is where ROP comes into play.

ROP leverages the fact that most programs contain small pieces of executable code called gadgets. A gadget is typically a sequence of machine instructions ending with a return instruction (ret). By chaining together multiple gadgets, an attacker can create a "rop chain" that achieves the desired behavior without directly injecting new code. The attacker locates and uses existing instructions within the program's code to manipulate the stack and achieve arbitrary control flow.

The key idea behind ROP is to repurpose the existing code in a way that allows the attacker to bypass security mechanisms and execute the desired actions. Gadgets can perform operations such as modifying registers, manipulating the stack, or invoking specific system calls. By carefully selecting and chaining gadgets together, the attacker can construct a series of instructions that achieve their intended goals.

One of the advantages of ROP is that it operates within the constraints of the existing program, making it difficult to detect and defend against. The attacker does not need to introduce new code or execute from writable memory areas, which are commonly restricted. Instead, ROP utilizes the program's legitimate code segments, effectively using them as building blocks for the attack.

To successfully perform a ROP attack, the attacker needs to have knowledge of the target program's memory layout, including the addresses of gadgets and their associated instructions. This information can be obtained through reverse engineering or by analyzing the target program's behavior.

To mitigate the risk of ROP attacks, developers and security practitioners employ various countermeasures. These include implementing control flow integrity (CFI) techniques, utilizing address space layout randomization (ASLR), performing input validation and sanitization, and employing stack canaries or other buffer overflow protections. Regular security updates and patches are also essential to address known vulnerabilities that attackers might exploit.

Overall, ROP is a sophisticated technique used by attackers to bypass security mechanisms in buffer overflow vulnerabilities. It highlights the importance of secure coding practices and ongoing security measures to protect against such attacks.

## Mitigation
How to prevent catastrophic failure? Mitigating buffer overflow attacks is crucial for ensuring the security and stability of software systems. Here are some common mitigation techniques used to prevent or minimize the impact of buffer overflow vulnerabilities:
1. Input Validation and Sanitization: Implement robust input validation and sanitization techniques to ensure that user-supplied input is properly checked and sanitized before being used in critical operations. This helps prevent malicious inputs from triggering buffer overflows.
2. Bounds Checking: Enforce strict bounds checking when accessing arrays or buffers to ensure that data is not written or read beyond the allocated boundaries. This can be done using built-in language features, compiler options, or manual checks in the code.
3. Stack Canaries: Use stack canaries or stack cookies as a defense mechanism. A stack canary is a random value placed before the return address on the stack. Before executing a function's return, the canary value is checked for integrity. If it has been modified, indicating a buffer overflow, an error or termination can be triggered. However, if the attacker can somehow read the memory, they could get the value of the canary.
   ![[Pasted image 20230523030905.png]]
4. Data Execution Prevention (DEP): Enable DEP, a security feature provided by modern operating systems, which prevents executing code from non-executable memory regions. DEP helps to mitigate attacks that rely on injecting and executing arbitrary code.
5. Address Space Layout Randomization (ASLR): Enable ASLR, another security feature provided by operating systems, which randomizes the memory addresses of executable modules, libraries, and stack locations. ASLR makes it harder for attackers to locate and exploit specific memory areas.
6. Compiler-Based Protections: Use compilers that provide security-focused features like stack smashing protection (e.g., GCC's `-fstack-protector`) or automatic bounds checking (e.g., Microsoft's /GS flag).
7. Static Code Analysis: Employ static code analysis tools to identify potential buffer overflow vulnerabilities during the development process. These tools can help identify coding errors and enforce secure coding practices.
8. Regular Security Updates and Patching: Stay up-to-date with security patches and updates for the software and libraries used in your system. Vulnerabilities that could lead to buffer overflow attacks are often discovered and patched over time, so timely updates are essential.
9. Secure Development Practices: Follow secure coding practices, such as using secure [[CRUD API|APIs]]and libraries, practicing input validation, and adhering to secure coding guidelines. Writing secure code from the beginning can significantly reduce the likelihood of buffer overflow vulnerabilities.
10. Code Reviews and Penetration Testing: Conduct regular code reviews and penetration testing to identify and address potential buffer overflow issues. A thorough review process helps uncover vulnerabilities and ensures that appropriate mitigation's are implemented.

It's important to note that no single mitigation technique can guarantee complete protection against buffer overflow attacks. A layered defense approach, combining multiple mitigation strategies, is recommended to enhance the security posture of software systems. Additionally, staying informed about emerging threats and security best practices is crucial for effectively mitigating buffer overflow vulnerabilities.

Prevention:
- Best practice to avoid buffer overflows:
	- Use memory safe languages
	- Use memory-safe abstractions in unsafe languages (say vectors or smart pointers in C++)
	- Use the compiler’s abilities
	- Run static analysers to identify potential bugs
	- Enable the protections allowed by the system
	- Do not override protection mechanisms for convenience

## Resources for Learning more
- https://www.youtube.com/watch?v=1S0aBV-Waeo
- http://phrack.org/issues/49/14.html
