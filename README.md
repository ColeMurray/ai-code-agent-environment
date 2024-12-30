# Jupyter Kernel Gateway for AI Agents

A secure Python code execution environment for AI agents using Jupyter Kernel Gateway. This project provides a containerized environment where AI agents can execute Python code safely with controlled access to system resources and modules.

## Features

- 🔒 Secure code execution environment
- 🐳 Docker containerization
- 🔍 Whitelist-based module access control
- 📊 Support for data science libraries (numpy, pandas, matplotlib, etc.)
- 🔌 Simple async client interface

## Quick Start

1. Clone the repository:
```bash
git clone https://github.com/yourusername/jupyter-kernel-gateway.git
cd jupyter-kernel-gateway
```

2. Build and run the Docker container:
```bash
docker build -t ai-kernel-gateway .
docker run -d -p 8888:8888 ai-kernel-gateway
```

3. Install the Python client dependencies:
```bash
pip install -r requirements.txt
```

4. Run the example agent:
```bash
python example_agent.py
```

## Project Structure

- `Dockerfile` - Container configuration for the kernel gateway
- `kernel_security.py` - Security layer for controlling module access
- `kernel_client.py` - Async Python client for interacting with the kernel
- `example_agent.py` - Example usage of the kernel client
- `requirements.txt` - Python client dependencies

## Security Features

The kernel gateway is configured with several security measures:

- Whitelisted Python modules:
  - Data science: numpy, pandas, matplotlib, seaborn, sklearn
  - Basic utilities: math, statistics, datetime
- Blocked modules: os, subprocess, sys, socket
- Restricted access to system resources
- No file system access from kernels

## Client Usage

```python
from kernel_client import KernelClient

async with KernelClient("http://localhost:8888") as client:
    result = await client.execute_code("""
        import numpy as np
        data = np.random.normal(0, 1, 1000)
        print(f"Mean: {np.mean(data):.2f}")
    """)
    print(result.output)
```

## API Reference

### KernelClient

The main client class for interacting with the kernel gateway.

Methods:
- `__init__(base_url: str)` - Initialize with gateway URL
- `async start()` - Start a new kernel session
- `async shutdown()` - Clean up resources
- `async execute_code(code: str, timeout: float = 30.0) -> ExecutionResult` - Execute Python code

### ExecutionResult

Dataclass containing execution results:
- `success: bool` - Whether execution was successful
- `output: str` - Standard output from code execution
- `error: Optional[str]` - Error message if execution failed

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT
