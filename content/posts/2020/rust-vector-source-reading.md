---
title: "Rust Vector 源码解析"
date: 2020-02-22T01:36:53+08:00
draft: false
---



### 主流程

* main@main.rs
* topology::start_validated@topology/mod.rs
* running_topology.spawn_all@topology/mod.rs
    * 这里不仅是新建，也负责diff and adjust
    * spawn_source
    * spawn_transform
    * spawn_sink
* 

### 概念树

拓扑逻辑
```
    let mut running_topology = RunningTopology {
        inputs: HashMap::new(),
        outputs: HashMap::new(),
        config: Config::empty(),
        shutdown_triggers: HashMap::new(),
        source_tasks: HashMap::new(),
        tasks: HashMap::new(),
        abort_tx,
    };
```
可以看到vector里的拓扑逻辑较为简单，
核心是in/out


