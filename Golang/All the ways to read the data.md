https://medium.com/@andreiboar/fundamentals-of-i-o-in-go-part-2-e7bb68cd5608

In Go, there are several ways to read and parse incoming messages, depending on the protocol, the format of the message, and the communication medium. Here's a comprehensive guide to understanding all the ways to read incoming messages:

---

### **1. Using `net.Conn`**

When dealing with raw TCP connections (`net.Conn`), you can read messages in various ways.

#### **1.1. Using `conn.Read`**

- Reads raw bytes into a buffer.
- Suitable for simple and small messages.

```go
buff := make([]byte, 1024)
n, err := conn.Read(buff)
if err != nil {
    fmt.Println("Error reading:", err)
    return
}
fmt.Println("Message received:", string(buff[:n]))
```

---

#### **1.2. Using `io.ReadFull`**

- Ensures the buffer is completely filled before returning.
- Useful when the message size is known in advance.

```go
buff := make([]byte, messageSize)
_, err := io.ReadFull(conn, buff)
if err != nil {
    fmt.Println("Error reading full message:", err)
    return
}
fmt.Println("Message received:", string(buff))
```

---

#### **1.3. Using `bufio.Reader`**

- Provides buffered reading for better performance.
- Use methods like `ReadBytes` or `ReadString` for delimited data.

```go
reader := bufio.NewReader(conn)
line, err := reader.ReadString('\n') // Read until newline
if err != nil {
    fmt.Println("Error reading line:", err)
    return
}
fmt.Println("Message received:", line)
```

---

#### **1.4. Using `binary.Read`**

- Decodes binary data directly into Go structs.
- Suitable for structured data with fixed-length fields.

```go
type Message struct {
    Field1 int32
    Field2 int16
}
var msg Message
err := binary.Read(conn, binary.BigEndian, &msg)
if err != nil {
    fmt.Println("Error reading binary message:", err)
    return
}
fmt.Printf("Decoded message: %+v\n", msg)
```

---

### **2. Using `io.Reader` Interface**

Go's `io.Reader` interface is implemented by many types (`net.Conn`, `os.File`, etc.), allowing flexibility in reading data.

#### **2.1. Reading All Data**

Use `io.ReadAll` to read the entire stream until EOF. Useful for small payloads.

```go
data, err := io.ReadAll(conn)
if err != nil {
    fmt.Println("Error reading all data:", err)
    return
}
fmt.Println("Message received:", string(data))
```

---

#### **2.2. Using `io.Reader.Read`**

- Reads data in chunks into a buffer.
- Basic way to process streams incrementally.

```go
buff := make([]byte, 1024)
for {
    n, err := conn.Read(buff)
    if err == io.EOF {
        break // End of data
    }
    if err != nil {
        fmt.Println("Error reading:", err)
        return
    }
    fmt.Print(string(buff[:n]))
}
```

---

### **3. Handling Length-Prefixed Messages**

When messages have a length prefix, first read the length, then read the payload.

```go
var messageLength int32
err := binary.Read(conn, binary.BigEndian, &messageLength)
if err != nil {
    fmt.Println("Error reading message length:", err)
    return
}

buff := make([]byte, messageLength)
_, err = io.ReadFull(conn, buff)
if err != nil {
    fmt.Println("Error reading message:", err)
    return
}
fmt.Println("Message received:", string(buff))
```

---

### **4. Reading Delimited Messages**

If messages are delimited (e.g., newline or special character):

#### **4.1. Line-Delimited Messages**

Use `bufio.Scanner` for line-delimited messages.

```go
scanner := bufio.NewScanner(conn)
for scanner.Scan() {
    fmt.Println("Message received:", scanner.Text())
}
if err := scanner.Err(); err != nil {
    fmt.Println("Error reading lines:", err)
}
```

#### **4.2. Custom Delimiters**

Use `bufio.Reader` and `ReadSlice` with a custom delimiter.

```go
reader := bufio.NewReader(conn)
for {
    line, err := reader.ReadSlice('|') // Custom delimiter
    if err != nil {
        fmt.Println("Error reading slice:", err)
        break
    }
    fmt.Println("Message received:", string(line))
}
```

---

### **5. Parsing JSON Messages**

For JSON-encoded messages, decode into Go structs.

```go
decoder := json.NewDecoder(conn)
var message map[string]interface{}
err := decoder.Decode(&message)
if err != nil {
    fmt.Println("Error decoding JSON:", err)
    return
}
fmt.Printf("Decoded JSON message: %+v\n", message)
```

---

### **6. Parsing Protocol Buffers (Protobuf)**

For Protobuf-encoded messages, use the `proto` package.

```go
import "google.golang.org/protobuf/proto"

// Assuming `MyProtoMessage` is a Protobuf message type.
var msg MyProtoMessage
buff := make([]byte, messageSize)
_, err := io.ReadFull(conn, buff)
if err != nil {
    fmt.Println("Error reading protobuf:", err)
    return
}
err = proto.Unmarshal(buff, &msg)
if err != nil {
    fmt.Println("Error unmarshaling protobuf:", err)
    return
}
fmt.Printf("Decoded Protobuf message: %+v\n", msg)
```

---

### **7. Reading HTTP Requests**

If you're handling HTTP traffic, use Go's `net/http` package.

```go
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
    body, err := io.ReadAll(r.Body)
    if err != nil {
        fmt.Println("Error reading HTTP body:", err)
        return
    }
    fmt.Println("HTTP Request Body:", string(body))
})
http.ListenAndServe(":8080", nil)
```

---

### **8. Advanced Streaming Protocols**

For advanced protocols like Kafka or WebSockets:

- Kafka: Use libraries like `segmentio/kafka-go`.
- WebSocket: Use libraries like `gorilla/websocket`.

---

### **Choosing the Right Approach**

- **Structured Data**: Use `binary.Read` or a specific decoding library (e.g., JSON, Protobuf).
- **Delimited Data**: Use `bufio.Scanner` or `bufio.Reader`.
- **Length-Prefixed Messages**: Read the length first, then the payload.
- **Streams**: Use chunked reading (`io.Reader`).
- **Protocol-Specific**: Use libraries for protocols like HTTP, Kafka, or WebSockets.

Let me know if you'd like examples tailored to your use case!