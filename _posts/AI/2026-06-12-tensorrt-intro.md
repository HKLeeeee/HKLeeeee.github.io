---
layout: post
title: "TensorRT 개론"
description: >
  NVIDIA TensorRT의 핵심 개념, 최적화 기법, PyTorch 모델 변환 워크플로우
sitemap: true
categories: ai
tags: [tensorrt, nvidia, inference, optimization, deep-learning]
---

# TensorRT 개론

TensorRT는 NVIDIA가 제공하는 딥러닝 추론(Inference) 최적화 SDK. 학습된 모델을 GPU에서 최대한 빠르게 실행하기 위한 프로덕션 배포 도구.

---

## TensorRT가 필요한 이유

학습(Training)과 추론(Inference)의 요구사항은 다르다.

| | 학습 | 추론 |
|---|---|---|
| 목표 | 정확도 최대화 | 지연시간(Latency) 최소화 |
| 배치 크기 | 크게 (메모리 허용 내) | 작게 (실시간 처리) |
| 정밀도 | FP32 | FP16, INT8 가능 |
| 그래디언트 | 필요 | 불필요 |

TensorRT는 추론에 특화된 최적화를 적용해 **같은 GPU에서 수배~수십배 빠른 성능**을 낸다.

---

## 핵심 최적화 기법

### 1. Layer Fusion (레이어 융합)
연속된 연산을 하나의 커널로 합쳐 메모리 왕복 감소.

```
# 최적화 전
Conv2D → BatchNorm → ReLU   (3번 GPU 메모리 접근)

# TensorRT 최적화 후
CBR Fused Kernel             (1번 GPU 메모리 접근)
```

### 2. Precision Calibration (정밀도 변환)
FP32 → FP16 또는 INT8 변환으로 처리량 2~4배 향상.

- **FP16**: 정확도 손실 거의 없음, Tensor Core 활용
- **INT8**: 캘리브레이션 데이터셋 필요, 최대 4x 속도 향상

### 3. Kernel Auto-Tuning
하드웨어별 최적 CUDA 커널 자동 선택.

### 4. Dynamic Shape
입력 크기가 가변적인 경우 지원 (TensorRT 6+).

---

## PyTorch → TensorRT 변환 워크플로우

```
PyTorch Model (.pth)
        ↓ torch.onnx.export()
ONNX Model (.onnx)
        ↓ trtexec 또는 Python API
TensorRT Engine (.engine)
        ↓ Runtime Inference
결과
```

### Step 1: ONNX 변환

```python
import torch
import torch.onnx

model = MyModel()
model.load_state_dict(torch.load("model.pth"))
model.eval()

dummy_input = torch.randn(1, 3, 224, 224)
torch.onnx.export(
    model,
    dummy_input,
    "model.onnx",
    opset_version=17,
    input_names=["input"],
    output_names=["output"],
    dynamic_axes={"input": {0: "batch_size"}}
)
```

### Step 2: TensorRT 엔진 빌드

```python
import tensorrt as trt

TRT_LOGGER = trt.Logger(trt.Logger.WARNING)

def build_engine(onnx_path, fp16=True):
    builder = trt.Builder(TRT_LOGGER)
    network = builder.create_network(
        1 << int(trt.NetworkDefinitionCreationFlag.EXPLICIT_BATCH)
    )
    parser = trt.OnnxParser(network, TRT_LOGGER)

    with open(onnx_path, "rb") as f:
        parser.parse(f.read())

    config = builder.create_builder_config()
    config.set_memory_pool_limit(trt.MemoryPoolType.WORKSPACE, 1 << 30)  # 1GB

    if fp16 and builder.platform_has_fast_fp16:
        config.set_flag(trt.BuilderFlag.FP16)

    return builder.build_serialized_network(network, config)
```

### Step 3: 추론

```python
import numpy as np

# 엔진 로드
runtime = trt.Runtime(TRT_LOGGER)
with open("model.engine", "rb") as f:
    engine = runtime.deserialize_cuda_engine(f.read())

context = engine.create_execution_context()

# 입력/출력 버퍼 할당 후 추론 실행
# (실제 구현은 pycuda 또는 CUDA Python 사용)
```

---

## torch2trt / Torch-TensorRT

직접 ONNX 변환 없이 PyTorch 모델을 바로 TensorRT로 변환하는 래퍼 라이브러리.

```python
from torch2trt import torch2trt

model_trt = torch2trt(model, [dummy_input], fp16_mode=True)

# torch 모델과 동일 인터페이스로 사용
output = model_trt(input_tensor)
```

---

## 지원 환경

- NVIDIA GPU (Turing 이상에서 INT8 Tensor Core 지원)
- CUDA 11.x / 12.x
- Python: `pip install tensorrt`
- Docker: `nvcr.io/nvidia/tensorrt` 이미지 권장

---

*Created by Claude Sonnet 4.6*
