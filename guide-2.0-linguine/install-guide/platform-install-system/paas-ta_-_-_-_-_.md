# PaaS-TA\_플랫폼\_설치\_자동화\_설치\_가이드

### Table of Contents

1. [개요](paas-ta_-_-_-_-_.md#1)
   * [목적](paas-ta_-_-_-_-_.md#2)
   * [범위](paas-ta_-_-_-_-_.md#3)
   * [참고자료](paas-ta_-_-_-_-_.md#4)
2. [플랫폼 설치 자동화 실행 환경 구성](paas-ta_-_-_-_-_.md#5)
   * [실행 환경을 위한 패키지 설치](paas-ta_-_-_-_-_.md#6)
   * [Ruby 및 BOSH 의존패키지 통합 설치](paas-ta_-_-_-_-_.md#7)
3. [플랫폼 설치 자동화 메뉴얼](paas-ta_-_-_-_-_.md#8)
   * [플랫폼 설치 자동화 실행](paas-ta_-_-_-_-_.md#9)

### Executive Summary

본 문서는 플랫폼 설치 자동화를 설치하는 가이드 문서로 플랫폼 설치 자동화를 실행할 수 있는 환경을 구성하여 실행하고 사용하는 방법에 대해서 설명하였다.

본 문서는 다음과 같은 내용들을 포함한다.

**플랫폼 설치 자동화 실행 환경 구성**

* ruby
* bosh-init
* bosh\_cli
* spiff
* java8
* maven
* mysql
* go

## 1.  문서 개요

### 1.1.  목적

본 문서는 플랫폼 설치 자동화 시스템의 설치를 위한 환경 구성에 대해 기술하였다.

### 1.2.  범위

본 문서에서는 Linux 환경\(Ubuntu 14.04\)을 기준으로 Openstack에 플랫폼 설치 자동화의 설치하는 방법에 대해 작성되었다.

### 1.3.  참고자료

본 문서는 Cloud Foundry의 Document를 참고로 작성하였다.

BOSH Document: [http://bosh.io](http://bosh.io)

CF & Diego Document: [http://docs.cloudfoundry.org/](http://docs.cloudfoundry.org/)

## 2.  플랫폼 설치 자동화 실행환경 구성

### 2.1. 실행 환경을 위한 패키지 설치

플랫폼 설치 자동화는 BOSH CLI\(command line interface\) 실행환경을 웹으로 구현한 것으로 BOSH CLI와 유사한 구동 환경을 구성할 필요가 있다. 2장에서 설치한 가상머신에 실행환경을 구성한다. 환경 구성에 있어서 전제조건으로 가상머신은 외부와 통신이 가능해야 한다.

플랫폼 설치 자동화의 실행환경을 구성하기 위해 다음의 패키지를 플랫폼 설치 자동화 설치 스크립트를 통해 자동으로 설치한다.

* Ruby \(1.9.3 이상\)
* bosh-init
* bosh\_cli
* spiff
* Java \(1.8 이상\)
* maven
* mysql
* go \(1.5 이상\)

### 2.2.  플랫폼 설치 자동화 설치

* 플랫폼 설치 자동화 설치는 ubuntu\(14.04 이상\)에서 실행 된다.

#### 1.  플랫폼 설치 자동화 설치 구성

| 파일 명 | 설명 |
| :--- | :--- |
| deployer-install.sh | 설치 스크립트 파일 |
| pds | 플랫폼 설치 자동화 서비스 등록 파일 |
| deployer | 플랫폼 설치 자동화 서비스 실행 파일 |
| deployerlog | Logrotate 설정 파일 |
| gopath.sh | Logrotate 실행 파일 |

#### 2.  플랫폼 설치 자동화 설치\(IEDA-WEB-INSTALLER\) 모듈과 플랫폼 설치 자동화\(OPENPAAS-IEDA-WEB\) 모듈을 다운로드 받는다.

[다운로드](https://paas-ta.kr/data/packages/2.0/PaaSTA-Env.zip)

```text
  IEDA-WEB-INSTALLER.tar
  OPENPAAS-IEDA-WEB.tar
```

#### 3.  다운로드 받은 IEDA-WEB-INSTALLER.tar 파일을 Home 디렉토리에 압축을 푼다.

```text
  $ tar xvf IEDA-WEB-INSTALLER.tar -C ~/
```

#### 4.  플랫폼 설치 자동화 설치 및 서비스 등록

```text
$ cd IEDA-WEB-INSTALLER
$ ./deployer-install.sh <OPENPAAS_IEDA_WEB.tar 파일이 있는 경로>/OPENPAAS_IEDA_WEB.tar <mysql 비밀번호>

ex)
$ ./deployer-install.sh ~/Downloads/OPENPAAS_IEDA_WEB.tar 1q2w3e4r5t
```

## 3.  플랫폼 설치 자동화 매뉴얼

본 장에서는 플랫폼 설치 자동화를 실행하는 방법과 메뉴 구성 및 화면 설명에 대해서 기술하였다.

### 3.1.  플랫폼 설치 자동화 실행

#### 1.  플랫폼 설치 자동화를 실행한다.

```text
# 플랫폼 설치 자동화 실행
$ pds start[stop/start/restart]
```

#### 2.  플랫폼 설치 자동화가 실행중인 계정에서 아래와 같이 설정 디렉토리가 생성되었는지 확인한다.

| 설정 디렉토리 | 설명 |
| :--- | :--- |
| {HOME}/.bosh\_plugin | 플랫폼 설치 자동화가 사용하는 기준 디렉토리 |
| {HOME}/.bosh\_plugin/stemcell | 스템셀 관리 디렉토리 |
| {HOME}/.bosh\_plugin/release | 릴리즈 관리 디렉토리 |
| {HOME}/.bosh\_plugin/deployment | 배포 관리 디렉토리 |
| {HOME}/.bosh\_plugin/deployment/manifest | 서비스팩 설치 관련 Manifest 관리 디렉토리 |
| {HOME}/.bosh\_plugin/key | CF 및 Diego 키 관리 디렉토리 |
| {HOME}/.bosh\_plugin/lock | 릴리즈, 스템셀 다운로드/업로드 및 Bootstrap 설치 실행 시 lock 관리 디렉토리 |
| {HOME}/.bosh\_plugin/temp | 임시 디렉토리 |

#### 3.  웹 브라우저를 이용해서 플랫폼 설치 자동화\([http://\[IP\]:8080](http://[IP]:8080)\) 화면이 출력되면 플랫폼 설치 자동화의 설치가 완료되며 로그인 화면으로 이동된다.

![](../../../.gitbook/assets/login%20%288%29.png)

#### 4. 참고

* 플랫폼 설치 자동화 활용
  * [플랫폼 설치 자동화 사용 가이드](../../use-guide/paas-ta_-_-_-_-_.md)

#### 5. 이전 버전 참고

* 플랫폼 설치 \(PaaS-TA v1.0\)
  * [플랫폼 설치 자동화](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Platform%20Install%20System/OpenPaaS_PaaSTA_Platform_Install_System_install_guide.md)
* 개인 환경 설치 \(PaaS-TA v1.0\)
  * [BOSH-Lite](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/BOSH%20Lite/OpenPaaS_PaaSTA_BOSH_Lite_install_guide.md)
* 운영 환경 설치 \(PaaS-TA v1.0\)
  * BOSH 설치\([AWS](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/BOSH/OpenPaaS_PaaSTA_BOSH_AWS_install_guide.md), [OpenStack](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/BOSH/OpenPaaS_PaaSTA_BOSH_Openstack_install_guide.md)\)
  * Controller 설치\([vSphere](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Controller/Controller_vSphere_install_guide.md),

    [AWS](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Controller/Controller_AWS_install_guide.md), [Openstack](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Controller/Controller_Openstack_install_guide.md)\)

  * Container 설치\([vSphere](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Container/Container_vSphere_install_guide.md),

    [AWS](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Container/Container_AWS_install_guide.md),

    [Openstack](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Documents-PaaSTA-1.0/blob/master/Install-Guide/Container/Container_Openstack_install_guide.md)\)

