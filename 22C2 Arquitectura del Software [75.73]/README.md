# Software Architecture Reports

## **Trabajo Práctico N°1**
### **Project Goal:**
The first report focuses on testing and analyzing multiple API endpoints using **Artillery**. The goal is to measure how well the system handles increasing loads and different traffic patterns.

### **Tests Conducted:**
1. **PING Endpoint:**  
   - A lightweight endpoint that returns "Pong."  
   - Tested under **stress, endurance, and spike conditions**.  
   - Performance degrades after 250 RPS, showing **timeouts and connection resets**.

2. **SYNC & ASYNC Endpoints:**  
   - SYNC makes an external request before responding, while ASYNC does not block execution.  
   - **ASYNC performs better**, handling up to 65 RPS without errors, whereas **SYNC starts failing at 10-12 RPS**.

3. **HEAVY Endpoint:**  
   - Simulates a computationally expensive task.  
   - The system **cannot handle more than 2 RPS without failing**, showing **high CPU usage and slow response times**.

### **Key Findings:**
- **ASYNC endpoints scale better** than SYNC endpoints under high load.
- Single-node setups often perform **more consistently** than multi-node setups, which sometimes show **higher error rates**.
- The **HEAVY endpoint** is a major bottleneck, indicating that **intensive computations need optimization**.

---

## **Trabajo Práctico N°2**
### **Project Goal:**
The second report expands on the first by testing **a Node.js API connected to a Python backend service** hosted on **Azure**. The project examines **scalability, caching strategies, and performance under load**.

### **Experiments Conducted:**
1. **Testing without Scaling (Single Node):**  
   - The system quickly reaches a **bottleneck at 4 RPS**, where **timeouts occur**.
   - **Datadog** monitoring shows **CPU saturation and network congestion** as key failure points.

2. **Testing with Horizontal Scaling (3 Node Instances):**  
   - Despite adding more instances, **the improvement is minimal**.
   - The **bottleneck shifts slightly**, but requests still fail at high loads.

3. **Introducing Redis Cache:**  
   - Added a **/cached** endpoint that stores responses in **Azure Redis Cache**.
   - When the cache **fills up**, performance **drops significantly**.
   - A **script was developed** to clear the cache periodically to prevent performance degradation.

### **Key Findings:**
- **Scaling horizontally did not significantly improve performance**, suggesting **backend inefficiencies** rather than lack of resources.
- **Adding caching improved response times** but introduced new issues when the cache filled up.
- **Azure network conditions affected test results**, highlighting the **impact of external factors** on cloud-based services.

---

## **General Conclusion from Both Reports:**
- **Performance bottlenecks were successfully identified** across different architectures.
- **ASYNC requests outperform SYNC requests**, making them preferable for scalable applications.
- **Caching is a powerful tool** but needs proper management to **prevent unexpected failures**.
- **System scaling is complex**—simply adding more resources is not always the solution.

Both reports contribute to understanding **system behavior under stress**, helping improve **scalability, reliability, and efficiency** in software architecture design. 🚀
