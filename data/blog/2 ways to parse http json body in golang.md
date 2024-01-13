
# Samples
---

## 1.  json.NewDecoder

```go
func handleUser(w http.ResponseWriter, r *http.Request) {
    var user User
    err := json.NewDecoder(r.Body).Decode(&user)
}
```

## 2.  json.Unmarshal
```go
func handleUser(w http.ResponseWriter, r *http.Request) {
    var user User
    p, _ := io.ReadAll(r.Body)
    err := json.Unmarshal(p, &user)
}
```

# Differences
---

- `json.NewDecoder()`将请求body读取为JSON token流，并用它来填充目标结构体。这种方式允许更高效地解析大型JSON负载，因为解码器只需要读取所需的JSON，以填充目标结构体。
- `json.Unmarshal()`将整个请求body读取为一个字节切片，并一次性解析JSON以填充目标结构体。这可能对于大型负载不太有效，因为它需要一次性将整个负载加载到内存中

在大多数情况下，这两种方法之间的性能差异通常是可以忽略不计的，因为大多数http请求body不会太大。使用哪种方法通常取决于个人喜好或应用程序的特定要求

另外 `json.NewDecoder()`在解析完后，剩下的body会保留下来，不会全部读完