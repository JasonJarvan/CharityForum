# CharityForum
# Overview
## Project Overview
This project has developed an online forum system, aimed at clarifying the core needs of system users and establishing a comprehensive, accurate, clear, and specific set of system specifications and design plans. This will assist the development team in efficiently constructing various components and functionalities of the system, while also providing users with a deeper understanding of the system. This document outlines the detailed demands and functional requirements of users for the system, serving as a confirmation of user requirements, a foundation for overall system design, and a reference for system verification and maintenance.

# CharityForum - Online Discussion Platform
## Features
- Supports user-selected usernames and passwords
- The purchase link is achieved by adding facebook or whatsapp.
- Users can leave messages for products.
- Users can modify or delete personal items and personal information.
- Allows posting new threads and responding to existing ones
- Members can send private messages within the platform, with automatic notifications for new messages
- Administrators can post announcements, with new announcements displayed at the top of the page in a scrolling manner
- Administrators can create and manage multiple sub-forums, set themes, appoint moderators, and independently open or close sub-forums
- Posts need to be approved by administrators, managed through "approve" or "delete" buttons
- Supports searching for content based on thread topics, keywords, authors, or sub-forums
- Administrators can control the opening and closing of the forum, and set access permissions
- Automatically identifies online users' IP addresses, operating systems, and browser versions, displaying an online user list
- Sends birthday reminders based on the birthday information provided by users
- Real-time statistics of online user numbers, posts, replies, visits, and clicks
## User Types
| User Category | Description |
| :-----------: | :---------: |
| Visitors | Limited to browsing posts |
| Registered Users | Aimed at the general public, providing a platform for discussing topics of common interest. Users can access the forum from various locations like internet cafes, offices, or homes to register, post, send private messages, and search, etc. |
| Forum Administrators | Responsible for posting announcements, setting security filters, reviewing posts, managing sub-forums, etc. |
## Key Functions
- “Register”: Users can create and edit personal profiles
- “Login”: Members can log into the system
- “Post and Reply”: Members can post new threads, reply, initiate polls, and display poll results
- “Private Messaging”: Users can exchange private messages, with unread message notifications
- “Content Filtering”: System filters user posts, marking reported information
- “Content Search”: Supports searching for existing posts in the forum
- “User Online Status”: Displays detailed information of online users
- “Birthday Reminder”: Automatically sends birthday reminders to users
- “Announcement Posting”: Administrators can post announcements
- “Sub-forum Management”: Administrators manage the themes and operational status of sub-forums
- “Content Review”: Reviews user-submitted content
- “Forum Statistics”: Displays and analyzes user activity data
## Tech Stack
- spring boot
- spring data jpa
- mysql
- spring security
- redis
- thymeleaf
- bootstrap4
## Deployment Guide
First, create a new database named db_second_hand_bbs in MySQL, then import the SQL file in the mysql folder of this project.

Modify the database configuration according to your local environment, the database configuration is in the application.properties file of the SpringBoot project.

Run the project in IntelliJ IDEA.

Alright, the server has started successfully. Now, simply enter the following URLs in the address bar:

http://localhost:8080/index

http://localhost:8080/admin/login to access the backend admin page.

You can now visit our project.

You can use the admin username and password, both are 'aaa'.


# Analysis of Requirements
## Functional Requirements
The system is broadly divided into two components:
A forum management system for administrators and a forum service system for all users.
As mentioned earlier, in our system, the BBS typically logs in via the web. Therefore, neither administrators nor users need to install the system. However, to interpret server-side scripting language code in web pages, the server side must install a corresponding web server (such as Apache or IIS), a script code interpretation engine (such as Apache Tomcat, recommended), and a database server (such as SQL Server). All users log into the forum management system after password verification to carry out backend management tasks like user management, discussion area management, and article management.

### Requirements for User Permissions
The forum system should be able to judge the user's level and identify four types of users with different permission levels after they log in to the forum service system with account password verification.
The first category is visitors, who have the permission to browse articles and query the basic information of registered users;
The second category is general users, who can post/browse/reply to topics in the forum discussion area and manage their personal information;
The third category is administrators, who can delete/feature topics, delete replied posts, block IDs, and unblock general users;
The fourth category is the main administrators, who have the highest authority and can add administrator permission changes on the basis of the administrators' rights. The detailed user permission initiation process is illustrated in the diagram.

### Data Flow Diagrams and Data Processing
Taking requests such as "password retrieval/change, posting/pinning topics, deleting posts, granting/revoking user admin rights," as examples, specific data flow diagrams are created to illustrate:

Function 1: Receive user requests to post/pin topics, delete posts, etc. (user ID, user information, target number, accompanying content or information), check the user table based on the user ID to verify if the user has corresponding permissions. If so, send the posting request information to the corresponding processing program for further processing; if not, notify the user of the error;

Function 2: Query the database, generate update, insert, select, etc., statements based on requests to post/feature articles, delete posts, etc. (user ID, user information, target number, accompanying content or information), modify or delete data, and update related tables' data;

## Data Requirements
Based on the system's data flow diagrams and data processing descriptions, the system's data structure is compiled:

### Conceptual Structure Design
Based on the results of the system requirement analysis, we designed some E-R diagrams as follows:

### Logical Design
We initially convert the E-R diagram into the following relational model (simplified version):

Users (user id, username, password, real name, address, gender, birthday, qq, nickname, registration date, total number of posts, user permission level, personal signature)

Articles (article number, user id of the poster, (username, user personal signature (these two items are read from the user table)), number of visitors, number of replies, article title, article content, posting date)

## System Menu Design
As previously mentioned, the BBS forum system is accessed via the web, i.e., system users go online and use IE to access the BBS forum system. Hence, its menu does not have a strict hierarchical structure like typical software menus. The system's menu structure is described as follows:

### Service System Menu Design
The login page of the service system's homepage should have three menu buttons: Login (after login: change information), Register, Anonymous, Management (displayed when admin rights are required). They direct the user to different functional pages of the system.

"Login" leads to a system service interface that requires permission verification, "Register" directs users to a new user registration interface. We take "Login" as a secondary menu; after entering the homepage, users can go to the login or registration interface. After logging in, the menu is divided into five secondary menu columns according to system functions: Personal Information, Homepage Browsing, Search, Logout, Management Menu.

"Personal Information" can have third-level menus as needed or for user convenience, generally including: (1) Personal information browsing; (2) Password change; (3) Personal information modification. The secondary menu of the management system is divided into the following items according to the functions it should perform:

- Grant/Revoke Admin Rights (enter the user id in the text box and click 'confirm')
- Delete User (enter the user id in the text box and click 'confirm')
- Personal Information Browsing
- Personal Information Modification

Each item in the first-level menu of the management system completes a specific function, so there is no need for a second-level menu.

In fact, due to the circular structure of web links, some third-level menu names may appear in some fourth-level menus, which is why the menu structure of the BBS system is not strictly hierarchical.

# Interface Design
## User

 Interface
Graphic user interface:
- Registration interface: Enter user information and click confirm to submit the content.
- Login interface: Enter the username that has been registered to become an official member.
- Browsing interface: Both guests and members have the right to browse articles posted by other users or administrators.
- Posting interface: Members have the right to post. They can comment on posts made by other users.
- Modification interface: Members have the right to modify their personal information.
- Administrator Information Modification: Super administrators and specific administrators have this right, and can delete member information, posts, and comments that contain inappropriate messages.

# Overall Design
## Structural Framework Introduction
## Entire System Operation Introduction
## Overall Database Design
### Data Dictionary
#### User Information Table - user

| No. | Field Name        | Field English Name | Field Meaning           | Data Type    | Primary Key (Y/N) | Unique (Y/N) | NULL (Y/N) | Remarks                        |
| --- | ----------------- | ------------------ | ----------------------- | ------------ | ----------------- | ------------ | ---------- | ------------------------------ |
| 1   | User ID           | id                 | Unique identifier       | int          | Y                 | Y            | N          | Auto-increment ID              |
| 2   | Username          | account            | ~                       | varchar(20)  |                   | Y            | N          | Starts with letter, alphanumeric (<20) |
| 3   | Password          | password           | ~                       | varchar(20)  |                   |              | N          | Greater than 6 characters after change (<20) |
| 4   | Nickname          | nickname           | ~                       | varchar(20)  |                   |              | N          | Up to 20 characters            |
| 5   | User Email Address| email              | ~                       | varchar(50)  |                   |              |            |                                |
| 6   | User Avatar       | photo              | Path to user avatar     | text         |                   |              |            | Stores image path              |
| 7   | Gender            | sex                | Male, Female            | char(2)      |                   |              |            |                                |
| 8   | User Permission Level | grade         | Member, Administrator judgment | int  |                   |              | N          | 1 for member, 2 for administrator |
| 9   | Registration Date | registrationdate   | Registration date       | date         |                   |              | N          |                                |
| 10  | User Points       | point              | Level judgment          | int          |                   |              |            | Default is 50 points           |
| 11  | Spare Field 1     | blank_1            | ~                       | text         |                   |              |            |                                |
| 12  | Spare Field 2     | blank_2            | ~                       | text         |                   |              |            |                                |

#### Session Table - session

| No. | Field Name     | Field English Name | Field Meaning       | Data Type   | Primary Key (Y/N) | Unique (Y/N) | NULL (Y/N) | Remarks                   |
| --- | -------------- | ------------------ | -------------------- | ----------- | ----------------- | ------------ | ---------- | ------------------------- |
| 1   | Session ID     | id                 | Unique identifier   | int         | Y                 | Y            | N          | Auto-increment ID         |
| 2   | Session Name   | name               | ~                    | varchar(50) |                   |              | N          | Up to 50 characters       |
| 3   | Moderator ID   | masterId           | ~                    | int         | Y                 |              | N          | Foreign key [references user table (id)] |
| 4   | Session Topic  | profile            | ~                    | varchar(50) |                   |              | N          | Up to 50 characters       |
| 5   | Post Count     | topicCount         | ~                    | int         |                   |              |            |                           |
| 6   | Click Rate     | clickCoount        | ~                    | int         |                   |              |            |                           |
| 7   | Spare Field 1  | blank_1            | ~                    | text        |                   |              |            |                           |
| 8   | Spare Field 2  | blank_2            | ~                    | text        |                   |              |            |                           |

#### Post Table - topic

| No. | Field Name         | Field English Name | Field Meaning       | Data Type   | Primary Key (Y/N) | Unique (Y/N) | NULL (Y/N) | Remarks                   |
| --- | ------------------ | ------------------ | -------------------- | ----------- | ----------------- | ------------ | ---------- | ------------------------- |
| 1   | Post ID            | id                 | Unique identifier   | int         | Y                 | Y            | N          | Auto-increment ID         |
| 2   | Session ID         | sId                | ~                    | int         | Y                 |              | N          | Foreign key [references session table ID (sId)] |
| 3   | Poster ID          | uId                | ~                    | int         | Y                 |              | N          | Foreign key [references user table ID (uId)] |
| 4   | Reply Count        | replyCount         | ~                    | int         |                   |              |
