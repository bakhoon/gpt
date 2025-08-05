# GPT Project

이 프로젝트는 Python 3.11.6을 사용하여 개발되었습니다.

## 환경 설정

### 1. Python 버전 관리 (pyenv-win)

이 프로젝트는 Python 3.11.6을 사용합니다. pyenv-win을 통해 Python 버전을 관리할 수 있습니다.

#### pyenv-win 설치

```powershell
# pyenv-win 설치
git clone https://github.com/pyenv-win/pyenv-win.git $env:USERPROFILE\.pyenv

# 환경 변수 설정
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_ROOT',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_HOME',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")

# PATH에 pyenv 추가
$currentPath = [System.Environment]::GetEnvironmentVariable('PATH', 'User')
$newPath = "$env:USERPROFILE\.pyenv\pyenv-win\bin;$env:USERPROFILE\.pyenv\pyenv-win\shims;$currentPath"
[System.Environment]::SetEnvironmentVariable('PATH', $newPath, 'User')
```

#### Python 3.11.6 설치 및 설정

```powershell
# Python 3.11.6 설치
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" install 3.11.6

# 전역 기본값으로 설정
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" global 3.11.6

# 설치된 버전 확인
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" versions

# Python 버전 확인
python --version
```

### 2. 가상환경 설정

#### 가상환경 생성

```powershell
# 가상환경 생성
python -m venv env
```

#### 가상환경 활성화

**PowerShell에서:**
```powershell
.\env\Scripts\Activate.ps1
```

**Command Prompt에서:**
```cmd
.\env\Scripts\activate.bat
```

가상환경이 활성화되면 터미널에 `(env)`가 표시됩니다.

#### 가상환경 비활성화

```powershell
deactivate
```

### 3. 패키지 관리

#### requirements.txt가 있는 경우:
```powershell
# 패키지 설치
pip install -r requirements.txt

# 패키지 목록 저장
pip freeze > requirements.txt
```

## 프로젝트 구조

```
gpt/
├── README.md
├── .gitignore
├── env/              # 가상환경 (git에서 제외됨)
└── ...               # 프로젝트 파일들
```

## 유용한 pyenv 명령어

```powershell
# 설치 가능한 Python 버전 보기
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" install --list

# 설치된 버전 보기
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" versions

# 특정 버전 설치
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" install <version>

# 전역 Python 버전 변경
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" global <version>

# 로컬 Python 버전 설정 (현재 폴더에서만)
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" local <version>

# shims 새로고침
& "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" rehash
```

## 트러블슈팅

### Python 버전이 변경되지 않는 경우

1. **PowerShell 재시작**: 새로운 PowerShell 세션을 시작합니다.

2. **PATH 수동 설정**:
   ```powershell
   $env:PATH = "$env:USERPROFILE\.pyenv\pyenv-win\bin;$env:USERPROFILE\.pyenv\pyenv-win\shims;" + $env:PATH
   ```

3. **shims 새로고침**:
   ```powershell
   & "$env:USERPROFILE\.pyenv\pyenv-win\bin\pyenv.bat" rehash
   ```

### 가상환경 활성화 오류

1. **PowerShell 실행 정책 변경**:
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

2. **가상환경 재생성**:
   ```powershell
   python -m venv env --clear
   ```

## 개발 환경

- **Python**: 3.11.6
- **OS**: Windows
- **Shell**: PowerShell
- **Python 관리**: pyenv-win