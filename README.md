# Alira Core Actions

## 개요
- PR/Push 이벤트 시 AI 분석 에이전트를 실행하고 결과를 GitHub Issue로 생성하는 Composite Action  
- Self-hosted 러너 전용(Hosted runner 지원 예정)
- 버전: v1.0.0

## 입력 (inputs)
| 이름                 | 필수 여부 | 설명                                                         | 기본값                   |
| -------------------- | --------- | ------------------------------------------------------------ | ------------------------ |
| `github_token`       | ✓         | GitHub API 호출에 사용할 토큰                                | –                        |
| `system_prompt_path` | ×         | 시스템 프롬프트 파일 경로(`.github/prompts/system.txt` 권장) |                          |
| `user_prompt_path`   | ×         | 사용자 프롬프트 파일 경로(`.github/prompts/user.txt` 권장)   |                          |
| `project_name`       | ×         | 분석 대상 프로젝트 디렉터리 이름                            | `pr_project`             |
| `cleanup`            | ×         | 실행 후 임시 디렉터리 삭제 여부 (`true`/`false`)            | `false`                  |

## 출력 (outputs)
- 새로 생성된 GitHub Issue

## 사용 예시
```yaml
name: CI
on:
  pull_request:
jobs:
  code-review:
    runs-on: self-hosted
    steps:
      - name: AI 분석 실행
        uses: SuresoftTechnologies/alira-ai-action@v1.0.0
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          cleanup: false
          system_prompt_path: .github/prompts/system.txt
          user_prompt_path: .github/prompts/user.txt
