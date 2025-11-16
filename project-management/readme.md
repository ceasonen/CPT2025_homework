

## Computer Organization and Design - Rev 1.1.1

**Instructor**: Dr. Hao Xu, Assistant Professor  
**Institution**: Tongji University  
**Office Hours**: Tuesday Afternoon or by Appointment, Zhixinguan 708a  

---

## Table of Contents

**Part I: Project Overview**

1. Course Framework
2. CHRONOS Project Requirements Specification
3. Assessment and Grading

**Part II: Weekly Guide**

- Week 1: System Planning & Computer Organization Fundamentals
- Week 2: Processor Architecture & Safety Analysis
- Week 3: Memory Hierarchy & Design Specification
- Week 4: I/O Systems & Implementation Launch
- Week 5: Parallelism & Distributed Integration
- Week 6: Reliability Engineering & Verification
- Week 7: System Performance & Final Deliverables

**Part III: Core Principles Reference**

- Computer Organization Principles
- Certification Engineering Principles
- Project Management Principles

**Part IV: Templates & Checklists**

- Requirements Templates
- Review Checklists
- Document Standards

---

# Part I: Project Overview

## 1. Course Framework

### 1.1 Teaching Philosophy

**"From Silicon to Systems, From Theory to Engineering"**

This course integrates computer organization theory with systems engineering practice through a complete industrial-grade project (CHRONOS):

```
Theory                    Practice Vehicle
──────────                ────────────────
Processor Architecture ──→ RISC-V C906
Memory Hierarchy      ──→ Consensus State Management
I/O Systems          ──→ Wireless Communication
Parallelism          ──→ Multi-node Coordination
Reliability          ──→ Fault Tolerance

Engineering Methods       Application
───────────────          ─────────────
ARP 4754A           ──→  System-level Requirements & Safety
DO-178C             ──→  Software Development Assurance
DO-254              ──→  Hardware Assessment
```

### 1.2 Course Structure

**Weekly Schedule (12 hours total):**

|Activity|Duration|Location|Focus|
|---|---|---|---|
|**In-Class (6 hours)**||||
|Lecture|2 hours|Classroom|Theory & Principles|
|Project Stand-up|1 hour|Classroom|Progress & Issues|
|Coding Session|3 hours|Lab|Hands-on Development|
|**Self-Study (6 hours)**||||
|Reading & Exercises|2 hours|-|Textbook chapters|
|Documentation|2 hours|-|Requirements, Design docs|
|Project Development|2 hours|-|Coding, Testing|

### 1.3 Assessment Structure

**Total: 100 points**

|Component|Weight|Details|
|---|---|---|
|**Class Performance**|20%|Attendance, Stand-up participation, Coding progress|
|**Final Exam**|30%|Computer organization theory + ARP 4754A concepts|
|**Project Deliverables**|30%|Documentation package (ARP/DO-178C/DO-254)|
|**Final Presentation**|10%|Technical presentation + Live demo|
|**Research Paper**|10%|IEEE-format paper (6 pages)|

### 1.4 Course Milestones

|Week|Checkpoint|Review Type|Deliverables|
|---|---|---|---|
|1|SRR|System Requirements Review|SDP, SRS v0.1|
|2|FHA|Functional Hazard Assessment|FHA, PSSA, SRS v1.0|
|3|PDR|Preliminary Design Review|Architecture, SDD v0.1|
|4|CDR|Critical Design Review|SDD v1.0, Code skeleton|
|5|Integration|Integration Review & FTA|Integrated system, FTA|
|6|Verification|Verification Review|Test results vs targets|
|7|Final|Final Presentation|Complete package, Paper|

---

## 2. CHRONOS Project Requirements Specification

### 2.1 Project Background

**Domain: Intelligent Warehouse Robot Coordination**

Multiple Automated Guided Vehicles (AGVs) must coordinate to complete order picking in a modern warehouse. Traditional centralized control has single-point failure risks and poor scalability. CHRONOS uses distributed consensus to enable autonomous coordination via wireless communication.

**Why This is an Teaching Project:**

- Covers all computer organization topics (processor, memory, I/O, parallelism)
- Real industrial scenario (warehouse automation)
- Safety-critical (robot collision may cause injury)
- Appropriate technical challenge (achievable in 7 weeks)

### 2.2 System Requirements Template

#### Requirements Numbering Scheme

```
SR-XXX: System Requirements (SR-001 to SR-999)
  ├─ SR-1XX: Functional Requirements
  ├─ SR-2XX: Performance Requirements
  ├─ SR-3XX: Safety Requirements
  ├─ SR-4XX: Reliability Requirements
  └─ SR-5XX: Interface/Constraint Requirements

SWR-XXX: Software Requirements (SWR-001 to SWR-999)
  ├─ SWR-1XXX: Consensus Module
  ├─ SWR-2XXX: Task Allocation
  ├─ SWR-3XXX: Path Management
  └─ SWR-4XXX: Communication Layer

HWR-XXX: Hardware Requirements (HWR-001 to HWR-099)
```

#### System Requirements Template

```
Requirement ID: SR-XXX
Title: [Brief descriptive title]
Category: [Functional/Performance/Safety/Reliability/Constraint]
Priority: [Critical/High/Medium/Low]

Description:
The system shall [specific, measurable requirement statement].

Rationale:
[Why this requirement exists, stakeholder need]

Acceptance Criteria:
[How to verify this requirement is satisfied]

Verification Method:
[Test/Analysis/Inspection/Demonstration]

Derived Requirements:
[SWR-XXX, HWR-XXX that implement this SR]

Parent Requirement:
[Stakeholder need or higher-level requirement]

Notes:
[Additional context, constraints, assumptions]
```

### 2.3 Core System Requirements

#### SR-100 Series: Functional Requirements

**SR-101: Distributed Consensus**

- The system shall implement RAFT consensus protocol
- Support 5-13 robot nodes
- Automatic leader election with fault tolerance ⌊N/2⌋

**SR-102: Task Allocation**

- Automatically assign new tasks to optimal robot
- Consider robot position, battery level, current load
- Prevent duplicate assignment via consensus

**SR-103: Collision Avoidance**

- Detect path conflicts between robots
- Reserve path segments to prevent simultaneous occupation
- Emergency stop capability

**SR-104: Node Management**

- Support dynamic node join/leave
- Detect node failure (heartbeat timeout)
- Automatic recovery and rebalancing

#### SR-200 Series: Performance Requirements

|Req ID|Parameter|Target Value|Measurement Method|
|---|---|---|---|
|SR-201|Task allocation latency|≤ 500ms (p95)|Timestamp logging|
|SR-202|Consensus convergence|≤ 2 seconds|Leader election timing|
|SR-203|System throughput|≥ 20 tasks/min|7-node configuration|
|SR-204|CPU utilization|< 80%|Normal load monitoring|
|SR-205|Memory footprint|< 10MB|Runtime measurement|

#### SR-300 Series: Safety Requirements

**SR-301: Collision Protection**

- Robot separation distance must be > 0.5m
- Collision probability < 0.1% (10⁻³)
- Verification: Path conflict detection testing

**SR-302: Fault Detection**

- Node failure detection time < 5 seconds
- Split-brain detection ≤ 2 heartbeat cycles
- Verification: Fault injection testing

**SR-303: Data Integrity**

- All messages use CRC32 checksum
- Corrupted data immediately discarded
- Verification: Bit error injection

#### SR-400 Series: Reliability Requirements

**SR-401: Fault Tolerance**

- Tolerate ⌊N/2⌋ simultaneous node failures
- Single node MTBF > 100 hours
- Verification: Failure mode testing

**SR-402: Network Adaptation**

- Operational at RSSI -85dBm
- Automatic adaptation to network quality
- Verification: RSSI variation testing

**SR-403: Recoverability**

- Automatic recovery from network partition
- State consistency guarantee
- Verification: Network partition testing

#### SR-500 Series: Constraints

**SR-501: Hardware Platform**

- RISC-V processor architecture (Milk-V Duo S)
- 64MB RAM minimum
- IEEE 802.11n wireless capability

**SR-502: Software Constraints**

- Programming language: C (ISO C11)
- Version control: Git
- Communication: UDP over WiFi

**SR-503: Engineering Standards**

- System development per ARP 4754A
- Software development per DO-178C Level C
- Hardware assessment per DO-254 COTS method

### 2.4 Requirements Management

**Requirements Traceability Matrix (RTM)**

|Stakeholder Need|System Req|Software Req|Hardware Req|Test Case|Status|
|---|---|---|---|---|---|
|Safe operation|SR-301|SWR-301-305|HWR-005|TC-301|✓|
|Efficient task completion|SR-201|SWR-201-210|HWR-002|TC-201|○|
|Fault tolerance|SR-401|SWR-401-408|-|TC-401|○|

**Legend:** ✓ Verified | ○ In Progress | ✗ Failed

**Requirements Change Control:**

1. Any requirement change requires change request (CR)
2. Impact analysis on dependent requirements
3. Update RTM and affected documents
4. Re-verification if needed

---

## 3. Technical Challenge Mapping

|Computer Organization Topic|CHRONOS Implementation|Technical Challenge|
|---|---|---|
|**ISA**|RISC-V RV64GC|Implement consensus with simple instructions|
|**Processor**|C906 Pipeline|Minimize hazards and stalls|
|**Memory**|Cache Optimization|Keep consensus state in cache|
|**Virtual Memory**|Address Translation|Enable or not? Trade-offs?|
|**I/O**|Wireless Communication|High interrupt frequency handling|
|**Parallelism**|Multi-node Coordination|Synchronization mechanisms|
|**Reliability**|Fault Tolerance|Byzantine fault detection|

---

# Part II: Weekly Guide

## Week 1: System Planning & Computer Organization Fundamentals

### Theme

**Establishing the Big Picture: From Requirements to Architecture**

### Computer Organization Core Principles

**Principle 1-1: Abstraction Layers**

```
Application Algorithm (RAFT Consensus)
    ↓
High-Level Language (C)
    ↓
Assembly Language (RISC-V)
    ↓
Machine Code (Binary)
    ↓
Hardware Execution (C906 Processor)
```

**Principle 1-2: Performance Equation**

```
Execution Time = Instruction Count × CPI × Clock Cycle Time
```

**Principle 1-3: Amdahl's Law**

```
Speedup = 1 / [(1 - P) + P/S]
```

Focus optimization on bottlenecks, not non-critical paths.

### ARP 4754A Core Principles

**Principle 1-4: V-Model Development**

```
Requirements ↔ Validation
Design ↔ Testing
Implementation ↔ Code Review
```

**Principle 1-5: Requirement Quality Attributes**

- **Necessary**: Must exist
- **Verifiable**: Can be tested/analyzed
- **Traceable**: Links to parent requirement

**Principle 1-6: Development Assurance Level (DAL)** Failure severity → Development rigor  
CHRONOS: Primarily DAL C (Major failures)

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: Computer Systems Overview**

- Five components: Input, Output, Memory, Datapath, Control
- Performance metrics: Latency, Throughput, Bandwidth
- RISC vs CISC philosophies

**Topic 2: ARP 4754A Introduction**

- System development lifecycle
- Requirements engineering
- Safety assessment overview

#### Project Stand-up (1 hour)

**Team Formation:**

- [ ] Form teams of 3-4 students
- [ ] Assign roles:
    - Project Manager
    - Safety Engineer
    - Software Engineer(s)
    - Hardware/Test Engineer
- [ ] Establish communication channels (WeChat/Slack)

**Initial Planning:**

- [ ] Review CHRONOS requirements template
- [ ] Discuss warehouse scenario
- [ ] Brainstorm initial requirements list

#### Coding Session (3 hours)

**Activity 1: Development Environment Setup**

- [ ] Install RISC-V toolchain
- [ ] Configure Git repository
- [ ] Test Milk-V Duo S board connection
- [ ] Compile and run "Hello World"

**Activity 2: Requirements Workshop**

- [ ] Identify 30-50 system requirements
- [ ] Use requirements template
- [ ] Classify requirements (Functional/Performance/Safety)
- [ ] Begin Requirements Traceability Matrix

### Self-Study (6 hours)

**Reading:**

- Patterson & Hennessy Chapter 1: Computer Abstractions and Technology
- ARP 4754A Section 4: System Development Process

**Tasks:**

- [ ] Draft System Development Plan (SDP)
- [ ] Complete System Requirements Specification v0.1
- [ ] Create project directory structure
- [ ] Test all hardware components

### Week 1 Checkpoint: SRR (System Requirements Review)

**Deliverables Checklist:**

- [ ] System Development Plan (5 pages)
- [ ] System Requirements Specification v0.1 (10 pages)
    - [ ] Minimum 30 requirements with SR-XXX IDs
    - [ ] Requirements categorized
    - [ ] Verification methods defined
- [ ] Git repository initialized
- [ ] Team roster and role assignments
- [ ] Hardware inventory list

**Review Preparation:**

- 15-minute presentation covering:
    - Project understanding
    - Requirements overview
    - Development approach
    - Schedule and milestones
- Be prepared to answer:
    - Why these requirements?
    - How will you verify each requirement?
    - Is the timeline realistic?

---

## Week 2: Processor Architecture & Safety Analysis

### Theme

**Deep Dive into Processor, Identify Hazards**

### Computer Organization Core Principles

**Principle 2-1: RISC Design Philosophy**

- Simple instructions, one operation each
- Fixed-length encoding (RISC-V: 32-bit)
- Register-rich (32 general-purpose registers)
- Load/Store architecture

**Principle 2-2: Pipeline Principles**

```
IF → ID → EX → MEM → WB
```

Ideal: CPI = 1  
Reality: Hazards cause stalls

**Principle 2-3: Pipeline Hazards**

- **Data Hazard**: RAW (Read After Write) → Forwarding
- **Control Hazard**: Branch → Prediction
- **Structural Hazard**: Resource conflict → Duplication

**Principle 2-4: Atomic Operations** In multi-core/distributed systems, use RISC-V LR/SC:

```
lr.d  (Load-Reserved)
sc.d  (Store-Conditional)
```

### ARP 4754A/DO-178C Core Principles

**Principle 2-5: Functional Hazard Assessment (FHA) Method**

```
Function → Failure Mode → Effect → Severity → Probability → Mitigation
```

**Severity Levels:**

- **Catastrophic**: Death/complete system loss
- **Hazardous**: Serious injury/major damage
- **Major**: Minor injury/significant impact
- **Minor**: Slight impact
- **No Effect**: No impact

**Principle 2-6: Safety Requirements Derivation** Every Major+ hazard → Must have safety requirement

**Principle 2-7: Software Requirements SMART Criteria**

- **S**pecific, **M**easurable, **A**chievable, **R**elevant, **T**estable

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: RISC-V Instruction Set Architecture**

- RV64I base instructions
- M extension (multiply/divide)
- A extension (atomic operations) - Critical for RAFT
- Function calling convention

**Topic 2: C906 Processor Microarchitecture**

- 8-stage pipeline
- Cache configuration (32KB I + 32KB D)
- Branch prediction
- Dual-core utilization strategy

#### Project Stand-up (1 hour)

**Progress Check:**

- [ ] SRR feedback addressed?
- [ ] Requirements finalized?
- [ ] Hazard brainstorming started?

**Blocker Discussion:**

- Technical challenges identified
- Resource needs
- Schedule concerns

#### Coding Session (3 hours)

**Activity 1: RISC-V Assembly Programming**

- [ ] Write factorial function in assembly
- [ ] Implement atomic increment using LR/SC
- [ ] Study function call stack frames

**Activity 2: FHA Workshop**

- [ ] List all CHRONOS major functions
- [ ] For each function, identify failure modes
- [ ] Assess severity and probability
- [ ] Target: Identify 20+ hazards

### Self-Study (6 hours)

**Reading:**

- Patterson & Hennessy Chapter 2: Instructions (RISC-V)
- Patterson & Hennessy Chapter 4: The Processor
- ARP 4754A Section 5: Safety Assessment Process

**Tasks:**

- [ ] Complete Functional Hazard Assessment
- [ ] Draft Preliminary System Safety Assessment (PSSA)
- [ ] Derive Software Requirements from System Requirements
- [ ] Hardware Requirements document

### Week 2 Checkpoint: FHA Review

**Deliverables Checklist:**

- [ ] Functional Hazard Assessment (8 pages)
    - [ ] Minimum 20 hazards identified
    - [ ] Severity and probability assessed
    - [ ] Mitigation strategies defined
- [ ] Preliminary System Safety Assessment (5 pages)
- [ ] Software Requirements Specification v1.0 (15 pages)
    - [ ] 80-100 software requirements (SWR-XXX)
    - [ ] Traceability to system requirements
    - [ ] Verification methods specified
- [ ] Hardware Requirements Document (3 pages)

**Review Preparation:**

- Present most critical 5 hazards
- Explain severity assessment rationale
- Demonstrate requirements traceability

---

## Week 3: Memory Hierarchy & Design Specification

### Theme

**Optimize Memory, Formalize Design**

### Computer Organization Core Principles

**Principle 3-1: Memory Hierarchy Pyramid**

```
Registers: 1 cycle, most expensive
L1 Cache: 2-3 cycles, 32KB
L2 Cache: 10+ cycles (if present)
Main Memory: 100+ cycles, 64MB
Storage: millions of cycles, 16GB
```

**Principle 3-2: Locality Principles**

- **Temporal Locality**: Recently accessed data likely accessed again
- **Spatial Locality**: Nearby data likely accessed

**Principle 3-3: Cache Mapping Trade-offs**

|Strategy|Pros|Cons|C906 Choice|
|---|---|---|---|
|Direct|Simple, fast|Many conflicts|-|
|Fully Associative|Few conflicts|Expensive|-|
|Set Associative|Balanced|Moderate|✓ (4-way)|

**Principle 3-4: Data Structure Alignment** Align data to cache line boundaries for optimal performance.

**Principle 3-5: Virtual Memory Trade-offs**

- **Pros**: Protection, sharing, flexibility
- **Cons**: TLB overhead, page table memory
- **CHRONOS Decision**: May disable (embedded, single-task)

### DO-178C Core Principles

**Principle 3-6: Design Completeness**

- High-Level Design: Module partitioning, interfaces
- Low-Level Design: Algorithm pseudocode, data structures
- **Purpose**: Eliminate ambiguity before coding

**Principle 3-7: Design Verifiability** Each design element must answer:

- How to verify this design meets requirements?
- Unit test? Integration test? Code review?

**Principle 3-8: Interface Design Clarity**

- Clear input/output specifications
- Error handling strategy
- Performance constraints (e.g., max execution time)

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: Memory Hierarchy**

- Cache operation principles
- Cache mapping strategies
- Performance analysis (AMAT)

**Topic 2: Virtual Memory**

- Paging mechanism
- TLB (Translation Lookaside Buffer)
- RISC-V Sv39 mode

#### Project Stand-up (1 hour)

**Design Discussion:**

- [ ] Architecture decisions made?
- [ ] Module interfaces defined?
- [ ] Data structure layouts planned?

**Risk Assessment:**

- Memory footprint concerns
- Performance bottlenecks
- Interface complexity

#### Coding Session (3 hours)

**Activity 1: Data Structure Design**

- [ ] Define RobotState structure (cache-aligned)
- [ ] Define ConsensusState structure
- [ ] Design message formats
- [ ] Memory layout planning

**Activity 2: Software Architecture Design**

- [ ] Module diagram: Consensus, Task, Path, Communication
- [ ] Interface Control Documents (ICDs)
- [ ] Data flow diagrams
- [ ] State machine diagrams (RAFT roles)

### Self-Study (6 hours)

**Reading:**

- Patterson & Hennessy Chapter 5: Memory Hierarchy
- DO-178C guidance on design documentation

**Tasks:**

- [ ] Complete Software Design Description (SDD)
- [ ] Write pseudocode for core algorithms
- [ ] Create code skeleton (all header files)
- [ ] Make project compilable

### Week 3 Checkpoint: PDR (Preliminary Design Review)

**Deliverables Checklist:**

- [ ] Software Design Description v1.0 (20 pages)
    - [ ] High-level architecture diagram
    - [ ] Module interface specifications
    - [ ] Core algorithm pseudocode
    - [ ] Data structure definitions
- [ ] Code skeleton
    - [ ] All header files complete
    - [ ] Function signatures defined
    - [ ] Compiles successfully
- [ ] Cache optimization strategy document (3 pages)
- [ ] Memory layout plan

**Review Preparation:**

- 60-minute design walkthrough
- Be prepared to defend:
    - Why this modular structure?
    - Interface design rationale
    - Performance estimates

---

## Week 4: I/O Systems & Implementation Launch

### Theme

**Handle Interrupts, Write Code**

### Computer Organization Core Principles

**Principle 4-1: I/O Evolution Logic**

```
Polling → Wastes CPU → Interrupts
Interrupts → High overhead for bulk data → DMA
```

**Principle 4-2: Interrupt Handling Principles**

- **Fast**: ISR should return quickly
- **Minimal**: Only essential operations in ISR
- **Deferred**: Complex logic in main loop

**Principle 4-3: Interrupt Priority** Hardware interrupts > Software interrupts  
Time-critical > Non-critical

**Principle 4-4: Bus Arbitration** When multiple devices compete:

- Fixed priority
- Round-robin
- Fair algorithms

**Principle 4-5: Memory-Mapped I/O** RISC-V approach: Device registers in address space

### DO-178C Core Principles

**Principle 4-6: Coding Standards Necessity**

- Consistency: Team collaboration
- Maintainability: Others can understand
- Safety: Avoid common pitfalls

**Principle 4-7: Code Review Value**

- Early defect detection
- Knowledge sharing
- DO-178C Level C requires peer review

**Principle 4-8: Implementation Discipline**

- Code follows design
- Every function has clear purpose
- Error handling consistent

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: I/O Systems**

- Polling vs Interrupts vs DMA
- RISC-V interrupt mechanism
- CSR registers (mstatus, mie, mip, mtvec)

**Topic 2: Bus Architecture**

- AMBA AXI protocol
- C906 bus structure
- Memory access timing

#### Project Stand-up (1 hour)

**Implementation Status:**

- [ ] Design finalized?
- [ ] Coding standards defined?
- [ ] Module assignments clear?

**Code Review Planning:**

- Review schedule
- Reviewer assignments
- Checklist preparation

#### Coding Session (3 hours)

**Activity: Core Implementation**

- [ ] RAFT state machine implementation
- [ ] Leader election logic
- [ ] Heartbeat mechanism
- [ ] Network communication layer (UDP sockets)
- [ ] Message serialization/deserialization
- [ ] CRC32 checksum implementation

**Coding Standards:**

- Function length ≤ 50 lines
- Cyclomatic complexity ≤ 10
- Meaningful variable names
- Comments for non-obvious logic

### Self-Study (6 hours)

**Reading:**

- Patterson & Hennessy Chapter 6: I/O Systems
- DO-178C coding standards guidance

**Tasks:**

- [ ] Continue implementation
- [ ] Conduct peer code reviews
- [ ] Document design decisions
- [ ] Begin integration testing preparation

### Week 4 Checkpoint: CDR (Critical Design Review)

**Deliverables Checklist:**

- [ ] RAFT core implementation (raft.c/h)
- [ ] Network communication layer (network.c/h)
- [ ] All code compiles without warnings
- [ ] Code review records
    - [ ] Review checklists completed
    - [ ] Issues documented and resolved
- [ ] Software Design Description v1.0 updated

**Review Preparation:**

- Code walkthrough (select key functions)
- Demonstrate compilation
- Explain design decisions

---

## Week 5: Parallelism & Distributed Integration

### Theme

**Multi-Node Coordination, Concurrency Control**

### Computer Organization Core Principles

**Principle 5-1: Parallelism Hierarchy**

```
Instruction-Level Parallelism (ILP): Pipeline, Superscalar
Thread-Level Parallelism (TLP): Multi-core
Task-Level Parallelism: Distributed systems
```

**Principle 5-2: Synchronization Costs**

- Locks: Mutual exclusion, but deadlock risk
- Lock-free: Atomic operations (LR/SC), more efficient

**Principle 5-3: Clock Synchronization Challenge**

- Different processors drift (ppm level)
- Network delay uncertainty
- **CHRONOS**: Use logical time (term numbers), not absolute time

**Principle 5-4: Consistency Models**

- Strong consistency: All nodes see same order (RAFT provides)
- Eventual consistency: Eventually converge (DNS, etc.)

### ARP 4754A Core Principles

**Principle 5-5: Integration Strategy**

- Incremental integration vs Big-bang
- **Recommended**: Bottom-up incremental
    - Test individual modules
    - Integrate pairwise
    - Finally full system

**Principle 5-6: Integration Testing Focus**

- Interfaces: Data passed correctly?
- Timing: Message order correct?
- Exceptions: Error propagation correct?

**Principle 5-7: Fault Tree Analysis (FTA)**

- Top-down: System failure → Component failures
- Identify combinations leading to hazards
- Quantitative reliability assessment

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: Parallelism and Synchronization**

- Multi-core architecture
- Atomic operations (RISC-V A extension)
- Lock-free data structures
- Distributed consensus principles

**Topic 2: System Integration**

- Integration strategies
- Interface testing
- Fault Tree Analysis (FTA) basics

#### Project Stand-up (1 hour)

**Integration Status:**

- [ ] Individual modules working?
- [ ] Integration plan defined?
- [ ] Test environment ready?

**Issue Resolution:**

- Interface mismatches
- Timing problems
- Performance concerns

#### Coding Session (3 hours)

**Activity: Multi-Node Integration**

- [ ] Log replication implementation
- [ ] Task allocation logic
- [ ] Path management module
- [ ] 2-node integration test (Leader + Follower)
- [ ] 3-node integration test (Leader election)
- [ ] 5-node system test

### Self-Study (6 hours)

**Reading:**

- Patterson & Hennessy Chapter 6: Parallelism
- ARP 4754A integration guidance

**Tasks:**

- [ ] Complete all module implementations
- [ ] Conduct multi-node integration testing
- [ ] Performance profiling and optimization
- [ ] System-level Fault Tree Analysis

### Week 5 Checkpoint: Integration Review & System FTA

**Deliverables Checklist:**

- [ ] Fully integrated system code
- [ ] Integration test report
    - [ ] 2-node test results
    - [ ] 3-node test results
    - [ ] 5-node test results
- [ ] System-level Fault Tree Analysis (5 pages)
    - [ ] Top event: System failure
    - [ ] Component failures identified
    - [ ] Probability calculations
- [ ] Performance profiling results
- [ ] Known issues list with mitigation plans

**Review Preparation:**

- Demonstrate 3-node system operation
- Show leader failure and re-election
- Present FTA findings

---

## Week 6: Reliability Engineering & Verification

### Theme

**Test, Test, Test**

### Computer Organization Core Principles

**Principle 6-1: Reliability Metrics**

- MTTF (Mean Time To Failure)
- MTTR (Mean Time To Repair)
- Availability = MTTF / (MTTF + MTTR)

**Principle 6-2: Redundancy Techniques**

- Space redundancy: Multiple nodes (RAFT)
- Time redundancy: Retransmission (network)
- Information redundancy: Checksums (CRC)

**Principle 6-3: Fault Detection**

- Heartbeat: Node liveness
- Checksum: Data corruption
- Timeout: Unresponsiveness

**Principle 6-4: Fault Tolerance Approach**

```
Detection → Isolation → Recovery
```

### DO-178C/ARP 4754A Core Principles

**Principle 6-5: Verification vs Validation**

- **Verification**: Did we build it right? (per requirements)
- **Validation**: Did we build the right thing? (user needs)

**Principle 6-6: Testing Hierarchy**

```
Unit Testing → Module functionality
Integration Testing → Module interaction
System Testing → Overall functionality
Acceptance Testing → Real-world scenarios
```

**Principle 6-7: Coverage Requirements (DO-178C Level C)**

- Statement coverage: Every statement executed once
- Decision coverage: Every decision True/False tested
- **Not required**: MC/DC (Level A/B only)

**Principle 6-8: Fault Injection Testing**

- Simulate node crashes
- Simulate packet loss
- Simulate message reordering

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: Reliability Engineering**

- Dependability concepts
- Fault, Error, Failure taxonomy
- Redundancy and fault tolerance

**Topic 2: Verification Methods**

- Testing strategies
- Coverage metrics
- Fault injection techniques

#### Project Stand-up (1 hour)

**Testing Status:**

- [ ] Test plan defined?
- [ ] Test cases written?
- [ ] Test environment configured?

**Results Review:**

- What passed?
- What failed?
- Mitigation plans for failures

#### Coding Session (3 hours)

**Activity: Comprehensive Testing**

- [ ] System functional testing (all requirements)
- [ ] Performance testing (latency, throughput)
- [ ] Reliability testing
    - [ ] RSSI variation (-40 to -90 dBm)
    - [ ] Packet loss (0% to 50%)
    - [ ] Node failure (tolerate ⌊N/2⌋)
- [ ] Safety verification
    - [ ] Collision avoidance
    - [ ] Split-brain detection
    - [ ] Data integrity (CRC)

### Self-Study (6 hours)

**Reading:**

- Reliability engineering chapters
- DO-178C verification guidance

**Tasks:**

- [ ] Complete all testing
- [ ] Compile test results
- [ ] Verification matrix (Requirements ↔ Tests)
- [ ] System Safety Assessment (SSA)

### Week 6 Checkpoint: Verification Review

**Deliverables Checklist:**

- [ ] Comprehensive Test Report (30+ pages)
    - [ ] Functional test results
    - [ ] Performance test results
    - [ ] Reliability test results
    - [ ] Safety verification results
- [ ] Verification Matrix (Requirements ↔ Tests complete)
- [ ] System Safety Assessment (SSA, 10 pages)
    - [ ] All hazards reviewed
    - [ ] Residual risks acceptable
- [ ] Performance comparison: Actual vs Design Targets
    - [ ] Latency achieved?
    - [ ] Throughput achieved?
    - [ ] Reliability targets met?

**Review Preparation:**

- Present verification results vs design targets
- Demonstrate fault injection tests
- Show 7-node stable operation

---

## Week 7: System Performance & Final Deliverables

### Theme

**Optimize, Document, Present**

### Computer Organization Core Principles

**Principle 7-1: Performance Optimization 80/20 Rule**

- 80% time spent in 20% of code
- Method: Measure first (profiling), then optimize

**Principle 7-2: Optimization Hierarchy**

```
Algorithm Level > Data Structure > Compiler Optimization > Assembly
```

**Principle 7-3: Compiler Optimization Flags**

- -O0: No optimization (debugging)
- -O2: Moderate optimization (recommended)
- -O3: Aggressive optimization
- -Os: Optimize for size

**Principle 7-4: Bottleneck Identification**

- CPU-bound: Algorithm optimization
- Memory-bound: Cache optimization
- I/O-bound: Asynchronous/batching

### ARP 4754A/DO-178C Core Principles

**Principle 7-5: Certification Closure**

- Software Accomplishment Summary (SAS)
- Hardware Accomplishment Summary (HAS)
- System Safety Assessment (SSA)

**Principle 7-6: Configuration Management**

- Baseline locked: Code + documents versioned
- Change control: Any modification needs review

**Principle 7-7: Documentation Completeness** Verify all artifacts exist:

- [ ] Planning documents
- [ ] Requirements documents
- [ ] Design documents
- [ ] Test documents
- [ ] Review records

### In-Class Activities (6 hours)

#### Lecture (2 hours)

**Topic 1: Performance Optimization**

- Profiling tools (perf)
- Optimization techniques
- Performance analysis

**Topic 2: Project Closure**

- Certification artifacts
- Final documentation
- Presentation skills

#### Project Stand-up (1 hour)

**Final Status:**

- [ ] All requirements met?
- [ ] All tests passed?
- [ ] Documentation complete?
- [ ] Presentation ready?

**Last Issues:**

- Critical bugs
- Documentation gaps
- Presentation concerns

#### Coding Session (3 hours)

**Activity: Final Polish**

- [ ] Performance optimization
- [ ] Bug fixes
- [ ] Code cleanup
- [ ] Final integration test
- [ ] 24-hour stability test setup

### Self-Study (6 hours)

**Tasks:**

- [ ] IEEE research paper (6 pages)
- [ ] Presentation slides (Beamer, Madrid+Wolverine)
- [ ] Software Accomplishment Summary (SAS)
- [ ] Hardware Accomplishment Summary (HAS)
- [ ] Archive all documents
- [ ] Prepare demo scenarios

### Week 7 Checkpoint: Final Presentation

**Deliverables Checklist:**

- [ ] Final source code (tagged v1.0 in Git)
- [ ] IEEE research paper (6 pages, PDF)
    - [ ] Abstract, Introduction, Methods, Experiments, Results, Conclusion
    - [ ] Figures: Architecture, Performance, Reliability
    - [ ] Comparison with RUBICONe paper
- [ ] Presentation slides (Beamer)
- [ ] Software Accomplishment Summary (SAS, 15 pages)
- [ ] Hardware Accomplishment Summary (HAS, 10 pages)
- [ ] Complete documentation package (ZIP)
- [ ] Demo video (backup)

**Final Presentation Structure (30 minutes):**

1. Project Background & Motivation (5 min)
2. Certification Approach (ARP/DO-178C/DO-254) (5 min)
3. Technical Implementation (Computer Organization perspective) (10 min)
4. Experimental Results & Live Demo (8 min)
5. Conclusions & Future Work (2 min)

**Preparation:**

- Rehearse presentation
- Test demo scenarios
- Prepare for technical Q&A
- Backup plans if hardware fails

---

# Part III: Core Principles Reference

## Computer Organization Principles

### Processor Design

1. **RISC Principles**: Simple instructions, fixed length, Load/Store
2. **Pipeline**: Overlap execution stages, watch for hazards
3. **Forwarding**: Resolve data hazards, reduce stalls
4. **Branch Prediction**: Mitigate control hazards

### Memory Systems

5. **Locality Principle**: Temporal + Spatial locality drives cache design
6. **Memory Hierarchy**: Speed-capacity-cost trade-offs
7. **Cache Mapping**: Direct (simple) vs Set-associative (balanced) vs Fully-associative (flexible)
8. **Data Alignment**: Avoid cross-cache-line access

### I/O Systems

9. **Interrupt over Polling**: Efficient asynchronous event handling
10. **DMA**: Offload bulk data transfer from CPU
11. **Memory-Mapped I/O**: RISC-V unified address space approach
12. **ISR Principles**: Fast in, fast out, defer complex work

### Parallelism & Reliability

13. **Atomic Operations**: Concurrency control foundation (LR/SC)
14. **Redundancy**: Space/Time/Information redundancy for reliability
15. **Fault Detection**: Heartbeat, checksum, timeout
16. **Fault Tolerance**: Detect → Isolate → Recover

### Performance

17. **Performance Equation**: Time = Instructions × CPI × Cycle
18. **Amdahl's Law**: Focus on bottlenecks
19. **Measure-Driven**: Profile before optimize
20. **Optimization Hierarchy**: Algorithm > Data Structure > Compiler > Assembly

---

## Certification Engineering Principles

### ARP 4754A (System Level)

21. **V-Model**: Development and verification are symmetric
22. **Requirement Quality**: Necessary, Verifiable, Traceable
23. **DAL Classification**: Severity determines rigor
24. **FHA Method**: Function → Failure → Effect → Mitigation
25. **Traceability**: Requirements → Design → Code → Tests complete chain

### DO-178C (Software Level)

26. **Software Levels**: Level A-E, different rigor levels
27. **Coding Standards**: Consistency, maintainability, safety
28. **Coverage**: Level C requires statement + decision coverage
29. **Code Review**: Peer review for early defect detection
30. **Independence**: Verification independent from development

### DO-254 (Hardware Level)

31. **COTS Method**: Assess applicability, don't redesign
32. **FMEA**: Failure Mode and Effects Analysis
33. **Qualification Testing**: Functional, performance, environmental
34. **Configuration Management**: Hardware version control

### Integration

35. **Incremental Integration**: Step-by-step, easier to debug
36. **Integration Testing**: Interface, timing, exception handling
37. **Documentation-Driven**: Documents as important as code
38. **Change Control**: Baseline changes require review
39. **Certification Closure**: SAS/HAS prove objectives met
40. **Reproducibility**: Complete CM for rebuilding anytime

---

## Project Management Principles

### Team Collaboration

41. **Role Clarity**: Clear responsibilities, avoid conflicts
42. **Communication**: Regular sync, timely issue resolution
43. **Code Review**: Mutual learning, quality improvement
44. **Git Discipline**: Branch strategy, clear commit messages

### Time Management

45. **Weekly Checkpoints**: Early deviation detection
46. **Risk Buffer**: Reserve 20% buffer time
47. **Critical Path**: Identify dependencies, prioritize
48. **Incremental Delivery**: Demonstrable results each week

### Quality Assurance

49. **Requirements-Driven**: All work traceable to requirements
50. **Continuous Integration**: Compile and test on every commit
51. **Documentation Sync**: Update docs with code changes
52. **Issue Tracking**: Record and track all problems to closure

---

# Part IV: Templates & Checklists

## Requirements Template

### System Requirement Template (SR-XXX)

```
┌─────────────────────────────────────────────────────┐
│ SYSTEM REQUIREMENT SPECIFICATION                    │
├─────────────────────────────────────────────────────┤
│ Requirement ID: SR-XXX                              │
│ Title: [Brief descriptive title]                   │
│ Category: ☐ Functional  ☐ Performance              │
│           ☐ Safety      ☐ Reliability              │
│           ☐ Constraint                              │
│ Priority: ☐ Critical  ☐ High  ☐ Medium  ☐ Low      │
├─────────────────────────────────────────────────────┤
│ Description:                                        │
│ The system shall [specific measurable statement].  │
│                                                     │
│ Rationale:                                          │
│ [Why this requirement exists]                      │
│                                                     │
│ Acceptance Criteria:                                │
│ [How to verify satisfaction]                       │
│                                                     │
│ Verification Method:                                │
│ ☐ Test  ☐ Analysis  ☐ Inspection  ☐ Demonstration │
│                                                     │
│ Derived Requirements:                               │
│ SWR-XXX: [Software requirement]                    │
│ HWR-XXX: [Hardware requirement]                    │
│                                                     │
│ Parent Requirement:                                 │
│ [Stakeholder need or higher-level requirement]    │
│                                                     │
│ Notes:                                              │
│ [Additional context, constraints, assumptions]     │
└─────────────────────────────────────────────────────┘
```

### Software Requirement Template (SWR-XXX)

```
┌─────────────────────────────────────────────────────┐
│ SOFTWARE REQUIREMENT SPECIFICATION                  │
├─────────────────────────────────────────────────────┤
│ Requirement ID: SWR-XXX                             │
│ Module: ☐ Consensus  ☐ Task  ☐ Path  ☐ Comm       │
│ Software Level: ☐ Level C  ☐ Level D  ☐ Level E   │
├─────────────────────────────────────────────────────┤
│ Description:                                        │
│ The [module] shall [specific action/behavior].     │
│                                                     │
│ Input:                                              │
│ [Data/events that trigger this requirement]        │
│                                                     │
│ Output:                                             │
│ [Expected results/behavior]                        │
│                                                     │
│ Error Handling:                                     │
│ [How to handle error conditions]                   │
│                                                     │
│ Performance:                                        │
│ [Timing constraints, if applicable]                │
│                                                     │
│ Parent Requirement:                                 │
│ SR-XXX: [System requirement]                       │
│                                                     │
│ Verification:                                       │
│ Test Case: TC-XXX                                   │
│ Expected Coverage: ☐ Statement  ☐ Decision         │
└─────────────────────────────────────────────────────┘
```

---

## Weekly Review Checklists

### Week 1: SRR Checklist

**Pre-Review (Team Self-Check):**

- [ ] System Development Plan complete (≥5 pages)
- [ ] System Requirements Specification v0.1 (≥30 requirements)
- [ ] All requirements have unique SR-XXX IDs
- [ ] Requirements classified (Functional/Performance/Safety/Constraint)
- [ ] Verification method specified for each requirement
- [ ] Git repository initialized with proper structure
- [ ] Team roster complete with roles
- [ ] Hardware tested and functional

**Review Meeting Preparation:**

- [ ] 15-minute presentation prepared
- [ ] Requirements summary slide
- [ ] Development approach slide
- [ ] Schedule/milestone slide
- [ ] Demo: Git repository structure
- [ ] Demo: Hello World on Milk-V Duo S

**Post-Review Actions:**

- [ ] Address all review comments
- [ ] Update SRS v0.2 if needed
- [ ] Finalize team communication channels
- [ ] Schedule Week 2 activities

---

### Week 2: FHA Review Checklist

**Pre-Review (Team Self-Check):**

- [ ] Functional Hazard Assessment complete (≥20 hazards)
- [ ] Each hazard has:
    - [ ] Function identified
    - [ ] Failure mode described
    - [ ] Effect on system analyzed
    - [ ] Severity classified (Catastrophic/Hazardous/Major/Minor)
    - [ ] Probability estimated
    - [ ] Mitigation strategy defined
- [ ] Preliminary System Safety Assessment (PSSA) complete
- [ ] Software Requirements Specification v1.0 (80-100 SWR-XXX)
- [ ] Hardware Requirements Document complete
- [ ] Requirements Traceability Matrix started (SR → SWR/HWR)

**Review Meeting Preparation:**

- [ ] Present top 5 critical hazards
- [ ] Explain severity assessment methodology
- [ ] Show requirements traceability examples
- [ ] Demonstrate RISC-V assembly exercises

**Post-Review Actions:**

- [ ] Revise FHA based on feedback
- [ ] Add missing hazards if identified
- [ ] Update PSSA
- [ ] Finalize software requirements baseline

---

### Week 3: PDR Checklist

**Pre-Review (Team Self-Check):**

- [ ] Software Design Description (SDD) complete (≥20 pages)
    - [ ] High-level architecture diagram
    - [ ] Module descriptions (Consensus, Task, Path, Comm)
    - [ ] Interface Control Documents (ICDs)
    - [ ] Data flow diagrams
    - [ ] State machine diagrams (RAFT)
- [ ] Core algorithms in pseudocode:
    - [ ] Leader election algorithm
    - [ ] Log replication algorithm
    - [ ] Task allocation algorithm
    - [ ] Path conflict resolution
- [ ] Data structures defined:
    - [ ] RobotState structure
    - [ ] ConsensusState structure
    - [ ] Message formats
- [ ] Code skeleton complete:
    - [ ] All .h files with function signatures
    - [ ] Makefile/CMake configured
    - [ ] Project compiles successfully
- [ ] Memory layout plan documented
- [ ] Cache optimization strategy defined

**Review Meeting Preparation:**

- [ ] 60-minute design walkthrough
- [ ] Architecture rationale
- [ ] Interface design justification
- [ ] Demo: Code skeleton compilation

**Post-Review Actions:**

- [ ] Address design feedback
- [ ] Update SDD v1.1
- [ ] Refine interfaces if needed
- [ ] Begin implementation preparation

---

### Week 4: CDR Checklist

**Pre-Review (Team Self-Check):**

- [ ] RAFT core implementation complete (raft.c/h)
    - [ ] State machine logic
    - [ ] Leader election
    - [ ] Heartbeat mechanism
    - [ ] Basic log structure
- [ ] Network communication layer (network.c/h)
    - [ ] UDP socket wrapper
    - [ ] Message serialization/deserialization
    - [ ] CRC32 implementation
- [ ] Code quality:
    - [ ] Compiles without warnings (gcc -Wall -Wextra)
    - [ ] Follows coding standards
    - [ ] Functions ≤ 50 lines
    - [ ] Cyclomatic complexity ≤ 10
- [ ] Code review records:
    - [ ] Peer review checklist completed
    - [ ] Issues documented
    - [ ] Resolutions verified
- [ ] SDD updated to reflect implementation decisions

**Review Meeting Preparation:**

- [ ] Code walkthrough of key functions
- [ ] Explain design-to-code mapping
- [ ] Demonstrate compilation
- [ ] Show code review process

**Post-Review Actions:**

- [ ] Fix critical code issues
- [ ] Refactor as needed
- [ ] Prepare for integration phase
- [ ] Update documentation

---

### Week 5: Integration Review & System FTA Checklist

**Pre-Review (Team Self-Check):**

- [ ] All modules implemented:
    - [ ] Consensus module complete
    - [ ] Task allocation module complete
    - [ ] Path management module complete
    - [ ] Communication layer complete
- [ ] Integration testing complete:
    - [ ] 2-node test (Leader + Follower) passed
    - [ ] 3-node test (Leader election) passed
    - [ ] 5-node test (Fault tolerance) passed
- [ ] System-level Fault Tree Analysis (FTA) complete:
    - [ ] Top event: System failure defined
    - [ ] Component failures identified
    - [ ] Boolean logic gates (AND/OR)
    - [ ] Probability calculations
    - [ ] Critical paths identified
- [ ] Performance profiling results:
    - [ ] Hot spots identified
    - [ ] Latency measurements
    - [ ] Throughput measurements
- [ ] Known issues documented with mitigation plans

**Review Meeting Preparation:**

- [ ] Demo: 3-node system operation
- [ ] Demo: Leader failure and re-election
- [ ] Present FTA findings
- [ ] Show integration test results

**Post-Review Actions:**

- [ ] Address integration issues
- [ ] Optimize critical paths
- [ ] Finalize system for testing phase
- [ ] Update FTA if needed

---

### Week 6: Verification Review Checklist

**Pre-Review (Team Self-Check):**

- [ ] Functional testing complete:
    - [ ] All SR-XXX requirements tested
    - [ ] Test cases documented
    - [ ] Results recorded (Pass/Fail)
- [ ] Performance testing complete:
    - [ ] Latency measured (target: ≤500ms p95)
    - [ ] Throughput measured (target: ≥20 tasks/min)
    - [ ] CPU utilization measured (target: <80%)
    - [ ] Memory footprint measured (target: <10MB)
- [ ] Reliability testing complete:
    - [ ] RSSI variation test (-40 to -90 dBm)
    - [ ] Packet loss test (0% to 50%)
    - [ ] Node failure test (tolerate ⌊N/2⌋)
- [ ] Safety verification complete:
    - [ ] Collision avoidance verified
    - [ ] Split-brain detection verified
    - [ ] Data integrity (CRC) verified
- [ ] Verification Matrix complete (Requirements ↔ Tests mapped)
- [ ] System Safety Assessment (SSA) complete
- [ ] Performance vs Design Targets comparison:
    - [ ] Latency: Achieved vs Target
    - [ ] Throughput: Achieved vs Target
    - [ ] Reliability: Achieved vs Target

**Review Meeting Preparation:**

- [ ] Present verification results summary
- [ ] Show actual vs target comparison
- [ ] Demo: Fault injection tests
- [ ] Demo: 7-node stable operation

**Post-Review Actions:**

- [ ] Address any test failures
- [ ] Complete residual testing
- [ ] Finalize SSA
- [ ] Prepare for final phase

---

### Week 7: Final Presentation Checklist

**Pre-Presentation (Team Self-Check):**

- [ ] Final source code:
    - [ ] Tagged as v1.0 in Git
    - [ ] All code committed
    - [ ] Build instructions in README
- [ ] IEEE research paper (6 pages):
    - [ ] Abstract (150-200 words)
    - [ ] Introduction with motivation
    - [ ] Related work (compare to RUBICONe)
    - [ ] Methodology (ARP 4754A approach)
    - [ ] System architecture
    - [ ] Implementation details
    - [ ] Experimental results (figures/tables)
    - [ ] Conclusion and future work
    - [ ] References (15-20 citations)
- [ ] Presentation slides (Beamer):
    - [ ] Madrid theme + Wolverine color scheme
    - [ ] 20-25 slides total
    - [ ] Clear structure (5+5+10+8+2 min)
- [ ] Software Accomplishment Summary (SAS):
    - [ ] All DO-178C Level C objectives addressed
    - [ ] Evidence provided
- [ ] Hardware Accomplishment Summary (HAS):
    - [ ] COTS justification complete
    - [ ] Qualification test results
- [ ] Complete documentation package:
    - [ ] All plans, requirements, designs
    - [ ] All test reports
    - [ ] All review records
    - [ ] Configuration index
- [ ] Demo preparation:
    - [ ] Demo scenarios scripted
    - [ ] Backup video recorded
    - [ ] All hardware tested

**Presentation Day:**

- [ ] Arrive 15 minutes early
- [ ] Test projector connection
- [ ] Test demo hardware
- [ ] Assign presentation roles:
    - [ ] Main presenter
    - [ ] Demo operator
    - [ ] Q&A responder
    - [ ] Timekeeper

**Post-Presentation Actions:**

- [ ] Submit all final documents
- [ ] Archive project repository
- [ ] Reflect on lessons learned

---

## Code Review Checklist

**Correctness:**

- [ ] Algorithm implements design correctly
- [ ] Logic handles all cases (including edge cases)
- [ ] Error conditions checked and handled
- [ ] Return values checked
- [ ] No off-by-one errors

**Safety:**

- [ ] Buffer overflows prevented
- [ ] Null pointer checks present
- [ ] Division by zero prevented
- [ ] Integer overflow/underflow considered
- [ ] No use of banned functions (malloc in critical code)

**Coding Standards:**

- [ ] Naming conventions followed
- [ ] Function length ≤ 50 lines
- [ ] Cyclomatic complexity ≤ 10
- [ ] Magic numbers replaced with named constants
- [ ] Comments for non-obvious code

**Performance:**

- [ ] No unnecessary memory allocations
- [ ] Data structures cache-friendly (aligned)
- [ ] Algorithms have acceptable complexity
- [ ] Critical paths optimized

**RAFT-Specific:**

- [ ] State transitions correct
- [ ] Term numbers managed properly
- [ ] Voting logic follows RAFT rules
- [ ] Log consistency checks present

---

## Test Case Template

```
┌─────────────────────────────────────────────────────┐
│ TEST CASE SPECIFICATION                             │
├─────────────────────────────────────────────────────┤
│ Test ID: TC-XXX                                     │
│ Test Type: ☐ Unit  ☐ Integration  ☐ System        │
│ Related Requirements: SR-XXX, SWR-XXX               │
│ Priority: ☐ Critical  ☐ High  ☐ Medium  ☐ Low      │
├─────────────────────────────────────────────────────┤
│ Purpose:                                            │
│ [What aspect of system is being tested]            │
│                                                     │
│ Preconditions:                                      │
│ [State of system before test]                      │
│                                                     │
│ Test Setup:                                         │
│ [Hardware configuration, software state]           │
│                                                     │
│ Test Procedure:                                     │
│ 1. [Step 1]                                         │
│ 2. [Step 2]                                         │
│ 3. [Step 3]                                         │
│ ...                                                 │
│                                                     │
│ Expected Results:                                   │
│ [What should happen if system correct]             │
│                                                     │
│ Pass/Fail Criteria:                                 │
│ [Specific measurable criteria]                     │
│                                                     │
│ Actual Results:                                     │
│ [Filled after execution]                           │
│                                                     │
│ Status: ☐ Pass  ☐ Fail  ☐ Blocked  ☐ Not Run      │
│                                                     │
│ Notes:                                              │
│ [Observations, anomalies, etc.]                    │
│                                                     │
│ Executed By: _______________ Date: _______         │
│ Reviewed By: _______________ Date: _______         │
└─────────────────────────────────────────────────────┘
```

---

## Document Standards

### Document Naming Convention

```
<ProjectName>_<DocumentType>_<Version>_<Date>.pdf

Examples:
CHRONOS_SRS_v1.0_20241115.pdf
CHRONOS_FHA_v1.2_20241122.pdf
CHRONOS_SDD_v2.0_20241129.pdf
```

### Version Control

- **v0.x**: Draft versions (internal review)
- **v1.0**: First baseline (formal review)
- **v1.x**: Minor updates (corrections, clarifications)
- **v2.0**: Major revision (significant changes)

### Document Header Template

```
┌─────────────────────────────────────────────────────┐
│ [DOCUMENT TITLE]                                    │
├─────────────────────────────────────────────────────┤
│ Project: CHRONOS                                    │
│ Document ID: [DOC-XXX]                              │
│ Version: [x.x]                                      │
│ Date: [YYYY-MM-DD]                                  │
│ Status: ☐ Draft  ☐ Review  ☐ Approved  ☐ Baseline │
├─────────────────────────────────────────────────────┤
│ Author(s): [Name(s)]                                │
│ Reviewer(s): [Name(s)]                              │
│ Approved By: [Instructor Name]                      │
└─────────────────────────────────────────────────────┘

Revision History:
┌─────────┬────────────┬──────────┬─────────────────┐
│ Version │    Date    │  Author  │  Description    │
├─────────┼────────────┼──────────┼─────────────────┤
│  0.1    │ 2024-11-01 │  Team    │  Initial draft  │
│  1.0    │ 2024-11-08 │  Team    │  First baseline │
└─────────┴────────────┴──────────┴─────────────────┘
```

---

## Quick Reference

### Important Contacts

- **Instructor**: Dr. Hao Xu
- **Email**: hxu@tongji.edu.cn
- **Office**: Zhixinguan 708a
- **Office Hours**: Tuesday Afternoon or by Appointment

### Key Tools

- **Development**: GCC RISC-V cross-compiler, Git
- **Analysis**: perf (performance), objdump (disassembly)
- **Documentation**: LaTeX (paper), Markdown (docs)
- **Hardware**: Milk-V Duo S, Serial console

### Document Abbreviations

- **SDP**: System Development Plan
- **SRS**: System Requirements Specification
- **FHA**: Functional Hazard Assessment
- **PSSA**: Preliminary System Safety Assessment
- **SSA**: System Safety Assessment
- **SDD**: Software Design Description
- **SAS**: Software Accomplishment Summary
- **HAS**: Hardware Accomplishment Summary
- **FTA**: Fault Tree Analysis
- **RTM**: Requirements Traceability Matrix

### Weekly Checkpoint Schedule

|Week|Day|Checkpoint|Deliverables Due|
|---|---|---|---|
|1|Fri|SRR|SDP, SRS v0.1|
|2|Fri|FHA Review|FHA, PSSA, SRS v1.0|
|3|Fri|PDR|SDD, Code skeleton|
|4|Fri|CDR|Core code, Reviews|
|5|Fri|Integration|Integrated system, FTA|
|6|Fri|Verification|Test reports, SSA|
|7|Fri|Final Presentation|All final documents|

---

## Final Thoughts

**Success Formula:**

```
Good Requirements
    + Traceable Design
    + Reviewed Code
    + Thorough Testing
    + Complete Documentation
    = Certifiable System
```

**Remember:**

- These standards exist for good reasons (learned from real failures)
- Process over perfection: Systematic approach builds confidence
- Documentation is as important as code
- Team collaboration multiplies individual efforts
- Ask questions early and often

**Course Philosophy:** _"The best way to understand computer organization is to build a complete system that depends on it."_

**Project Motto:** _"Alea iacta est" - The die is cast. Cross the RUBICONe and build trustworthy distributed systems!_

---

**Good luck with your project!**

_This handbook is your roadmap. Refer to it weekly, follow the checklists, and you will succeed._

---

**END OF HANDBOOK**
