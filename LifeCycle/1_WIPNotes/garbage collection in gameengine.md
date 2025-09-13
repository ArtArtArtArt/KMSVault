---
state: ⚙️
type: interviewquestion
tags:
 - interview 
 - programming/gamedev/gameEngine 
---
# garbage collection in gameengine

# In UnrealEngine specifically


## **Key Points About Garbage Collection in Unreal Engine**
(taken from chatgpt https://chatgpt.com/c/67892bfb-e858-8002-9b78-f3425317ce52)
### **1. UObject-Based System**

- Unreal Engine's garbage collector works only on objects derived from `UObject`.
- Non-UObject memory allocations (like C++ pointers) are not managed by GC and must be handled manually.

---

### **2. Reference Tracking**

- The garbage collector tracks object references via the `UObject` system.
- Only objects with no external references (outside GC-tracked references) are eligible for garbage collection.

---

### **3. Root Set**

- Objects in the **Root Set** are never garbage collected.
- You can add objects to the Root Set using `AddToRoot()` and remove them using `RemoveFromRoot()`.

---

### **4. [[Mark-and-Sweep Algorithm]]**

- The GC uses a **mark-and-sweep** algorithm:
    1. **Mark Phase:** Objects with valid references are marked as reachable.
    2. **Sweep Phase:** Objects not marked are destroyed and their memory is reclaimed.

---

### **5. GC Trigger Points**

- Garbage collection is triggered during specific moments, such as:
    - Level transitions.
    - Periodic checks based on the engine's GC settings.
    - Explicit calls to `CollectGarbage()` in your code.

---

## **Best Practices**

### **1. Avoid Circular References**

- Unreal's GC cannot handle circular references. Use weak pointers (`TWeakObjectPtr`) or `TWeakPtr` where necessary.

### **2. Use Smart Pointers**

- Use Unreal Engine's smart pointers like `TSharedPtr` and `TUniquePtr` for non-UObject memory management.

### **3. Manage Non-UObject Memory**

- Manually manage non-UObject memory (e.g., raw C++ pointers or dynamically allocated memory).

### **4. Profiling GC Performance**

- Use Unreal's profiling tools like `stat garbage` to monitor and optimize GC performance.

### **5. Avoid Excessive UObject Creation**

- Frequently creating and destroying UObjects can burden the GC. Reuse objects when possible.

### **6. Object Lifespan**

- Ensure objects are explicitly destroyed or dereferenced when no longer needed.
