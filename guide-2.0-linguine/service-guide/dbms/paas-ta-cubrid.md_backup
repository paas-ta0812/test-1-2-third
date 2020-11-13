# Table of Contents 123

1. [문서 개요](paas-ta-cubrid.md#1)
   * [1.1. 목적](paas-ta-cubrid.md#2)
   * [1.2. 범위](paas-ta-cubrid.md#3)
   * [1.3. 시스템 구성도](paas-ta-cubrid.md#4)
   * [1.4. 참고자료](paas-ta-cubrid.md#5)
2. [Cubrid 서비스팩 설치](paas-ta-cubrid.md#6)
   * [2.1. 설치전 준비사항](paas-ta-cubrid.md#7)
   * [2.2. Cubrid 서비스 릴리즈 업로드](paas-ta-cubrid.md#8)
   * [2.3. Cubrid 서비스 Deployment 파일 수정 및 배포](paas-ta-cubrid.md#9)
   * [2.4. Cubrid 서비스 브로커 등록](paas-ta-cubrid.md#10)
3. [Cubrid 연동 Sample App 설명](paas-ta-cubrid.md#11)
   * [3.1. Sample App 구조](paas-ta-cubrid.md#12)
   * [3.2. PaaS-TA에서 서비스 신청](paas-ta-cubrid.md#13)
   * [3.3. Sample App에 서비스 바인드 신청 및 App 확인](paas-ta-cubrid.md#14)
4. [Cubrid Client 툴 접속](paas-ta-cubrid.md#15)
   * [4.1. Putty 다운로드 및 터널링](paas-ta-cubrid.md#16)
   * [4.2. Cubrid Manager 설치 및 연결](paas-ta-cubrid.md#17)

## 1. 문서 개요

### 1.1. 목적

본 문서\(Cubrid 서비스팩 설치 가이드\)는 전자정부표준프레임워크 기반의 PaaS-TA에서 제공되는 서비스팩인 Cubrid 서비스팩을 Bosh를 이용하여 설치 하는 방법과 PaaS-TA의 SaaS 형태로 제공하는 Application 에서 Cubrid 서비스를 사용하는 방법을 기술하였다.

### 1.2. 범위

설치 범위는 Cubrid 서비스팩을 검증하기 위한 기본 설치를 기준으로 작성하였다.

### 1.3. 시스템 구성도

본 문서의 설치된 시스템 구성도입니다. Cubrid Server, Cubrid 서비스 브로커로 최소사항을 구성하였다.  
![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/1-3-0-0.png)

| 구분 | 스펙 |
| :--- | :--- |
| \(cubrid\_resource\_pools\) | 1vCPU / 1GB RAM / 8GB Disk |
| paasta-cubrid-broker | \(cubrid\_resource\_pools\) |
| Cubrid | \(cubrid\_resource\_pools\) |

### 1.4. 참고자료

[http://bosh.io/docs](http://bosh.io/docs)  
[http://docs.cloudfoundry.org/](http://docs.cloudfoundry.org/)

## 2. Cubrid 서비스팩 설치

### 2.1. 설치전 준비사항

본 설치 가이드는 Linux 환경에서 설치하는 것을 기준으로 하였다.  
서비스팩 설치를 위해서는 먼저 BOSH CLI 가 설치 되어 있어야 하고 BOSH 에 로그인 및 target 설정이 되어 있어야 한다.  
 BOSH CLI 가 설치 되어 있지 않을 경우 먼저 BOSH 설치 가이드 문서를 참고 하여 BOSH CLI를 설치 해야 한다.  


* PaaS-TA에서 제공하는 압축된 릴리즈 파일들을 다운받는다. \(PaaSTA-Deployment.zip, PaaSTA-Sample-Apps.zip, PaaSTA-Services.zip\)
* 다운로드 위치

  > PaaSTA-Services : [https://paas-ta.kr/data/packages/2.0/PaaSTA-Services.zip](https://paas-ta.kr/data/packages/2.0/PaaSTA-Services.zip)  
  > PaaSTA-Deployment : [https://paas-ta.kr/data/packages/2.0/PaaSTA-Deployment.zip](https://paas-ta.kr/data/packages/2.0/PaaSTA-Deployment.zip)  
  > PaaSTA-Sample-Apps : [https://paas-ta.kr/data/packages/2.0/PaaSTA-Sample-Apps.zip](https://paas-ta.kr/data/packages/2.0/PaaSTA-Sample-Apps.zip)

### 2.2. Cubrid 서비스 릴리즈 업로드

* Release Root 디렉토리로 이동하여 업로드 되어 있는 릴리즈 목록을 확인한다.

> $ cd ../../  
>  $ bosh releases  
>    
>  RSA 1024 bit CA certificates are loaded due to old openssl compatibility  
>  Acting as user 'admin' on 'bosh'  
>    
>  +--------------------------------------+-----------+-------------+  
>  \| Name \| Versions \| Commit Hash \|  
>   
> +--------------------------------------+-----------+-------------+  
>   
> \| cf \| 247 _\| af4efe9f+ \|_  
>  _\| cflinuxfs2-rootfs \| 1.40.0_ \| 19fe09f4+ \|  
>  \| diego \| 1.1.0 _\| 2298c8d4 \|_  
>  _\| empty-release \| 1+dev.1_ \| 00000000 \|  
>  \| etcd \| 86 _\| 2dfbef00+ \|_  
>  _\| garden-runc \| 1.0.3_ \| c6c4c73c \|  
>  \| openpaas-paasta-pinpoint \| 2.0 _\| 34e02d07+ \|_  
>  _\| openpaas-redis \| 1.0_ \| af975e0f \|  
>  \| paasta-eclipse-che \| 2.0 _\| 00000000 \|_  
>  _\| paasta-glusterfs \| 2.0_ \| 85e3f01e+ \|  
>  \| paasta-mysql \| 2.0 _\| 85e3f01e+ \|_  
>  _\| paasta-portal-object-storage-release \| 0+dev.1_ \| 00000000 \|  
>  \| paasta-redis \| 2.0 \| 2d766084+ \|  
>  +--------------------------------------+-----------+-------------+  
>  \(\*\) Currently deployed  
>  \(+\) Uncommitted changes  
>    
>  Releases total: 13  
>  Cubrid 서비스 릴리즈가 업로드 되어 있지 않은 것을 확인

* Cubrid 서비스 릴리즈를 업로드한다.

> $ bosh upload release {서비스 릴리즈 파일 PATH}  
>    
>  $ bosh upload release paasta-cubrid-2.0.tgz  
>    
>  RSA 1024 bit CA certificates are loaded due to old openssl compatibility  
>  Acting as user 'admin' on 'bosh'  
>    
>  Verifying manifest...  
>  Extract manifest OK  
>  Manifest exists OK  
>  Release name/version OK  
>    
>  File exists and readable OK  
>  Read package 'cubrid' \(1 of 4\) OK  
>  Package 'cubrid' checksum OK  
>  Read package 'java7' \(2 of 4\) OK  
>  Package 'java7' checksum OK  
>  Read package 'cli' \(3 of 4\) OK  
>  Package 'cli' checksum OK  
>  Read package 'cubrid\_broker' \(4 of 4\) OK  
>  Package 'cubrid\_broker' checksum OK  
>  Package dependencies OK  
>  Checking jobs format OK  
>  Read job 'cubrid' \(1 of 4\), version 45427cb5f3b6c86df80bb2de38c12e98aec7b95f OK  
>  Job 'cubrid' checksum OK  
>  Extract job 'cubrid' OK  
>  Read job 'cubrid' manifest OK  
>  Check template 'cubrid\_ctl.erb' for 'cubrid' OK  
>  Check template 'cubrid.conf.erb' for 'cubrid' OK  
>  Check template 'cubrid\_broker.conf.erb' for 'cubrid' OK  
>  Check template 'cubrid\_broker\_init.sql.erb' for 'cubrid' OK  
>  Check template '.cubrid.sh.erb' for 'cubrid' OK  
>  Job 'cubrid' needs 'cubrid' package OK  
>  Monit file for 'cubrid' OK  
>  Read job 'cubrid\_broker\_deregistrar' \(2 of 4\), version 49602e528fa68a557ece12688b6b278a1134ed27 OK  
>  Job 'cubrid\_broker\_deregistrar' checksum OK  
>  Extract job 'cubrid\_broker\_deregistrar' OK  
>  Read job 'cubrid\_broker\_deregistrar' manifest OK  
>  Check template 'errand.sh.erb' for 'cubrid\_broker\_deregistrar' OK  
>  Job 'cubrid\_broker\_deregistrar' needs 'cli' package OK  
>  Monit file for 'cubrid\_broker\_deregistrar' OK  
>  Read job 'cubrid\_broker' \(3 of 4\), version c73852bd8115be216e32b69bc6ee5f0bb5444b06 OK  
>  Job 'cubrid\_broker' checksum OK  
>  Extract job 'cubrid\_broker' OK  
>  Read job 'cubrid\_broker' manifest OK  
>  Check template 'bin/cubrid\_broker\_ctl' for 'cubrid\_broker' OK  
>  Check template 'bin/monit\_debugger' for 'cubrid\_broker' OK  
>  Check template 'data/properties.sh.erb' for 'cubrid\_broker' OK  
>  Check template 'helpers/ctl\_setup.sh' for 'cubrid\_broker' OK  
>  Check template 'helpers/ctl\_utils.sh' for 'cubrid\_broker' OK  
>  Check template 'config/cubrid\_broker.yml.erb' for 'cubrid\_broker' OK  
>  Check template 'config/application-mvc.properties.erb' for 'cubrid\_broker' OK  
>  Check template 'config/datasource.properties.erb' for 'cubrid\_broker' OK  
>  Check template 'config/logback.xml.erb' for 'cubrid\_broker' OK  
>  Check template 'config/bosh.pem.erb' for 'cubrid\_broker' OK  
>  Job 'cubrid\_broker' needs 'cubrid\_broker' package OK  
>  Job 'cubrid\_broker' needs 'java7' package OK  
>  Monit file for 'cubrid\_broker' OK  
>  Read job 'cubrid\_broker\_registrar' \(4 of 4\), version 8a89128e95a9707a30697bda7a9d7a678a2fd109 OK  
>  Job 'cubrid\_broker\_registrar' checksum OK  
>  Extract job 'cubrid\_broker\_registrar' OK  
>  Read job 'cubrid\_broker\_registrar' manifest OK  
>  Check template 'errand.sh.erb' for 'cubrid\_broker\_registrar' OK  
>  Job 'cubrid\_broker\_registrar' needs 'cli' package OK  
>  Monit file for 'cubrid\_broker\_registrar' OK  
>    
>  Release info  
>  ------------  
>  Name: paasta-cubrid  
>  Version: 2.0  
>    
>  Packages  
>
>
> * cubrid \(36065bb22d1e816657d176c902246231347361e2\) 
> * java7 \(cb28502f6e89870255182ea76e9029c7e9ec1862\) 
> * cli \(24305e50a638ece2cace4ef4803746c0c9fe4bb0\) 
> * cubrid\_broker \(25717cfb95347c7ca5ed1e6cbdda701315789cfc\)  
>
>
>   Jobs  
>
> * cubrid \(45427cb5f3b6c86df80bb2de38c12e98aec7b95f\) 
> * cubrid\_broker\_deregistrar \(49602e528fa68a557ece12688b6b278a1134ed27\) 
> * cubrid\_broker \(c73852bd8115be216e32b69bc6ee5f0bb5444b06\) 
> * cubrid\_broker\_registrar \(8a89128e95a9707a30697bda7a9d7a678a2fd109\)  
>
>
>   License  
>
> * none  
>
>
>   Checking if can repack release for faster upload...  
>
>
>   cubrid \(36065bb22d1e816657d176c902246231347361e2\) UPLOAD  
>
>
>   java7 \(cb28502f6e89870255182ea76e9029c7e9ec1862\) SKIP  
>
>
>   cli \(24305e50a638ece2cace4ef4803746c0c9fe4bb0\) SKIP  
>
>
>   cubrid\_broker \(25717cfb95347c7ca5ed1e6cbdda701315789cfc\) UPLOAD  
>
>
>   cubrid \(45427cb5f3b6c86df80bb2de38c12e98aec7b95f\) UPLOAD  
>
>
>   cubrid\_broker\_deregistrar \(49602e528fa68a557ece12688b6b278a1134ed27\) UPLOAD  
>
>
>   cubrid\_broker \(c73852bd8115be216e32b69bc6ee5f0bb5444b06\) UPLOAD  
>
>
>   cubrid\_broker\_registrar \(8a89128e95a9707a30697bda7a9d7a678a2fd109\) UPLOAD  
>
>
>   Release repacked \(new size is 181.8M\)  
>
>
>   Uploading release  
>
>
>   release-repac:  96%  
>    \|ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo         \| 174.5MB  26.1MB/s ETA:  00:00:00  
>
>
>   Director task 1285  
>
>
>   Started extracting release &gt; Extracting release. Done \(00:00:02\)  
>
>
>   Started verifying manifest &gt; Verifying manifest. Done \(00:00:00\)  
>
>
>   Started resolving package dependencies &gt; Resolving package dependencies. Done \(00:00:00\)  
>
>
>   Started creating new packages  
>
>
>   Started creating new packages &gt; cubrid/36065bb22d1e816657d176c902246231347361e2. Done \(00:00:03\)  
>
>
>   Started creating new packages &gt; java7/cb28502f6e89870255182ea76e9029c7e9ec1862. Done \(00:00:03\)  
>
>
>   Started creating new packages &gt; cli/24305e50a638ece2cace4ef4803746c0c9fe4bb0. Done \(00:00:00\)  
>
>
>   Started creating new packages &gt; cubrid\_broker/25717cfb95347c7ca5ed1e6cbdda701315789cfc. Done \(00:00:01\)  
>
>
>    Done creating new packages \(00:00:07\)  
>
>
>   Started creating new jobs  
>
>
>   Started creating new jobs &gt; cubrid/45427cb5f3b6c86df80bb2de38c12e98aec7b95f. Done \(00:00:00\)  
>
>
>   Started creating new jobs &gt; cubrid\_broker\_deregistrar/49602e528fa68a557ece12688b6b278a1134ed27. Done \(00:00:00\)  
>
>
>   Started creating new jobs &gt; cubrid\_broker/c73852bd8115be216e32b69bc6ee5f0bb5444b06. Done \(00:00:00\)  
>
>
>   Started creating new jobs &gt; cubrid\_broker\_registrar/8a89128e95a9707a30697bda7a9d7a678a2fd109. Done \(00:00:00\)  
>
>
>    Done creating new jobs \(00:00:00\)  
>
>
>   Started release has been created &gt; paasta-cubrid/2.0. Done \(00:00:00\)  
>
>
>   Task 1285 done  
>
>
>   Started        2017-01-06 06:52:33 UTC  
>
>
>   Finished    2017-01-06 06:52:42 UTC  
>
>
>   Duration    00:00:09  
>
>
>   release-repac:  96%  
>    \|ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo         \| 174.9MB  10.9MB/s Time: 00:00:16  
>
>
>   Release uploaded

* 업로드 된 Cubrid 릴리즈를 확인한다. 

> $ bosh releases  
>    
>  RSA 1024 bit CA certificates are loaded due to old openssl compatibility  
>  Acting as user 'admin' on 'bosh'  
>    
>  +--------------------------------------+-----------+-------------+  
>  \| Name \| Versions \| Commit Hash \|  
>  +--------------------------------------+-----------+-------------+  
>  \| cf \| 247 _\| af4efe9f+ \|_  
>  _\| cflinuxfs2-rootfs \| 1.40.0_ \| 19fe09f4+ \|  
>  \| diego \| 1.1.0 _\| 2298c8d4 \|_  
>  _\| empty-release \| 1+dev.1_ \| 00000000 \|  
>  \| etcd \| 86 _\| 2dfbef00+ \|_  
>  _\| garden-runc \| 1.0.3_ \| c6c4c73c \|  
>  \| openpaas-paasta-pinpoint \| 2.0 _\| 34e02d07+ \|_  
>  _\| openpaas-redis \| 1.0_ \| af975e0f \|  
>  \| paasta-cubrid \| 2.0 \| 85e3f01e+ \|  
>  \| paasta-eclipse-che \| 2.0 _\| 00000000 \|_  
>  _\| paasta-glusterfs \| 2.0_ \| 85e3f01e+ \|  
>  \| paasta-mysql \| 2.0 _\| 85e3f01e+ \|_  
>  _\| paasta-portal-object-storage-release \| 0+dev.1_ \| 00000000 \|  
>  \| paasta-redis \| 2.0 \| 2d766084+ \|  
>  +--------------------------------------+-----------+-------------+  
>  \(\*\) Currently deployed  
>  \(+\) Uncommitted changes  
>    
>  Releases total: 14  
>  Cubrid 서비스 릴리즈가 업로드 되어 있는 것을 확인

### 2.3.  Cubrid 서비스 Deployment 파일 수정 및 배포

BOSH Deployment manifest 는 components 요소 및 배포의 속성을 정의한 YAML 파일이다. Deployment manifest 에는 sotfware를 설치 하기 위해서 어떤 Stemcell \(OS, BOSH agent\) 을 사용할것이며 Release \(Software packages, Config templates, Scripts\) 이름과 버전, VMs 용량, Jobs params 등을 정의가 되어 있다.

* PaaSTA-Deployment.zip 파일 압축을 풀고 폴더안에 있는 IaaS별 Cubrid Deployment 파일을 복사한다.

  예\) vsphere 일 경우 paasta\_cubrid\_vsphere\_2.0.yml를 복사

  다운로드 받은 Deployment Yml 파일을 확인한다. \(pasta\_cubrid\_vsphere\_2.0.yml\)

> $ ls –all  
>    
>  total 851588  
>  drwxrwxr-x 5 inception inception 4096 Jan 9 10:18 .  
>  drwxrwxr-x 11 inception inception 4096 Dec 21 09:28 ..  
>    
>  -rw-r--r-- 1 inception inception 6614 Jan 6 16:14 paasta\_cubrid\_vsphere\_2.0.yml  
>  -rw-rw-r-- 1 inception inception 6382 Jan 9 10:18 paasta\_mysql\_vsphere\_2.0.yml

* Director UUID를 확인한다.
* BOSH CLI가 배포에 대한 모든 작업을 허용하기위한 현재 대상 BOSH Director의 UUID와 일치해야한다. ‘bosh status’ CLI 을 통해서 현재 BOSH Director 에 target 되어 있는 UUID를 확인할수 있다.

> $ bosh status ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-1-0-9.png)

* Deploy시 사용할 Stemcell을 확인한다.

> $ bosh stemcells ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-1-0-10.png)
>
> Stemcell 목록이 존재 하지 않을 경우 BOSH 설치 가이드 문서를 참고 하여 Stemcell 3215.4 버전을 업로드를 해야 한다.

* Deployment 파일을 서버 환경에 맞게 수정한다. \(vsphere 용으로 설명, 다른 IaaS는 해당 Deployment 파일의 주석내용을 참고\)

> $ vi paasta-cubrid-vsphere-1.0.yml
>
> ```yaml
> # paasta-cubrid-vsphere 설정 파일 내용
> ---
> name: paasta-cubrid-service  # 서비스 배포이름(필수)
> director_uuid: 0bc8d3c2-e032-4c7e-a99c-e23eea7091fc #bosh status 에서 확인한 Director UUID을 입력(필수)
>
> release:
>   name: paasta-cubrid  #서비스 릴리즈 이름(필수)
>   version: 1.0   #서비스 릴리즈 버전(필수):latest 시 업로드된 서비스 릴리즈 최신버전
>
> compilation:          # 컴파일시 필요한 가상머신의 속성(필수)
>   workers: 4          # 컴파일 하는 가상머신의 최대수(필수)
>   network: default    # Networks block에서 선언한 network 이름(필수)
>   cloud_properties:   # 컴파일 VM을 만드는 데 필요한 IaaS의 특정 속성 (instance_type, availability_zone), 직접 cpu,disk,ram 사이즈를 넣어도 됨
>     ram: 2048
>     disk: 8096
>     cpu: 2
>
> # this section describes how updates are handled
> update:
>   canaries: 1                 # canary 인스턴스 수(필수)
>   canary_watch_time: 30000    # canary 인스턴스가 수행하기 위한 대기 시간(필수)
>   update_watch_time: 30000    # non-canary 인스턴스가 수행하기 위한 대기 시간(필수)
>   max_in_flight: 4            # non-canary 인스턴스가 병렬로 update 하는 최대 개수(필수)
>
> networks:                     # 네트워크 블록에 나열된 각 서브 블록이 참조 할 수있는 작업이 네트워크 구성을 지정, 네트워크 구성은 네트워크 담당자에게 문의 하여 작성 요망
> - name: default
>   subnets:
>   - cloud_properties:
>       name: Internal          # vsphere 에서 사용하는 network 이름(필수)
>     dns:                      # DNS 정보
>     - 10.30.20.24
>     - 8.8.8.8
>     gateway: 10.30.20.23
>     name: default_unused
>     range: 10.30.0.0/16
>     reserved:                 # 설치시 제외할 IP 설정
>     - 10.30.0.1 - 10.30.20.22
>     - 10.30.20.24 - 10.30.40.255
>     static:
>     - 10.30.60.11 - 10.30.60.70 #사용 가능한 IP 설정
>
> resource_pools:               # 배포시 사용하는 resource pools를 명시하며 여러 개의 resource pools 을 사용할 경우 name 은 unique 해야함(필수)
>   - name: cubrid_resource_pools # 고유한 resource pool 이름
>     network: default
>     stemcell:
>       name: bosh-vsphere-esxi-ubuntu-trusty-go_agent  # stemcell 이름(필수)
>       version: 3215.4                # stemcell 버전(3215.4 버전으로 사용, aws 3263.28)
>     cloud_properties:         # 컴파일 VM을 만드는 데 필요한 IaaS의 특정 속성을 설명 (instance_type, availability_zone), 직접 cpu, disk, 메모리 설정가능
>       cpu: 1
>       disk: 8192
>       ram: 4096
>
> jobs:
>   - name: cubrid  #작업 이름(필수): Cubrid 서버
>     template: cubrid  # job template 이름(필수)
>     instances: 1  # job 인스턴스 수(필수)
>     resource_pool: cubrid_resource_pools  # resource_pools block에 정의한 resource pool 이름(필수)
>     persistent_disk: 16384  # 영구적 디스크 사이즈 정의(옵션): 16G
>     networks:     # 네트워크 구성정보
>     - name: default   # Networks block에서 선언한 network 이름(필수)
>       static_ips:
>       - 10.30.60.23   # 사용할 IP addresses 정의(필수) Cubrid 서버 IP
>   - name: cubrid_broker   #작업 이름(필수): Cubrid 서비스 브로커
>     template: cubrid_broker  # job template 이름(필수)
>     instances: 1  # job 인스턴스 수(필수)
>     resource_pool: cubrid_resource_pools  # resource_pools block에 정의한 resource pool 이름(필수)
>     networks: # 네트워크 구성정보
>     - name: default   # Networks block에서 선언한 network 이름(필수)
>       static_ips:
>       - 10.30.60.22   # 사용할 IP addresses 정의(필수)
>   - name : cubrid_broker_registrar  # 작업 이름: 서비스 브로커 등록
>     template : cubrid_broker_registrar
>     instances: 1
>     lifecycle: errand   # bosh deploy시 vm에 생성되어 설치 되지 않고 bosh errand 로 실행할때 설정, 주로 테스트 용도에 쓰임
>     resource_pool: cubrid_resource_pools
>     networks:
>     - name: default
>     properties:
>       broker: # 서비스 브로커 설정 정보
>         host: 10.30.60.22 # 서비스 브로커 IP 
>         name: CubridDB  # CF에서 서비스 브로커를 생성시 생기는 서비스 이름 브로커에 고정되어있는 값
>         password: cloudfoundry  # 브로커 접근 아이디 비밀번호(필수)
>         username: admin   # 브로커 접근 아이디(필수)
>         protocol: http
>         port: 8080  # 브로커 포트
>       cf:
>         admin_password: admin   # CF 사용자의 패스워드
>         admin_username: admin   # CF 사용자 이름
>         api_url: https://api.115.68.46.30.xip.io   # CF 설치시 설정한 api uri 정보(필수)
>     release: paasta-cubrid
>   - name : cubrid_broker_deregistrar  # 작업 이름: 서비스 브로커 삭제
>     template : cubrid_broker_deregistrar
>     instances: 1
>     lifecycle: errand
>     resource_pool: cubrid_resource_pools
>     networks:
>     - name: default
>     properties:
>       broker:
>         host: 10.30.60.22
>         name: CubridDB
>         password: cloudfoundry
>         username: admin
>         protocol: http
>         port: 8080
>       cf:
>         admin_password: admin
>         admin_username: admin
>         api_url: https://api.115.68.46.30.xip.io
>     release: openpaas-cubrid
>
> meta:
>   apps_domain: 115.68.46.30.xip.io   # CF 설치시 설정한 apps 도메인 정보
>   environment: null
>   external_domain: 115.68.46.30.xip.io   # CF 설치시 설정한 외부 도메인 정보
>   nats: # CF 설치시 설정한 nats 정보
>     machines:
>     - 10.30.40.11
>     password: admin
>     port: 4222
>     user: nats
>   syslog_aggregator: null
>
> properties:
>   cubrid:   # Cubrid 설정 정보
>     max_clients: 200
>   cubrid_broker:  # Cubrid Servcice Broker 설정 정보
>     cubrid_ip: 10.30.60.23 # Cubrid IP
>     cubrid_db_port: 30000 # Cubrid Port
>     cubrid_db_name: cubrid_broker   # Cubrid service 관리를 위한 데이터베이스 이름
>     cubrid_db_user: dba   # 브로커 관리용 데이터베이스 접근 사용자이름
>     cubrid_db_passwd: openpaas  # 브로커 관리용 데이터베이스 접근 사용자 비밀번호
>     cubrid_ssh_port: 22   # Cubrid가 설치된 서버 SSH 접속 포트
>     cubrid_ssh_user: root # Cubrid가 설치된 서버 SSH 접속 사용자 이름
>     cubrid_ssh_passwd: c1oudc0w # Cubrid가 설치된 서버 SSH 접속 사용자 비밀번호
>     cubrid_ssh_sudo_passwd: c1oudc0w # Cubrid가 설치된 서버 sudo 비밀번호
> ```

* Deploy 할 deployment manifest 파일을 BOSH 에 지정한다.

> $ bosh deployment {Deployment manifest 파일 PATH}  
>    
>  $ bosh deployment paasta\_cubrid\_vsphere\_2.0.yml  
>    
>  inception@inception:~/bosh-space/deployment$ bosh deployment paasta\_cubrid\_vsphere\_2.0.yml   
>  RSA 1024 bit CA certificates are loaded due to old openssl compatibility  
>  Deployment set to '/mnt/bosh-space/deployment/paasta\_cubrid\_vsphere\_2.0.yml'

* Cubrid 서비스팩을 배포한다.

> $ bosh deploy  
>    
>  RSA 1024 bit CA certificates are loaded due to old openssl compatibility  
>  Acting as user 'admin' on deployment 'paasta-cubrid-service' on 'bosh'  
>  Getting deployment properties from director...  
>  Unable to get properties list from director, trying without it...  
>    
>  Detecting deployment changes  
>  ----------------------------  
>  resource\_pools:  
>
>
> * name: cubrid\_resource\_pools  
>
>
>   network: default  
>
>
>   stemcell:  
>
>
>   name: bosh-vsphere-esxi-ubuntu-trusty-go\_agent  
>
>
>    version: '3263.8'  
>
>
>   cloud\_properties:  
>
>
>    cpu: 1  
>
>
>    disk: 8192  
>
>
>    ram: 2048  
>
>
>   compilation:  
>
>
>   workers: 4  
>
>
>   network: default  
>
>
>   cloud\_properties:  
>
>
>    ram: 2048  
>
>
>    disk: 8096  
>
>
>    cpu: 2  
>
>
>   networks:  
>
> * name: default  
>
>
>   subnets:  
>
>
>   * cloud\_properties:  
>
>
>      name: Internal  
>
>
>     dns:  
>
>
>     * 8.8.8.8  
>
>
>       gateway: 10.30.20.23  
>
>
>       name: default\_unused  
>
>
>       range: 10.30.0.0/16  
>
>
>       reserved:  
>
>     * 10.30.0.1 - 10.30.20.22 
>     * 10.30.20.24 - 10.30.40.255  
>
>
>       static:  
>
>     * 10.30.60.11 - 10.30.60.70  
>
>
>       releases:  
>
> * name: paasta-cubrid  
>
>
>   version: '2.0'  
>
>
>   update:  
>
>
>   canaries: 1  
>
>
>   canary\_watch\_time: 120000  
>
>
>   update\_watch\_time: 120000  
>
>
>   max\_in\_flight: 4  
>
>
>   jobs:  
>
> * name: cubrid  
>
>
>   template: cubrid  
>
>
>   instances: 1  
>
>
>   resource\_pool: cubrid\_resource\_pools  
>
>
>   networks:  
>
>
>   * name: default  
>
>
>     static\_ips:  
>
>
>     * 10.30.60.23 
>
> * name: cubrid\_broker  
>
>
>   template: cubrid\_broker  
>
>
>   instances: 1  
>
>
>   resource\_pool: cubrid\_resource\_pools  
>
>
>   networks:  
>
>
>   * name: default  
>
>
>     static\_ips:  
>
>
>     * 10.30.60.22 
>
> * name: cubrid\_broker\_registrar  
>
>
>   template: cubrid\_broker\_registrar  
>
>
>   instances: 1  
>
>
>   lifecycle: errand  
>
>
>   resource\_pool: cubrid\_resource\_pools  
>
>
>   networks:  
>
>
>   * name: default  
>
>
>     properties:  
>
>
>     broker:  
>
>
>      host: ""  
>
>
>      name: ""  
>
>
>      password: ""  
>
>
>      username: ""  
>
>
>      protocol: ""  
>
>
>      port: ""  
>
>
>     cf:  
>
>
>      admin\_password: ""  
>
>
>      admin\_username: ""  
>
>
>      api\_url: ""  
>
>
>     release: paasta-cubrid  
>
> * name: cubrid\_broker\_deregistrar  
>
>
>   template: cubrid\_broker\_deregistrar  
>
>
>   instances: 1  
>
>
>   lifecycle: errand  
>
>
>   resource\_pool: cubrid\_resource\_pools  
>
>
>   networks:  
>
>
>   * name: default  
>
>
>     properties:  
>
>
>     broker:  
>
>
>      host: ""  
>
>
>      name: ""  
>
>
>      password: ""  
>
>
>      username: ""  
>
>
>      protocol: ""  
>
>
>      port: ""  
>
>
>     cf:  
>
>
>      admin\_password: ""  
>
>
>      admin\_username: ""  
>
>
>      api\_url: ""  
>
>
>     release: paasta-cubrid  
>
>
>     name: paasta-cubrid-service  
>
>
>     director\_uuid: d363905f-eaa0-4539-a461-8c1318498a32  
>
>
>     meta:  
>
>
>     apps\_domain: 115.68.46.30.xip.io  
>
>
>     environment:   
>
>
>     external\_domain: 115.68.46.30.xip.io  
>
>
>     nats:  
>
>
>     machines:  
>
>
>     * 10.30.110.31  
>
>
>       password: nats  
>
>
>       port: 4222  
>
>
>       user: nats  
>
>
>       syslog\_aggregator:   
>
>
>       properties:  
>
>
>       cubrid:  
>
>
>       max\_clients: ""  
>
>
>       cubrid\_broker:  
>
>
>       cubrid\_ip: ""  
>
>
>       cubrid\_db\_port: ""  
>
>
>       cubrid\_db\_name: ""  
>
>
>       cubrid\_db\_user: ""  
>
>
>       cubrid\_db\_passwd: ""  
>
>
>       cubrid\_ssh\_port: ""  
>
>
>       cubrid\_ssh\_user: ""  
>
>
>       cubrid\_ssh\_passwd: ""  
>
>
>       cubrid\_ssh\_sudo\_passwd: ""  
>
>
>       Please review all changes carefully  
>
>
>       Deploying  
>
>
>       ---------  
>
>
>       Are you sure you want to deploy? \(type 'yes' to continue\): yes  
>
>
>       Director task 1303  
>
>
>       Deprecation: Ignoring cloud config. Manifest contains 'networks' section.  
>
>
>       Started preparing deployment &gt; Preparing deployment. Done \(00:00:00\)  
>
>
>       Started preparing package compilation &gt; Finding packages to compile. Done \(00:00:00\)  
>
>
>       Started compiling packages  
>
>
>       Started compiling packages &gt; cli/24305e50a638ece2cace4ef4803746c0c9fe4bb0  
>
>
>       Started compiling packages &gt; java7/cb28502f6e89870255182ea76e9029c7e9ec1862  
>
>
>       Started compiling packages &gt; cubrid/36065bb22d1e816657d176c902246231347361e2  
>
>
>       Done compiling packages &gt; cli/24305e50a638ece2cace4ef4803746c0c9fe4bb0 \(00:01:18\)  
>
>
>       Done compiling packages &gt; java7/cb28502f6e89870255182ea76e9029c7e9ec1862 \(00:01:28\)  
>
>
>       Started compiling packages &gt; cubrid\_broker/25717cfb95347c7ca5ed1e6cbdda701315789cfc  
>
>
>       Done compiling packages &gt; cubrid/36065bb22d1e816657d176c902246231347361e2 \(00:02:20\)  
>
>
>       Done compiling packages &gt; cubrid\_broker/25717cfb95347c7ca5ed1e6cbdda701315789cfc \(00:01:16\)  
>
>
>       Done compiling packages \(00:02:44\)  
>
>
>       Started creating missing vms  
>
>
>       Started creating missing vms &gt; cubrid/a6bf1096-1c12-4d7e-bbc8-03ba517ff5f6 \(0\)  
>
>
>       Started creating missing vms &gt; cubrid\_broker/be5bcafa-3b09-4300-a85d-c7935c3e05a7 \(0\)  
>
>
>       Done creating missing vms &gt; cubrid/a6bf1096-1c12-4d7e-bbc8-03ba517ff5f6 \(0\) \(00:00:53\)  
>
>
>       Done creating missing vms &gt; cubrid\_broker/be5bcafa-3b09-4300-a85d-c7935c3e05a7 \(0\) \(00:00:53\)  
>
>
>       Done creating missing vms \(00:00:53\)  
>
>
>       Started updating instance cubrid &gt; cubrid/a6bf1096-1c12-4d7e-bbc8-03ba517ff5f6 \(0\) \(canary\). Done \(00:02:33\)  
>
>
>       Started updating instance cubrid\_broker &gt; cubrid\_broker/be5bcafa-3b09-4300-a85d-c7935c3e05a7 \(0\) \(canary\). Done \(00:02:22\)  
>
>
>       Task 1303 done  
>
>
>       Started        2017-01-06 07:15:20 UTC  
>
>
>       Finished    2017-01-06 07:23:52 UTC  
>
>
>       Duration    00:08:32  
>
>
>       Deployed 'paasta-cubrid-service' to 'bosh'

* 배포된 Cubrid 서비스팩을 확인한다.

> $ bosh vms paasta-cubrid-service  
>    
>  RSA 1024 bit CA certificates are loaded due to old openssl compatibility  
>  Acting as user 'admin' on deployment 'paasta-cubrid-service' on 'bosh'  
>    
>   
>  Director task 1312  
>    
>  Task 1312 done  
>    
>  +--------------------------------------------------------+---------+-----+-----------------------+-------------+  
>  \| VM \| State \| AZ \| VM Type \| IPs \|  
>  +--------------------------------------------------------+---------+-----+-----------------------+-------------+  
>  \| cubrid/0 \(a6bf1096-1c12-4d7e-bbc8-03ba517ff5f6\) \| running \| n/a \| cubrid\_resource\_pools \| 10.30.60.23 \|  
>  \| cubrid\_broker/0 \(be5bcafa-3b09-4300-a85d-c7935c3e05a7\) \| running \| n/a \| cubrid\_resource\_pools \| 10.30.60.22 \|  
>  +--------------------------------------------------------+---------+-----+-----------------------+-------------+  
>    
>  VMs total: 2

### 2.4. Cubrid 서비스 브로커 등록

Cubrid 서비스팩 배포가 완료 되었으면 Application에서 서비스 팩을 사용하기 위해서 먼저 Cubrid 서비스 브로커를 등록해 주어야 한다.  
서비스 브로커 등록시 PaaS-TA에서 서비스브로커를 등록할 수 있는 사용자로 로그인이 되어있어야 한다.

* 서비스 브로커 목록을 확인한다.

> $ cf service-brokers ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-4-0-0.png)

* Cubrid 서비스 브로커를 등록한다.

> $ cf create-service-broker {서비스팩 이름} {서비스팩 사용자ID} {서비스팩 사용자비밀번호} [http://{서비스팩](http://{서비스팩) URL}
>
> * 서비스팩 이름 : 서비스 팩 관리를 위해 PaaS-TA에서 보여지는 명칭이다. 서비스 Marketplace에서는 각각의 API 서비스 명이 보여지니 여기서 명칭은 서비스팩 리스트의 명칭이다.  
> * 서비스팩 사용자ID / 비밀번호 : 서비스팩에 접근할 수 있는 사용자 ID입니다. 서비스팩도 하나의 API 서버이기 때문에 아무나 접근을 허용할 수 없어 접근이 가능한 ID/비밀번호를 입력한다.  
> * 서비스팩 URL : 서비스팩이 제공하는 API를 사용할 수 있는 URL을 입력한다.  
>
> $ cf create-service-broker cubrid-service-broker admin cloudfoundry [http://10.30.60.22:8080](http://10.30.60.22:8080)  
> ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-4-1-0.png)

* 등록된 Cubrid 서비스 브로커를 확인한다.

> $ cf service-brokers ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-4-2-0.png)

* 접근 가능한 서비스 목록을 확인한다.

> $ cf service-access ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-4-3-0.png)
>
> 서비스 브로커 생성시 디폴트로 접근을 허용하지 않는다.

* 특정 조직에 해당 서비스 접근 허용을 할당하고 접근 서비스 목록을 다시 확인한다. \(전체 조직\)

> $ cf enable-service-access CubridDB  
> $ cf service-access  
> ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/2-4-4-0.png)

## 3. Cubrid연동 Sample App 설명

본 Sample Web App은 PaaS-TA에 배포되며 Cubrid의 서비스를 Provision과 Bind를 한 상태에서 사용이 가능하다.

### 3.1. Sample App 구조

Sample Web App은 PaaS-TA에 App으로 배포가 된다. App을 배포하여 구동시 Bind 된 Cubrid 서비스 연결정보로 접속하여 초기 데이터를 생성하게 된다. 배포 완료 후 정상적으로 App 이 구동되면 브라우져나 curl로 해당 App에 접속 하여 Cubrid 환경정보\(서비스 연결 정보\)와 초기 적재된 데이터를 보여준다.

Sample Web App 구조는 다음과 같다.

| 이름 | 설명 |
| :--- | :--- |
| src | Sample 소스 디렉토리 |
| manifest.yml | PaaS-TA에 app 배포시 필요한 설정을 저장하는 파일 |
| pom.xml | 메이븐 project 설정 파일 |
| target | 메이븐 빌드시 생성되는 디렉토리\(war 파일, classes 폴더 등\) |

* PaaS-TA-Sample-Apps을 다운로드 받고 Service 폴더안에 있는 Cubrid Sample Web App인 hello-spring-cubrid를 복사한다.

> $ ls -all ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-1-0-0.png)

### 3.2. PaaS-TA에서 서비스 신청

Sample Web App에서 Cubrid 서비스를 사용하기 위해서는 서비스 신청\(Provision\)을 해야 한다. \*참고: 서비스 신청시 PaaS-TA에서 서비스를신청 할 수 있는 사용자로 로그인이 되어 있어야 한다.

* 먼저 PaaS-TA Marketplace에서 서비스가 있는지 확인을 한다.

> $ cf marketplace ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-2-0-0.png)

* Marketplace에서 원하는 서비스가 있으면 서비스 신청\(Provision\)을 한다.

> $ cf create-service {서비스명} {서비스플랜} {내서비스명}
>
> * 서비스명 : CubridDB로 Marketplace에서 보여지는 서비스 명칭이다.  
> * 서비스플랜 : 서비스에 대한 정책으로 plans에 있는 정보 중 하나를 선택한다. Cubrid 서비스는 100mb, 1gb를 지원한다.  
> * 내서비스명 : 내 서비스에서 보여지는 명칭이다. 이 명칭을 기준으로 환경설정정보를 가져온다.  
>
> $ cf create-service CubridDB utf8 cubrid-service-instance  
> ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-2-1-0.png)

* 생성된 Cubrid 서비스 인스턴스를 확인한다.

> $ cf services ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-2-2-0.png)

### 3.3. Sample App에 서비스 바인드 신청 및 App 확인

서비스 신청이 완료되었으면 Sample Web App 에서는 생성된 서비스 인스턴스를 Bind 하여 App에서 Cubrid 서비스를 이용한다.  
\*참고: 서비스 Bind 신청시 PaaS-TA에서 서비스 Bind신청 할 수 있는 사용자로 로그인이 되어 있어야 한다.

* Sample Web App 디렉토리로 이동하여 manifest 파일을 확인한다.

> $ cd hello-spring-cubrid  
> $ vi manifest.yml
>
> ```yaml
> ---
> applications:
> - name: hello-spring-cubrid # 배포할 App 이름
>   memory: 512M # 배포시 메모리 사이즈
>   instances: 1 # 배포 인스턴스 수
>   path: target/hello-spring-cubrid-1.0.0-BUILD-SNAPSHOT.war #배포하는 App 파일 PATH
> ```
>
> 참고: ./build/libs/hello-spring-cubrid.war 파일이 존재 하지 않을 경우 gradle 빌드를 수행 하면 파일이 생성된다.

* --no-start 옵션으로 App을 배포한다.  

  --no-start: App 배포시 구동은 하지 않는다.

> $ cf push --no-start  
>  ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-0-0.png)

* 배포된 Sample App을 확인하고 로그를 수행한다.

> $ cf apps  
>  ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-1-0.png)
>
> $ cf logs {배포된 App명}  
>  $ cf logs hello-spring-cubrid ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-2-0.png)

* Sample Web App에서 생성한 서비스 인스턴스 바인드 신청을 한다. 

> $ cf bind-service hello-spring-cubrid cubrid-service-instance ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-3-0.png)

* 바인드가 적용되기 위해서 App을 재기동한다.

> $ cf restart hello-spring-cubrid ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-4-0.png)  
> ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-4-1.png)

* \(참고\) 바인드 후 App구동시 Cubrid 서비스 접속 에러로 App 구동이 안될 경우 보안 그룹을 추가한다.

> - rule.json 화일을 만들고 아래와 같이 내용을 넣는다.  
>
>
> $ vi rule.json
>
> ```javascript
> [
>   {
>     "protocol": "tcp",
>     "destination": "10.30.60.23",
>     "ports": "30000"
>   }
> ]
> ```
>
> - 보안 그룹을 생성한다.  
>
>
> $ cf create-security-group CubridDB rule.json ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-5-0.png)
>
> - 모든 App에 Cubrid 서비스를 사용할수 있도록 생성한 보안 그룹을 적용한다.  
>
>
> $ cf bind-running-security-group CubridDB ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-6-0.png)
>
> - App을 리부팅 한다.  
>
>
> $ cf restart hello-spring-cubrid ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-7-0.png)

* App이 정상적으로 Cubrid 서비스를 사용하는지 확인한다.

> - curl 로 확인   
>  $ curl hello-spring-cubrid.115.68.46.30.xip.io
>
> ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-8-0.png)
>
> - 브라우져에서 확인  
>
>
> ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/3-3-8-1.png)

## 4. Cubrid Client 툴 접속

Application에 바인딩된 Cubrid 서비스 연결정보는 Private IP로 구성되어 있기 때문에 Cubrid Client 툴에서 직접 연결할수 없다. 따라서 Cubrid Client 툴에서 SSH 터널, Proxy 터널 등을 제공하는 툴을 사용해서 연결하여야 한다. 본 가이드는 무료 SSH 및 텔넷 접속 툴인 Putty를 이용하여 SSH 터널을 통해 연결 하는 방법을 제공하며 Cubrid Client 툴로써는 Cubrid에서 제공하는 Cubrid Manager로 가이드한다. Cubrid Manager 에서 접속하기 위해서 먼저 SSH 터널링 할수 있는 VM 인스턴스를 생성해야한다. 이 인스턴스는 SSH로 접속이 가능해야 하고 접속 후 Open PaaS 에 설치한 서비스팩에 Private IP 와 해당 포트로 접근이 가능하도록 시큐리티 그룹을 구성해야 한다. 이 부분은 vSphere관리자 및 OpenPaaS 운영자에게 문의하여 구성한다.

### 4.1.  Putty 다운로드 및 터널링

Putty 프로그램은 SSH 및 텔넷 접속을 할 수 있는 무료 소프트웨어이다.

* Putty를 다운로드 하기 위해 아래 URL로 이동하여 파일을 다운로드 한다. 별도의 설치과정없이 사용할 수 있다. [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-0-0.png)
* 다운받은 putty.exe.파일을 더블클릭하여 실행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-1-0.png)
* Session 탭의 Host name과 Port란에. OpenPaaS 운영 관리자에게 제공받은 SSH 터널링 가능한 서버 정보를 입력한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-2-0.png)
* Connection-&gt;SSH-&gt;Tunnels 탭에서 Source port\(내 로컬에서 접근할 포트\), Destination\(터널링으로 연결할 서버정보\)를 입력하고 Local, Auto를 선택 후 Add를 클릭한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-3-0.png) ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-3-1.png) 서버 정보는 Application에 바인드되어 있는 서버 정보를 입력한다. cf env  명령어로 이용하여 확인한다. 예\) $ cf env hello-spring-cubrid ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-4-0.png)
* Session 탭에서 Saved Sessions에 저장할 이름을 입력하고 Save를 눌러 저장한 후 Open버튼을 누른다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-5-0.png)
* 서버 접속정보를 입력하여 접속하여 터널링을 완료한다. 만약 ssh 인증이 Password방식이 아닌 Key인증 방식일 경우, Connection-&gt;SSH-&gt;인증탭의 '인증 개인키 파일'에 key 파일을 등록하여 인증한다. Key파일의 확장자가 .pem이라면 putty설치시 같이 설치된 puttygen을 사용하여 ppk파일로 변환한뒤 사용한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-1-6-0.png)

### 4.2.  Cubrid Manager 설치 & 연결

Cubrid Manager 프로그램은 Cubrid에서 제공하는 무료로 사용할 수 있는 소프트웨어이다.

* Cubrid Manager를 다운로드 하기 위해 아래 URL로 이동하여 설치파일을 다운로드 한다. [http://ftp.cubrid.org/CUBRID\_Tools/CUBRID\_Manager/](http://ftp.cubrid.org/CUBRID_Tools/CUBRID_Manager/) ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-0-0.png)
* 다운받은 파일을 더블클릭하여 실행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-1-0.png)
* 한국어를 선택하고 OK를 누른다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-2-0.png)
* 다음을 눌러 계속 진행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-3-0.png)
* 동의함을 눌러 계속 진행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-4-0.png)
* 바로가기 옵션을 선택 후 다음을 눌러 계속 진행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-5-0.png)
* 설치 경로를 입력하고 설치를 눌러 설치를 시작한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-6-0.png)
* 설치가 완료되면 다음을 눌러 계속 진행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-7-0.png)
* 마침을 눌러 설치를 완료한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-8-0.png)
* 설치된 Cubrid Manager를 실행하면 처음 나오는 화면이다. Workspace를 선택 후 OK를 눌러 실행한다. 만약 이 창을 다시보기를 원치않는다면 '기본적으로 이것을 사용하고 다시 물어 보지 않기' 옵션을 선택한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-9-0.png)
* 관리 모드, 질의 모드 둘중 목적에 맞게 선택 후 확인을 눌러 실행한다. 여기서는 질의 모드로 실행한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-10-0.png)
* 연결정보를 입력하기 위해서 연결 정보 등록을 누른다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-11-0.png)
* Server에 접속하기 위한 Connection 정보를 입력한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-12-0.png) 서버 정보는 Application에 바인드되어 있는 서버 정보를 입력한다. cf env  명령어로 이용하여 확인한다. 예\) $ cf env hello-spring-cubrid ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-13-0.png)
* 연결 테스트 버튼을 클릭하여 접속 테스트를 한다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-14-0.png) 정보가 정상적으로 입력되었다면 '연결이 성공하였습니다.'라는 메시지가 나온다. 확인 버튼을 눌러 창을 닫는다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-15-0.png)
* 연결 버튼을 클릭하여 접속한다 ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-16-0.png)
* 접속이 완료되면 좌측에 스키마 정보가 나타난다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-17-0.png)
* 질의 편집기 버튼을 클릭하면 오른쪽 창에 query를 입력할 수 있는 창이 열린다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-18-0.png)
* 우측 화면에 쿼리 항목에 Query문을 작성한 후 실행 버튼\(삼각형\)을 클릭한다. 쿼리문에 이상이 없다면 정상적으로 결과를 얻을 수 있을 것이다. ![](https://github.com/jhuhm13579/trans-test/tree/4fcd590011a086170f8b12fc902f71d3d4e564fc/images/paasta-service/cubrid/4-2-19-0.png)

