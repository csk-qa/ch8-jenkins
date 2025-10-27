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
            // 현재 브랜치 정보 수동 확인
            script {
                def branch = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                echo "현재 브랜치: ${branch}"
        
                if (branch == 'main' || branch == 'origin/main') {
                    sh 'npm start'
                } else {
                    echo "Start stage skipped (현재 브랜치가 main이 아님)"
                }
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
