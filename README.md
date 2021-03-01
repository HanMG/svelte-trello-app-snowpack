https://www.inflearn.com/course/%EC%8A%A4%EB%B2%A8%ED%8A%B8-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C#

# 결과물 
https://competent-keller-61aa8f.netlify.app/

# svelte-trello-app-snowpack
trello 라는 Todo 서비스를 svelte를 이용하여 클론 구현

기존의 rollup 기반의 svelte-trello-app을

snowpack 기반으로 이관

# snowpack
snowpack은 번들러가 아닌 프론트엔드 빌드 도구라고함.

상세내용:
https://heropy.blog/2020/10/31/snowpack/

# autoprefixer와 postcss 설치 적용

['@snowpack/plugin-svelte', {
	preprocess: require('svelte-preprocess')({
		scss: {
			prependData: '@import "./src/scss/main.scss";'
		},
		postcss: {
			plugins: [
				require('autoprefixer')()
			]
		},
		babel: babelOptions()
	})
}], 


# 콘솔 제거
rollup에서 사용한 strip이 아니라

babel-plugin-transform-remove-console 을 사용

@snowpack/plugin-svelte' 의 옵션으로 
babe: babelOptions()

'@snowpack/plugin-babel' 의 옵션으로
transformOptions: babelOptions()

위의 것들을 추가.

'@snowpack/plugin-dotenv' 을 적용 후,
const production = process.env.NODE_ENV === 'production'
개발모드인지 생산모드인지를 체크해서 transform-remove-console을 적용할 수 있도록 함

같은 내용을 전역화
function babelOptions() {
    return {
        plugins: production
                ? ['transform-remove-console']
                : [] 
    }
}

# alias (경로 별칭)
rollup과 달리 설치 필요 X
alias: {
	'~' : './src'
}

# 코드 최적화(최소화)
rollup 에서는 terser였는데 

snowpack 에서는 @snowpack/plugin-optimize을 설치 후 
plugins에 그냥 적용시켜주면 됨

# 배포

rollup은 /public으로 배포하면 됐었는데
snowpack은 /build으로 배포