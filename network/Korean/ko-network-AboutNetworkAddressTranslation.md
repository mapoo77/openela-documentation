<!--
SPDX-FileCopyrightText: 2024 Mahyun Kim <mahyun.kim@navercorp.com>
SPDX-FileCopyrightText: 2024 NAVER Cloud Company

SPDX-License-Identifier: CC-BY-SA-4.0
-->
# 네트워크 주소 변환

네트워크 주소 변환\(NAT\)은 다른 주소 체계를 사용하여 개인 네트워크 내의 컴퓨터 또는 컴퓨터 그룹에 공용 주소를 할당하는 프로세스입니다. 공용 IP 주소는 모든 요청이 여러 서버가 아닌 하나의 서버로 가는 것처럼 가장합니다. NAT는 조직이 자금을 조달해야 하는 공용 IP 주소의 수를 제한하는 데 유용합니다. NAT는 또한 내부 네트워크의 세부 정보를 숨김으로써 추가 보안을 제공합니다.

`netfilter` 커널 하위 시스템은 패킷 필터링을 위한 테이블 외에도 NAT를 구현하기 위한 `nat` 테이블을 제공합니다. 커널은 새로운 들어오거나 나가는 연결을 생성하는 패킷을 처리할 때마다 'nat' 테이블을 참조합니다.

기본적으로 IP 전달이 활성화되어 있으며 시스템은 구성된 네트워크 인터페이스 간에 패킷을 라우팅할 수 있습니다. IP 전달이 활성화되어 있는지 확인하려면 다음 명령을 사용하십시오.:

```
sudo sysctl -a | grep ip_forward
```

후속 출력에서 ​​'net.ipv4.ip_forward' 값 '1'은 IP 전달이 활성화되었음을 나타냅니다.

다음 명령을 사용하여 시스템의 IP 전달 상태를 변경할 수 있습니다.:

```
sudo sysctl -w net.ipv4.ip_forward=0|1
```

명령을 실행하면 새 상태가 표시됩니다. 시스템을 재부팅해도 변경 사항이 유지되도록 하려면 명령 출력 줄을 복사하여 `/etc/sysctl.conf` 파일에 추가하세요.

방화벽 구성 GUI\(`firewall-config`\)를 사용하여 매스커레이딩 및 포트 전달을 구성할 수도 있습니다.
