##### argparse 库
- [[终端运行Python脚本]]
- [[Python命令行参数]]
- [[class argparse.ArgumentParser]] 解析器类: 创建解析器
- [[ArgumentParser.add_argument()]] 实例方法: 添加参数
- [[ArgumentParser.parse_args()]] 实例方法: 解析参数
```python
import argparse
# 保存test.py文件通过命令行调用传参
# python test.py input.txt output.txt --mode read --verbose --debug --num 10000 --uppercase

def main():
    parser = argparse.ArgumentParser(description='A comprehensive argparse example')

    # 位置参数
    parser.add_argument('input_file', help='Input file path')
    parser.add_argument('output_file', help='Output file path')

    # 必选参数
    parser.add_argument('--mode', required=True, choices=['read', 'write'], help='Choose operation mode')

    # 可选参数
    parser.add_argument('--verbose', '-v', action='store_true', help='Enable verbose mode')
    parser.add_argument('--debug', action='store_true', help='Enable debug mode')
    parser.add_argument('--num', type=int, default=5, help='Number of iterations')

    # 标志参数
    parser.add_argument('--uppercase', action='store_true', help='Convert to uppercase')

    args = parser.parse_args()

    if args.verbose:
        print("Verbose mode enabled")

    if args.debug:
        print("Debug mode enabled")

    print(f"Input file: {args.input_file}")
    print(f"Output file: {args.output_file}")
    print(f"Mode: {args.mode}")
    print(f"Number of iterations: {args.num}")

    if args.uppercase:
        print("Uppercase conversion enabled")

    if args.encrypt:
        print("Encryption enabled")
    elif args.decrypt:
        print("Decryption enabled")

if __name__ == '__main__':
    main()

```


