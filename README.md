# CSCV2025-FINAL-WRITEUP-CASECHARLIE
This is write up for challenge Case Charlie (Forensics) in CSCV2025 FINAL

**From MTA.SUPPORT (Military Technical Academy)**

Hi everyone, last Saturday I have solved this forensics challenge in the final round of Cybersecurity Contest Viet Nam 2025. Today, I will tell you how to solve this 400 points challenge.

<img width="608" height="706" alt="image" src="https://github.com/user-attachments/assets/963c8459-23e6-49bd-9751-8c03a5154149" />


**1, Preparation**

- First, I download the file gave by Author (This file is nearly 10GB so that I had downloaded it 2 days before the contest started). After download and unzip file, I have 3 files below
<img width="1632" height="361" alt="image" src="https://github.com/user-attachments/assets/54bf3da0-4483-4d40-9126-59b913aeef33" />

- Next, I read file Readme.pdf and read all the information of this situation
<img width="1154" height="654" alt="image" src="https://github.com/user-attachments/assets/17889a97-dce5-4030-9162-4bc9c83bc59a" />
- Collecting all the information and the password to unzip file evidences, I conclude that this is a cybercrime investigation involving unauthorized hacking, data theft and crypto. My task is to analyze the seized server, recover information related to the suspect, and answer investigative questions
  
=> I need to analysis file evidences.vmdk (get this file after unzip `evidences`) and connect to the instance and answer question

- Following, I fetch instance and connect to my virtual machine by netcat
  <img width="688" height="128" alt="image" src="https://github.com/user-attachments/assets/80402a2a-d47e-4f8b-a81a-02a1034ea404" />
  
=> This challenge request us to answer 6 questions relate to a cybercrime

**2, Analysis**

**Question 1:**  What was the last time the suspect logged into the server? (UTC / 24 hours format)  

- Because we all know that wtmp is a file that records every login/logout session. When a user logs in, Linux writes a new record to wtmp. When the user logs out, another record is written.

→ Every new login → wtmp is written → the file is “modified”. So that I find the wtmp in the disk and note the last time this file modified

`root/var/log/wtmp`

<img width="1913" height="916" alt="image" src="https://github.com/user-attachments/assets/f7c9b4ab-6311-4c3b-9a9b-f4f869f02a7d" />

- It can be easy to see that the answer is `2025-11-08 04:32:56`

**Question 2:** The suspect used a chat application to communicate. What is the name of this application? Format: chatapp. Example: whatsapp, telegram, Discord

- The author give us a example of chat application, so that I need to file a suspect app contain the communication between suspects
- After find information for nearly 30 minutes, I finally find a doubt conversation between s3v3n_wOndEr113 and the0nlymak3r1338
<img width="1895" height="915" alt="image" src="https://github.com/user-attachments/assets/9286141f-f5b1-4c22-b9d9-f5fe8c5344bb" />
- The first line is: **12:56 -!- Irssi: Starting query in liberachat with the0nlymak3r1338**

  -> the suspect app is `Irssi`

**Question 3** Identify the usernames (handles) of the suspect and their contact in the chat application. (Case Sensitive) Format: uS3rNaME13, c0nT4cTn4m3

- This question is easy because I have already found 2 peoples chatting in the logs
  -> the usernames is: `s3v3n_wOndEr113, the0nlymak3r1338`

**Question 4** What was the last time the suspect sent a message to their contact? (UTC / 24 hours format) Format: YYYY-MM-DD HH:MM  

- The author ask us when the time the conversation ended, read the log and scroll to the end, it is easy to see that the time is 04:36
- The chat is opened Fri Nov 07 12:56:16 2025 (On the top of the log)
  -> `the answer is: 2025-11-08 04:36`

**Question 5** What command did the suspect use to overwrite the current user's .bash_history file to cover their tracks?

