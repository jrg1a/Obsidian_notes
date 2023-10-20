Access control refers to the mechanisms and processes that are used to regulate and manage access to resources, systems, or information. It is a fundamental aspect of computer security that ensures that only authorized entities can access and perform actions on resources while preventing unauthorized access and maintaining data confidentiality, integrity, and availability.

Access control involves defining and enforcing policies that determine who can access what resources, under what conditions, and with what privileges. The goal is to protect sensitive data, prevent unauthorized modifications or disclosures, and maintain the overall security and integrity of a system.

There are several commonly used access control models and mechanisms, including:
1. Discretionary Access Control (DAC): DAC is based on the concept of discretionary access rights, where the resource owner has the discretion to define access permissions for other users or entities. Each resource has an associated access control list (ACL) that specifies the permissions granted to different users or groups.
2. Mandatory Access Control (MAC): MAC is a more strict and centralized access control model that is typically used in high-security environments. It assigns security labels to both users and resources and enforces access decisions based on predefined rules and policies. The labels are used to determine the level of sensitivity or classification of the resource, and access is granted or denied based on the security clearances of users.
3. Role-Based Access Control (RBAC): RBAC assigns access permissions based on predefined roles or job functions. Users are assigned roles, and permissions are associated with those roles. This simplifies administration by grouping users with similar access requirements into roles, making it easier to manage access control policies.
4. Attribute-Based Access Control (ABAC): ABAC is a flexible access control model that considers various attributes of users, resources, and environmental conditions to make access control decisions. It uses policies that define rules based on attribute values and evaluates those rules dynamically to determine access rights.

Access control mechanisms can be implemented at different levels, including the operating system, network infrastructure, databases, web applications, and other software systems. Access control can involve authentication mechanisms to verify the identity of users, authorization mechanisms to determine their access privileges, and audit mechanisms to monitor and log access events for security analysis and compliance.

Effective access control is crucial for protecting sensitive information, preventing unauthorized access and data breaches, and ensuring compliance with security policies and regulations. It is an integral part of designing and implementing secure systems and plays a significant role in maintaining the confidentiality, integrity, and availability of data and resources.

## Subjects, Objects and Actions
In access control, subjects, objects, and actions are key elements that play a central role in determining and enforcing access permissions and security policies. Here's a closer look at each of these concepts:
1. Subjects: Subjects are entities that can initiate actions and interact with resources or objects in a system. Subjects are often referred to as actors or users and can represent individuals, processes, or system components. Subjects can have unique identifiers and are associated with attributes such as roles, permissions, and authentication credentials. Subjects are the entities for which access control decisions are made.
2. Objects: Objects, also known as resources, are the entities that subjects access or interact with. Objects can represent various system resources such as files, databases, network devices, web services, or any other entity that needs protection. Objects have their own set of attributes and properties that define their characteristics and behavior. Examples of object attributes include ownership, sensitivity, classification, and access permissions.
3. Actions: Actions refer to the operations or activities that subjects can perform on objects. Actions are typically defined based on the functionalities and requirements of the system. Examples of actions include read, write, execute, delete, create, modify, or any other operation specific to the system or resource being accessed. 

Together, subjects, objects, and actions form the basis for access control decisions. Access control policies define the relationship between subjects, objects, and actions and specify which subjects are allowed or denied access to specific objects for certain actions. The policies may be based on various criteria such as the subject's identity, role, group membership, attributes, or any other relevant factors.

Access control mechanisms evaluate the access control policies and enforce the defined permissions. When a subject requests access to an object, the access control mechanism checks whether the subject's credentials and authorization allow the requested action on the object. If the access is authorized, the action is performed; otherwise, the access is denied, and appropriate measures, such as generating an access control violation alert, may be taken.

By effectively managing subjects, objects, and actions, access control systems provide a structured approach to ensure that only authorized entities can perform allowed actions on resources. This helps protect sensitive data, prevent unauthorized modifications or disclosures, and maintain the overall security and integrity of the system. Access control plays a crucial role in maintaining confidentiality, integrity, and availability while enabling secure and controlled access to resources in a system.

## Mandatory Access Control
Mandatory Access Control (MAC) is a model used in access control systems to enforce security policies.
- MAC is a model in which access control decisions are based on the classification and labels assigned to subjects and objects. It is a more rigid and centralized approach to access control.
- Security labels are used to classify objects and subjects based on their sensitivity, importance, or other predefined attributes. These labels are typically assigned by system administrators or security officers.
- Access decisions are made by comparing the security labels of subjects with the security labels of objects and applying a set of predefined rules or policies. These rules determine whether a subject is allowed to access or perform actions on an object based on their security clearances and the classification of the object.
- MAC is commonly used in highly secure environments such as military systems, government agencies, or organizations with strict information protection requirements.
Example:
- In a military organization, a classified document may be labeled as "Top Secret" while an employee may have a security clearance of "Secret." The MAC policy would enforce that only individuals with a security clearance higher than or equal to the classification level of the document can access it.
- SELinux
- Linux Security Models (AppArmor)
- Mandatory Integrity Control on Windows (Extending ACLs)
- Language based mechanisms (e.g. Java Security Manager)
- Modern operating systems have mandatory access control on resources such as CPU, memory and storage.

## Discretionary Access Control (DAC)
A model used in access control systems to enforce security policies.
- DAC is a more flexible and decentralized access control model in which the owners or creators of objects have the discretion to control access to those objects.
- In DAC, access control decisions are based on the identity or attributes of subjects, as well as the permissions granted by the owners or administrators of the objects.
- Owners or administrators are granted the authority to define access permissions and grant or revoke access rights to other subjects. This allows for more granular control and flexibility in determining who can access an object and what actions they can perform on it.
- DAC is commonly used in general-purpose operating systems, file systems, and many commercial applications.
Example:
- In a file-sharing system, a user who creates a file can specify which other users or groups are allowed to read, write, or modify the file. The user has discretionary control over the access permissions of the file and can modify them as needed.
- E-mail:
	- When you create an email account, you become the owner of that account. You have the authority to set a password for the account, which grants you exclusive access to your emails.
	- As the owner, you can also grant access to other individuals by sharing your email password with them. You have discretionary control over who can access your emails and perform actions such as reading, sending, or deleting messages.
- WIFI passwords:
	- As the owner or administrator of a Wi-Fi network, you have the discretion to set a password to control access to the network.
	- When you set a Wi-Fi password, you determine who can connect to the network and access the internet. Only individuals who know the password can gain access, and you can change or revoke the password at any time, granting or denying access as you see fit.
- Both email and Wi-Fi passwords exemplify the discretionary nature of access control. The owners have the authority to define access permissions by setting and managing passwords, allowing or restricting access to the respective resources (email account and Wi-Fi network) based on their discretion.

## MAC vs DAC
- MAC is more centralized and imposes security policies based on classification and labels assigned to subjects and objects. DAC, on the other hand, allows owners or administrators to determine access permissions based on their discretion.
- MAC is typically used in high-security environments with strict information protection requirements, while DAC is more commonly used in general-purpose systems where flexibility and user control are desired.
- MAC provides a higher level of control and is less susceptible to accidental or intentional misuse, as access decisions are made centrally and enforced uniformly. DAC, on the other hand, provides more user autonomy but can be less restrictive and more prone to potential security risks if permissions are not carefully managed.

It's important to note that MAC and DAC are not mutually exclusive, and many systems combine elements of both models to achieve a balance between security and flexibility based on their specific requirements.

## Access Control Models
Access Control Models provide a framework for enforcing access control policies and managing the security of information systems. Here's an overview of three prominent access control models:
1. Bell-LaPadula Model (1973):
    - The Bell-LaPadula (BLP) model focuses on confidentiality and is designed to protect sensitive information from [[Authentication|unauthorized]] access.
    - It introduces the concept of security levels, such as "Top Secret," "Secret," "Confidential," and "Unclassified," to categorize information based on its sensitivity.
    - The model enforces two main principles: the "No Read Up" property, which prevents information flow from lower to higher security levels, and the "No Write Down" property, which prevents information flow from higher to lower security levels.
    - BLP aims to prevent unauthorized users from accessing classified information and ensure that information is only accessed by users with the necessary security clearances.
2. Biba Model (1975):
    - The Biba model focuses on data integrity, ensuring that information is not modified or corrupted by unauthorized actions.
    - It introduces the concept of integrity levels, such as "High Integrity," "Medium Integrity," and "Low Integrity," to categorize information based on its criticality.
    - The model enforces two main principles: the "No Read Down" property, which prevents information flow from higher to lower integrity levels, and the "No Write Up" property, which prevents information flow from lower to higher integrity levels.
    - Biba aims to prevent unauthorized users from compromising data integrity by modifying or corrupting information that they are not authorized to modify.
3.  Graham-Denning Model:
    - The Graham-Denning model focuses on the creation, deletion, and ownership of objects within a system.
    - It defines the rules and procedures for creating and deleting objects and specifies how ownership of objects can be transferred.
    - The model emphasizes the principle of "rights amplification," where users can only perform actions on objects they own or have been granted access to.
    - The Graham-Denning model helps ensure that object creation and ownership are managed securely and that unauthorized users cannot manipulate or gain control over objects they do not own.

These access control models provide a structured approach to access control and help organizations enforce security policies based on the specific requirements of confidentiality, integrity, and object ownership.

### Access Control List
Access Control Lists (ACL) is a common access control model used to enforce security and manage access rights in information systems. Here's an overview:
- Access Control Lists are a widely used access control model that associates permissions with individual users or groups.
- In an ACL model, each object or resource has an associated list of access control entries (ACEs), which define the access permissions for specific users or groups.
- ACEs typically include information such as the identity of the user or group, the type of access allowed (e.g., read, write, execute), and any additional conditions or restrictions.
- ACLs provide fine-grained control over access rights, allowing administrators to define specific permissions for different users or groups on a per-object basis.
- ![[Pasted image 20230523102112.png]]
- ![[Pasted image 20230523102133.png]]
- Mathematical Description:
- ![[Pasted image 20230523102205.png]]

### Role-Based Access Control (RBAC)
- Role-Based Access Control is a widely adopted access control model that associates permissions with roles, which are then assigned to users.
- In an RBAC model, users are assigned roles based on their job functions or responsibilities, and access permissions are associated with these roles.
- This model simplifies access management by allowing administrators to define roles and assign permissions to those roles, rather than assigning permissions to individual users.
- ![[Pasted image 20230523102317.png]]
- RBAC provides scalability and flexibility, as access rights can be easily managed and updated by modifying the roles assigned to users.
- ![[Pasted image 20230523102344.png]]
- Example of RBAC in code:
```Java
U = {alice,bob} and  
R = {doctor, patient}  
P = {writePerscription, withdrawMedicine}  
RolePerm = {(doctor,writePerscription), (patient,  
withdrawMedicine)}  
UserRoles =  
{(alice,doctor),(bob,patient),(alice,patient)}
```

### Capability-Based Access Control (CBAC)
- Capability-Based Access Control is a security model that grants access rights based on possession of specific capabilities or tokens.
- In a CBAC model, each user or entity is assigned a set of capabilities that represent their access permissions.
- Users can only perform actions or access resources for which they possess the appropriate capabilities.
- Capabilities can be seen as proof of authorization, and users can transfer or delegate their capabilities to other entities if allowed by the system.
- CBAC provides fine-grained control over access, as users can only exercise the capabilities they possess.
- ![[Pasted image 20230523102605.png]]

These access control models offer different approaches to managing access rights and enforcing security policies. The choice of model depends on the specific requirements of the system, the complexity of access control rules, and the desired level of flexibility in managing access rights. Organizations often choose a combination of these models to implement a comprehensive access control strategy.

### Access Control in UNIX Systems
Access control in the UNIX system is primarily governed by the discretionary access control (DAC) mechanism, which is based on user and group permissions. In UNIX-like operating systems, each file and directory has associated access control lists (ACLs) that define who can access or modify them. The permissions are categorized into three levels: read (r), write (w), and execute (x), with different combinations determining the access rights for the owner, group, and others.

However, the UNIX access control model has certain vulnerabilities that can be exploited by attackers. Here are a few examples:
1. Privilege Dropping:
    - UNIX systems often run with elevated privileges for certain processes or services to perform specific tasks.
    - Attackers can target these privileged processes to gain unauthorized access or execute malicious code.
    - To mitigate this, UNIX systems implement the principle of least privilege (POLP), which involves dropping privileges after performing privileged operations to limit the potential damage an attacker can do.
2. Exploiting Weak File Permissions:
    - Misconfigurations or incorrect permissions on files or directories can lead to unintended access by unauthorized users.
    - Attackers may exploit weak file permissions to gain access to sensitive data, modify critical system files, or escalate privileges.
    - Regular monitoring and enforcement of appropriate permissions are essential to minimize the risk of unauthorized access.
3. Exploiting Set-UID Programs:
    - Set-UID (Set User ID) programs allow users to execute a program with the privileges of the program owner.
    - If a Set-UID program has vulnerabilities or is improperly configured, attackers can exploit it to gain elevated privileges.
    - It is crucial to carefully review and validate the security of Set-UID programs to prevent privilege escalation attacks.
4. Race Conditions:
    - Race conditions occur when the outcome of a process depends on the sequence and timing of events.
    - Attackers can exploit race conditions to bypass access controls and gain unauthorized access to resources or manipulate files.
    - Proper synchronization mechanisms and secure coding practices are necessary to mitigate race condition vulnerabilities.

To enhance the security of access control in UNIX systems, additional security measures such as mandatory access control (MAC) mechanisms like SELinux or AppArmor, intrusion detection systems, and regular security audits are recommended. It is crucial to keep the system updated with security patches, follow security best practices, and limit unnecessary privileges to minimize the risk of attacks.