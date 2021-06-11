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

#### Mac air M1 암호
* (secret)

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

### 접속 권한 수정
```sql

CREATE USER 'ci_user'@'localhost' IDENTIFIED BY 'secret';
CREATE USER 'ci_user'@'%' IDENTIFIED BY 'secret';

GRANT ALL PRIVILEGES ON ci0611.* TO 'ci_user'@'localhost' WITH GRANT OPTION;

GRANT ALL PRIVILEGES ON ci0611.* TO 'ci_user'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;



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
% kill -9 75845
% kill -9 75846
```






