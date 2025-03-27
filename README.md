# Process Tree Kernel Module

This repository contains a Linux kernel module that creates and displays a process tree. The module lists all running processes in a hierarchical format, showing parent-child relationships.

## 📁 **File Structure**

```
├── Makefile
├── main.c
```

### **Files Explained**

- **main.c** – Implements the kernel module that traverses and displays the process tree.
- **Makefile** – Automates the compilation and module loading/unloading process.

## 📝 **Explanation**

### **How It Works**

1. **Kernel Module Setup**

   - The `main.c` file defines the initialization (`init_module`) and cleanup (`cleanup_module`) functions for the kernel module.
   - The module traverses the process tree using the `task_struct` structure provided by the Linux kernel.

2. **Process Traversal**

   - The module starts at the `init_task` (representing the first process, PID 1).
   - It recursively traverses child processes using the `list_for_each_entry` macro.
   - The parent-child relationships are maintained using the `task_struct`'s `children` and `sibling` fields.

3. **Output to Kernel Log**

   - The process tree is logged using `printk`.
   - The output can be viewed using the `dmesg` command.

## ⚙️ **Compilation**

To compile the kernel module, use the provided Makefile:

```bash
make
```

This will generate an output file:

- `main.ko` – The kernel module object file.

## 🚀 **Execution**

### 1. Insert Module

To insert the kernel module:

```bash
sudo insmod main.ko
```

### 2. View Kernel Logs

To view the output of the module:

```bash
dmesg
```

This will display the process tree in the kernel log.

### 3. Remove Module

To remove the kernel module:

```bash
sudo rmmod main
```

### 4. Clean Up

To remove the compiled files:

```bash
make clean
```

## 🛠️ **Requirements**

- GCC compiler
- Linux kernel headers installed
- Root permissions

## ❗ **Troubleshooting**

- If you encounter a `module not found` error, ensure that the kernel headers are properly installed.
- If the process tree does not appear in `dmesg`, try loading the module again.

