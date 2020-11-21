# API 문서 자동화

## 왜 문서를 자동화 해야 할까?
* 백엔드 개발자와 프론트엔드 개발자 사이의 커뮤니케이션 비용을 절감할 수 있다.
* API는 수시로 변하므로, 자동화를 하지 않으면 실제 API와 문서와의 불일치가 생길 수 있다.

## API 서버 빌드시 자동으로 문서를 생성하도록 하려면?
* Swagger
* Spring Rest Doc

## Swagger
* 어노테이션 기반 REST API 문서 자동화
* 빌드시 문서를 자동으로 생성한다.
* 대화형 API 콘솔을 자동으로 생성한다. - 빠르게 API 기능 테스트를 수행할 수 있다. (Posman 같은 역할을 할 수 있다.)

### Swagger 어노테이션
* `@Api` - Controller 단위 REST API 메타데이터 명시
* `@ApiOperation` - 하나의 REST API 요청 URL에 매핑, 문서화 대상으로 처리
* `@ApiRaram`, `@ApilmplicitParam` - REST API 호출시 전달되는 파라미터에 대한 설명
* `@ApiModelProperty` - Model Class 필드에 대한 설명

### Swagger 단점
* 변경 이력관리가 안된다.
* 코드 침투적이다. (어노테이션이 도배될 수 있다)

## 적용 예시
![1](../etc/img/api_문서_자동화(1).jpeg)

![2](../etc/img/api_문서_자동화(2).jpeg)

![3](../etc/img/api_문서_자동화(3).jpeg)

![4](../etc/img/api_문서_자동화(4).jpeg)
