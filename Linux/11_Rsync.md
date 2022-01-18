# Rsync - Remote Sync

`rsync -a src/ destination`: src폴더 아래의 모든 파일을 destination이란 폴더로 보낸다.
`rsync -av [전송할것] [받는곳]`

## Rsync 네트워크 전송

`rsync -azP [전송할것] [주소예: gunwoo@192.168.0.65:~/rsync/dest]`: `gunwoo@192.168.0.65:~/rsync/dest`에 전송하는데 파일을 압축(`z`)해서 전송한다.
