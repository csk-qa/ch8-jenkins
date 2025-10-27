node {
    // ✅ 환경 변수 설정
    env.PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"

    try {
        stage('Checkout') {
            // Git 저장소 체크아웃
            checkout scm
        }

        stage('Install') {
            // 의존성 설치
            sh 'npm install'
        }

        stage('Test') {
            // 테스트 실행
            sh 'npm test'
        }

        stage('Start') {
            // 현재 브랜치 정보 출력 (디버깅용)
            echo "현재 브랜치: ${env.BRANCH_NAME ?: env.GIT_BRANCH}"

            // main 또는 origin/main 일 때만 실행
            if (env.BRANCH_NAME == 'main' || env.GIT_BRANCH == 'origin/main') {
                sh 'npm start'
            } else {
                echo "Start stage skipped (현재 브랜치가 main이 아님)"
            }
        }

        // ✅ 성공 시 메시지
        echo 'Pipeline 성공적으로 완료!'

    } catch (err) {
        // ❌ 실패 시 메시지
        echo 'Pipeline 실패!'
        echo "에러 내용: ${err}"
        currentBuild.result = 'FAILURE'
        throw err
    }
}
