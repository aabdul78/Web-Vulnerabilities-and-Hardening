# Web-Vulnerabilities-and-Hardening
Homework 15

Web Application 1: Your Wish is My Command Injection

I continued my journey to enhance my technical expertise by gaining a deeper understanding of web vulnerabilities and system hardening techniques used to protect critical web infrastructure. My goal was to develop a comprehensive understanding of how web attacks are constructed, both conceptually and practically.

To begin, I accessed my Vagrant environment and opened a browser. I navigated to the webpage: http://192.168.13.25 and selected the Command Injection option. This page is part of a new web application developed by Replicants to allow customers to ping an IP address. The application returns the results of the ping command to the user.

Behind the scenes, when the Submit button is clicked, the IP address entered in the field is injected into a system command that is executed on the Replicants' web server. The specific command executed is ping, with 8.8.8.8 being the default injected value from the field. This process is akin to running the same command directly from the command line.

Upon discovering that Replicants' new application is vulnerable to command injection, I was tasked with using the dot-dot-slash method to create two payloads. These payloads were designed to display the contents of the following files:

/etc/passwd
/etc/hosts

Command Injection Prevention:

Avoid system calls and user input—to prevent threat actors from inserting characters into the OS command.
Set up input validation—to prevent attacks like XSS and SQL Injection.
Create a white list—of possible inputs, to ensure the system accepts only pre-approved inputs.

Reference page for my mitigation strategies.

https://www.imperva.com/learn/application-security/command-injection/

Running the etc/passowrd 

![image](https://github.com/user-attachments/assets/f363bd01-ca8f-449a-918c-08587acfdde8)

Running the etc/hosts

![image](https://github.com/user-attachments/assets/59302da4-3c67-417b-a7f3-ee60c500d5ea)


Web Application 2: A Brute Force to Be Reckoned With

I opened a browser within my **Vagrant** environment and navigated to the webpage **http://192.168.13.35/**. This page is an administrative web application featuring a basic login interface, where an administrator can enter their username and password before selecting the **Login** button.

- If the user/password combination is correct, it will return a successful message.
- If the user/password combination is incorrect, it will return the message, "Invalid credentials.


Open a browser before capturing traffic

![image](https://github.com/user-attachments/assets/4944e076-280a-47bb-b33b-4eb826a48892


Capturing traffic on proxy

![image](https://github.com/user-attachments/assets/b91e18a0-ff03-4336-9255-21b9e4996395)

Sending capturing traffic to intruder on proxy

![image](https://github.com/user-attachments/assets/a70a27de-1a3e-4198-8c6a-162cec5833ac)

I used **Burp Suite**, specifically the **Burp Suite Intruder** feature, to test if any of the administrator accounts in the web application were vulnerable to a brute-force attack. A list of administrators and their compromised passwords was provided for this task.

![image](https://github.com/user-attachments/assets/5c726a3e-c90f-4375-8705-8644a65d2c03)

Blocking Brute Force Attacks:

The most obvious way to block brute-force attacks is to simply lock out accounts after a defined number of incorrect password attempts. Account lockouts can last a specific duration, such as one hour, or the accounts could remain locked until manually unlocked by an administrator.

Reference page for my mitigation strategies.

https://owasp.org/www-community/controls/Blocking_Brute_Force_Attacks

Web Application 3: Where's the BeEF?


On Vagrant, I opened the command line and executed the following command: sudo beef. This command launches the BeEF (Browser Exploitation Framework) application and outputs various details about the application to the terminal. Among these details, several URLs are provided to access BeEF’s User Interface (UI), such as: UI_URL: http://127.0.0.1:3000/ui/panel.

BeEF is a practical client-side attack tool designed to exploit web browser vulnerabilities in order to evaluate the security posture of a target. The process involves an attacker deploying a small snippet of code, known as a BeEF Hook, which is typically injected into a target website via cross-site scripting (XSS). When users visit the infected website, their browsers become "hooked." Once a browser is hooked, it is referred to as a zombie — an infected browser awaiting instructions from the BeEF control panel.

The BeEF control panel provides hundreds of exploits that can be launched against the hooked browsers, enabling a wide range of attacks including...

- Social engineering attacks
- Stealing confidential data from the victim's machine
- Accessing system and network information from the victim's machine

To access the simulated infected website, I opened the site that had been compromised with a **BeEF hook**. This allowed me to view a list of folders containing hundreds of exploits that could be executed against the hooked browser. 

First, I attempted a **social engineering phishing exploit**, which involved creating a fake Google login popup. This exploit could capture user credentials, such as usernames and passwords, as the victim might easily mistake it for a legitimate login prompt. I successfully hooked into **Replicants' website** and tested a few BeEF exploits to evaluate their effectiveness.

Setting up fake facebook loging page

![image](https://github.com/user-attachments/assets/e8f1d52e-0fd4-4df9-bc9d-cc630b9bfd59)

The captured username and the password:

![image](https://github.com/user-attachments/assets/fa682c9f-6c4c-4213-bd5d-346af025ae80)

Setting up fake google loging website:

![image](https://github.com/user-attachments/assets/0debc193-d8f4-4baf-b06d-da7a72d90d5c)

Captured the username and passowrd they used:

![image](https://github.com/user-attachments/assets/b2f765f7-5a0f-4f75-8b81-4e45afcbf283)

Setting up fake notifaction bar:

![image](https://github.com/user-attachments/assets/179977d6-8d84-4a7b-bf32-c4d7fb1f1c23)

The fake notification bar clicked:

![image](https://github.com/user-attachments/assets/39449d46-049c-4501-b515-12bf737935b3)

Setting up fake Geolocation:

![image](https://github.com/user-attachments/assets/6f086a6f-df51-49f4-bf14-3c8512566b08)


Outlining mitigation strategies agains this kind of attacks:

It's important to keep your system up to date, but this is a given and wouldn't have protected you from the recent IE 0-day vulnerability.

Most browser-based exploits rely on JavaScript in some way, and tools like **NoScript** can help mitigate these types of attacks.

By default, **Google Safe Browsing API** is used by **Firefox** and **Chrome** to block access to sites known to be involved in browser-based attacks. However, this does not provide protection against targeted **BeEF** attacks.

Some **Antivirus software** can integrate with your browser to prevent exploits from loading, which could potentially block a targeted BeEF attack. However, antivirus programs aren't foolproof and can be bypassed.

To better protect yourself, plan for the possibility of a breach. Consider performing most of your browsing within a **virtual machine (VM)** and restore it to a clean state regularly—ideally once a week or once a month. Always assume that your system may have been compromised, and make it a habit to change your passwords frequently.

Reference page for my mitigation strategies.

https://security.stackexchange.com/questions/22828/what-are-methods-for-preventing-browser-hooking-drive-by-downloads















