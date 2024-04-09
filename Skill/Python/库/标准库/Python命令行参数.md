##### Python命令行参数
- 希望在命令行中传递参数时，通过名称来指定参数的值，而不仅仅通过位置来传递
- 这是一段示例，可保存为`test.py`，在终端通过下面脚本调用
- `python test.py --input input.txt --output output.txt --verbose`
- 创建解析器 -> 添加参数 -> 解析参数
```python
import argparse

def main():
    parser = argparse.ArgumentParser(description="Example script with named arguments.")

    parser.add_argument('--input', required=True, help='Input file name')
    parser.add_argument('--output', required=True, help='Output file name')
    parser.add_argument('--verbose', action='store_true', help='Enable verbose mode')

    args = parser.parse_args()

    print("Input file:", args.input)
    print("Output file:", args.output)
    if args.verbose:
        print("Verbose mode is enabled")

if __name__ == '__main__':
    main()
```
