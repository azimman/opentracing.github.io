---
layout: post
title: "weekly hangout: C#, HTTP encoding, key-value logging, reusing existing log instrumentation"
---


- @bensigelman - C# OT proposal outstanding; has a different approach to inject/join since C# has real generics
- There was a discussion around HTTP and whether it deserves special treatment. In Go, URL encoding happens automatically (there’s an http carrier) but not so in other languages. Some tracers needs to have a policy about how various components get into and out of http headers. The trouble is that Tracer impls do not actually manage the HTTP encode/decode directly in present-day OpenTracing: should they?
  - Much followup discussion in https://github.com/opentracing/opentracing.github.io/issues/98
- A logging proposal by @yurishkuro: if we agree to key-value logging API we should add it to the GH issue. 
- @jmacd believes in key-value logging but thinks we need to show need/benefit before we invest further. It’s good that OT has not tried to pin down a context propagation spec because it will depend a lot on style.
- @jmacd proposed that we establish a context propagation idiom or library for each language. This way a non OT library can get OT context. Then we can add logging plugins to us the active OT span to redirect logs appropriately. That said, we need some way to guarantee that high-throughput logs are only serialized as-needed.
