## FastAPI简介

FastAPI是一个现代的、高性能的Web框架，用于基于Python 3.7+标准库的API开发。它基于标准的Python类型提示，使用Pydantic进行数据验证和序列化，并使用Starlette作为Web框架基础，支持异步编程，使得它在性能上非常优越。

文档如下：[FastAPI官方文档](https://fastapi.tiangolo.com/zh/learn/)

### 1. FastAPI的核心特点

- **高性能**：FastAPI的性能接近NodeJS和Go，并且在大多数情况下，比Django和Flask等传统框架更快。
- **类型提示**：利用Python的类型提示，提供自动API文档生成，减少错误，提高开发速度。
- **自动文档**：自动生成OpenAPI和JSON Schema文档，方便开发者和用户使用API。
- **依赖注入**：内置强大的依赖注入系统，支持复杂的依赖管理。

### 2. 安装FastAPI

要安装FastAPI和Uvicorn（用于运行FastAPI应用的ASGI服务器），可以使用以下命令：

```bash
pip install fastapi uvicorn
```

### 3. 基本示例

下面是一个简单的FastAPI应用示例，展示了如何创建和运行一个基本的API。

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="127.0.0.1", port=8000)
```

### 4. 路由和请求处理

FastAPI支持RESTful风格的路由，并且能够处理各种HTTP方法（GET、POST、PUT、DELETE等）。可以使用装饰器定义路由，并指定路径参数和查询参数。

```python
@app.post("/items/")
def create_item(item: Item):
    return item

@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    return {"item_id": item_id, **item.dict()}

@app.delete("/items/{item_id}")
def delete_item(item_id: int):
    return {"item_id": item_id}
```

### 5. 数据验证和序列化

FastAPI使用Pydantic进行数据验证和序列化。你可以定义Pydantic模型来验证请求体的数据，并自动生成API文档。

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None
```

### 6. 异步支持

FastAPI内置异步支持，使得处理高并发请求变得更高效。可以使用async def定义异步路由处理函数。

```python
import asyncio

@app.get("/async")
async def async_read():
    await asyncio.sleep(1)
    return {"message": "This is an async endpoint"}
```

### 7. 中间件和依赖注入

FastAPI支持中间件和依赖注入，可以方便地进行请求拦截和依赖管理。

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.get("/depend")
def read_with_dependency(common: str = Depends(common_dependency)):
    return {"message": common}
```

### 8. 自动生成文档

FastAPI自动生成Swagger UI和ReDoc文档，方便查看和测试API。

- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

### 9. 部署

可以使用Uvicorn或其他ASGI服务器部署FastAPI应用。以下是一个简单的部署示例：

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

### 总结

FastAPI是一个强大且高效的Web框架，适用于构建现代API应用。其高性能、类型安全、自动文档生成等特点，使得它在开发速度和性能方面具有明显优势。希望这个简介能够帮助你了解FastAPI的基本概念和应用。