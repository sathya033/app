// pipeline {
//   agent any

//   stages {
//     stage('Checkout') {
//       steps {
//         git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//       }
//     }

//     stage('Install Dependencies') {
//       steps {
//         script {
//           def nodeModulesExists = fileExists('node_modules')
//           if (!nodeModulesExists) {
//             echo 'node_modules not found. Running npm install...'
//             bat 'npm install'
//           } else {
//             echo 'node_modules already installed. Skipping npm install.'
//           }
//         }
//       }
//     }

//     stage('Install Angular CLI') {
//       steps {
//         script {
//           def angularCliInstalled = bat(script: 'ng version', returnStatus: true) == 0
//           if (!angularCliInstalled) {
//             echo 'Angular CLI not found. Installing...'
//             bat 'npm install -g @angular/cli'
//           } else {
//             echo 'Angular CLI already installed. Skipping installation.'
//           }
//         }
//       }
//     }
//     stage('Build Angular App') {
//       steps {
//         bat 'ng build'
//       }
//     }

//     stage('Serve and Watch for Changes') {
//       steps {
//         script {
//           def deliverScriptExists = fileExists('e2e/jenkins/scripts/deliver.bat')
//           if (deliverScriptExists) {
//             echo 'Starting Angular Server...'
//             powershell 'Set-ExecutionPolicy Unrestricted -Scope Process; Unblock-File -Path ".\\e2e\\jenkins\\scripts\\deliver.bat"'
//             bat 'start /B .\\e2e\\jenkins\\scripts\\deliver.bat'
//           } else {
//             error 'Deliver script not found! Stopping pipeline.'
//           }
//         }
//       }
//     }
//   }
//   stage('Build Backend') {
//     steps {
//     script {
//       def backendDir = 'backend'
//       dir(backendDir) {
//       bat 'npm install'
//       bat 'npm run build'
//       }
//     }
//     }
//   }

//   post {
//     success {
//       echo '  Build Successful! Angular is running with live reload.'
//     }
//     failure {
//       echo ' Build Failed!'
//     }
//   }
// }




// pipeline {
//     agent any

//     environment {
//         NODE_VERSION = "22"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     nvm install %NODE_VERSION%
//                     nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     if not exist node_modules (
//                         echo node_modules not found. Running npm install...
//                         npm install
//                     ) else (
//                         echo node_modules already installed. Skipping npm install.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Install Angular CLI') {
//             steps {
//                 script {
//                     bat '''
//                     where ng >nul 2>nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli
//                     ) else (
//                         echo Angular CLI already installed. Skipping installation.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Build Frontend and Backend in Parallel') {
//             parallel {
//                 stage('Build Angular Frontend') {
//                     steps {
//                         bat 'ng build --configuration=production'
//                     }
//                 }
//                 stage('Build Backend') {
//                     steps {
//                         bat '''
//                         cd backend
//                         npm install
//                         npm run build
//                         '''
//                     }
//                 }
//             }
//         }

//         stage('Serve and Watch for Changes') {
//             steps {
//                 script {
//                     if (fileExists('e2e/jenkins/scripts/deliver.bat')) {
//                         echo 'Starting Angular Server...'
//                         bat 'powershell Set-ExecutionPolicy Unrestricted -Scope Process'
//                         bat 'powershell Unblock-File -Path ".\\e2e\\jenkins\\scripts\\deliver.bat"'
//                         bat 'start /B .\\e2e\\jenkins\\scripts\\deliver.bat'
//                     } else {
//                         error 'Deliver script not found! Stopping pipeline.'
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo ' Build Successful! Angular and Backend are running.'
//         }
//         failure {
//             echo ' Build Failed!'
//         }
//     }
// }

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// pipeline {
//     agent any

//     environment {
//         NODE_VERSION = "22"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     for /f "tokens=*" %%v in ('nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
//                     if not defined FOUND_NODE (
//                         echo Node.js %NODE_VERSION% not found. Installing...
//                         nvm install %NODE_VERSION%
//                     ) else (
//                         echo Node.js %NODE_VERSION% already installed. Skipping installation.
//                     )
//                     nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking if dependencies need installation...
//                     if exist package.json (
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Dependencies outdated or missing. Running npm install...
//                             npm install
//                         ) else (
//                             echo All dependencies are already installed. Skipping npm install.
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Install Angular CLI') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Angular CLI...
//                     where ng >nul 2>nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli
//                     ) else (
//                         echo Angular CLI is already installed.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Build Frontend and Backend in Parallel') {
//             parallel {
//                 stage('Build Angular Frontend') {
//                     steps {
//                         bat 'ng build --configuration=production'
//                     }
//                 }
//                 stage('Build Backend') {
//                     steps {
//                         bat '''
//                         cd backend
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Installing missing dependencies for backend...
//                             npm install
//                         ) else (
//                             echo Backend dependencies are already installed.
//                         )
//                         npm run build
//                         '''
//                     }
//                 }
//             }
//         }

//         stage('Serve and Watch for Changes') {
//             steps {
//                 script {
//                     if (fileExists('e2e/jenkins/scripts/deliver.bat')) {
//                         echo 'Starting Angular Server...'
//                         bat 'powershell Set-ExecutionPolicy Unrestricted -Scope Process'
//                         bat 'powershell Unblock-File -Path ".\\e2e\\jenkins\\scripts\\deliver.bat"'
//                         bat 'start /B .\\e2e\\jenkins\\scripts\\deliver.bat'
//                     } else {
//                         error 'Deliver script not found! Stopping pipeline.'
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo ' Build Successful! Angular and Backend are running.'
//         }
//         failure {
//             echo ' Build Failed!'
//         }
//     }
// }



//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

// pipeline {
//     agent any

//     environment {
//         NODE_VERSION = "22"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     for /f "tokens=*" %%v in ('nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
//                     if not defined FOUND_NODE (
//                         echo Node.js %NODE_VERSION% not found. Installing...
//                         nvm install %NODE_VERSION%
//                     ) else (
//                         echo Node.js %NODE_VERSION% already installed. Skipping installation.
//                     )
//                     nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking frontend dependencies...
//                     if exist package.json (
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Dependencies outdated or missing. Running npm install...
//                             npm install
//                         ) else (
//                             echo All dependencies are already installed. Skipping npm install.
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Checking backend dependencies...
//                     cd backend
//                     if exist package.json (
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Installing missing dependencies for backend...
//                             npm install
//                         ) else (
//                             echo Backend dependencies are already installed.
//                         )
//                     ) else (
//                         echo Backend package.json not found! Exiting...
//                         exit /b 1
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Install Angular CLI') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Angular CLI...
//                     where ng >nul 2>nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli
//                     ) else (
//                         echo Angular CLI is already installed.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Start Backend & Frontend') {
//             steps {
//                 script {
//                     bat '''
//                     echo Starting backend server...
//                     start /B cmd /c "cd backend && npm run dev"

//                     echo Starting Angular frontend...
//                     start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                     '''
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo ' Servers are running! Frontend and Backend are live.'
//         }
//         failure {
//             echo ' Failed to start servers.'
//         }
//     }
// }

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "22"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     for /f "tokens=*" %%v in ('nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
//                     if not defined FOUND_NODE (
//                         echo Node.js %NODE_VERSION% not found. Installing...
//                         nvm install %NODE_VERSION%
//                     ) else (
//                         echo Node.js %NODE_VERSION% already installed. Skipping installation.
//                     )
//                     nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking frontend dependencies...
//                     if exist package.json (
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Dependencies outdated or missing. Running npm install...
//                             npm install
//                         ) else (
//                             echo All dependencies are already installed. Skipping npm install.
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Checking backend dependencies...
//                     cd backend
//                     if exist package.json (
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Installing missing dependencies for backend...
//                             npm install
//                         ) else (
//                             echo Backend dependencies are already installed.
//                         )
//                     ) else (
//                         echo Backend package.json not found! Exiting...
//                         exit /b 1
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Install Angular CLI') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Angular CLI...
//                     where ng >nul 2>nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli
//                     ) else (
//                         echo Angular CLI is already installed.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Build and Deploy') {
//             steps {
//                 script {
//                     if (params.Type_of_Build == 'Test') {
//                         echo "Starting Test Environment"
//                         bat '''
//                         echo Starting backend server...
//                         start /B cmd /c "cd backend && npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo "Starting Production Environment"
//                         bat '''
//                         echo Running production build...
//                         call deliver.bat 'start /B .\\e2e\\jenkins\\scripts\\deliver.bat'
//                         '''
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo ' Servers are running! Frontend and Backend are live.'
//         }
//         failure {
//             echo ' Build failed. Check logs for details.'
//         }
//     }
// }








// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "22"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     for /f "tokens=*" %%v in ('nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
//                     if not defined FOUND_NODE (
//                         echo Node.js %NODE_VERSION% not found. Installing...
//                         nvm install %NODE_VERSION%
//                     ) else (
//                         echo Node.js %NODE_VERSION% already installed. Skipping installation.
//                     )
//                     nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking frontend dependencies...
//                     if exist package.json(
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Dependencies outdated or missing. Running npm install...
//                             npm install
//                         ) else (
//                             echo All dependencies are already installed. Skipping npm install.
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Checking backend dependencies...
//                     cd backend
//                     if exist package.json (
//                         npm ci --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Installing missing dependencies for backend...
//                             npm install
//                         ) else (
//                             echo Backend dependencies are already installed.
//                         )
//                     ) else (
//                         echo Backend package.json not found! Exiting...
//                         exit /b 1
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Install Angular CLI') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Angular CLI...
//                     where ng >nul 2>nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli
//                     ) else (
//                         echo Angular CLI is already installed.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Build and Deploy') {
//             steps {
//                 script {
//                     if (params.Type_of_Build == 'Test') {
//                         echo " Starting Test Environment..."
//                         bat '''
//                         echo Starting backend server...
//                         start /B cmd /c "cd backend && npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo " Starting Production Environment..."
//                         bat '''
//                         REM Kill any previous Angular server process if running
//                         if exist .pidfile (
//                           set /p PID=<.pidfile
//                           taskkill /F /PID %PID%
//                           del .pidfile
//                           echo Stopped previous Angular server.
//                         )

//                         echo Building the Angular project...
//                         ng build --configuration=production
//                         if %ERRORLEVEL% NEQ 0 (
//                           echo Build failed!
//                           exit /b %ERRORLEVEL%
//                         )
//                         echo  Build succeeded.

//                         echo Starting backend server in production mode...
//                         start /B cmd /c "cd backend && npm run start"

//                         echo Starting Angular frontend in production mode...
//                         start /B cmd /c "npx serve -s dist"

//                         echo  Angular app is running in production mode.
//                         '''
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo ' Servers are running! Frontend and Backend are live.'
//         }
//         failure {
//             echo ' Build failed. Check logs for details.'
//         }
//     }
// }



pipeline {
    agent any

    parameters {
        choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
    }

    environment {
        NODE_VERSION = "18"
    }

    stages {
        stage('Setup Node.js via NVM') {
            steps {
                script {
                    bat '''
                    echo Checking Node.js version...
                    set FOUND_NODE=
                    for /f "tokens=*" %%v in ('nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
                    if not defined FOUND_NODE (
                        echo Node.js %NODE_VERSION% not found. Installing...
                        nvm install %NODE_VERSION%
                    ) else (
                        echo Node.js %NODE_VERSION% already installed. Skipping installation.
                    )
                    nvm use %NODE_VERSION%
                    node -v
                    npm -v
                    '''
                }
            }
        }

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/sathya033/app.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    bat '''
                    echo Checking frontend dependencies...
                    if exist package.json (
                        echo package.json found. Checking dependencies...
                        npm install --dry-run > nul 2>&1
                        if %ERRORLEVEL% NEQ 0 (
                            echo Dependencies outdated or missing. Running npm ci...
                            npm ci
                        ) else (
                            echo All dependencies are installed.
                        )
                    ) else (
                        echo package.json not found! Exiting...
                        exit /b 1
                    )

                    echo Checking backend dependencies...
                    if exist backend (
                        cd backend
                        if exist package.json (
                            npm install --dry-run > nul 2>&1
                            if %ERRORLEVEL% NEQ 0 (
                                echo Installing missing dependencies for backend...
                                npm ci
                            ) else (
                                echo Backend dependencies are already installed.
                            )
                        ) else (
                            echo Backend package.json not found! Exiting...
                            exit /b 1
                        )
                    ) else (
                        echo Backend directory not found! Exiting...
                        exit /b 1
                    )
                    '''
                }
            }
        }

        stage('Install Angular CLI') {
            steps {
                script {
                    bat '''
                    echo Checking Angular CLI...
                    where ng >nul 2>nul
                    if %ERRORLEVEL% NEQ 0 (
                        echo Angular CLI not found. Installing...
                        npm install -g @angular/cli@14
                    ) else (
                        echo Angular CLI is already installed.
                    )
                    '''
                }
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    if (params.Type_of_Build == 'Test') {
                        echo "Starting Test Environment..."
                        bat '''
                        echo Starting backend server...
                        start /B cmd /c "cd backend && npm run dev"

                        echo Starting Angular frontend in development mode...
                        start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
                        '''
                    } else {
                        echo "Starting Production Environment..."
                        bat '''
                        REM Stop any previous Angular process if running
                        if exist .pidfile (
                          set /p PID=<.pidfile
                          taskkill /F /PID %PID%
                          del .pidfile
                          echo Stopped previous Angular server.
                        )

                        echo Building the Angular project...
                        ng build --configuration=production
                        if %ERRORLEVEL% NEQ 0 (
                          echo Build failed!
                          exit /b %ERRORLEVEL%
                        )
                        echo Build succeeded.

                        echo Starting backend server in production mode...
                        start /B cmd /c "cd backend && npm run start"

                        echo Starting Angular frontend in production mode...
                        cd frontend
                        start /B cmd /c "npx serve -s dist"

                        echo Angular app is running in production mode.
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Servers are running! Frontend and Backend are live.'
        }
        failure {
            echo 'Build failed. Check logs for details.'
        }
    }
}




// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "22"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     for /f "tokens=*" %%v in ('nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
//                     if not defined FOUND_NODE (
//                         echo Node.js %NODE_VERSION% not found. Installing...
//                         nvm install %NODE_VERSION%
//                     ) else (
//                         echo Node.js %NODE_VERSION% already installed. Skipping installation.
//                     )
//                     nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/Integrated-Chat-App.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Installing frontend dependencies...
//                     npm ci

//                     cd backend
//                     echo Installing backend dependencies...
//                     npm ci
//                     '''
//                 }
//             }
//         }

//         stage('Install Angular CLI') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Angular CLI...
//                     npx ng version >nul 2>nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli
//                     ) else (
//                         echo Angular CLI is already installed.
//                     )
//                     '''
//                 }
//             }
//         }

//         stage('Build and Deploy') {
//             steps {
//                 script {
//                     if (params.Type_of_Build == 'Test') {
//                         echo "Starting Test Environment..."
//                         bat '''
//                         echo Starting backend server...
//                         cd backend
//                         start "Backend" cmd /c "npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         cd ..
//                         start "Frontend" cmd /c "npx ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo "Starting Production Environment..."
//                         bat '''
//                         echo Killing any previous Angular process...
//                         taskkill /F /IM "node.exe" /T >nul 2>nul

//                         echo Building the Angular project...
//                         npx ng build --configuration=production
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Build failed!
//                             exit /b %ERRORLEVEL%
//                         )
//                         echo Build succeeded.

//                         echo Starting backend server in production mode...
//                         start "Backend" cmd /c "cd backend && npm run start"

//                         echo Starting Angular frontend in production mode...
//                         start "Frontend" cmd /c "npx serve -s dist"
//                         '''
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Servers are running! Frontend and Backend are live.'
//         }
//         failure {
//             echo 'Build failed. Check logs for details.'
//         }
//     }
// }

