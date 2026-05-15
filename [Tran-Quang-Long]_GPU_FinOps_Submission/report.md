#### 💡 Note for Cell 4 (Cluster Metrics)
> **Observation:** Note that `Total Power Draw` often correlates more closely with `GPU Utilization` than `Memory Usage`. In a FinOps context, tracking power (W) is essential for "GreenOps" and understanding the actual electricity overhead in on-premise vs. cloud environments.

#### 💡 Note for Cell 9 (Spot Preemption)
> **FinOps Insight:** Spot instances are a "Best-Effort" resource. The key to successful Spot usage isn't avoiding preemption, but building **fault-tolerant architectures**. By using frequent model checkpointing to S3/Cloud Storage, we treat preemption as a minor delay rather than a financial loss.

#### 💡 Note for Cell 13 (Waste Report)
> **The Cost of Idleness:** A GPU that is "allocated" but has 0% utilization costs exactly the same as one at 100% utilization. My analysis shows that **Idle Cost** is the primary driver of budget overrun. Implementing a "Time-to-Live" (TTL) for idle kernels is the highest-priority optimization here.

#### 💡 Note for Cell 24 (Real GPU Comparison)
> **Technical Deep Dive:** The speedup observed in AMP is primarily due to the utilization of **Tensor Cores** on the T4/A100 architecture. Tensor Cores are hardware-accelerated for FP16 matrix multiplication. By switching from FP32, we reduce memory bandwidth bottlenecks and increase TFLOPS throughput, directly lowering the "Price-per-Step."

#### 💡 Note for Cell 31 (Challenge Strategy)
> **Final Conclusion:** To meet the $5,000 budget, we cannot rely on hardware alone. We must combine **Software Optimization (AMP)**, **Purchasing Models (Spot)**, and **Infrastructure Orchestration (Autoscaling)**. This multi-layered approach is the core of a mature FinOps practice.
