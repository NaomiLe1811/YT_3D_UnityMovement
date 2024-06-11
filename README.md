# YT_3D_UnityMovement
**Cách thứ 1**: Sử dụng transform.position

Transform.position: Việc trực tiếp thao tác trên thuộc tính vị trí của thành phần Transform cho phép bạn đặt vị trí chính xác của đối tượng trong không gian.

```csharp
Vector3 newPosition = transform.position + new Vector3(0f, yOffset, 0f);
transform.position = newPosition;
```
**Cách thứ 2**: Sử dụng Transform.Translate

Bạn có thể sử dụng phương thức Translate của thành phần Transform để di chuyển một đối tượng theo các trục của nó 

Phương thức **`Translate()`** của thành phần **`Transform`** và thuộc tính **`transform.position`** đều được sử dụng để di chuyển đối tượng trong không gian 3D của Unity, nhưng chúng có một số điểm khác biệt:

1. **transform.position**:
    - **`transform.position`** là một thuộc tính của **`Transform`** đại diện cho vị trí của đối tượng trong không gian toạ độ toàn cầu (world space).
    - Khi bạn gán giá trị cho **`transform.position`**, bạn đang thiết lập vị trí tuyệt đối của đối tượng trong không gian toạ độ toàn cầu.
2. **Translate()**:
    - **`Translate()`** là một phương thức của **`Transform`** được sử dụng để di chuyển đối tượng theo hệ tọa độ cục bộ của chính nó.
    - Khi bạn sử dụng **`Translate()`**, bạn đang thay đổi vị trí của đối tượng dựa trên hướng và khoảng cách di chuyển cục bộ. Điều này có nghĩa là nó di chuyển đối tượng theo hướng trục cục bộ của nó thay vì theo hướng của toạ độ toàn cầu.

Ví dụ, nếu bạn muốn di chuyển một đối tượng 5 đơn vị về phía trước:

- Sử dụng **`transform.position`**, bạn sẽ phải tính toán vị trí mới của đối tượng trong không gian toạ độ toàn cầu.
- Sử dụng **`Translate()`**, bạn chỉ cần gọi phương thức này với tham số khoảng cách di chuyển và nó sẽ tự động di chuyển theo hướng cục bộ của đối tượng.

```csharp
transform.Translate(0f, yOffset, 0f);
```

**Cách thứ 3**: Sử dụng Rigidbody.velocity 
Nếu đối tượng của bạn có một thành phần Rigidbody đính kèm và bạn muốn di chuyển nó trong mô phỏng vật lý, bạn có thể thao tác trên thuộc tính vận tốc của nó.

Rigidbody rb = GetComponent<Rigidbody>();
rb.velocity = new Vector3(rb.velocity.x, desiredYVelocity, rb.velocity.z);

```csharp
Rigidbody rb = GetComponent<Rigidbody>();
```

- **`GetComponent<Rigidbody>()`**: Đây là một phương thức được sử dụng để truy xuất thành phần Rigidbody đính kèm với đối tượng hiện tại. Điều này giúp bạn có thể tương tác với các tính năng vật lý của đối tượng, như di chuyển hoặc tác động lực.

```csharp
csharpCopy code
rb.velocity = new Vector3(rb.velocity.x, desiredYVelocity, rb.velocity.z);
```

- **`rb.velocity`**: Đây là thuộc tính của thành phần Rigidbody, đại diện cho vận tốc hiện tại của đối tượng trong không gian ba chiều.
- **`new Vector3(rb.velocity.x, desiredYVelocity, rb.velocity.z)`**: Đây là cách bạn cập nhật vận tốc của đối tượng. Trong trường hợp này, bạn giữ nguyên vận tốc theo trục x và z (để đảm bảo đối tượng không thay đổi vận tốc trên các trục này), và chỉ thay đổi vận tốc theo trục y bằng giá trị **`desiredYVelocity`**.
- **`desiredYVelocity`**: Đây là giá trị vận tốc theo trục y mà bạn muốn đối tượng của mình di chuyển đến. Bằng cách thay đổi giá trị này, bạn có thể kiểm soát cách đối tượng của bạn di chuyển theo trục y.
  
** tại sao phương thức này cần dùng đến rigibody mà ko phải new vector3 như các phương thức khác?**

Phương thức **`GetComponent<Rigidbody>()`** cần được sử dụng vì thông thường, khi chúng ta muốn tương tác với tính năng vật lý của một đối tượng trong Unity, đó là thông qua thành phần **`Rigidbody`** được gắn kèm với đối tượng đó.

Khi chúng ta muốn thay đổi vận tốc của một đối tượng trong không gian ba chiều, chúng ta cần cập nhật thông qua thuộc tính **`velocity`** của thành phần **`Rigidbody`**. Điều này là do thành phần **`Rigidbody`** chịu trách nhiệm quản lý vận tốc và vật lý của đối tượng, bao gồm việc xử lý va chạm và áp dụng lực.

Trong khi đó, việc sử dụng **`new Vector3`** để tạo ra một vector mới là phù hợp khi chúng ta muốn tạo ra hoặc cập nhật vị trí, quay, hoặc kích thước của đối tượng. Tuy nhiên, khi muốn thay đổi vận tốc, điều này phải được thực hiện thông qua **`Rigidbody`** để đảm bảo tính đồng bộ và tính chính xác trong việc mô phỏng vật lý của đối tượng.

**Cách thứ 4**: Sử dụng Rigidbody.MovePosition
Tương tự như việc set position thuộc tính vị trí, nhưng được thiết kế cho các đối tượng trong mô phỏng vật lý. Điều này phù hợp hơn nếu bạn muốn di chuyển đối tượng với tương tác vật lý.
```csharp
Rigidbody rb = GetComponent<Rigidbody>();
Vector3 newPosition = rb.position + new Vector3(0f, yOffset, 0f);
rb.MovePosition(newPosition);
```

**Cách thứ 5**: Sử dụng Rigidbody.AddForce

Phương thức **`Rigidbody.AddForce`** được sử dụng để áp dụng một lực lên một đối tượng được xác định bởi thành phần **`Rigidbody`**. Thường được sử dụng để di chuyển đối tượng trong không gian 3D dưới tác động của lực vật lý, ví dụ như trọng lực hoặc lực đẩy.
```csharp
Rigidbody rb = GetComponent<Rigidbody>();
Vector3 force = new Vector3(0f, desiredYForce, 0f);
rb.AddForce(force, ForceMode.Force);
```

**Vậy ngoài những cách này ra thì còn cách nào nữa ko?**

Vẫn còn, ví dụ như bạn muốn  sử dụng phương thức**`transform.position`** để khiến đối tượng 3D di chuyển về phía trước trong Unity. Dưới đây là một số cách phổ biến:

1. **Sử dụng Vector3.forward hoặc Vector3.back**:
Bạn có thể sử dụng các hằng số Vector3 như **`Vector3.forward`** hoặc **`Vector3.back`** để di chuyển đối tượng theo hướng phía trước hoặc phía sau. Ví dụ:
    
    ```csharp
    csharpCopy code
    transform.position += transform.forward * speed * Time.deltaTime; // Di chuyển về phía trước
    ```
    
    Trong đó **`speed`** là tốc độ di chuyển mong muốn và **`Time.deltaTime`** là thời gian giữa các khung hình để làm cho di chuyển mượt mà hơn.
    
2. **Sử dụng Vector3.Normalize**:
Bạn có thể chuẩn hóa vector hướng của **`transform.forward`** để đảm bảo rằng di chuyển luôn có cùng tốc độ, bất kể hướng:
    
    ```csharp
    csharpCopy code
    transform.position += transform.forward.normalized * speed * Time.deltaTime;
    ```
    
3. **Sử dụng Quaternion**:
Bạn cũng có thể sử dụng Quaternion để xoay hướng của **`transform.position`** trước khi di chuyển:
    
    ```csharp
    csharpCopy code
    transform.position += (Quaternion.Euler(0, transform.eulerAngles.y, 0) * Vector3.forward) * speed * Time.deltaTime;
    ```
    
    Trong đó **`transform.eulerAngles.y`** là góc quay của đối tượng theo trục y.

   hoặc ví dụ sử dụng phương thức **Rigidbody.AddForce** để di chuyển đối tượng về phía trước, chúng ta có thể

1. **Sử dụng Vector3.forward**:

```csharp
csharpCopy code
rigidbody.AddForce(Vector3.forward * force);
```

Trong đó **`force`** là một số biểu thị cường độ của lực áp dụng lên nhân vật, và **`Vector3.forward`** đại diện cho hướng di chuyển về phía trước.

1. **Sử dụng transform.forward và force**:

```csharp
csharpCopy code
rigidbody.AddForce(transform.forward * force);
```

Tương tự như cách sử dụng **`Vector3.forward`**, nhưng sử dụng **`transform.forward`** để xác định hướng di chuyển.

1. **Sử dụng các phương thức ForceMode khác nhau**:

```csharp
csharpCopy code
rigidbody.AddForce(Vector3.forward * force, ForceMode.Impulse);
```

Bạn có thể sử dụng các **`ForceMode`** khác nhau như **`Force`**, **`Acceleration`**, **`Impulse`**, hoặc **`VelocityChange`** để kiểm soát cách lực được áp dụng lên đối tượng.

1. **Kết hợp với Input từ bàn phím hoặc thiết bị đầu vào**:

```csharp
csharpCopy code
float horizontalInput = Input.GetAxis("Horizontal");
float verticalInput = Input.GetAxis("Vertical");
Vector3 movement = new Vector3(horizontalInput, 0f, verticalInput);
rigidbody.AddForce(movement * force);
```


