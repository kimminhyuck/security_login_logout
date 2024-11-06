11월06일
로그인 시큐리티와, 자동로그인, 로그아웃시 쿠키삭제, jsp에서 로그인한 사용자정보 보여주기, BCryptPasswordEncoder을 security-context.xml에 추가하여 비밀번호를 암호화함 ,CSRF 토큰 적용완료

sql문 ---------시작

create table users(
    username varchar2(50) not null primary key,
    password varchar2(50) not null,
    enabled char(1) default '1');
    
create table authorities (
    username varchar2(50) not null,
    authority varchar2(50) not null,
    constraint fk_authorities_users foreign key(username) references users(username));
    

insert into users (username, password) values ('user00' , 'pw00');  
insert into users (username, password) values ('member00' , 'pw00');  
insert into users (username, password) values ('admin00' , 'pw00');  

insert into authorities (username, authority) VALUES ('user00', 'ROLE_USER');  
insert into authorities (username, authority) VALUES ('member00', 'ROLE_MANAGER');  
insert into authorities (username, authority) VALUES ('admin00', 'ROLE_MANAGER');   
insert into authorities (username, authority) VALUES ('admin00', 'ROLE_ADMIN');   
 
create table tbl_member(
    userid varchar2(50) not null primary key,
    userpw varchar2(100) not null,
    username varchar2(100) not null,
    regdate date default sysdate,
    updatedate date default sysdate,
    enabled char(1) default '1');
    
create table tbl_member_auth(
    userid varchar2(50) not null,
    auth varchar2(50) not null,
    constraint fk_member_auth foreign key (userid)
    REFERENCES tbl_member(userid));

create table persistent_logine(
    username varchar(64) not null,
    series varchar(64) primary key,
    token varchar(64) not null,
    last_used timestamp not null);

DROP TABLE tbl_member;
DROP TABLE tbl_member_auth;
select * from tbl_member;
select * from tbl_member_auth;
commit;

sql문 ---------끝  
