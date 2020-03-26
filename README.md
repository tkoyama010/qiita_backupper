# qiita_backupper

## Overview

It is a tool to back up the article of the specified account.

## Requirement

- Python3.X
- Requests (Python libraries)
```sh
pip install requests
```

## Usage

#### 1. Run bachup.sh
```sh
$ ./backup.sh $ACCOUNT_NAME $FORMAT
[OK!] AAAAA
[OK!] BBBBB
[OK!] CCCCC
```

|Arguments|Details|
|:---:|:---|
|$USER_NAME|Your account neme of Qiita|
|$FORMAT|all / md / html|

## License
[MIT](https://github.com/i-tanaka730/qiita_backupper/blob/master/LICENSE)

## Author
[Ikuya Tanaka](https://github.com/i-tanaka730)
