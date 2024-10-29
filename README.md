# README

## Overview

The **Disk and Server Performance Metrics Collection Script** is a comprehensive tool designed to monitor and analyze both disk and server performance metrics in real-time. This script not only collects key performance indicators but also gathers SMART (Self-Monitoring, Analysis, and Reporting Technology) data for each disk, providing valuable insights into their health and potential failure points.

The metrics are categorized into three main levels:
1. **S.M.A.R.T. Attributes**: Collects various SMART attributes to monitor disk health.
2. **Disk-Level Performance Metrics**: Focuses on individual disk operations like I/O activities, queue sizes, throughput, and operational statuses.
3. **Server-Level Performance Metrics**: Captures system-wide performance indicators, including CPU, memory usage, network traffic, and disk utilization.

## S.M.A.R.T. Attributes

The script gathers the following SMART attributes, which are crucial for assessing disk health:

| SMART ID | Attribute Name                       |
|----------|-------------------------------------|
| 1        | Read_Error_Rate                     |
| 3        | Spin-Up_Time                        |
| 4        | Start/Stop_Count                    |
| 5        | Reallocated_Sectors_Count           |
| 7        | Seek_Error_Rate                     |
| 9        | Power-On_Hours                      |
| 10       | Spin_Retry_Count                    |
| 12       | Power_Cycle_Count                   |
| 187      | Reported_UNC_Errors                 |
| 188      | Command_Timeout                      |
| 191      | G-sense_error_rate                  |
| 192      | Power-off_Retract_Count             |
| 193      | Load/Unload_Cycle_Count             |
| 194      | Temperature_Celsius                  |
| 198      | Uncorrectable_Sector_Count          |
| 199      | UltraDMA_CRC_Error_Count            |

These attributes provide essential insights into potential disk failures, performance degradation, and overall reliability. Monitoring these values can help preemptively identify issues before they result in data loss or disk failures.

## Disk-Level Metrics

Disk-level metrics provide insights into the health, workload, and throughput of each disk in the server. Key metrics collected include:

- **DiskStatus**: Reflects the current disk status (e.g., healthy, busy, error).
- **IOQueueSize**: The number of I/O requests in the queue. High values may indicate heavy load.
- **ReadSuccess_Throughput**: Disk read throughput, measured in KB/s.
- **ReadWorkItem_QueueTime**: Average queue time for read requests, in ms.
- **ReadWorkItem_SuccessQps**: Number of successful read operations per second.
- **ReadWorkItem_ProcessTime**: Execution time for read operations, measured via `r_await`.
- **Background_Checksum_ReadFailQps**: Rate of failed integrity checks (e.g., SMART attributes 1, 7, 198).
- **TempFile_WriteWorkItem_SuccessQps**: Successful write operations for temporary files per second.
- **TempFile_WriteSuccess_Throughput**: Write throughput for temporary files.
- **NormalFile_WriteWorkItem_SuccessQps**: Successful writes for normal files.
- **NormalFile_WriteWorkItem_QueueTime**: Queue time for write operations on normal files.
- **NormalFile_WriteSuccess_Throughput**: Write throughput for normal files.

## Server-Level Metrics

These metrics provide a higher-level view of the entire server’s performance, identifying system-wide impacts on disk longevity and stability:

- **disk_util**: Max and average disk utilization percentages, indicating disk load and potential wear.
- **tcp_segs_stat (tcp_outsegs)**: Number of TCP segments sent, highlighting network operations impacting the disk.
- **page_activity (page_in/page_out)**: Page activity indicating memory swap activity, impacting disk usage.
- **disk_summary (total_disk_read/total_disk_write)**: Overall data read and written to disks, helping to track wear levels.
- **memory_summary (mem_res)**: Reserved memory usage, with high swap reliance indicating increased disk activity.
- **cpu_summary (cpu_kernel)**: Kernel mode CPU load, which can indicate I/O processing demands on the CPU.
- **udp_stat (udp_outdatagrams/udp_indatagrams)**: UDP datagrams sent/received, which can correlate with disk write/read operations.
- **net_pps_summary (net_pps_receive/net_pps_transmit)**: Packets received/transmitted per second, highlighting network load on disk.
- **net_summary (receive_speed)**: Network data receive speed, indicating potential large data writes to disk.
- **tcp_currestab**: Active TCP connections, with many connections often indicating high disk access demand.

## Usage

To start the script:

1. Clone or download this repository.
2. Install any required dependencies (if applicable).
3. Run the script using:
   ```bash
   python disk_metrics.py
