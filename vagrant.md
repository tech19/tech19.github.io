# vagrant

> must set provider ex)virtualBox  \
> Make sure that VBoxManage.exe from Oracle's VirtualBox installation is added to the system path.&#x20;

[https://junistory.blogspot.com/2017/08/virtualbox-vagrant.html](https://junistory.blogspot.com/2017/08/virtualbox-vagrant.html) : node.js로 Youtube 다루기

## Vagrantfile:

*   vagrant init 명령어로 Vagrantfile를 생성&#x20;

    &#x20;config.vm.box = Vagrant를 실행할 때 Vagrant Cloud에서 centos65-x64 가상머신을 자동으로 다운   &#x20;

    &#x20;config.vm.box = "puphpet/centos65-x64"&#x20;

[https://puphpet.com/](https://puphpet.com/) tool for configuring a Vagrant machine and generating a VagrantFile [https://app.vagrantup.com/boxes/search](https://app.vagrantup.com/boxes/search)

```
Vagrant.configure(2) do |config|
  config.vm.box = "phpstorm/phpstorm-base-vm"          
end
```

## Vagrant up

First time: vagrant up _provider virtualbox_ \
Vagrant 실행이 처음이라면 가상머신을 다운로드받아 설치를 하고 기동을 하고 이미 설치가 되어 있다면 그냥 기동만 \
This will configure the virtual machine in VirtualBox if this hasn't been done yet, as well as boot it.

## Vagrant ssh

가상머신이 실행되었으면 가상머신에 접속 \
Host : 127.0.0.1 \
Port : 2222 \
Username : vagrant \
Password : vagrant \
Private key : c:/vagrant/.vagrant/machines/default/virtualbox/private\_key \
Error connecting to remote host 127.0.0.1: Connection refused: connect

**lumen 책의꺼로**

## 웹서버를 사용하기 위한 설정

호스트머신에 띄워져있는 가상머신의 웹서버에 접속을 하기위해서는 Vagrantfile에 몇가지 설정을 추가해야 합니다. 먼저 호스트머신으로 접속한 port(8080)를 가상머신의 port(80)로 전달을 해야 합니다. config.vm.network "forwarded\_port", guest: 80, host: 8080 \
그리고 가상머신의 아이피주소를 설정을 해 주어야 합니다. config.vm.network "private\_network", ip: "192.168.33.10" \
마지막으로 가상머신과 호스트머신과의 실시간 자동으로 동기화되는 폴더를 설정해야 합니다. 호스트머신에서 소스파일을 수정하게 되면 바로 가상머신의 소스파일도 변경이 되기때문에 개발작업은 호스트머신에서 실행은 가상머신에서 하는 것이 가능해 집니다.

*   가상머신의 80포트를 호스트머신의 8080 포트에 할당함

    config.vm.network "forwarded\_port", guest: 80, host: 8080
*   가상머신의 IP를 아래 설정한 IP주소에 할당함

    config.vm.network "private\_network", ip: "192.168.33.10"
* 가상머신의 폴더와 호스트 머신의 폴더를 공유함(동기화)
* 별도로 세팅을 하지 않은경우 호스트머신의 vagrant설정이 있는 폴더와 가상머신의 /vagrant 폴더가 동기화 됨
*   config.vm.synced\_folder "호스트머신의 경로", "가상머신의 경로"

    폴더공유 에러 발생 시 : 호스트머신에 플러그인을 설치하여 관리하면 편리합니다.

> vagrant plugin install vagrant-vbguest 기본적인 Vagrant 명령어 모음

| 명령어             | 설명           |
| --------------- | ------------ |
| vagrant up      | 가상머신 기동      |
| vagrant status  | 가상머신 상태 확인   |
| vagrant ssh     | 가상머신에 접속     |
| vagrant halt    | 가상머신 정지      |
| vagrant suspend | 가상머신 휴면      |
| vagrant resume  | 가상머신 휴면에서 복원 |
| vagrant reload  | 가상머신 재시동     |
| vagrant destroy | 가상머신 제거      |

box manages boxes: installation, removal, etc. \
destroy stops and deletes all traces of the vagrant machine \
global-status outputs status Vagrant environments for this user \
halt stops the vagrant machine \
help shows the help for a subcommand \
init initializes a new Vagrant environment by creating a Vagrantfile \
login log in to HashiCorp's Vagrant Cloud \
package packages a running vagrant environment into a box \
plugin manages plugins: install, uninstall, update, etc. \
port displays information about guest port mappings \
powershell connects to machine via powershell remoting \
provision provisions the vagrant machine \
push deploys code in this environment to a configured destination \
rdp connects to machine via RDP \
reload restarts vagrant machine, loads new Vagrantfile configuration \
resume resume a suspended vagrant machine \
snapshot manages snapshots: saving, restoring, etc. \
ssh connects to machine via SSH \
ssh-config outputs OpenSSH valid configuration to connect to the machine \
status outputs status of the vagrant machine \
suspend suspends the machine \
up starts and provisions the vagrant environment \
validate validates the Vagrantfile \
version prints current and latest Vagrant version

## How to share box
