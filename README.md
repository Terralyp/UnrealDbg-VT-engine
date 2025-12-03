# UnrealDbg Project Detailed Introduction



This project is a debugging system built upon VT (Intel Virtualization Technology) designed to bypass game-driven anti-debugging mechanisms. Its user interface, developed in Delphi, offers an intuitive and convenient operating experience, while the core code, written in C++, leverages VT's powerful capabilities to enable debugging of game drivers.
During the development of game cheats, the anti-debugging mechanisms within game drivers often pose significant challenges to debugging efforts. Traditional debugging tools frequently fail to bypass these mechanisms, making debugging difficult. By leveraging VT technology, this project establishes an independent debugging framework capable of circumventing game driver anti-debugging mechanisms, providing developers and security testers with an effective debugging solution.

Breaking Anti-Debugging Mechanisms: Utilizing VT technology to bypass game driver anti-debugging mechanisms, enabling debugging of game drivers.
Self-Built Debugging System: Constructed an independent debugging system that does not rely on traditional debugging tools, enhancing debugging flexibility and reliability.
Intuitive User Interface: The user interface, developed using Delphi, provides an intuitive and convenient operating experience, facilitating debugging operations for users.
C++ Core Code: Core code written in C++ leverages the powerful capabilities of VT technology to deliver efficient and stable debugging functionality.

## I. Project Overview
UnrealDbg is a self-built debugging system project designed to bypass game-driven anti-debugging mechanisms. Developed using a hybrid approach of Delphi and C++ programming, it supports both Windows 10 and Windows 11 operating systems. Leveraging VT (Intel Virtualization Technology), this project constructs a comprehensive debugging solution encompassing multiple functional modules, including key registration, encryption, debugging, loading, and hooking.

## II. Project Structure and Detailed Analysis of Each Module

(1) UnrealDbg Main Project
This folder serves as the core directory of the project, containing the primary code and resources related to the self-built debugging system based on VT technology. It was developed using Delphi. Detailed analysis of each module follows.
- **Project Files**:
    - `UnrealDbg.dpr`: The main program file for the Delphi project, serving as the entry point for the application.
    - `UnrealDbg.dproj`: The configuration file for the Delphi project, containing compilation options, dependencies, and other information.
    - `UnrealDbg.dproj.local`: Local project configuration file storing developer-specific settings.
    - `UnrealDbg.res`: Delphi resource file containing icons, menus, and other resource information.
Developed using Delphi. Detailed analysis of each module.
- **Subfolders**:
    - **Forms**: Stores Delphi form files defining user interface layouts and interaction logic. For example, `Main.dfm` and `Main.pas` might define the main interface for a debugging tool.
    - **Globals**: Contains files defining global variables, such as `GlobalVar.pas`, used to share data across the entire project.
    - **Network**: Contains functionality related to network operations. For example, `KeyVerification.pas` may handle card key verification by interacting with servers over the network.
    - **ExternalCall**: Holds code for interacting with external DLLs. Examples include `D_encryptionDll.pas` and `UnrealDbgDll.pas`, which call functions in encryption DLLs and debug core DLLs.
    - **LogSystem**: Responsible for logging, such as `Log.pas` which may implement log writing and management functions.
    - **Handler**: May contain various event handlers for processing user actions and system events.
    - **Common**: Contains code, header files, utility classes, etc., shared across multiple subprojects within the project.
    - **KernelApi**: Involves kernel-level API calls for interacting with the operating system kernel.
    - **Threads**: Contains multithreading-related code to implement concurrent operations, enhancing program performance and responsiveness.
    - **res**: Stores resource files such as icons and images.

(2) CardRegistration Module
Implements card code registration functionality, providing a user interface for entering and verifying card codes.
- **Core Files**:
    - `卡密注册.dpr`: Delphi project main executable file containing the program entry point.
    - `卡密注册.dproj`: Delphi project configuration file containing compilation options, dependencies, and other information.
    - `CardKeyRegistration.dproj.local`: Local project configuration file containing developer-specific settings.
    - `CardKeyRegistration.res`: Delphi resource file containing icons, menus, and other resource information.
- **Functionality Implementation**: Interacts with the server to validate user-entered card keys, ensuring only authorized users can utilize the debugging tool.

### (3) D - Encryption Module
Related to encryption functionality, used to encrypt data and ensure its security.
- **Core Files**:
    - `D_encryption.dpr`: Delphi project main program file containing the program entry point.
    - `D_encryption.dproj`: Delphi project configuration file containing compilation options, dependencies, and other information.
    - `D_encryption.dproj.local`: Local project configuration file containing developer-specific settings.
    - `D_encryption.res`: Delphi resource file containing icons, menus, and other resource information.
- **Encryption Algorithms**: May utilize encryption algorithms such as Blowfish to encrypt sensitive data (e.g., card keys, debugging information).

### (4) DbgkSysWin10 and DbgkSysWin11 Modules
These debugging-related modules, designed specifically for Windows 10 and Windows 11 systems, provide a suite of interfaces and functional implementations for debugging operations. They assist in bypassing game driver anti-debugging mechanisms.
- **Core Files**:
    - `DbgkApi.h` and `DbgkApi.cpp`: Define and implement debug-related API functions such as `NtCreateDebugObject` and `NtDebugActiveProcess` for creating debug objects and activating debugging processes.
    - `Driver.h` and `Driver.cpp`: Core driver files. `DriverEntry` handles driver initialization, while `Unload` manages resource cleanup.
    - `Globals.h` and `Globals.cpp`: Define and manage global variables.
    - `Memory` folder: Contains memory read/write code for operations like reading game process memory data.
    - `Asm` folder: Holds assembly code files for high-performance or low-level operations, such as modifying CPU register values.
    - `Hooks` folder: Specifically the `EptHook` subfolder, used to implement hooking functionality to intercept specific operations in the system or target process, such as function calls or system calls.
    - `Init` folder: Contains initialization-related code, such as symbol resolution and initialization, ensuring the debugging tool can correctly recognize and handle system symbols.
    - `Encrypt` folder: Particularly the `Blowfish` subfolder, potentially used to implement encryption functionality for secure transmission of debugging data.
    - `Log` folder: Contains logging-related code to record information during the debugging process, aiding developers in troubleshooting.
    - `List` folder: Contains code for linked list implementation, managing debug objects, process information, and similar data structures.
    - `Hvm` folder: Holds virtual machine-related code for interacting with the VM. It creates a virtual environment using VT technology to bypass the game driver's anti-debugging mechanisms.

(5) Loader Module
Presumably used to load other modules, drivers, or programs—such as loading game drivers, debugging modules, or other necessary components—to enable debugging functionality. It may load DLL files by calling Windows API functions like `LoadLibrary`.

(6) Hook Module
Implements hooking techniques to intercept specific operations within the system or target process, such as function calls or system calls. Custom code is inserted before and after these operations to bypass game-driven anti-debugging mechanisms. Potential implementation methods include EPT hooks and function hooks.
- **Core Files**:
    - `dllmain.h`: Defines hook-related functions and variables, such as `SetupHook` for setting hooks and `UnHook` for unloading hooks.
    - `detours.h`: Contains definitions for the Detours library, a library for function interception and replacement used to implement hook functionality.

(7) VT_Driver Module
VT_Driver Project Overview
VT_Driver is a driver project based on Intel VT (Virtualization Technology), designed to leverage virtualization techniques to create a virtual machine environment. This enables bypassing game driver anti-debugging mechanisms, facilitating the debugging of game drivers. Written in C++, this project interacts closely with the operating system kernel to implement a series of complex functions, including virtual machine management, memory virtualization, hooking techniques, and debug event handling.
Bypassing Anti-Debugging Mechanisms: The VT_Driver module leverages Intel VT (Virtualization Technology) to create a virtual machine environment, enabling it to bypass game drivers' anti-debugging mechanisms. This allows developers to more conveniently analyze and modify game drivers during debugging, identifying issues such as performance bottlenecks and logical errors.
Multi-System Debugging Adaptation: The DbgkSysWin11 and DbgkSysWin10 modules are specifically developed for Windows 11 and Windows 10 systems, ensuring effective debugging functionality across different operating system versions.
### Project File Structure Analysis
- **Core Files**:
    - `Driver.cpp`: The driver's entry point file, containing the `DriverEntry` and `Unload` functions responsible for driver initialization and unloading operations.
    - `EPT.cpp`: Implements Extended Page Table (EPT) functionality, such as EPT hooks and memory mapping management, enabling memory virtualization and hooking techniques.
    - `vmexit_handler.cpp`: Handles virtual machine exit events, executing corresponding actions based on exit reasons, such as interrupt injection and instruction modification.
    - `vmcall_handler.cpp`: Handles the `VMCall` instruction, executing corresponding functions based on the `VMCall` reason, such as EPT hook operations and breakpoint setting.
- **Header Files**:
    - `Driver.h`: Defines driver constants, function prototypes, and data structures, such as `IOCTL` codes and logging macros.
    - `vmexit_handler.h`: Defines the enumeration type for virtual machine exit reasons, the union for VM exit instruction information, and prototypes for handling functions.
    - `vmcall_reason.h`: Defines the `VMCall` reason enumeration type, used to distinguish different `VMCall` functionalities.

### Key Code Analysis

#### 1. `DriverEntry` Function (`Driver.cpp`)
```cpp
EXTERN_C
NTSTATUS DriverEntry(_In_ PDRIVER_OBJECT DriverObject, _In_ PUNICODE_STRING RegistryPath)
{
    UNREFERENCED_PARAMETER(DriverObject);
    UNREFERENCED_PARAMETER(RegistryPath);

    DriverObject->DriverUnload = Unload;
    KdPrint(("DriverEntry!!!\n"));

    NTSTATUS nStatus = STATUS_SUCCESS;

    if (InitNtoskrnlSymbolsTable())
    {
        if (!hv::virtualization_support()) {
            outDebug("VMX operation is not supported on this processor.\n");
            return STATUS_UNSUCCESSFUL;
        }

        hv::InitGlobalVariables();
        if (vmm_init() == false)
        {
            hv::disable_vmx_operation();
            free_vmm_context();
            outDebug("Vmm initialization failed");
            return STATUS_UNSUCCESSFUL;
        }
        outDebug("�������سɹ�!!!\n");
    }
    else
    {
        nStatus = STATUS_UNSUCCESSFUL;
        outDebug("��������ʧ��!!!\n");
    }
    return nStatus;
}
```
- **Function**: The driver's entry point, responsible for initializing the driver and launching the Virtual Machine Monitor (VMM).
- **Detailed Steps**:
    1. Set the driver's unload function to `Unload`.
    2. Call the `InitNtoskrnlSymbolsTable` function to initialize the Ntoskrnl symbol table.
    3. Check if the processor supports VT technology. If not supported, output an error message and return a failure status.
    4. Initialize global variables and call the `vmm_init` function to start the VMM.
    5. If VMM initialization fails, terminate VT operations, release related resources, output an error message, and return a failure status.
    6. If all operations succeed, output a success message and return a success status.
#### 2. `vmexit_handler` 函数（`vmexit_handler.cpp`）
```cpp
EXTERN_C
bool vmexit_handler(guest_context* guest_registers, PFXSAVE64 fxsave)
{
    __vcpu* vcpu = reinterpret_cast<__vcpu*>(_readfsbase_u64());

    guest_registers->rsp = hv::vmread(GUEST_RSP);

    vcpu->vmexit_info.reason = hv::vmread(VM_EXIT_REASON) & 0xffff;
    vcpu->vmexit_info.qualification = hv::vmread(EXIT_QUALIFICATION);
    vcpu->vmexit_info.guest_rflags.all = hv::vmread(GUEST_RFLAGS);
    vcpu->vmexit_info.guest_rip = hv::vmread(GUEST_RIP);
    vcpu->vmexit_info.instruction_length = hv::vmread(VM_EXIT_INSTRUCTION_LENGTH);
    vcpu->vmexit_info.instruction_information = hv::vmread(VM_EXIT_INSTRUCTION_INFORMATION);
    vcpu->vmexit_info.guest_registers = guest_registers;
    vcpu->vmexit_info.fxsave = fxsave;

    vcpu->hide_vm_exit_overhead = false;
    dispatch_vm_exit(vcpu);

    if (vcpu->vmx_off_state.vmx_off_executed == true)
    {
        vcpu->vcpu_status.vmm_launched = false;
        RestoreGuest();
        return true;
    }

    return false;
}
```
- **Functionality**: Handles virtual machine exit events and performs corresponding actions based on the exit reason.
- **Detailed Steps**:
    1. Obtain the current VCPU pointer via the `_readfsbase_u64` function.
    2. Read relevant information from the VMCS, such as `GUEST_RSP` and `VM_EXIT_REASON`, and store it in the `vcpu->vmexit_info` structure.
    3. Call the `dispatch_vm_exit` function to distribute processing based on the exit reason.
    4. If the `VMXOFF` operation is detected as executed, set the VMM startup state to `false`, restore the Guest state, and return `true` to indicate processing should stop.
    5. Otherwise, return `false` to continue processing.

#### 3. `vmexit_vmcall_handler` function (`vmcall_handler.cpp`)
```cpp
void vmexit_vmcall_handler(__vcpu* vcpu)
{
    bool status = true;
    unsigned __int64 vmcall_reason = 0;
    unsigned __int64 vmcall_parameter1 = 0;
  // ... Other parameter definitions

    if ((vcpu->vmexit_info.guest_registers->rax != VMCALL_IDENTIFIER) &&
        (vcpu->vmexit_info.guest_registers->eax != VMCALL_IDENTIFIER2))
    {
        if (ept::handler_vmcall_rip(*vcpu->ept_state))
        {
            return;
        }
        hv::inject_interruption(EXCEPTION_VECTOR_UNDEFINED_OPCODE, INTERRUPT_TYPE_HARDWARE_EXCEPTION, 0, false);
        return;
    }

    if (vcpu->vmexit_info.guest_registers->eax == VMCALL_IDENTIFIER2)
    {
        vmcall_reason = vcpu->vmexit_info.guest_registers->ecx;
        vmcall_parameter1 = vcpu->vmexit_info.guest_registers->edx;
    }
    else
    {
        vmcall_reason = vcpu->vmexit_info.guest_registers->rcx;
        vmcall_parameter1 = vcpu->vmexit_info.guest_registers->rdx;
        // 
    }

    switch (vmcall_reason)
    {
    case VMCALL_TEST:
        adjust_rip(vcpu);
        break;
    case VMCALL_VMXOFF:
        call_vmxoff(vcpu);
        adjust_rip(vcpu);
        break;
    // 
    }

    vcpu->vmexit_info.guest_registers->rax = status;
}
```
- **Functionality**: Handles the `VMCall` instruction and executes corresponding actions based on the specific `VMCall` cause.
- **Detailed Steps**:
    1. Check if the `VMCall` belongs to this driver. If not, attempt to handle the `VMCall RIP` hook. If unsuccessful, inject an undefined opcode exception.
    2. Retrieve the `VMCall` reason and arguments based on its identifier (`VMCALL_IDENTIFIER` or `VMCALL_IDENTIFIER2`).
    3. Use a `switch` statement to handle different `VMCall` reasons: e.g., adjust the instruction pointer for `VMCALL_TEST`, or call the `call_vmxoff` function to exit VMX mode for `VMCALL_VMXOFF`.
    4. Store the processing result in `vcpu->vmexit_info.guest_registers->rax`.

### Project Feature Summary
- **Virtual Machine Management**: Initializes and launches the VMM via the `DriverEntry` function, utilizing the `vmexit_handler` function to handle virtual machine exit events, enabling effective management of virtual machines.
- **Memory Virtualization**: The `EPT.cpp` file implements EPT-related functionality. Through EPT hooking technology, memory accesses can be intercepted and processed to achieve memory virtualization.
- **Debugging Capabilities**: The `VMCall` mechanism provides extensive debugging features, such as setting breakpoints, hiding software breakpoints, and reading EPT fake page memory, facilitating debugging of game drivers.
- **Exception Handling**: The `vmexit_handler` and `vmcall_handler` functions handle exceptional conditions, including undefined opcode injection exceptions and general protection faults, ensuring system stability.


### Project Advantages and Application Scenarios
- **Advantages**: Leveraging Intel VT technology, it effectively bypasses anti-debugging mechanisms in game drivers, offering robust debugging capabilities that enhance debugging efficiency and success rates.
- **Application Scenarios**: Primarily used in game development and debugging, it assists developers in rapidly identifying and resolving issues within game drivers. It is also applicable in system security research and software debugging domains.


### (8) UnrealDbgDll Module
A dynamic-link library (DLL) project implementing core functionality related to the custom debugging system. It encapsulates debugging-related features for easy access by other modules, facilitates coordinated operation across the entire debugging system through module interactions, and enables cross-platform support.
- **Core Files**:
    - `dllmain.cpp`: The DLL's entry point file, implementing the `DllMain` function to handle DLL loading and unloading events.
    - `InitSymbol` function: Initializes the symbol table by obtaining system function addresses via the `GetProcAddress` function.
    - `DispatchSymbol` function: Sends symbol table data to the driver to enable proper handling of debug information.
    - `Initialize` function: Responsible for initializing the debug tool, including loading the symbol table and sending debug data.

III. Code Function Analysis

(1) Debug State Enumeration
```cpp
enum _DBG_STATE
{
    DbgIdle = 0,  // Debugger idle state
    DbgReplyPending = 1,
    DbgCreateThreadStateChange = 2,
    DbgCreateProcessStateChange = 3,
    DbgExitThreadStateChange = 4,
    DbgExitProcessStateChange = 5,
    DbgExceptionStateChange = 6,
    DbgBreakpointStateChange = 7,
    DbgSingleStepStateChange = 8,
    DbgLoadDllStateChange = 9,
    DbgUnloadDllStateChange = 10,
};
```
This enumeration defines the various states of the debugger, used to track state changes during the debugging process.

(2) Debugging changes in the message structure state.
```cpp
typedef struct _DBGKM_APIMSG {
    PORT_MESSAGE h;
    DBGKM_APINUMBER ApiNumber;
    NTSTATUS ReturnedStatus;
    union {
        DBGKM_EXCEPTION Exception;
        DBGKM_CREATE_THREAD CreateThread;
        DBGKM_CREATE_PROCESS CreateProcess;
        DBGKM_EXIT_THREAD ExitThread;
        DBGKM_EXIT_PROCESS ExitProcess;
        DBGKM_LOAD_DLL LoadDll;
        DBGKM_UNLOAD_DLL UnloadDll;
        DBGKM_ERROR_MSG ErrorMsg;
    } u;
} DBGKM_APIMSG, * PDBGKM_APIMSG;
```
This structure defines the format of debug messages, comprising a message header, API ID, return status, and specific message content. The union enables storage of different types of debug messages.

(3) Debugging Event Structures
```cpp
typedef struct _DEBUG_EVENT
{
    LIST_ENTRY EventList;
    KEVENT ContinueEvent;
    CLIENT_ID ClientId;
    _EPROCESS* Process;  
    _ETHREAD* Thread;    
    NTSTATUS Status;  
    ULONG Flags;
    _ETHREAD* BackoutThread;  
    DBGKM_APIMSG ApiMsg;  
} DEBUG_EVENT, * PDEBUG_EVENT;
```
This structure defines the format for debugging events, encompassing an event list, continuation events, client ID, process and thread information, status codes, flags, and debug messages. It is used to record and process events during the debugging process.

## IV. Project Advantages
- **Cross-System Support**: Compatible with both Windows 10 and Windows 11 operating systems, ensuring broad compatibility.
- **Hybrid Programming**: Utilizes a hybrid Delphi and C++ programming approach, leveraging the strengths of both languages—Delphi for rapid user interface development and C++ for implementing low-level debugging functions and kernel drivers.
- **Secure and Reliable**: Ensures the security and legitimacy of the debugging tool through license key registration and encryption technology, preventing unauthorized use and data leaks.
- **Powerful Features**: Offers extensive debugging capabilities, including process debugging, thread debugging, DLL load/unload debugging, and breakpoint debugging, catering to diverse debugging requirements.

## V. Application Scenarios
- **Game Development**: Debugs game drivers, bypasses anti-debugging mechanisms, and helps developers quickly identify and resolve issues within games.
- **System Security Research**: Investigates operating system kernel mechanisms and anti-debugging techniques, providing insights for system security protection.
- **Software Debugging**: Debugs other software requiring anti-debugging bypass, enhancing debugging efficiency and success rates.
