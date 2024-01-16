## Auto NLP Action
Github-экшен для автоматической валидации задач по курсу NLP.

### Как пользоваться
1. Подключить Github Pages к своему репозиторию (Settings -> Pages). В разделе Build and deployment выбрать опцию `Deploy from a branch`.
2. Создать в репозитории папку .github, в ней также создать папку workflows.
3. Внутри .github/workflows создать скрипт run-notebook.yml и заполнить его следующим содержимым:
```yml
name: Check notebook
on: [pull_request]
jobs:
  run:
    permissions:
        pages: write
        id-token: write
        pull-requests: write
    environment:
        name: github-pages
        url: ${{ steps.deployment.outputs.page_url }}${{ github.head_ref }}
        
    runs-on: ubuntu-latest
    steps:
    - uses: danilkladnitsky/auto-nlp-action@v0.0.4-alpha
      with:
        home-task-filename: notebook.ipynb
``` 
4. Создать ветку с домашним заданием. При этом название ветки будет использовано в качестве URL, по которому будет доступен сформированный Jupyter-notebook.
5. Выполнить задание и запушить изменения в созданную ветку. Сформировать Pull Request.
6. Ждать проверки!
