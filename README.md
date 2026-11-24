# Password-Security-Assessment-Using-Hydra
A hands-on cybersecurity project demonstrating password security assessment using THC Hydra in Kali Linux. Includes FTP authentication testing, custom wordlists, Nmap service identification, practical implementation, result analysis, and security recommendations in an isolated virtual lab.
# Password Security Assessment Using Hydra in Kali Linux

## 1. Introduction

THC Hydra is a popular password auditing tool used by cybersecurity professionals and penetration testers to evaluate authentication security.

It supports multiple network protocols, including FTP, SSH, HTTP, SMB, and others.

This project demonstrates the practical implementation of Hydra in Kali Linux to perform a controlled dictionary-based password security assessment against an authorized Metasploitable 2 virtual machine.

## 2. Project Objectives

- Understand the functionality of THC Hydra.
- Install and configure Hydra in Kali Linux.
- Understand dictionary-based password auditing.
- Identify FTP services using Nmap.
- Create a custom test password list.
- Perform an authorized FTP authentication audit.
- Analyze the results of the assessment.
- Understand password security vulnerabilities.
- Recommend security improvements.

## 3. Lab Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| Target Machine | Metasploitable 2 |
| Virtualization | VMware Workstation Pro |
| Security Tool | THC Hydra |
| Network Scanning Tool | Nmap |
| Target Protocol | FTP |
| FTP Port | 21 |
| Testing Method | Dictionary-based password auditing |

## 4. Network Configuration

Both virtual machines were configured on an isolated private VMware network.

### Network Details

| Machine | IP Address |
|---|---|
| Kali Linux | 192.168.153.128 |
| Metasploitable 2 | 192.168.153.129 |


## 5. Hydra Installation

First, the Kali Linux package repository was updated.

```bash
sudo apt update
```

Hydra was installed using:

```bash
sudo apt install hydra -y
```

To verify the installation:

```bash
hydra -h
```

**Screenshot 01: Hydra Installation**

<img width="1035" height="647" alt="image" src="https://github.com/user-attachments/assets/0ecb7fd4-cfcd-43e2-adb2-e3bed05dc858" />


**Screenshot 02: Hydra Help Menu**

<img width="1035" height="647" alt="image" src="https://github.com/user-attachments/assets/5ffced80-db4b-4a4d-b366-5ac97435b574" />


## 6. Target Network Connectivity

The IP address of Kali Linux was identified using:

```bash
ip addr
```

The IP address of Metasploitable 2 was identified using:

```bash
ifconfig
```

Network connectivity was tested using:

```bash
ping -c 4 192.168.153.129
```

**Screenshot 03: Kali Linux IP Address**

<img width="1035" height="647" alt="image" src="https://github.com/user-attachments/assets/0faaf219-4bac-4ccf-bd48-09f29e9b2bcb" />


**Screenshot 04: Metasploitable 2 IP Address**

<img width="1025" height="340" alt="image" src="https://github.com/user-attachments/assets/f77183a0-81d2-4c38-988f-69d1a0078a28" />


**Screenshot 05: Successful Ping Test**

<img width="1035" height="529" alt="image" src="https://github.com/user-attachments/assets/1b8066ce-362b-4d81-9c27-92a5d90649ed" />


## 7. FTP Service Identification

Nmap was used to identify the FTP service running on the target machine.

Command:

```bash
nmap -sV -p 21 192.168.153.129
```

The scan was used to determine whether port 21 was open and identify the FTP service.

**Screenshot 06: Nmap FTP Service Detection**

<img width="1035" height="528" alt="image" src="https://github.com/user-attachments/assets/3814916a-e5e9-48ae-aba5-fe089292c4b7" />


## 8. Creating a Custom Password List

A project directory was created in Kali Linux.

```bash
mkdir -p ~/Hydra-Project
cd ~/Hydra-Project
```

A custom test password list was created.

```bash
nano passwords.txt
```

Sample test entries:

```text
test123
password123
admin123
msfadmin
```

The password list was verified using:

```bash
cat passwords.txt
```

**Screenshot 07: Creating the Custom Password List**

<img width="1035" height="528" alt="image" src="https://github.com/user-attachments/assets/8f8f81db-31e5-41a3-95cc-ad9670447526" />


## 9. Hydra Command Implementation

The following command was used for the authorized FTP password audit:

```bash
hydra -l msfadmin -P passwords.txt -t 2 -V ftp://192.168.153.129
```

### Command Explanation

| Parameter | Description |
|---|---|
| hydra | Starts the Hydra application |
| -l | Specifies a single username |
| msfadmin | Authorized test account |
| -P | Specifies a password list |
| passwords.txt | Custom test password file |
| -t 2 | Uses two parallel tasks |
| -V | Displays attempted login details |
| ftp:// | Specifies FTP protocol |

**Screenshot 8: Hydra audit result**

<img width="1035" height="528" alt="image" src="https://github.com/user-attachments/assets/082b7268-ece6-437e-a961-c48dc773df8a" />


## 10. Hydra Assessment Results

Hydra was executed against the FTP service in the isolated virtual lab.

The tool tested the custom password candidates against the authorized test account.

### Results Table

| Parameter | Observation |
|---|---|
| Target IP | 192.168.153.129 |
| Protocol | FTP |
| Port | 21 |
| Username | msfadmin |
| Wordlist | passwords.txt |
| Number of Candidates | 4 |
| Authentication Result | [21][ftp] host: 192.168.153.129   login: msfadmin   password: msfadmin |

**Screenshot 9: Hydra Authentication Audit Results**

<img width="1035" height="528" alt="image" src="https://github.com/user-attachments/assets/0ecd1f2f-1028-4591-8650-2ec9558ac19f" />


## 11. Result Analysis

The assessment demonstrated how dictionary-based password auditing works.

Hydra attempts authentication using the supplied username and password candidates.

If a valid credential is found, the tool reports the successful authentication result.

This practical exercise demonstrates that weak or default passwords can expose network services to unauthorized access.

The results should be interpreted only in the context of the authorized lab environment.

## 12. Security Recommendations

The following security measures can help improve authentication security:

1. Use strong and unique passwords.
2. Avoid default usernames and passwords.
3. Disable unnecessary network services.
4. Prefer SFTP instead of unencrypted FTP.
5. Implement account lockout or rate limiting.
6. Monitor repeated authentication failures.
7. Implement multi-factor authentication where supported.
8. Regularly audit authentication security.

## 13. Learning Outcomes

After completing this project, I gained practical knowledge of:

- Installing and using THC Hydra.
- Understanding password auditing techniques.
- Identifying FTP services using Nmap.
- Creating custom password lists.
- Understanding authentication weaknesses.
- Analyzing password audit results.
- Understanding the importance of strong passwords.
- Performing authorized security testing in a virtual lab.

## 14. Conclusion

This project demonstrated the practical use of THC Hydra in Kali Linux for password security assessment.

An isolated Metasploitable 2 environment was used to understand dictionary-based FTP authentication testing.

The exercise highlighted the security risks associated with weak and default passwords and demonstrated the importance of implementing strong authentication policies.

All activities were performed within an authorized virtual lab environment.

## 15. Disclaimer

This project was developed for educational purposes and authorized cybersecurity testing.

THC Hydra should only be used against systems that you own or have explicit permission to test.

Unauthorized password attacks against third-party systems are prohibited.
