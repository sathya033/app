


// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "18"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     set FOUND_NODE=
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
//                 git url: 'https://github.com/sathya033/app.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking frontend dependencies...
//                     if exist package.json (
//                         echo package.json found. Checking dependencies...
//                         npm install --dry-run > nul 2>&1
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Dependencies outdated or missing. Running npm ci...
//                             npm ci
//                         ) else (
//                             echo All dependencies are installed.
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Checking backend dependencies...
//                     if exist backend (
//                         cd backend
//                         if exist package.json (
//                             npm install --dry-run > nul 2>&1
//                             if %ERRORLEVEL% NEQ 0 (
//                                 echo Installing missing dependencies for backend...
//                                 npm ci
//                             ) else (
//                                 echo Backend dependencies are already installed.
//                             )
//                         ) else (
//                             echo Backend package.json not found! Exiting...
//                             exit /b 1
//                         )
//                     ) else (
//                         echo Backend directory not found! Exiting...
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
//                         npm install -g @angular/cli@14
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
//                         start /B cmd /c "cd backend && npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo "Starting Production Environment..."
//                         bat '''
//                         REM Stop any previous Angular process if running
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
//                         echo Build succeeded.

//                         echo Starting backend server in production mode...
//                         start /B cmd /c "cd backend && npm run start"

//                         echo Starting Angular frontend in production mode...
//                         cd frontend
//                         start /B cmd /c "npx serve -s dist"

//                         echo Angular app is running in production mode.
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




// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "18"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     set FOUND_NODE=
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
//                 git url: 'https://github.com/sathya033/app.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking frontend dependencies...
//                     if exist package.json (
//                         echo package.json found. Running npm install...
//                         npm ci
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Error installing frontend dependencies!
//                             exit /b 1
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Checking backend dependencies...
//                     if exist backend (
//                         cd backend
//                         if exist package.json (
//                             echo package.json found. Running npm install...
//                             npm ci
//                             if %ERRORLEVEL% NEQ 0 (
//                                 echo Error installing backend dependencies!
//                                 exit /b 1
//                             )
//                         ) else (
//                             echo Backend package.json not found! Exiting...
//                             exit /b 1
//                         )
//                     ) else (
//                         echo Backend directory not found! Exiting...
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
//                         npm install -g @angular/cli@14
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Failed to install Angular CLI!
//                             exit /b 1
//                         )
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
//                         start /B cmd /c "cd backend && npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo "Starting Production Environment..."
//                         bat '''
//                         REM Stop any previous Angular process if running
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
//                         echo Build succeeded.

//                         echo Starting backend server in production mode...
//                         start /B cmd /c "cd backend && npm run start"

//                         echo Starting Angular frontend in production mode...
//                         cd frontend
//                         start /B cmd /c "npx serve -s dist"

//                         echo Angular app is running in production mode.
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


// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "18"
//     }

//     stages {
//         stage('Setup Node.js via NVM') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking Node.js version...
//                     set FOUND_NODE=
//                     for /f "tokens=*" %%v in ('call nvm list ^| findstr /C:"%NODE_VERSION%"') do set FOUND_NODE=%%v
//                     if not defined FOUND_NODE (
//                         echo Node.js %NODE_VERSION% not found. Installing...
//                         call nvm install %NODE_VERSION%
//                     ) else (
//                         echo Node.js %NODE_VERSION% already installed. Skipping installation.
//                     )
//                     call nvm use %NODE_VERSION%
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/app.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking frontend dependencies...
//                     if exist package.json (
//                         echo package.json found. Running npm install...
//                         npm ci --legacy-peer-deps
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Error installing frontend dependencies!
//                             exit /b 1
//                         )
//                     ) else (
//                         echo package.json not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Checking backend dependencies...
//                     if exist backend (
//                         cd backend
//                         if exist package.json (
//                             echo package.json found. Running npm install...
//                             npm ci --legacy-peer-deps
//                             if %ERRORLEVEL% NEQ 0 (
//                                 echo Error installing backend dependencies!
//                                 exit /b 1
//                             )
//                         ) else (
//                             echo Backend package.json not found! Exiting...
//                             exit /b 1
//                         )
//                     ) else (
//                         echo Backend directory not found! Exiting...
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
//                     npm list -g @angular/cli | findstr @angular/cli >nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli@14
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Failed to install Angular CLI!
//                             exit /b 1
//                         )
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
//                         start /B cmd /c "cd backend && npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         start /B cmd /c "ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo "Starting Production Environment..."
//                         bat '''
//                         REM Stop any previous Angular process if running
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
//                         echo Build succeeded.

//                         echo Starting backend server in production mode...
//                         start /B cmd /c "cd backend && npm run start"

//                         echo Starting Angular frontend in production mode...
//                         cd frontend
//                         start /B cmd /c "npx serve -s dist"

//                         echo Angular app is running in production mode.
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


// pipeline {
//     agent any

//     parameters {
//         choice(name: 'Type_of_Build', choices: ['Test', 'Prod'], description: 'Choose the build type')
//     }

//     environment {
//         NODE_VERSION = "18"
//         NVM_HOME = "C:\\Users\\sathiyamoorthim\\AppData\\Local\\nvm"
//         NVM_SYMLINK = "C:\\nvm4w\\nodejs"
//         PATH = "${env.NVM_HOME};${env.NVM_SYMLINK};${env.PATH}"
//     }

//     stages {
//         stage('Check NVM and Node.js') {
//             steps {
//                 script {
//                     bat '''
//                     echo Checking NVM installation...
//                     where nvm || (echo NVM not found! Exiting... & exit /b 1)
                    
//                     echo Checking Node.js version...
//                     nvm list
                    
//                     echo Installing and using Node.js %NODE_VERSION%...
//                     nvm install %NODE_VERSION%
//                     nvm use %NODE_VERSION%
                    
//                     echo Node.js and npm versions:
//                     node -v
//                     npm -v
//                     '''
//                 }
//             }
//         }

//         stage('Checkout Code') {
//             steps {
//                 git url: 'https://github.com/sathya033/app.git', branch: 'master'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 script {
//                     bat '''
//                     echo Installing frontend dependencies...
//                     if exist frontend (
//                         cd frontend
//                         if exist package.json (
//                             echo package.json found. Running npm install...
//                             npm install --legacy-peer-deps
//                             if %ERRORLEVEL% NEQ 0 (
//                                 echo Error installing frontend dependencies!
//                                 exit /b 1
//                             )
//                         ) else (
//                             echo package.json not found! Exiting...
//                             exit /b 1
//                         )
//                         cd ..
//                     ) else (
//                         echo Frontend directory not found! Exiting...
//                         exit /b 1
//                     )

//                     echo Installing backend dependencies...
//                     if exist backend (
//                         cd backend
//                         if exist package.json (
//                             echo package.json found. Running npm install...
//                             npm install --legacy-peer-deps
//                             if %ERRORLEVEL% NEQ 0 (
//                                 echo Error installing backend dependencies!
//                                 exit /b 1
//                             )
//                         ) else (
//                             echo Backend package.json not found! Exiting...
//                             exit /b 1
//                         )
//                     ) else (
//                         echo Backend directory not found! Exiting...
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
//                     npm list -g @angular/cli | findstr @angular/cli >nul
//                     if %ERRORLEVEL% NEQ 0 (
//                         echo Angular CLI not found. Installing...
//                         npm install -g @angular/cli@14
//                         if %ERRORLEVEL% NEQ 0 (
//                             echo Failed to install Angular CLI!
//                             exit /b 1
//                         )
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
//                         start /B cmd /c "cd backend && npm run dev"

//                         echo Starting Angular frontend in development mode...
//                         start /B cmd /c "cd frontend && ng serve --host 0.0.0.0 --port 4200 --live-reload true"
//                         '''
//                     } else {
//                         echo "Starting Production Environment..."
//                         bat '''
//                         REM Stop any previous Angular process if running
//                         if exist .pidfile (
//                           set /p PID=<.pidfile
//                           taskkill /F /PID %PID%
//                           del .pidfile
//                           echo Stopped previous Angular server.
//                         )

//                         echo Building the Angular project...
//                         cd frontend
//                         ng build --configuration=production
//                         if %ERRORLEVEL% NEQ 0 (
//                           echo Build failed!
//                           exit /b %ERRORLEVEL%
//                         )
//                         cd ..

//                         echo Starting backend server in production mode...
//                         start /B cmd /c "cd backend && npm run start"

//                         echo Starting Angular frontend in production mode...
//                         start /B cmd /c "npx serve -s frontend/dist"

//                         echo Angular app is running in production mode.
//                         '''
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo '✅ Build and deployment successful! Servers are running.'
//         }
//         failure {
//             echo '❌ Build failed. Check logs for details.'
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
        NVM_HOME = "C:\\Users\\sathiyamoorthim\\AppData\\Local\\nvm"
        NVM_SYMLINK = "C:\\nvm4w\\nodejs"
        PATH = "${env.NVM_HOME};${env.NVM_SYMLINK};${env.PATH}"
    }

    stages {
        stage('Check NVM and Node.js') {
            steps {
                script {
                    bat '''
                    echo Checking NVM installation...
                    where nvm || (echo NVM not found! Exiting... & exit /b 1)

                    echo Checking Node.js version...
                    nvm list

                    echo Installing and using Node.js %NODE_VERSION%...
                    nvm install %NODE_VERSION%
                    nvm use %NODE_VERSION%

                    echo Node.js and npm versions:
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
                    echo Installing frontend dependencies...
                    if exist package.json (
                        echo package.json found. Running npm install...
                        npm install --legacy-peer-deps
                        if %ERRORLEVEL% NEQ 0 (
                            echo Error installing dependencies!
                            exit /b 1
                        )
                    ) else (
                        echo package.json not found! Exiting...
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
                    npm list -g @angular/cli | findstr @angular/cli >nul
                    if %ERRORLEVEL% NEQ 0 (
                        echo Angular CLI not found. Installing...
                        npm install -g @angular/cli@14
                        if %ERRORLEVEL% NEQ 0 (
                            echo Failed to install Angular CLI!
                            exit /b 1
                        )
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

                        echo Starting Angular frontend in production mode...
                        start /B cmd /c "npx serve -s dist/app"

                        echo Angular app is running in production mode.
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful! Servers are running.'
        }
        failure {
            echo '❌ Build failed. Check logs for details.'
        }
    }
}
