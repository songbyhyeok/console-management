# ConsoleManagementPrograms
Youtube 음악 CRUD 프로그램
![프로젝트 구현 목표](https://github.com/songbyhyeok/ConsoleManagementPrograms/assets/63230518/50bd29b6-1330-4fee-a2d9-dc19c09c940a)
![ERD_2차](https://github.com/songbyhyeok/ConsoleManagementPrograms/assets/63230518/5b1ac7d5-3e1c-45d5-a360-35cb5fb0fb7d)

### 재생목록에 음악을 담는 프로그램입니다.
&nbsp;

### DB Oracle Script
#### -- 계정 권한 부여
CREATE USER C##CONSOLE_PROJECT IDENTIFIED BY CONSOLE_PROJECT;
#####
GRANT RESOURCE, CONNECT TO C##CONSOLE_PROJECT;
#####
ALTER USER C##CONSOLE_PROJECT QUOTA UNLIMITED ON USERS;

#### -- 테이블 생성

CREATE TABLE MEMBER (
    MEMBER_NO NUMBER CONSTRAINT PK_MEMBER_NO PRIMARY KEY,
    MEMBER_NAME VARCHAR2(30) CONSTRAINT NN_MEMBER_NAME NOT NULL,
    MEMBER_NICKNAME VARCHAR2(30) CONSTRAINT NN_MEMBER_NICKNAME NOT NULL
);

CREATE TABLE ROOM (
    ROOM_NO NUMBER CONSTRAINT PK_ROOM_NO PRIMARY KEY,
    ROOM_TITLE VARCHAR2(30) CONSTRAINT NN_ROOM_TITLE NOT NULL,
    ROOM_DESCRIPTION VARCHAR2(30) CONSTRAINT NN_ROOM_DESCRIPTION NOT NULL,
    MEMBER_NO NUMBER,
    CONSTRAINT FK_MEMBER_NO FOREIGN KEY(MEMBER_NO) REFERENCES MEMBER(MEMBER_NO)
);

CREATE TABLE PLAYLIST (
    ROOM_NO NUMBER,
    CONSTRAINT FK_ROOM_NO FOREIGN KEY(ROOM_NO) REFERENCES ROOM(ROOM_NO),
    MUSIC_NO NUMBER,
    CONSTRAINT FK_MUSIC_NO FOREIGN KEY(MUSIC_NO) REFERENCES MUSIC(MUSIC_NO)
);

CREATE TABLE MUSIC (
    MUSIC_NO NUMBER CONSTRAINT PK_MUISC_NO PRIMARY KEY,
    MUSIC_TITLE VARCHAR2(30) CONSTRAINT NN_MUSIC_TITLE NOT NULL,
    MUSIC_ARTIST VARCHAR2(30) CONSTRAINT NN_MUSIC_ARTIST NOT NULL,
    MUSIC_ALBUM VARCHAR2(30),
    MUSIC_COMPOSER VARCHAR2(30)
);

#### -- 시퀀스 객체 생성

CREATE SEQUENCE SEQ_MEMBER_CODE
START WITH 1
INCREMENT BY 1
MAXVALUE 100
NOCYCLE
NOCACHE;

CREATE SEQUENCE SEQ_MUSIC_CODE
START WITH 1
INCREMENT BY 1
MAXVALUE 100
NOCYCLE
NOCACHE;

CREATE SEQUENCE SEQ_PLAYLIST_CODE
START WITH 1
INCREMENT BY 1
MAXVALUE 100
NOCYCLE
NOCACHE;

