# Korean Input

## ubuntu 18

1. 한글 입력 [패키지 설정](http://awesometic.tistory.com/87), [단축키 설정](https://steemkr.com/ubuntu/@sjc333/18-04) 

> Korean(hangul)이 안보이면 reboot 

```
sudo add-apt-repository ppa:createsc/3beol
sudo apt-get update; sudo apt-get install ibus ibus-hangul
ibus-setup #ibus-setup-hangul
```

## ubuntu 16

ibus : http://techlog.gurucat.net/288

    
    sudo add-apt-repository ppa:createsc/3beol
    sudo apt-get update; sudo apt-get install ibus ibus-hangul
    

키 맵핑 

    System Settings에서 Keyboard 실행
    Shortcuts 탭 선택한 후 Typing 항목 선택
    모든 항목(Switch to next source, Switch to previous source, Alternative Characters Key)을 Disabled로 설정(Back 키를 누르면 Disabled가 됨)
    Compose Key 항목을 Right Alt로 변경



fcitx : http://androidtest.tistory.com/52, http://snowdeer.github.io/linux/2018/01/21/ubuntu-16p04-install-korean-keyboard/


