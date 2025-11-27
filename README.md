## Mastra bug description

When running Mastra in serve mode (mastra serve / nx run nuomy-ai:serve) on a Linux environment, we encounter repeated TypeError: fetch failed errors with ETIMEDOUT causes.

The issue occurs during content generation workflows (e.g., markdown-composer, sorting-lines-composer). The generation itself often completes (sometimes after retries), but the process is spammed with these connection errors, and log flushing fails.

Full service log:
```
npx nx run mastra-ai:serve

> nx run mastra-ai:serve

Mastra telemetry is enabled, but the required instrumentation file was not loaded. If you are using Mastra outside of the mastra server environment, see: https://mastra.ai/en/docs/observability/tracing#tracing-outside-mastra-server-environment If you are using a custom instrumentation file or want to disable this warning, set the globalThis.___MASTRA_TELEMETRY___ variable to true in your instrumentation file.
Mastra telemetry is deprecated and will be removed on the Nov 4th release. Instead use AI Tracing. More info can be found here: https://github.com/mastra-ai/mastra/issues/8577 and here: https://mastra.ai/en/docs/observability/ai-tracing/overview
 Mastra API running on port http://0.0.0.0:4111/api
Braintrust exporter: No span data found for span {
  traceId: '64e70dc89841ef3be28a0c52528adfa1',
  spanId: '76a110127d3c113c',
  spanName: "loop: 'dowhile'",
  spanType: 'workflow_loop',
  isRootSpan: false,
  parentSpanId: 'cae2a65a93c1e1b7',
  method: 'handleSpanStarted'
}
Braintrust exporter: No Braintrust span found for span update/end {
  traceId: '64e70dc89841ef3be28a0c52528adfa1',
  spanId: '76a110127d3c113c',
  spanName: "loop: 'dowhile'",
  spanType: 'workflow_loop',
  isRootSpan: false,
  parentSpanId: 'cae2a65a93c1e1b7',
  method: 'handleSpanEnd'
}
Braintrust exporter: No span data found for span {
  traceId: 'fbd1fa43280de3f070c408a66da88f5f',
  spanId: '4fd0c1fece1f2f14',
  spanName: "loop: 'dowhile'",
  spanType: 'workflow_loop',
  isRootSpan: false,
  parentSpanId: '898a3a6beea0c738',
  method: 'handleSpanStarted'
}
Braintrust exporter: No Braintrust span found for span update/end {
  traceId: 'fbd1fa43280de3f070c408a66da88f5f',
  spanId: '4fd0c1fece1f2f14',
  spanName: "loop: 'dowhile'",
  spanType: 'workflow_loop',
  isRootSpan: false,
  parentSpanId: '898a3a6beea0c738',
  method: 'handleSpanEnd'
}
Braintrust exporter: No span data found for span {
  traceId: '6bfa99664cf16c87cb6f855a183710aa',
  spanId: 'a7bef66aa6013631',
  spanName: "loop: 'dowhile'",
  spanType: 'workflow_loop',
  isRootSpan: false,
  parentSpanId: '0728ec6a4932cc4b',
  method: 'handleSpanStarted'
}
Braintrust exporter: No Braintrust span found for span update/end {
  traceId: '6bfa99664cf16c87cb6f855a183710aa',
  spanId: 'a7bef66aa6013631',
  spanName: "loop: 'dowhile'",
  spanType: 'workflow_loop',
  isRootSpan: false,
  parentSpanId: '0728ec6a4932cc4b',
  method: 'handleSpanEnd'
}
[markdown-composer] Starting markdown generation {
  stepId: 'markdown-composer',
  hasOutline: true,
  outlineName: 'Orientation to Data Analysis'
}
[markdown-composer] Requesting stream from agent {
  stepId: 'markdown-composer',
  promptLength: 2244,
  timestamp: '2025-11-27T13:48:59.663Z'
}
[markdown-composer] Stream response received from agent {
  stepId: 'markdown-composer',
  streamRequestDuration: 8,
  timestamp: '2025-11-27T13:48:59.672Z'
}
[markdown-composer] Starting stream consumption with timeout protection { stepId: 'markdown-composer', timestamp: '2025-11-27T13:48:59.672Z' }
[StreamConsumer:markdown-composer] Starting stream consumption {
  stepId: 'markdown-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:48:59.673Z'
}
[StreamConsumer:markdown-composer] First chunk received {
  stepId: 'markdown-composer',
  timeToFirstChunk: 8749,
  firstChunkSize: 2,
  timestamp: '2025-11-27T13:49:08.422Z'
}
[StreamConsumer:markdown-composer] Stream completed successfully {
  stepId: 'markdown-composer',
  duration: 8815,
  timeToFirstChunk: 8749,
  chunkCount: 290,
  contentLength: 1494,
  contentPreview: '{"content": "# Orientation to Data Analysis\\n\\n## Learning Objectives\\n- Understand the basic steps of the data analysis process.\\n- Recognize the importance of data analysis in real-world application',
  contentEnd: '\\nReflect on how you can apply these steps in your own projects to enhance your analytical skills."}',
  timestamp: '2025-11-27T13:49:08.488Z'
}
[markdown-composer] Stream consumption completed {
  stepId: 'markdown-composer',
  isComplete: true,
  duration: 8815,
  chunkCount: 290,
  contentLength: 1494
}
[markdown-composer] Parsing JSON from response { stepId: 'markdown-composer', contentLength: 1494 }
[markdown-composer] JSON parsed successfully { stepId: 'markdown-composer', hasContent: true }
[markdown-composer] Creating generated material { stepId: 'markdown-composer', contentLength: 1449 }
[markdown-composer] Markdown generation completed successfully { stepId: 'markdown-composer', materialId: undefined }
[question-composer] Starting question generation {
  stepId: 'question-composer',
  hasOutline: true,
  outlineName: 'Data Types Quiz'
}
[question-composer] Requesting stream from agent {
  stepId: 'question-composer',
  promptLength: 1509,
  timestamp: '2025-11-27T13:49:08.512Z'
}
[question-composer] Stream response received from agent {
  stepId: 'question-composer',
  streamRequestDuration: 7,
  timestamp: '2025-11-27T13:49:08.519Z'
}
[question-composer] Starting stream consumption with timeout protection { stepId: 'question-composer', timestamp: '2025-11-27T13:49:08.519Z' }
[StreamConsumer:question-composer] Starting stream consumption {
  stepId: 'question-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:49:08.519Z'
}
[StreamConsumer:question-composer] First chunk received {
  stepId: 'question-composer',
  timeToFirstChunk: 426,
  firstChunkSize: 1,
  timestamp: '2025-11-27T13:49:08.945Z'
}
[StreamConsumer:question-composer] Stream completed successfully {
  stepId: 'question-composer',
  duration: 8778,
  timeToFirstChunk: 426,
  chunkCount: 105,
  contentLength: 426,
  contentPreview: '{ "type": "question", "data": {\n' +
    '    "text": "Which of the following is NOT a common data type used in data analysis?",\n' +
    '    "code": "",\n' +
    '    "code_language": "",\n' +
    '    "answers": ["Integer", "String", "Bo',
  contentEnd: `d Boolean. 'Image' is not typically considered a standard data type in data analysis contexts."\n` +
    '  }}',
  timestamp: '2025-11-27T13:49:17.297Z'
}
[question-composer] Stream consumption completed {
  stepId: 'question-composer',
  isComplete: true,
  duration: 8778,
  chunkCount: 105,
  contentLength: 426
}
[question-composer] Parsing JSON from response { stepId: 'question-composer', contentLength: 426 }
[question-composer] JSON parsed successfully { stepId: 'question-composer', hasQuestions: false }
[question-composer] Creating generated material { stepId: 'question-composer' }
[question-composer] Question generation completed successfully { stepId: 'question-composer', materialId: undefined }
[markdown-composer] Starting markdown generation {
  stepId: 'markdown-composer',
  hasOutline: true,
  outlineName: 'Understanding Data Cleaning'
}
[markdown-composer] Requesting stream from agent {
  stepId: 'markdown-composer',
  promptLength: 2536,
  timestamp: '2025-11-27T13:49:17.322Z'
}
[markdown-composer] Stream response received from agent {
  stepId: 'markdown-composer',
  streamRequestDuration: 10,
  timestamp: '2025-11-27T13:49:17.332Z'
}
[markdown-composer] Starting stream consumption with timeout protection { stepId: 'markdown-composer', timestamp: '2025-11-27T13:49:17.332Z' }
[StreamConsumer:markdown-composer] Starting stream consumption {
  stepId: 'markdown-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:49:17.333Z'
}
log request failed. Elapsed time: 27.015 seconds. Payload size: 836.
Error: TypeError: fetch failed
Sleeping for 1s
[StreamConsumer:markdown-composer] First chunk received {
  stepId: 'markdown-composer',
  timeToFirstChunk: 35803,
  firstChunkSize: 2,
  timestamp: '2025-11-27T13:49:53.136Z'
}
[StreamConsumer:markdown-composer] Stream progress {
  stepId: 'markdown-composer',
  duration: 35803,
  timeSinceFirstChunk: 0,
  chunkCount: 1,
  contentLength: 2,
  lastChunkSize: 2
}
[StreamConsumer:markdown-composer] Stream completed successfully {
  stepId: 'markdown-composer',
  duration: 35866,
  timeToFirstChunk: 35803,
  chunkCount: 352,
  contentLength: 1716,
  contentPreview: '{"content":"# Understanding Data Cleaning\\n\\n## Learning Objectives\\n- Define data cleaning and its importance in data analysis.\\n- Identify common methods used in data cleaning.\\n\\n## Introduction\\nD',
  contentEnd: ' **Key Takeaway**: Clean data is the foundation of reliable analysis and informed decision-making."}',
  timestamp: '2025-11-27T13:49:53.199Z'
}
[markdown-composer] Stream consumption completed {
  stepId: 'markdown-composer',
  isComplete: true,
  duration: 35866,
  chunkCount: 352,
  contentLength: 1716
}
[markdown-composer] Parsing JSON from response { stepId: 'markdown-composer', contentLength: 1716 }
[markdown-composer] JSON parsed successfully { stepId: 'markdown-composer', hasContent: true }
[markdown-composer] Creating generated material { stepId: 'markdown-composer', contentLength: 1665 }
[markdown-composer] Markdown generation completed successfully { stepId: 'markdown-composer', materialId: undefined }
[sorting-lines-composer] Starting sorting lines generation {
  stepId: 'sorting-lines-composer',
  hasOutline: true,
  outlineName: 'Data Cleaning Steps'
}
[sorting-lines-composer] Requesting stream from agent { stepId: 'sorting-lines-composer', promptLength: 1383 }
[sorting-lines-composer] Stream response received, consuming with timeout protection { stepId: 'sorting-lines-composer' }
[StreamConsumer:sorting-lines-composer] Starting stream consumption {
  stepId: 'sorting-lines-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:49:53.242Z'
}
Encountered error when constructing records to flush. Retrying
TypeError: fetch failed
    at node:internal/deps/undici/undici:14900:13
    at processTicksAndRejections (node:internal/process/task_queues:95:5)
    at runNextTicks (node:internal/process/task_queues:64:3)
    at listOnTimeout (node:internal/timers:545:9)
    at process.processTimers (node:internal/timers:519:7)
    at async _HTTPConnection.post (file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90682:11)
    at async _HTTPConnection.post_json (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90714:22)
    at async computeLoggerMetadata (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:89142:22)
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91143:19
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91147:30 {
  [cause]: AggregateError [ETIMEDOUT]: 
      at internalConnectMultiple (node:net:1122:18)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at Timeout.internalConnectMultipleTimeout (node:net:1716:5)
      at listOnTimeout (node:internal/timers:583:11)
      at process.processTimers (node:internal/timers:519:7) {
    code: 'ETIMEDOUT',
    [errors]: [
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error]
    ]
  }
}
Sleeping for 1s
[StreamConsumer:sorting-lines-composer] First chunk received {
  stepId: 'sorting-lines-composer',
  timeToFirstChunk: 91733,
  firstChunkSize: 1,
  timestamp: '2025-11-27T13:51:24.975Z'
}
[StreamConsumer:sorting-lines-composer] Stream progress {
  stepId: 'sorting-lines-composer',
  duration: 91733,
  timeSinceFirstChunk: 0,
  chunkCount: 1,
  contentLength: 1,
  lastChunkSize: 1
}
[StreamConsumer:sorting-lines-composer] Stream completed successfully {
  stepId: 'sorting-lines-composer',
  duration: 91772,
  timeToFirstChunk: 91733,
  chunkCount: 210,
  contentLength: 817,
  contentPreview: '{ "type": "sorting-lines", "data": {\n' +
    '    "text": "Arrange the steps of data cleaning in the correct order.",\n' +
    '    "language": "en",\n' +
    '    "isCode": false,\n' +
    '    "lines": [\n' +
    '        { "id": "step1", "text": ',
  contentEnd: 'ndardizing data formats, validating data accuracy, and finally documenting the cleaning process."\n' +
    '}}',
  timestamp: '2025-11-27T13:51:25.014Z'
}
[sorting-lines-composer] Stream consumption completed {
  stepId: 'sorting-lines-composer',
  isComplete: true,
  duration: 91772,
  chunkCount: 210,
  contentLength: 817
}
[sorting-lines-composer] Parsing JSON from response { stepId: 'sorting-lines-composer', contentLength: 817 }
[sorting-lines-composer] JSON parsed successfully { stepId: 'sorting-lines-composer', hasLines: false }
[sorting-lines-composer] Creating generated material { stepId: 'sorting-lines-composer' }
[sorting-lines-composer] Sorting lines generation completed successfully { stepId: 'sorting-lines-composer', materialId: undefined }
[markdown-composer] Starting markdown generation {
  stepId: 'markdown-composer',
  hasOutline: true,
  outlineName: 'Exploratory Data Analysis Guide'
}
[markdown-composer] Requesting stream from agent {
  stepId: 'markdown-composer',
  promptLength: 2572,
  timestamp: '2025-11-27T13:51:25.050Z'
}
[markdown-composer] Stream response received from agent {
  stepId: 'markdown-composer',
  streamRequestDuration: 9,
  timestamp: '2025-11-27T13:51:25.059Z'
}
[markdown-composer] Starting stream consumption with timeout protection { stepId: 'markdown-composer', timestamp: '2025-11-27T13:51:25.060Z' }
[StreamConsumer:markdown-composer] Starting stream consumption {
  stepId: 'markdown-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:51:25.060Z'
}
Encountered error when constructing records to flush. Retrying
TypeError: fetch failed
    at node:internal/deps/undici/undici:14900:13
    at processTicksAndRejections (node:internal/process/task_queues:95:5)
    at runNextTicks (node:internal/process/task_queues:64:3)
    at process.processTimers (node:internal/timers:516:9)
    at async _HTTPConnection.post (file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90682:11)
    at async _HTTPConnection.post_json (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90714:22)
    at async computeLoggerMetadata (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:89142:22)
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91143:19
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91147:30 {
    at async LazyValue.callable (file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91132:49) {
  [cause]: AggregateError [ETIMEDOUT]: 
      at internalConnectMultiple (node:net:1122:18)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at Timeout.internalConnectMultipleTimeout (node:net:1716:5)
      at listOnTimeout (node:internal/timers:583:11)
      at process.processTimers (node:internal/timers:519:7) {
    code: 'ETIMEDOUT',
    [errors]: [
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error]
    ]
  }
}
Sleeping for 2s
Encountered error when constructing records to flush
Failed to construct log records to flush after 3 attempts. Dropping batch
Encountered error when constructing records to flush. Retrying
TypeError: fetch failed
    at node:internal/deps/undici/undici:14900:13
    at processTicksAndRejections (node:internal/process/task_queues:95:5)
    at runNextTicks (node:internal/process/task_queues:64:3)
    at listOnTimeout (node:internal/timers:545:9)
    at process.processTimers (node:internal/timers:519:7)
    at async _HTTPConnection.post (file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90682:11)
    at async _HTTPConnection.post_json (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90714:22)
    at async computeLoggerMetadata (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:89142:22)
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91143:19
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91147:30 {
  [cause]: AggregateError [ETIMEDOUT]: 
      at internalConnectMultiple (node:net:1122:18)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at Timeout.internalConnectMultipleTimeout (node:net:1716:5)
      at listOnTimeout (node:internal/timers:583:11)
      at process.processTimers (node:internal/timers:519:7) {
    code: 'ETIMEDOUT',
    [errors]: [
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error]
    ]
  }
}
Sleeping for 1s
[StreamConsumer:markdown-composer] First chunk received {
  stepId: 'markdown-composer',
  timeToFirstChunk: 34740,
  firstChunkSize: 2,
  timestamp: '2025-11-27T13:51:59.800Z'
}
[StreamConsumer:markdown-composer] Stream progress {
  stepId: 'markdown-composer',
  duration: 34740,
  timeSinceFirstChunk: 0,
  chunkCount: 1,
  contentLength: 2,
  lastChunkSize: 2
}
Encountered error when constructing records to flush. Retrying
TypeError: fetch failed
    at node:internal/deps/undici/undici:14900:13
    at processTicksAndRejections (node:internal/process/task_queues:95:5)
    at runNextTicks (node:internal/process/task_queues:64:3)
    at listOnTimeout (node:internal/timers:545:9)
    at process.processTimers (node:internal/timers:519:7)
    at async _HTTPConnection.post (file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90682:11)
    at async _HTTPConnection.post_json (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:90714:22)
    at async computeLoggerMetadata (file:///root/mastra-workspace/apps/mastra-ai/.mastra/output/mastra.mjs:89142:22)
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91143:19
    at async file:///root/workspace/apps/mastra-ai/.mastra/output/mastra.mjs:91147:30 {
  [cause]: AggregateError [ETIMEDOUT]: 
      at internalConnectMultiple (node:net:1122:18)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at internalConnectMultiple (node:net:1190:5)
      at Timeout.internalConnectMultipleTimeout (node:net:1716:5)
      at listOnTimeout (node:internal/timers:583:11)
      at process.processTimers (node:internal/timers:519:7) {
    code: 'ETIMEDOUT',
    [errors]: [
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error],
      [Error], [Error]
    ]
  }
}
Sleeping for 2s
[StreamConsumer:markdown-composer] Stream progress {
  stepId: 'markdown-composer',
  duration: 49838,
  timeSinceFirstChunk: 15098,
  chunkCount: 257,
  contentLength: 1085,
  lastChunkSize: 3
}
[StreamConsumer:markdown-composer] Stream completed successfully {
  stepId: 'markdown-composer',
  duration: 49887,
  timeToFirstChunk: 34740,
  chunkCount: 488,
  contentLength: 2086,
  contentPreview: '{"content": "# Exploratory Data Analysis Guide\\n\\n## Learning Objectives\\n\\n- Understand the purpose and importance of Exploratory Data Analysis (EDA).\\n- Identify key techniques and tools used in EDA',
  contentEnd: '\\nBy regularly practicing EDA, you enhance your ability to interpret and analyze data effectively."}',
  timestamp: '2025-11-27T13:52:14.947Z'
}
[markdown-composer] Stream consumption completed {
  stepId: 'markdown-composer',
  isComplete: true,
  duration: 49887,
  chunkCount: 488,
  contentLength: 2086
}
[markdown-composer] Parsing JSON from response { stepId: 'markdown-composer', contentLength: 2086 }
[markdown-composer] JSON parsed successfully { stepId: 'markdown-composer', hasContent: true }
[markdown-composer] Creating generated material { stepId: 'markdown-composer', contentLength: 2012 }
[markdown-composer] Markdown generation completed successfully { stepId: 'markdown-composer', materialId: undefined }
[missing-code-block-composer] Starting missing code block generation {
  stepId: 'missing-code-block-composer',
  hasOutline: true,
  outlineName: 'Exploratory Data Analysis Practice'
}
[missing-code-block-composer] Requesting stream from agent { stepId: 'missing-code-block-composer', promptLength: 3385 }
[missing-code-block-composer] Stream response received, consuming with timeout protection { stepId: 'missing-code-block-composer' }
[StreamConsumer:missing-code-block-composer] Starting stream consumption {
  stepId: 'missing-code-block-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:52:14.998Z'
}
Encountered error when constructing records to flush
Failed to construct log records to flush after 3 attempts. Dropping batch
[StreamConsumer:missing-code-block-composer] First chunk received {
  stepId: 'missing-code-block-composer',
  timeToFirstChunk: 35104,
  firstChunkSize: 1,
  timestamp: '2025-11-27T13:52:50.102Z'
}
[StreamConsumer:missing-code-block-composer] Stream progress {
  stepId: 'missing-code-block-composer',
  duration: 35105,
  timeSinceFirstChunk: 1,
  chunkCount: 1,
  contentLength: 1,
  lastChunkSize: 1
}
[StreamConsumer:missing-code-block-composer] Stream completed successfully {
  stepId: 'missing-code-block-composer',
  duration: 35192,
  timeToFirstChunk: 35104,
  chunkCount: 340,
  contentLength: 1118,
  contentPreview: '{ "type": "missing-code-block", "data": { "text": "Fill in the missing steps in an exploratory data analysis process.", "code": "import pandas as pd\\n\\ndef exploratory_data_analysis(data):\\n    # Step',
  contentEnd: 'nspecting the first few rows, and obtaining summary statistics to understand the dataset better." }}',
  timestamp: '2025-11-27T13:52:50.190Z'
}
[missing-code-block-composer] Stream consumption completed {
  stepId: 'missing-code-block-composer',
  isComplete: true,
  duration: 35192,
  chunkCount: 340,
  contentLength: 1118
}
[missing-code-block-composer] Parsing JSON from response { stepId: 'missing-code-block-composer', contentLength: 1118 }
[missing-code-block-composer] JSON parsed successfully { stepId: 'missing-code-block-composer', hasCode: false }
[missing-code-block-composer] Creating generated material { stepId: 'missing-code-block-composer' }
[missing-code-block-composer] Missing code block generation completed successfully { stepId: 'missing-code-block-composer', materialId: undefined }
[markdown-composer] Starting markdown generation {
  stepId: 'markdown-composer',
  hasOutline: true,
  outlineName: 'Data Analysis Recap and Next Steps'
}
[markdown-composer] Requesting stream from agent {
  stepId: 'markdown-composer',
  promptLength: 2598,
  timestamp: '2025-11-27T13:52:50.243Z'
}
[markdown-composer] Stream response received from agent {
  stepId: 'markdown-composer',
  streamRequestDuration: 11,
  timestamp: '2025-11-27T13:52:50.254Z'
}
[markdown-composer] Starting stream consumption with timeout protection { stepId: 'markdown-composer', timestamp: '2025-11-27T13:52:50.254Z' }
[StreamConsumer:markdown-composer] Starting stream consumption {
  stepId: 'markdown-composer',
  timeoutMs: 300000,
  startTime: '2025-11-27T13:52:50.255Z'
}
log request failed. Elapsed time: 37.46 seconds. Payload size: 155069.
Error: TypeError: fetch failed
Sleeping for 1s
log request failed. Elapsed time: 33.659 seconds. Payload size: 155069.
Error: TypeError: fetch failed
Sleeping for 2s
[StreamConsumer:markdown-composer] First chunk received {
  stepId: 'markdown-composer',
  timeToFirstChunk: 145556,
  firstChunkSize: 2,
  timestamp: '2025-11-27T13:55:15.811Z'
}
[StreamConsumer:markdown-composer] Stream progress {
  stepId: 'markdown-composer',
  duration: 145556,
  timeSinceFirstChunk: 0,
  chunkCount: 1,
  contentLength: 2,
  lastChunkSize: 2
}
[StreamConsumer:markdown-composer] Stream completed successfully {
  stepId: 'markdown-composer',
  duration: 145632,
  timeToFirstChunk: 145556,
  chunkCount: 249,
  contentLength: 1231,
  contentPreview: '{"content":"# Data Analysis Recap and Next Steps\\n\\n## Learning Objectives\\n- Summarize key concepts in data analysis.\\n- Identify next steps for further learning.\\n\\n## Key Concepts Recap\\n- **Data C',
  contentEnd: 'cisions. Continue your learning journey by diving into advanced topics and practical applications."}',
  timestamp: '2025-11-27T13:55:15.887Z'
}
[markdown-composer] Stream consumption completed {
  stepId: 'markdown-composer',
  isComplete: true,
  duration: 145632,
  chunkCount: 249,
  contentLength: 1231
}
[markdown-composer] Parsing JSON from response { stepId: 'markdown-composer', contentLength: 1231 }
[markdown-composer] JSON parsed successfully { stepId: 'markdown-composer', hasContent: true }
[markdown-composer] Creating generated material { stepId: 'markdown-composer', contentLength: 1195 }
[markdown-composer] Markdown generation completed successfully { stepId: 'markdown-composer', materialId: undefined }
log request failed after 3 retries. Dropping batch
```
