# 📦 `protos`

Этот репозиторий содержит `.proto`-описания gRPC-сервисов и автогенерируемый Go-код для микросервисов.

## 📁 Структура

```
.
├── proto/                  # Исходные .proto файлы
│   ├── auth/
│   │   └── auth.proto
│   └── permissions/
│       └── permissions.proto
├── gen/                    # Сгенерированные .pb.go файлы
│   └── go/
│       ├── auth/
│       │   ├── auth.pb.go
│       │   └── auth_grpc.pb.go
│       └── permissions/
│           ├── permissions.pb.go
│           └── permissions_grpc.pb.go
└── Taskfile.yml            # Команда для генерации кода
```

---

## 🧪 Использование

### Установка зависимостей

Убедись, что у тебя установлены:

- [`protoc`](https://grpc.io/docs/protoc-installation/)
- Плагины Go:
  ```bash
  go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
  go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
  ```

---

### Генерация кода

```bash
task gen
```

Или вручную:

```bash
protoc \
  --go_out=./gen/go --go_opt=paths=source_relative \
  --go-grpc_out=./gen/go --go-grpc_opt=paths=source_relative \
  proto/auth/auth.proto proto/permissions/permissions.proto
```

---

## 🚀 Использование в других сервисах

Добавь зависимость через Go modules:

```bash
go get github.com/rof1ch/protos@v0.1.0
```

Импортируй в коде:

```go
import "github.com/rof1ch/protos/gen/go/auth"
import "github.com/rof1ch/protos/gen/go/permissions"
```

---

## 🔄 Автоматическая генерация

См. [`.github/workflows/proto-generate.yml`](.github/workflows/proto-generate.yml) — код будет сгенерирован автоматически при изменении `.proto`.

---

## 📌 Рекомендации

- Используй `git tag v0.x.x` для управления версиями.
- Обновляй зависимости в микросервисах через `go get`.