stage name: 'Docker Tests', concurrency: 1
node {
     checkout scm
     echo "Stage 1: Run Docker Tests"
     echo "${BRANCH_NAME}"
     sh './scripts/test-docker.sh'
}

stage name: 'Composer Update', concurrency: 1
node {
    sh './scripts/dcomposer.sh install --prefer-dist'
}

stage name: 'Pre-Checking', concurrency: 1
parallel (
    phase1: {
        node {
            parallel (
                phase1: { sh "echo lint css; sleep 10s; echo done w/ css" },
                phase2: { sh "echo lint php; sleep 15s; echo done w/ php" },
                phase3: { sh "echo lint js; sleep 15s; echo done w/ js" }
            )
        }
    },

    phase2: {
        node {
            parallel (
                phase1: { sh "echo PHP Tests" },
                phase2: { sh "echo SonarQube Tests" },
                phase3: { sh "echo PHP Unit Tests" },
                phase4: { sh "echo JS Unit Tests" }
            )
        }
    }
)

stage name: 'Asset Generation', concurrency: 1
node {
    echo "Build assets"
}
stage name: 'Setup Environment', concurrency: 1
node {
    echo "Pull DB of Record"
    echo "Drush CR"
    echo "Drush FR"
    echo "Drush CR"
}

stage name: 'Run Tests', concurrency: 1
node {
    parallel (
        phase1: { echo "CodeCeption" },
        phase2: { echo "CSS" },
        phase3: { echo "SEO" },
        phase4: { echo "Analytics"},
        phase5: { echo "Social" }
    )
    echo "Load"
    echo "Test No Logs"
}