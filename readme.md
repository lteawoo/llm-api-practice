# OpenAI API 주요 엔드포인트
## Chat Completions
* URL: /v1/chat/completions
* Chat GPT를 사용하는 것 처럼 프롬프트에서 텍스트를 생성하기 위한 API
* 코드, 수학 방정식, 구조화된 JSON 데이터, 사람이 쓴 것과 같은 산문 등을 생성 가능
```javascript
return await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer '
      },
      body: JSON.stringify({
        'model': 'gpt-4o-mini',
        'messages': [
          {
            'role': 'developer',
            'content': 'You are a helpful assistant.',
          },
          {
            'role': 'user',
            'content': 'let me know what is a gpt'
          }
        ]
      })
    })
```
## Fine-tuning
* URL: /v1/fine-tuning
* 사전 훈련 모델을 추가로 훈련시킴, 프롬프트에 여러 예제를 제공할 필요가 없으므로, 비용 절감과 대기 시간이 짧아짐
* 과정: 훈련 데이터 업로드 -> 모델 학습 -> 결과 평가 -> 평가에 따라 1단계로 다시 -> 파인 튜닝 모델 사용
```javascript
import OpenAI from "openai";

const openai = new OpenAI();

const fineTune = await openai.fineTuning.jobs.create({
  training_file: 'file-abc123',
  model: 'gpt-4o-mini-2024-07-18'
});
```
## Image
### Generations
* URL: /v1/images/generations
* 프롬프트로 이미지를 생성함
```javascript
return await fetch('https://api.openai.com/v1/images/generations', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer '
      },
      body: JSON.stringify({
        'model': 'dall-e-2',
        'prompt': "cat is playing nexon game",
        "n": 1,
        "size": "256x256"
      })
    })
```
![alt text](openai/image.png)
### Edit
* URL: /v1/images/edit
* 마스크를 사용하여 특정 영역을 대체하거나 편집, 확장할 수 있음
```javascript
const selectedFile = document.getElementById("input").files[0]
    const selectedFile2 = document.getElementById("input2").files[0]
    const formData = new FormData()
    formData.append('model', 'dall-e-2')
    formData.append('image', selectedFile)
    formData.append('mask', selectedFile2)
    formData.append('prompt', 'the dog is playing game')
    formData.append('n', 1)
    formData.append('size', '256x256')

    return await fetch('https://api.openai.com/v1/images/edits', {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer '
      },
      body: formData
    })
```
![alt text](openai/editimage.png)
### Variations
* URL: /v1/images/variations
* 입력 이미지를 변형 시킴
