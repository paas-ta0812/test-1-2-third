# PaaS-TA 모니터링 화면 가이드\_v1.0

\#\# Table of Contents 1. [문서 개요](paas-ta-_v1.0-1.md#1)

* [1.1. 목적](paas-ta-_v1.0-1.md#2)
* [1.2. 범위](paas-ta-_v1.0-1.md#3)
  1. [PaaS-TA 모니터링 화면 사용자 계정 생성](paas-ta-_v1.0-1.md#4)
* [2.1.  모니터링 화면 사용자 계정 생성 - 관리자](paas-ta-_v1.0-1.md#5)
* [2.2.  모니터링 화면 사용자 계정 생성 - 사용자](paas-ta-_v1.0-1.md#6)
  1. [PaaS-TA 모니터링 화면 매뉴얼](paas-ta-_v1.0-1.md#7)
* [3.1.  Data Sources 생성](paas-ta-_v1.0-1.md#8)
* [3.2.  Dashboard Import](paas-ta-_v1.0-1.md#9)     
* [3.3.  Dashboard 생성](paas-ta-_v1.0-1.md#10)
* [3.4.  Chart 생성](paas-ta-_v1.0-1.md#11)
* [3.5.  Table 생성](paas-ta-_v1.0-1.md#12)
  1. [PaaS-TA 모니터링 메인 화면](paas-ta-_v1.0-1.md#13)

 \# 1. 문서 개요

### 1.1. 목적

본 문서는 PaaS-TA 모니터링 화면 사용 방법에 대해 기술하였다.

 \#\#\# 1.2. 범위 본 문서는 Windows 환경을 기준으로 PaaS-TA 모니터링 화면을 사용하는 방법에 대해 작성되었다.

## 2.  PaaS-TA 모니터링 화면 사용자 계정 생성

본 장에서는 PaaS-TA 모니터링 화면을 사용하기 위한 계정 생성 방법에 대해서 기술하였다. 모니터링 관리자가 사용자 계정을 생성하거나, 일반 사용자가 회원등록 화면을 통해 생성할 수 있다.

 \#\#\# 2.1. 모니터링 화면 사용자 계정 생성 - 관리자 1. PaaS-TA 모니터링 화면에 접속한다. !\[2-1-1\] 2. 관리자 계정정보를 입력 후, “로그인” 버튼을 클릭한다. !\[2-1-2\] 3. “사용자등록 화면”으로 이동한다. !\[2-1-3\] 4. 사용자 추가버튼\(Add new user\)을 클릭한다. !\[2-1-4\] 5. 사용자 정보를 등록한다. !\[2-1-5\] 6. 기본 사용자 권한 및 정보를 변경하고자 할 경우 "Edit" 버튼을 클릭한다. !\[2-1-6\] 7. 사용자 정보를 변경한다. !\[2-1-7\]

### 2.2.  모니터링 화면 사용자 계정 생성 - 사용자

1. PaaS-TA 모니터링 화면에 접속한다. ![](../../.gitbook/assets/2-1-1%20%2829%29.png)
2. 회원가입\(Sign-up\) 탭을 선택한다. ![](../../.gitbook/assets/2-2-2%20%286%29.png)
3. 유효한 이메일 정보를 입력한다. ![](../../.gitbook/assets/2-2-3%20%284%29.png)
4. 사용자 정보를 입력한다. ![](../../.gitbook/assets/2-2-4%20%282%29.png)
5. 메인화면으로 이동한다.

 \# 3. 모니터링 화면 매뉴얼 본 장에서는 PaaS-TA 모니터링 화면의 메뉴 구성 및 화면 설명에 대해서 기술하였다.

### 3.1.  Data Sources 생성

모니터링 메인화면 Chart 또는 Table에서 사용할 Data Source를 생성하는 방법에 대해서 기술하였다.

### 3.1.1 상단 "PaaS TA Monitor" 메뉴를 클릭하고, 팝업된 메뉴 리스트에서 "Data Sources"를 선택한다.

![](../../.gitbook/assets/3-1-1%20%285%29.png)

### 3.1.2 "Add data source"를 선택한다.

![](../../.gitbook/assets/3-1-2%20%282%29.png)

### 3.1.3 "Data Source" 정보를 입력한다.

![](../../.gitbook/assets/3-1-3%20%282%29.png)

> DataSource 정보는 추후에 화면에 보여줄 Graph 또는 Table 차트 생성시 사용된다. 예를 들어, Bosh 서비스의 CPU Chart를 생성시, 생성한 Bosh 서비스의 DataSource가 "Bosh" 이면, CPU Chart 생성화면의 Metrics Tab의 Panel data source 부분을 "Bosh"로 선택한다.

 \#\#\# 3.2. Dashboard Import 기존에 생성된 모니터링 메인화면 Dashboard를 Import하는 방법에 대해서 기술하였다. \#\#\# 3.2.1 상단 "PaaS TA Monitor" 메뉴를 클릭하고, 팝업된 메뉴 리스트에서 "Dashboards"를 선택 후, "Import" 메뉴를 클릭한다. !\[3-2-1\] \#\#\# 3.2.2 "Upload json file" 버튼을 클릭한 뒤, Import 시킬 Json 설정 파일을 선택한다. !\[3-2-2\]

### 3.3.  Dashboard 생성

모니터링 메인화면 Dashboard를 생성하는 방법에 대해서 기술하였다.

### 3.3.1 상단 Main 버튼을 클릭하고, 팝업된 메뉴 하단의 "Create New" 버튼을 클릭한다.

![](../../.gitbook/assets/3-3-1%20%282%29.png)

### 3.3.2 상단의 설정버튼\(\*\)을 클릭한다.

![](../../.gitbook/assets/3-3-2%20%282%29.png)

### 3.3.3 팝업된 메뉴에서 "Setting" 을 선택한다.

![](../../.gitbook/assets/3-3-3%20%282%29.png)

### 3.3.4 Dashboard 관련 정보를 입력한다.

![](../../.gitbook/assets/3-3-4%20%282%29.png)

 \#\#\# 3.4. Chart 생성 Dashboard 화면에서 보고자하는 Chart를 생성하는 방법에 대해서 기술한다. \#\#\# 3.4.1 왼쪽 상단에 위치한 버튼을 클릭하여 팝업된 메뉴에서, "Graph"를 선택한다. !\[3-4-1\] \#\#\# 3.4.2 생성된 Chart 의 "Panel Title"를 클릭하여 팝업된 메뉴에서 "Edit"를 선택한다. !\[3-4-2\] \#\#\# 3.4.3 Chart 설정 메뉴에서 "Metrics" 탭 화면을 선택한다. !\[3-4-3\] \#\#\# 3.4.4 "Panel data source" 영역을 클릭하여, 팝업된 메뉴에서 연결하고자 하는 데이터 소스를 선택한다. &gt; 위의 DataSource 생성 부분에서 생성한 DataSource와 연동된다. &gt; 각각의 DataSource에서 관리하는 데이터베이스와 Measurement 정보는 아래를 참조한다. - \[Monitoring Database & Measurements\]\(https://github.com/PaaS-TA/Guide-2.0-Linguine-/blob/master/Use-Guide/PaaS-TA%20%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81%20DB%20%EB%B0%8F%20Metrics%20%EA%B0%80%EC%9D%B4%EB%93%9C.md\) !\[3-4-4\] \#\#\# 3.4.5 Chart에서 보여주고자 하는 데이터를 조회하는 쿼리를 생성한다. !\[3-4-5\] \#\#\# 3.4.6 쿼리 결과에 해당하는 정보가 Chart로 보여진다. !\[3-4-6\]

### 3.5.  Table 생성

Dashboard 화면에서 보고자하는 Table을 생성하는 방법에 대해서 기술한다.

### 3.5.1 왼쪽 상단에 위치한 버튼을 클릭하여 팝업된 메뉴에서, "Table"를 선택한다.

![](../../.gitbook/assets/3-5-1%20%282%29.png)

### 3.5.2 Table 설정 메뉴에서 "Metrics" 탭 화면을 선택한다.

![](../../.gitbook/assets/3-5-2%20%282%29.png)

### 3.5.3 "Panel data source" 영역을 클릭하여, 팝업된 메뉴에서 연결하고자 하는 데이터 소스를 선택한다.

![](../../.gitbook/assets/3-5-3%20%282%29.png)

### 3.5.4 Table에서 보여주고자 하는 데이터를 조회하는 쿼리를 생성한다.

![](../../.gitbook/assets/3-5-4-1%20%282%29.png) ![](../../.gitbook/assets/3-5-4-2%20%282%29.png) ![](../../.gitbook/assets/3-5-4-3%20%282%29.png)

### 3.5.5 퀴리 결과에 해당하는 정보가 Table로 보여진다.

![](../../.gitbook/assets/3-3-5%20%282%29.png)

## 4. 모니터링 메인 화면

위의 과정을 통해 생성된 메인화면이다. ![](../../.gitbook/assets/main%20%282%29.png)

