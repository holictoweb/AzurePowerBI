# super set 설치


```
# 기본 패키지 설치 

sudo apt-get install build-essential libssl-dev libffi-dev libsasl2-dev libldap2-dev

```

```
sudo pip3 install apache-superset

sudo superset db upgrade

sudo superset fab create-admin

sudo superset init 

# superset 실행 
sudo superset run -p 8088 --with-threads --reload --debugger
```


### chart



### dashboard


#### Edit CSS
- 대시보드 화면 우측 상단의 수정 버튼을 눌러서 수정 상태로 변경 한 이후에 옵션 클릭 -> edit css
- 각 chart의 title 지우기

```
.chart-header {
  display: none;
}
```
