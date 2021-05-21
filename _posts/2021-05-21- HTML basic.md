---
layout: post
title: API Gateway API에서 CORS 오류 해결하기.
date:   2021-05-22 10:00:35 +0300
image:  pexels-anderson-miranda-1975781
---
![CORS](/images/CORS_1.png.png))
![CORS](/images/CORS_2.png.png))

### 1. CORS (Cross-Origin Resource Sharing)란?

교차 출처 리소스 공유 또는 CORS는 최신 웹 브라우저의 보안 기능입니다. 이를 통해 웹 브라우저는 외부 웹 사이트 또는 서비스를 요청할 수있는 도메인을 협상 할 수 있습니다. CORS는 JavaScript 용 AWS SDK를 사용하여 브라우저 애플리케이션을 개발할 때 중요한 고려 사항입니다. 리소스에 대한 대부분의 요청은 웹 서비스의 엔드 포인트와 같은 외부 도메인으로 전송되기 때문입니다. JavaScript 환경에서 CORS 보안을 적용하는 경우 서비스를 사용하여 CORS를 구성해야합니다.

CORS는 다음을 기반으로 교차 출처 요청에서 리소스 공유를 허용할지 여부를 결정합니다.

+ 요청을하는 특정 도메인

+ HTTP 요청 유형 (GET, PUT, POST, DELETE 등)

### 2. CORS의 작동 원리
[![How--CORS--Works](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/images/cors-overview.png)]
가장 간단한 경우 브라우저 스크립트는 다른 도메인의 서버에서 리소스에 대한 GET 요청을합니다. 해당 서버의 CORS 구성에 따라 요청이 GET 요청을 제출할 수있는 권한이있는 도메인의 요청 인 경우 교차 원본 서버는 요청 된 리소스를 반환하여 응답합니다.

요청 도메인 또는 HTTP 요청 유형이 승인되지 않은 경우 요청이 거부됩니다. 그러나 CORS를 사용하면 실제로 요청을 제출하기 전에 요청을 프리 플라이트 할 수 있습니다. 이 경우 OPTIONS 액세스 요청 작업이 전송 되는 프리 플라이트 요청이 만들어 집니다. 교차 원본 서버의 CORS 구성이 요청 도메인에 대한 액세스 권한을 부여하면 서버는 요청 도메인이 요청 된 리소스에 대해 만들 수있는 모든 HTTP 요청 유형을 나열하는 프리 플라이트 응답을 다시 보냅니다.

### 3. CORS 구성
Amazon S3 버킷에서 작업을 수행하려면 먼저 CORS 구성이 필요합니다. 일부 JavaScript 환경에서는 CORS가 적용되지 않을 수 있으므로 CORS를 구성 할 필요가 없습니다. 예를 들어 Amazon S3 버킷에서 애플리케이션을 호스팅하고 다음에서 리소스에 액세스하는 경우*.s3.amazonaws.com 또는 다른 특정 엔드 포인트의 경우 요청이 외부 도메인에 액세스하지 않습니다. 따라서이 구성에는 CORS가 필요하지 않습니다. 이 경우 CORS는 Amazon S3 이외의 서비스에 계속 사용됩니다.




### 4. API Gateway API에서 CORS 오류 해결하기.

서버가 CORS 표준에 필요한 HTTP 헤더를 반환하지 않으면 Cross-Origin Resource Sharing(CORS) 오류가 발생합니다. API Gateway REST API 또는 HTTP API에서 CORS 오류를 해결하려면 CORS 표준을 충족하도록 API를 다시 구성합니다.

해결 방법
다음 예에서는 CORS 오류를 나타내는 'Access-Control-Allow-Origin' 헤더 없음을 해결하는 방법을 보여줍니다. 그러나 유사한 절차를 사용하여 모든 CORS 오류를 해결할 수 있습니다. 예: Access-Control-Allow-Methods 헤더에서 메서드를 지원하지 않음(Method not supported under Access-Control-Allow-Methods header) 오류 및 ‘Access-Control-Allow-Headers’ 헤더 없음(No ‘Access-Control-Allow-Headers’ headers present) 오류.

참고: 'Access-Control-Allow-Origin' 헤더 없음(No 'Access-Control-Allow-Origin' header present) 오류는 다음과 같은 이유로 발생할 수 있습니다.

API가 필요한 CORS 헤더를 반환하는 OPTIONS 메서드로 구성되지 않았습니다.
다른 메서드 유형(예: GET, PUT 또는 POST)이 필요한 CORS 헤더를 반환하도록 구성되지 않았습니다.
프록시 통합 또는 비 프록시 통합이 있는 API가 필요한 CORS 헤더를 반환하도록 구성되지 않았습니다.
프라이빗 REST API의 경우 잘못된 호출 URL이 호출되거나 트래픽이 인터페이스 Virtual Private Cloud(VPC) 엔드포인트로 라우팅되지 않습니다.
오류 원인 확인
API Gateway에서 CORS 오류의 원인을 확인하는 방법에는 두 가지가 있습니다.

API를 호출할 때 HTTP 아카이브(HAR) 파일을 만듭니다. 그런 다음 API 응답에 반환된 파라미터의 헤더를 검사하여 파일의 오류 원인을 확인합니다.
브라우저의 개발자 도구를 사용하여 실패한 API 요청의 요청 및 응답 파라미터를 확인합니다.
오류가 발생하는 API 리소스에서 CORS를 사용하도록 설정합니다.
REST API의 경우 API Gateway 콘솔을 사용하여 리소스에서 CORS 활성화를 참조하세요. HTTP API에 대한 자세한 내용은 HTTP API에 대한 CORS 구성을 참조하세요.

중요: HTTP API에 대해 CORS를 구성하는 경우 API Gateway는 API에 대해 구성된 OPTIONS 경로가 없더라도 사전 OPTIONS 요청에 대한 응답을 자동으로 보냅니다. CORS 요청의 경우 API Gateway는 구성된 CORS 헤더를 통합의 응답에 추가합니다.

CORS를 활성화하는 동안 다음을 수행해야 합니다.

<api-name> API에 대한 게이트웨이 응답의 경우 DEFAULT 4XX 및 DEFAULT 5XX 확인란을 선택합니다.
참고: 이러한 기본 옵션을 선택하면 요청이 엔드포인트에 도달하지 않는 경우에도 API Gateway는 필수 CORS 헤더로 응답합니다. 예를 들어 요청에 잘못된 리소스 경로가 포함된 경우 API Gateway는 403 “인증 토큰 누락”(403 "Missing Authentication Token") 오류로 계속 응답합니다.

메서드에 대해 OPTIONS 메서드가 아직 선택되어 있지 않은 경우 해당 확인란을 선택합니다. 또한 CORS 요청에 사용할 수 있는 다른 모든 메서드의 확인란을 선택합니다. 예: GET, PUT 및 POST.
참고: API Gateway 콘솔에서 CORS를 활성화할 때 OPTIONS 메서드가 리소스에 아직 존재하지 않는 경우 OPTIONS 메서드가 추가됩니다. 또한 필요한 Access-Control-Allow-* 헤더를 사용하여 OPTIONS 메서드의 200 응답을 구성합니다. 콘솔을 사용하여 CORS를 이미 활성화한 경우 다시 활성화하면 기존 값을 덮어씁니다.

필요한 CORS 헤더를 반환하도록 REST API 통합 구성
응답에 필요한 CORS 헤더를 보내도록 백엔드 AWS Lambda 함수 또는 HTTP 서버를 구성합니다. Access-Control-Allow-Origin에서 도메인 목록을 반환하려면 목록의 도메인 이름을 Access-Control-Allow-Origin 헤더 값으로 보내도록 백엔드를 구성해야 합니다.

중요: 프록시 통합을 사용하는 경우 API Gateway에서 통합 응답을 설정하여 API 백엔드에서 반환된 응답 파라미터를 수정할 수 없습니다. 프록시 통합에서 API Gateway는 백엔드 응답을 클라이언트에 직접 전달합니다.

비 프록시 통합을 사용하는 경우 필요한 CORS 헤더를 반환하도록 API Gateway에서 통합 응답을 수동으로 설정합니다.

참고: 비 프록시 통합을 사용하는 API의 경우 API Gateway 콘솔을 사용하여 리소스에서 CORS를 활성화하면 필요한 CORS 헤더가 리소스에 자동으로 추가됩니다.

인터페이스 엔드포인트의 프라이빗 DNS 설정 확인(프라이빗 REST API에만 해당)
프라이빗 REST API의 경우 연결된 인터페이스 VPC 엔드포인트에 프라이빗 DNS가 활성화되어 있는지 확인합니다.

인터페이스 엔드포인트에 프라이빗 DNS가 활성화되어 있는 경우, 프라이빗 DNS 이름으로 Amazon Virtual Private Cloud(Amazon VPC) 내에서 프라이빗 API를 호출하여 CORS 오류를 방지합니다.

프라이빗 DNS가 활성화되지 않은 경우 호출 URL에서 VPC 엔드포인트의 IP 주소로 트래픽을 수동으로 라우팅합니다.

참고: 프라이빗 DNS의 사용 여부에 관계없이 https://api-id.execute-api.region.amazonaws.com/stage-name이라는 호출 URL을 사용합니다. api-id, region 및 stage-name의 값을 API에 필요한 값으로 바꿔야 합니다. 

자세한 내용은 프라이빗 API를 호출하는 방법을 참조하세요.

중요: 프라이빗 DNS를 사용하지 않을 때 CORS를 사용하도록 설정한 경우 다음 제한 사항에 유의해야 합니다.

Amazon VPC 내에서 프라이빗 API에 액세스하는 데 엔드포인트 전용 퍼블릭 DNS 이름을 사용할 수 없습니다.
브라우저의 요청은 호스트 헤더 조작을 허용하지 않으므로 호스트 헤더 옵션을 사용할 수 없습니다.
헤더를 포함하지 않는 사전 OPTIONS 요청을 트리거하기 때문에 x-apigw-api-id 사용자 지정 헤더를 사용할 수 없습니다. x-apigw-api-id 헤더를 사용하는 API 호출은 API에 도달하지 못합니다.
