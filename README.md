# YT_3D_UnityMovement
**Cách thứ 1**: Sử dụng transform.position

Transform.position: Việc trực tiếp thao tác trên thuộc tính vị trí của thành phần Transform cho phép bạn đặt vị trí chính xác của đối tượng trong không gian.

```csharp
Vector3 newPosition = transform.position + new Vector3(0f, yOffset, 0f);
transform.position = newPosition;
```

