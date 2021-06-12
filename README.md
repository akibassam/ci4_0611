# MAC 세팅

## Homebrew 설치

### 참고 사이트
* https://brew.sh/
* https://designdepot.tistory.com/209

### 설치 및 실행

```sh 
# M1 칩
% /bin/bash -c "$(curl -fsSL https://gist.githubusercontent.com/nrubin29/bea5aa83e8dfa91370fe83b62dad6dfa/raw/48f48f7fef21abb308e129a80b3214c2538fc611/homebrew_m1.sh)"

# 인텔 칩
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 실행
% eval $(/opt/homebrew/bin/brew shellenv)
```


### 자동 실행
* .zshrc에 내용 추가

```sh
% vi ~/.zshrc

# M1 칩
export PATH=/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
eval $(/opt/homebrew/bin/brew shellenv)

# 인텔 칩
export PATH=/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
export PATH=/usr/local/bin:/usr/local/sbin:$PATH
```


## PHP 설치
```sh
% brew install php
```


## composer 설치

### 참고 사이트
* https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos
* https://www.lesstif.com/php-and-laravel/php-composer-23757293.html




### 설치 파일 이용
* download installer
* run installer ```	php installer ```
* remove installer

### 글로벌 설정
```sh
% vi ~/.zshrc

export PATH=/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
eval $(/opt/homebrew/bin/brew shellenv)
alias composer="php /usr/local/bin/composer/composer.phar"

% source ~/.zshrc
```

## MySQL

### 설치 
```sh
% brew install mysql
% brew install mysql-client
% brew install --cask mysqlworkbench
```

### 실행 / 실행 / 비밀번호 설정 / 종료
```sh
% brew services start mysql
% mysql -uroot -p
mysql > exit
% mysql_secure_installation
% brew services stop mysql
```

### 암호 레벨 확인
```sql
SHOW VARIABLES LIKE 'validate_password%';
```

### 데이터베이스 생성, 테이블 생성 및 데이터 입력
```sql
CREATE DATABASE ci0611;

CREATE TABLE news (
    id int(11) NOT NULL AUTO_INCREMENT,
    title varchar(128) NOT NULL,
    slug varchar(128) NOT NULL,
    body text NOT NULL,
    PRIMARY KEY (id),
    KEY slug (slug)
);

INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
(3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
```

### 유저 생성, 접속 권한 설정

* MySQL 8부터 사용되는 인증 플러그인: caching_sha2_password
  * 보안 연결이나 RSA 보안을 사용하지 않으면 아래와 같은 에러 발생

```sh
Authentication plugin 'caching_sha2_password' cannot be loaded:
```

#### MySQL 8 이상 버전일 경우 
```sql
CREATE USER 'nd_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'secret';
CREATE USER 'nd_user'@'%' IDENTIFIED WITH mysql_native_password BY 'secret';
```

#### MySQL 8 이전 버전일 경우
```sql
CREATE USER 'ci_user'@'localhost' IDENTIFIED BY 'secret';
CREATE USER 'ci_user'@'%' IDENTIFIED BY 'secret';
```
#### 권한 부여
```sql
GRANT ALL PRIVILEGES ON ci0611.* TO 'nd_user'@'localhost' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON ci0611.* TO 'nd_user'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;
```



### 유저 확인 
```sql
SELECT Host,User,plugin,authentication_string FROM mysql.user;
```

## Codeigniter 4

### 설치
```sh
% composer create-project codeigniter4/appstarter my-project
```

### 기타
```sh
# 실행
% php spark serve

# 프로세스 확인
% ps -ef | grep php
  502 75845 74467   0 11:15AM ttys000    0:00.06 php spark serve
  502 75846 75845   0 11:15AM ttys000    0:00.21 /opt/homebrew/Cellar/php/8.0.7/bin/php -S localhost:8080 -t /Users/hyunsung.lee/Desktop/yispg/ci4/ci0611_01/public/ /Users/hyunsung.lee/Desktop/yispg/ci4/ci0611_01/vendor/codeigniter4/framework/system/Commands/Server/rewrite.php

# 강제 종료 
% kill -9 75846
```






