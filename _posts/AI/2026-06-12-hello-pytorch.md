---
layout: post
title: "Hello PyTorch"
description: >
  딥러닝 프레임워크 PyTorch의 핵심 개념과 기본 사용법 개요
sitemap: true
categories: ai
tags: [pytorch, deep-learning, python]
---

# Hello PyTorch

PyTorch는 Meta(Facebook AI Research)가 개발한 오픈소스 딥러닝 프레임워크. Python 친화적 설계와 동적 계산 그래프(Dynamic Computation Graph)로 연구 및 프로덕션 모두에서 널리 사용된다.

---

## PyTorch vs TensorFlow

| | PyTorch | TensorFlow |
|---|---|---|
| 계산 그래프 | 동적 (실행 시 구성) | 정적 (사전 정의) |
| 디버깅 | Python 디버거 그대로 사용 | 별도 도구 필요 |
| 주요 사용처 | 연구 | 연구 + 프로덕션 |
| 생태계 | HuggingFace, torchvision | TFX, Keras |

---

## 핵심 개념

### Tensor
PyTorch의 기본 데이터 구조. NumPy ndarray와 유사하지만 GPU 연산 지원.

```python
import torch

x = torch.tensor([[1.0, 2.0], [3.0, 4.0]])
print(x.shape)   # torch.Size([2, 2])
print(x.dtype)   # torch.float32

# GPU로 이동
if torch.cuda.is_available():
    x = x.cuda()
```

### Autograd
자동 미분(Automatic Differentiation) 엔진. `requires_grad=True`로 연산 추적 활성화.

```python
x = torch.tensor(3.0, requires_grad=True)
y = x ** 2 + 2 * x + 1  # y = x^2 + 2x + 1

y.backward()          # dy/dx 계산
print(x.grad)         # tensor(8.) → 2x+2 = 2*3+2 = 8
```

### nn.Module
모델 정의의 기본 단위. 모든 커스텀 모델은 `nn.Module`을 상속.

```python
import torch.nn as nn

class SimpleNet(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(784, 256)
        self.fc2 = nn.Linear(256, 10)
        self.relu = nn.ReLU()

    def forward(self, x):
        x = self.relu(self.fc1(x))
        return self.fc2(x)

model = SimpleNet()
```

### Training Loop

```python
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
criterion = nn.CrossEntropyLoss()

for epoch in range(10):
    for inputs, labels in dataloader:
        optimizer.zero_grad()        # 그래디언트 초기화
        outputs = model(inputs)      # forward
        loss = criterion(outputs, labels)
        loss.backward()              # backward
        optimizer.step()             # 가중치 업데이트
```

---

## 주요 모듈

| 모듈 | 용도 |
|---|---|
| `torch.nn` | 레이어, 손실함수, 활성화함수 |
| `torch.optim` | SGD, Adam 등 최적화 알고리즘 |
| `torch.utils.data` | Dataset, DataLoader |
| `torchvision` | 이미지 데이터셋, 변환, pretrained 모델 |
| `torchaudio` | 오디오 처리 |
| `torchtext` | 텍스트 처리 |

---

## 설치

```bash
# CPU only
pip install torch torchvision

# CUDA 11.8
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118

# CUDA 12.1
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
```

---

*Created by Claude Sonnet 4.6*
