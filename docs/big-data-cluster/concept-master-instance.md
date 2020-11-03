---
title: 마스터 인스턴스란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터의 SQL Server 마스터 인스턴스를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 57de001599923d46139883f2f8a691f9d682abf3
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914313"
---
# <a name="what-is-the-master-instance-in-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 마스터 인스턴스란?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터에서 *SQL Server 마스터 인스턴스* 의 역할을 설명합니다. 마스터 인스턴스는 연결, 스케일 아웃 쿼리, 메타데이터 및 사용자 데이터베이스, 기계 학습 서비스를 관리하기 위해 SQL Server 빅 데이터 클러스터에서 실행되는 SQL Server 인스턴스입니다.

SQL Server 마스터 인스턴스는 다음과 같은 기능을 제공합니다.

## <a name="connectivity"></a>연결

SQL Server 마스터 인스턴스는 클러스터에 대해 외부에서 액세스할 수 있는 TDS 엔드포인트를 제공합니다. 다른 SQL Server 인스턴스와 마찬가지로 이 엔드포인트에 Azure Data Studio 또는 SQL Server Management Studio와 같은 SQL Server 도구나 애플리케이션을 연결할 수 있습니다.

## <a name="scale-out-query-management"></a>스케일 아웃 쿼리 관리

SQL Server 마스터 인스턴스에는 [컴퓨팅 풀](concept-compute-pool.md) 노드의 SQL Server 인스턴스에 쿼리를 분산하는 데 사용되는 스케일 아웃 쿼리 엔진이 있습니다. 스케일 아웃 쿼리 엔진을 사용하면 추가 구성없이 Transact-SQL을 통해 클러스터의 모든 Hive 테이블에 액세스할 수도 있습니다.

## <a name="metadata-and-user-databases"></a>메타데이터 및 사용자 데이터베이스

SQL 마스터 인스턴스에는 표준 SQL Server 시스템 데이터베이스 외에도 다음과 같은 항목이 있습니다.

- HDFS 테이블 메타데이터를 포함하는 메타데이터 데이터베이스
- 데이터 평면 분할된 데이터베이스 맵
- 클러스터 데이터 평면에 대한 액세스를 제공하는 외부 테이블 세부 정보
- 사용자 데이터베이스에 정의된 PolyBase 외부 데이터 원본 및 외부 테이블

SQL Server 마스터 인스턴스에 고유한 사용자 데이터베이스를 추가할 수도 있습니다.

## <a name="machine-learning-services"></a>Machine Learning Services

SQL Server Machine Learning Services는 SQL Server에서 Java, R 및 Python 코드를 실행하는 데 사용되는 데이터베이스 엔진의 추가 기능입니다. 이 기능은 핵심 엔진 프로세스에서 외부 프로세스를 분리하는 SQL Server 확장성 프레임워크를 기반으로 하지만 저장 프로시저, R 또는 Python 문을 포함하는 T-SQL 스크립트, T-SQL을 포함하는 Java, R 또는 Python 코드로 관계형 데이터와 완전히 통합됩니다.

Machine Learning Services는 SQL Server 빅 데이터 클러스터의 일부로, SQL Server 마스터 인스턴스에서 기본적으로 사용할 수 있습니다. 즉, SQL Server 마스터 인스턴스에서 외부 스크립트 실행을 사용하도록 설정하면 sp_execute_external_script를 사용하여 Java, R 및 Python 스크립트를 실행할 수 있습니다.

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>빅 데이터 클러스터에서 Machine Learning Services의 장점

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 사용하여 일반적으로 엔터프라이즈 데이터베이스에 저장된 차원 데이터에 빅 데이터를 쉽게 연결할 수 있습니다. 빅 데이터의 가치는 조직의 일부만 사용하는 것이 아니라 보고서, 대시보드 및 애플리케이션에도 포함될 때 크게 증가합니다. 이와 동시에 데이터 과학자는 Spark/HDFS 에코시스템 도구를 계속 사용하면서 SQL Server 마스터 인스턴스와 SQL Server 마스터 인스턴스를 ‘통해’ 액세스할 수 있는 외부 데이터 원본의 데이터를 실시간으로 쉽게 액세스할 수 있습니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 사용하면 엔터프라이즈 데이터 레이크로 더 많은 작업을 수행할 수 있습니다. SQL Server 개발자와 분석가는 다음 작업을 수행할 수 있습니다.

* 엔터프라이즈 데이터 레이크의 데이터를 사용하는 애플리케이션을 빌드합니다.
* Transact-SQL 쿼리를 사용하여 모든 데이터를 추론합니다.
* SQL Server 도구와 애플리케이션으로 구성된 기존 에코시스템을 사용하여 엔터프라이즈 데이터에 액세스하고 분석합니다.
* 데이터 가상화 및 데이터 마트를 통해 데이터 이동의 필요성을 줄입니다.
* 빅 데이터 시나리오에서 Spark를 계속 사용합니다.
* Spark 또는 SQL Server로 지능형 엔터프라이즈 애플리케이션을 빌드하여 데이터 레이크에서 모델을 학습합니다.
* 최상의 성능을 위해 프로덕션 데이터베이스에서 모델을 운영합니다.
* 실시간 분석을 위해 데이터를 엔터프라이즈 데이터 마트에 직접 스트리밍합니다.
* 대화형 분석 및 BI 도구를 사용하여 시각적으로 데이터를 탐색합니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
