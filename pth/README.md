## 모델 저장 및 불러오기
### 모델 저장
1. 전체를 저장하고 싶은 경우
```python
torch.save(mode, 'model.pth')
torch.model('model.pth')
```
2. 매개변수만 저장하고 싶은 경우(권장)
```python
torch.save(model.state_dict(), 'model.pth')
model.load_state_dict(torch.load('model.pth'))
```