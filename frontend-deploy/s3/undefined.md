# 개요

<mark style="background-color:green;">SSG 배포</mark>는 "정적 사이트 생성기(Static Site Generator)"를 사용한 웹사이트 배포를 의미합니다. 이 방식은 동적 웹사이트와는 달리 서버에서 실시간으로 페이지를 생성하는 대신, 빌드 시점에 모든 페이지를 정적 파일로 미리 생성하여 배포하는 방법입니다.

#### SSG(Static Site Generator)의 특징:

1. **정적 파일 생성**: SSG는 HTML, CSS, JavaScript 같은 <mark style="background-color:purple;">정적 파일을 생성</mark>합니다. 이러한 파일들은 서버에서 별도의 처리 없이 그대로 제공될 수 있습니다.
2. **성능 및 보안**: 정적 파일은 서버 사이드 프로세싱이 필요 없기 때문에, <mark style="background-color:purple;">페이지 로딩이 빠르고 보안성이 높은 편</mark>입니다.
3. **SEO 최적화**: 정적 파일은 검색 엔진에 의해 쉽게 인덱싱될 수 있어 SEO(검색 엔진 최적화)에 유리합니다.
4. **호스팅 용이**: 정적 파일은 GitHub Pages, Netlify, Vercel 같은 간단한 정적 파일 호스팅 서비스에 쉽게 배포할 수 있습니다.
5. **확장성**: 트래픽이 증가해도 서버 부하가 크게 증가하지 않아, 많은 트래픽을 손쉽게 처리할 수 있습니다.

#### SSG 사용 예시:

인기 있는 SSG에는 Jekyll, Hugo, Gatsby, Next.js(정적 모드), Nuxt.js(정적 모드) 등이 있습니다. 이들 도구는 마크다운, JSON, YAML 등의 데이터 소스를 사용하여 사이트의 각 페이지를 빌드 시점에 HTML로 변환합니다.

#### SSG 배포 과정:

1. **콘텐츠 작성**: 마크다운 파일 등을 사용하여 콘텐츠를 작성합니다.
2. **빌드**: SSG 도구를 사용하여 사이트의 모든 페이지를 정적 파일로 빌드합니다.
3. **배포**: 생성된 정적 파일들을 정적 파일 호스팅 서비스에 업로드하여 배포합니다.

SSG를 사용한 배포는 웹사이트의 복잡성, 유지 관리, 비용 등 여러 면에서 이점을 제공합니다. 하지만, 실시간 콘텐츠 업데이트나 사용자 인터랙션을 많이 필요로 하는 동적인 웹 애플리케이션에는 적합하지 않을 수 있습니다.

## SSR vs SSG vs CSR

서버에서 사전 렌더링 하는 것까지가 Next.js 의 특징이고,&#x20;

사전 렌더링을 동적으로 해서 페이지를 생성하느냐, 정적으로 페이지를 생성하느냐의 차이가 SSR 과 SSG의 차이라고 보면된다.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

SSG 는 빌드를 진행할 때 pages 폴더에서 작성한 각 페이지들에 대해 각각의 HTML 문서를 생성해 static 한 파일로 생성한다.

그리고 해당 페이지에 요청이 올 때 마다 이미 생성된 HTML 문서를 반환한다.

따라서 CSR 보다 응답속도가 빠르고 Next.js 에서도 SSG를 사용하는 것을 권장한다.



하지만 그렇다고 해서 무조건이라는것은 없다 상황이라는게 존재하고 상황에 따라서 배포를 하는것이 언제나 최고의 방법이다.
